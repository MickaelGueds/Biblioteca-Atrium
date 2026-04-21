# Obsidian - Configuração Recomendada

## Visão Geral

Obsidian é o IDE para seu wiki LLM. É onde você visualiza, navega e interage com o conhecimento que o LLM constrói.

## Configuração Essencial

### 1. Estrutura de Pastas

```
[seu-wiki-obsidian]/
├── raw/                    ← Fontes originais (IMUTÁVEL)
│   ├── papers/
│   ├── articles/
│   ├── images/
│   └── ...
├── wiki/                   ← Markdown gerado pelo LLM
│   ├── entities/
│   ├── concepts/
│   ├── sources/
│   ├── comparisons/
│   ├── synthesis/
│   ├── index.md
│   └── log.md
└── CLAUDE.md               ← Schema (instruções para o LLM)
```

### 2. Configuração de Arquivos e Links

**Settings → Files and Links → Attachment folder path**

```
raw/assets
```

**Por que?**
- Centraliza todas as imagens baixadas
- Evita caminhos relativos quebrados
- Facilita backup e versionamento

**Settings → Files and Links → Default location for new attachments**

```
In subfolder under current folder
```

**Por que?**
- Mantém arquivos próximos do markdown que os referencia
- Facilita organização por projeto/tema

**Settings → Files and Links → New link format**

```
Shortest path when possible
```

**Por que?**
- Links mais limpos: `[[Self-Attention]]` em vez de `[[concepts/self-attention]]`
- O LLM pode gerar links mais naturalmente

### 3. Configuração de Hotkeys

**Settings → Hotkeys → Search**

```
Ctrl+Shift+P     → Command palette (rápido para buscar comandos)
Ctrl+Shift+O    → Quick switcher (trocar arquivo rápido)
Ctrl+Shift+F    → Global search (busca em todo wiki)
Ctrl+G          → Go to line (ir para linha específica)
```

**Settings → Hotkeys → Download**

```
Ctrl+Shift+D    → Download attachments for current file
```

**Por que?**
- Após usar Web Clipper, pressiona este hotkey para baixar todas as imagens
- Imagens ficam em `raw/assets` em vez de URLs quebradas

### 4. Configuração de Editor

**Settings → Editor → Spacious line length**

```
Ligado
```

**Por que?**
- Leitura mais confortável
- Melhor para revisão de conteúdo longo

**Settings → Editor → Show line number**

```
Ligado
```

**Por que?**
- Facilita referenciar partes específicas do texto
- Útil quando discute com LLM sobre um parágrafo específico

**Settings → Editor → Use Vim key bindings**

```
[Opcional] Ligado se usa Vim
```

### 5. Configuração de Graph View

**Settings → Graph View → Groups**

```
By tags
```

**Por que?**
- Conexões por tema (entities, concepts, sources, synthesis)
- Mais fácil identificar comunidades

**Settings → Graph View → Show local graph**

```
Ligado
```

**Por que?**
- Mostra apenas conexões da página atual
- Menos clutter, mais focado

**Settings → Graph View → Number of hops**

```
1
```

**Por que?**
- 1 hop = conexões diretas da página atual
- Limite para não sobrecarregar visualmente

## Plugins Essenciais

### 1. Obsidian Web Clipper (Obrigatório)

**Instalação**
```
Settings → Community Plugins → Browse → Search "Web Clipper"
```

**Uso**
1. Visite artigo que deseja salvar
2. Clique no ícone do Obsidian na barra do navegador
3. Escolha pasta de destino (ex: `raw/articles/`)
4. Clique "Save"
5. Pressione `Ctrl+Shift+D` para baixar imagens (importante!)

**Resultados**
- Artigo salvo como markdown em `raw/articles/`
- Imagens baixadas para `raw/assets/`
- URLs de imagens substituídas por caminhos locais

### 2. Dataview (Recomendado)

**Instalação**
```
Settings → Community Plugins → Browse → Search "Dataview"
```

**Uso**
Consultas dinâmicas sobre frontmatter YAML de páginas.

**Exemplo 1: Listar todos os conceitos**

```dataview
TABLE without id file.link as "Conceito"
FROM "wiki/concepts"
WHERE type = "concept"
SORT last_updated DESC
```

**Exemplo 2: Páginas atualizadas recentemente**

```dataview
TABLE file.link as "Página", last_updated as "Atualizado"
FROM "wiki"
WHERE last_updated
SORT last_updated DESC
LIMIT 10
```

**Exemplo 3: Páginas por tag**

```dataview
LIST
FROM "wiki"
WHERE contains(tags, "attention")
```

**Por que usar?**
- Visões dinâmicas do wiki
- Queries poderosas sem escrever código
- Útil para revisar, encontrar páginas desatualizadas

### 3. Canvas (Opcional)

**Instalação**
```
Settings → Community Plugins → Browse → Search "Canvas"
```

**Uso**
Mapas visuais de conexões entre conceitos.

**Como criar**
1. Comando: `Ctrl+N` → "Create new canvas"
2. Arraste arquivos do explorer para o canvas
3. Conecte com linhas
4. Agrupe em clusters por tema

