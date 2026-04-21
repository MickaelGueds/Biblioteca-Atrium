# Onboarding - Começando com o Cognexus

## 📋 Visão geral

Tutorial para começar a usar o Cognexus Knowledge Base powered by graphify. Você vai aprender a construir o grafo inicial, navegar pelo conhecimento, e adicionar novos conteúdos.

## 🎯 Objetivos de aprendizado

Ao final deste tutorial, você será capaz de:
- Construir o grafo de conhecimento inicial
- Navegar pelo GRAPH_REPORT.md para descobrir conceitos centrais
- Usar queries para encontrar relações específicas
- Adicionar novos conteúdos e atualizar o grafo

## ⏱️ Tempo estimado

- Leitura: 10 minutos
- Prática: 20 minutos
- Total: 30 minutos

## 📚 Pré-requisitos

Conhecimentos necessários:
- Uso básico de terminal/bash

Ferramentas necessárias:
- graphify instalado: `pip install graphifyy`
- OpenCode, Claude Code, ou outro assistente de IA configurado

## 🚀 Passo a passo

### Passo 1: Prepare o ambiente

Primeiro, certifique-se de que está no diretório do projeto:

```bash
cd ~/Atrium_Knowledge
```

Verifique a estrutura:

```bash
ls -la
```

Você deve ver as pastas `raw/`, `graphify-out/`, `templates/`, etc.

### Passo 2: Construa o grafo inicial

Execute o graphify no conteúdo existente:

```bash
/graphify ./raw --wiki --obsidian
```

O que isso faz:
- Lê todos os arquivos em `raw/`
- Extrai conceitos e relacionamentos
- Constrói um grafo NetworkX
- Aplica clustering Leiden para detectar comunidades
- Gera wiki navegável em `graphify-out/wiki/`
- Cria vault do Obsidian em `graphify-out/obsidian/`

### Passo 3: Entenda o GRAPH_REPORT.md

O arquivo mais importante é `graphify-out/GRAPH_REPORT.md`. Leia-o:

```bash
cat graphify-out/GRAPH_REPORT.md
```

O que você vai encontrar:

**🔥 God Nodes (Nós de Deus)**
- Conceitos centrais com muitas conexões
- Comece por aqui para entender a base de conhecimento
- Ex: "Graphify", "Knowledge Graph", "Maintenance"

**🔗 Surprising Connections (Conexões Surpreendentes)**
- Relações não óbvias que o grafo descobriu
- Ranqueadas por score de relevância
- Ex: Como "Graphify" se conecta a "Repository Pattern"

**❓ Suggested Questions (Perguntas Sugeridas)**
- Perguntas que o grafo está posicionado para responder
- Use-as como ponto de partida para exploração

### Passo 4: Navegue pela wiki gerada

O graphify gera uma wiki Wikipedia-style em `graphify-out/wiki/`:

```bash
ls graphify-out/wiki/
```

Você verá:
- `index.md` - Índice principal
- `{community}.md` - Artigo por comunidade detectada

Leia o índice:

```bash
cat graphify-out/wiki/index.md
```

Isso mostra como o conteúdo foi organizado em comunidades automaticamente.

### Passo 5: Faça queries no grafo

Use queries para descobrir relações específicas:

```bash
# Pergunta geral
/graphify query "como graphify se conecta a padrões de conhecimento?"

# Caminho específico entre dois conceitos
/graphify path "Graphify" "Repository"

# Explicação de um conceito
/graphify explain "Knowledge Graph"
```

Cada query mostra:
- Nós envolvidos
- Tipo de relação
- Score de confiança
- Fonte (arquivo onde foi encontrado)

### Passo 6: Visualize o grafo interativo

Abra a visualização no navegador:

```bash
firefox graphify-out/graph.html
# ou
xdg-open graphify-out/graph.html
```

Na visualização:
- Clique em nós para ver detalhes
- Arraste para reorganizar
- Use a busca para encontrar conceitos
- Filtre por comunidade