**Exemplo de uso**
- Canvas de "Transformer Architecture" com todos os componentes conectados
- Canvas de "Conhecimento em Evolução" mostrando como conceitos se conectam ao longo do tempo

### 4. Marp (Opcional, para apresentações)

**Instalação**
```
Settings → Community Plugins → Browse → Search "Marp"
```

**Uso**
Criar apresentações (slides) em markdown.

**Exemplo**
```markdown
---
marp: true
theme: gaia
paginate: true
---

# Transformer Architecture

## Components

1. Encoder
2. Decoder
3. Attention Mechanism

---

# Attention Mechanism

---

Thank you!
```

**Exportar**
Comando: `Ctrl+P` → "Marp: Export to PDF/HTML"

### 5. Advanced Tables (Recomendado)

**Instalação**
```
Settings → Community Plugins → Browse → Search "Advanced Tables"
```

**Uso**
Edição de tabelas mais poderosa.

**Funcionalidades**
- `Tab`: próxima célula
- `Enter`: nova linha abaixo
- `Ctrl+Enter`: nova linha acima
- `Alt+Seta esquerda/direita`: mover coluna
- `Ctrl+Alt+Seta cima/baixo`: mover linha

## Padrões de Uso do Obsidian

### 1. Trabalho com o LLM

**Fluxo típico**:

```
1. Obsidian aberto à esquerda
   - Navega wiki, segue links, lê páginas

2. LLM aberto à direita (terminal/chat)
   - Você pergunta, LLM responde

3. LLM faz edições no wiki
   - LLM: "Atualizei wiki/concepts/self-attention.md"
   - Você: Vê atualização em tempo real no Obsidian

4. Você revisa
   - Clica em `Ctrl+Shift+O` → digita "self-attention" → vai para página
   - Lê atualização
   - Retorna ao LLM: "Parece bom, mas adicione X"

5. LLM ajusta
   - LLM: "Adicionei X na página"
   - Você: Vê ajuste em tempo real
```

**Hotkeys úteis**:
```
Ctrl+Shift+O    → Quick switcher (trocar página rápido)
Ctrl+Click      → Abrir link em painel lateral
Ctrl+E          → Modo leitura (limpo)
Ctrl+Shift+E   → Modo edição
```

### 2. Navegação do Wiki

**Página inicial**: `wiki/index.md`
- Catálogo de tudo no wiki
- Comece aqui quando quer explorar

**Graph View**: `Ctrl+G`
- Conexões visuais
- Útil para ver comunidades e hubs

**Backlinks**: Painel lateral direito
- Páginas que linkam para a página atual
- Útil para ver contexto

**Outlinks**: Painel lateral esquerdo (Links)
- Páginas que a página atual linka
- Útil para seguir contexto

**Local Graph**: Botão no canto superior direito de cada página
- Conexões da página atual apenas
- Menos clutter que Graph View global

### 3. Busca e Descoberta

**Busca global**: `Ctrl+Shift+F`
- Busca em todo wiki
- Útil para encontrar conceitos específicos

**Busca em tags**: `tag:attention` na busca global
- Encontra todas as páginas com tag "attention"

**Busca em frontmatter**: Use Dataview
```dataview
TABLE file.link as "Página", type as "Tipo", last_updated as "Atualizado"
FROM "wiki"
WHERE type = "concept" AND contains(tags, "attention")
SORT last_updated DESC
```

**Quick switcher**: `Ctrl+Shift+O`
- Digita nome da página (fuzzy search)
- Útil para ir direto a página específica

### 4. Revisão e Edição

**Modo leitura**: `Ctrl+E`
- Visual limpo para revisão
- Sem formatação markdown visível

**Modo edição**: `Ctrl+Shift+E`
- Vê markdown raw
- Útil para ajustes manuais

**Diff de mudanças**: Comando: `Ctrl+P` → "Open diff view"
- Compara versão atual com versão anterior
- Útil para ver o que o LLM mudou

**Split view**: `Ctrl+\`
- Abre mesmo arquivo em dois painéis
- Um em modo leitura, um em modo edição
- Útil para revisar ao mesmo tempo que edita

## Git Integration

### 1. Configurar Git

```bash
cd [seu-wiki-obsidian]
git init
git add .
git commit -m "Initial commit: wiki structure"
```

### 2. Comandos Úteis

**Ver mudanças do LLM**:
```bash
git status        → Arquivos modificados pelo LLM
git diff          → O que mudou
git diff wiki/concepts/self-attention.md → Mudanças em página específica
```

**Reverter mudanças do LLM**:
```bash
git checkout wiki/concepts/self-attention.md → Reverte para última versão commitada
```

**Histórico de uma página**:
```bash
git log --oneline wiki/concepts/self-attention.md → Histórico de commits da página
```

### 3. Padrão de Commits

**Commits diários** (automatizado, opcional):
```bash
git add wiki/
git commit -m "Update wiki: $(date +'%Y-%m-%d')"
```

**Commits por ingestão de fonte** (manual):
```bash
git add raw/papers/novo-paper.md wiki/
git commit -m "Add source: Self-Attention with Relative Position Representations"
```

**Commits por consulta/arquivamento** (manual):
```bash
git add wiki/synthesis/comparativa-attention.md
git commit -m "Archive query: Comparison of positional encoding approaches"
```

## Padrões de Frontmatter YAML

### Obrigatório (todas as páginas)

```yaml
---
type: concept  # ou: entity, source, synthesis, comparison
tags: [attention, neural-networks, optimization]
last_updated: 2026-04-21
sources_count: 3
---
```

### Opcional (conforme necessário)

```yaml
---
type: concept
tags: [...]
last_updated: 2026-04-21
sources_count: 3

# Para páginas de conceito
related_concepts: [Positional Encoding, Self-Attention]
related_entities: [Google Brain, OpenAI]
difficulty: intermediate
# difficulty: beginner | intermediate | advanced

# Para páginas de entidade
related_entities: [Google, OpenAI, Anthropic]
related_people: [Vaswani, Ashish]
related_concepts: [Attention, Self-Attention]

# Para páginas de síntese
query_date: 2026-04-21
related_queries: [position encoding comparison, attention optimization]
related_sources: [raw/papers/attention-is-all-you-need.pdf]

# Para páginas de fonte
original_title: "Attention Is All You Need"
original_authors: [Vaswani, Ashish]
original_date: 2017-06-12
url: https://arxiv.org/abs/1706.03762
---
```

## Padrões de Links

### Links Bidirecionais (Obrigatório)

**Se cria link A → B, também crie B → A**

**Exemplo**:
```markdown
# Positional Encoding

## Relacionamentos
- [[Self-Attention]] → é usado em
- [[Relative Positional Encoding]] ← variação deste
```

```markdown
# Self-Attention

## Relacionamentos
- [[Positional Encoding]] → é usado com
- [[Multi-Head Attention]] → é usado em
```

**Por que?**
- Navegação bidirecional mais natural
- Obsidian mostra backlinks automaticamente
- Wiki fica mais interconectado

### Links com Texto

**Boa prática**: Usar link limpo quando possível, texto quando necessário

**Link limpo**:
```markdown
Veja [[Positional Encoding]] para detalhes.
```

**Link com texto**:
```markdown
Veja [a versão relativa]([[Relative Positional Encoding]]) para detalhes.
```

### Links para Arquivos Raw

**Padrão**: `[[raw/papers/nome-do-paper.pdf]]`

**Por que?**
- Fácil encontrar fonte original
- LLM pode rastrear citações

**Exemplo**:
```markdown
## Fontes
1. [[Attention Is All You Need]] (raw/papers/attention-is-all-you-need.pdf)
```

## Troubleshooting

### Problema: Links Quebrados

**Sintoma**: Link `[[X]]` aparece vermelho (arquivo não existe)

**Causa**: LLM criou link para página que não existe

**Solução 1**: Criar página
```
Comando: Ctrl+N → Criar nova página → Nome: X
```

**Solução 2**: Atualizar link
```markdown
Mudar: [[X]] → [[Y]]  (ou remover link)
```

**Prevenção**: Pedir ao LLM para verificar links durante manutenção

### Problema: Imagens não Carregam

**Sintoma**: `![[imagem.png]]` aparece quebrado

**Causa**: Imagem não foi baixada (ainda está como URL)

**Solução**: Usar Obsidian Web Clipper + Hotkey
```
1. Re-abra artigo original no navegador
2. Use Web Clipper novamente
3. Salve na mesma pasta
4. Pressione Ctrl+Shift+D para baixar imagens
```

**Prevenção**: Sempre usar Web Clipper + Ctrl+Shift+D

### Problema: Graph View muito Crowded

**Sintoma**: Muitos nós e conexões, impossível navegar

**Causa**: Wiki grande, Graph View mostrando tudo

**Solução 1**: Usar Local Graph
```
Botão no canto superior direito da página → Mostra apenas conexões da página atual
```

**Solução 2**: Filtrar por tags
```
Settings → Graph View → Groups → By tags
Configura: Mostrar apenas tags específicas (ex: "attention", "transformer")
```

**Solução 3**: Limitar número de hops
```
Settings → Graph View → Number of hops → 1 (ou 2)
```

### Problema: Dataview queries lentas

**Sintoma**: Queries Dataview demoram segundos para carregar

**Causa**: Wiki grande, Dataview precisa ler todos os arquivos

**Solução 1**: Limitar resultados
```dataview
TABLE file.link
FROM "wiki"
WHERE type = "concept"
SORT last_updated DESC
LIMIT 20  ← Limite a 20 resultados
```

**Solução 2**: Filtrar por pasta
```dataview
TABLE file.link
FROM "wiki/concepts"  ← Apenas uma pasta
WHERE type = "concept"
SORT last_updated DESC
```

**Solução 3**: Usar índices
```dataview
TABLE file.link
FROM "wiki"
WHERE type = "concept" AND file.ctime >= date(today) - dur(30 days)  ← Apenas últimos 30 dias
SORT last_updated DESC
```

---

**Próximo**: Ferramentas: Busca qmd