### Passo 7: Adicione novo conteúdo

Vamos adicionar um novo padrão usando o template:

```bash
cp templates/pattern.md raw/patterns/meu-primeiro-padrao.md
```

Edite o arquivo:

```bash
vim raw/patterns/meu-primeiro-padrao.md
# ou use seu editor preferido
```

Preencha pelo menos:
- Nome do padrão
- Visão geral (o que faz)
- Problema (resolve o quê?)
- Solução (como funciona)

### Passo 8: Atualize o grafo

Agora que adicionou novo conteúdo, atualize o grafo:

```bash
/graphify ./raw --update
```

O parâmetro `--update`:
- Usa cache SHA256
- Reprocessa apenas arquivos alterados
- Mescla no grafo existente
- Muito mais rápido que reconstruir do zero

Verifique as mudanças:

```bash
cat graphify-out/GRAPH_REPORT.md
```

Procure:
- Novas conexões
- Conceitos atualizados
- Perguntas sugeridas alteradas

### Passo 9: Configure atualização automática (opcional)

Para automatizar atualizações após commits git:

```bash
graphify hook install
```

Agora, cada vez que você commitar mudanças no conteúdo, o grafo se atualiza automaticamente.

### Passo 10: Integre com Obsidian (opcional)

Se você usa Obsidian, já gerou o vault:

```bash
ls graphify-out/obsidian/
```

Abra o Obsidian e aponte para esta pasta. Você terá:
- Arquivos markdown por nó/conceito
- Links bidirecionais [[ ]]
- Integração com plugins do Obsidian

## ✅ Verificação

Para confirmar que você completou o tutorial:

- [ ] Grafo construído com sucesso (`graphify-out/graph.json` existe)
- [ ] Leu e entendeu `GRAPH_REPORT.md`
- [ ] Navegou pela wiki em `graphify-out/wiki/`
- [ ] Fez pelo menos uma query com sucesso
- [ ] Visualizou o grafo no navegador
- [ ] Adicionou novo conteúdo em `raw/`
- [ ] Atualizou o grafo com `--update`
- [ ] (Opcional) Configurou hooks do git

## 🐛 Solução de problemas

| Problema | Causa provável | Solução |
|----------|---------------|---------|
| "command not found: graphify" | graphify não instalado | `pip install graphifyy` |
| "No such file: graphify-out/" | Grafo não construído | Execute `/graphify ./raw` |
| Queries retornam vazio | Conteúdo insuficiente | Adicione mais arquivos em `raw/` |
| Custo de tokens alto | Primeira execução | Updates subsequentes são muito mais baratos |
| Conexões não fazem sentido | Precisa de mais contexto | Use `--mode deep` para inferência mais agressiva |

## 💡 Dicas

- **Comece pelo GRAPH_REPORT.md**: É o mapa de navegação principal
- **Use queries específicas**: `graphify query` é mais eficiente que grep
- **Adicione conteúdo gradualmente**: Não precisa tudo de uma vez
- **Visualize o grafo**: Muitas vezes connections ficam óbvias visualmente
- **Mantenha templates**: Usam templates em `templates/` para consistência

## 📖 Leitura adicional

- [graphify README completo](https://github.com/safishamsi/graphify)
- [graphify CLI docs](https://github.com/safishamsi/graphify#usage)
- [NetworkX docs](https://networkx.org/documentation/stable/)

## 🔗 Conceitos relacionados

- [[Pattern: Graphify as Knowledge Center]]: O padrão subjacente
- [[Practice: Continuous Graph Maintenance]]: Como manter atualizado
- [[Tutorial: Advanced Graph Queries]]: Queries mais complexas (próximo tutorial)

## 📝 Notas

Este tutorial foca no fluxo básico. Tópicos avançados incluem:
- Queries complexas com `--dfs` e `--budget`
- Integração MCP para automatização
- Clustering customizado
- Exportação para Neo4j ou GraphML

## 🏷️ Tags

`#tutorial #onboarding #graphify #beginner`
