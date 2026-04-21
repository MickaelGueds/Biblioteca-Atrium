# 📦 Estrutura Completa da Pasta Otimização de Contexto

## 🗂️ Estrutura de Arquivos

```
otimizacao-de-contexto/
├── README.md                                    ← Guia rápido para começar
│
├── 01-conceitos/                                ← Fundamentos
│   ├── ideia-central.md                         ← Tradução completa do Karpathy
│   ├── arquitetura.md                           ← 3 camadas (Raw, Wiki, Schema)
│   └── diferenciais.md                          ← Wiki LLM vs RAG tradicional
│
├── 02-implementacao/                           ← Como usar na prática
│   ├── fluxo-ingestao.md                        ← Adicionar novas fontes
│   ├── consultas.md                             ← Fazer perguntas ao wiki
│   ├── manutencao.md                            ← Health-check e correções
│   └── indice-e-log.md                          ← Navegação no wiki
│
├── 03-casos-de-uso/                             ← Exemplos reais
│   ├── pessoal.md                               ← Autodesenvolvimento, saúde
│   ├── pesquisa.md                              ← Pesquisa acadêmica
│   ├── leitura-livros.md                        ← Wiki companheiro de livros
│   └── equipe-negocio.md                        ← Wiki interno de empresa
│
└── 04-ferramentas/                              ← Ferramentas recomendadas
    ├── obsidian.md                              ← Configuração do Obsidian
    ├── busca-qmd.md                             ← Local search engine
    ├── marp.md                                  ← Slides em markdown
    └── dataview.md                              ← Queries dinâmicas
```

## 🎯 Por Onde Começar?

### Rota 1: Curioso (Quer entender a ideia)

**Tempo**: 30 minutos

1. `README.md` (5 min)
   - O que é, como usar, por que funciona

2. `01-conceitos/ideia-central.md` (15 min)
   - Ideia principal completa
   - Casos de uso

3. `01-conceitos/arquitetura.md` (10 min)
   - 3 camadas explicadas
   - Como funciona

**Resultado**: Entende a ideia, sabe quando usar

---

### Rota 2: Prático (Quer começar a usar)

**Tempo**: 1-2 horas

1. `README.md` (5 min)
   - Visão geral

2. `02-implementacao/fluxo-ingestao.md` (30 min)
   - Como adicionar fontes
   - Como o LLM processa

3. `02-implementacao/consultas.md` (20 min)
   - Como fazer perguntas
   - Tipos de consultas

4. `04-ferramentas/obsidian.md` (30 min)
   - Configurar Obsidian
   - Instalar plugins

**Resultado**: Sabe como usar Wiki LLM, pronto para começar

---

### Rota 3: Específico (Quer aplicar a um caso específico)

**Tempo**: 1 hora

1. `README.md` (5 min)
   - Visão geral

2. Escolha um caso:
   - **Pessoal**: `03-casos-de-uso/pessoal.md` (55 min)
   - **Pesquisa**: `03-casos-de-uso/pesquisa.md` (55 min)
   - **Livros**: `03-casos-de-uso/leitura-livros.md` (55 min)
   - **Equipe**: `03-casos-de-uso/equipe-negocio.md` (55 min)

3. `02-implementacao/fluxo-ingestao.md` (opcional, se precisar)

**Resultado**: Sabe como aplicar ao seu caso específico

---

## 📊 Comparação de Rotas

| Rota | Tempo | Resultado | Pra quem é |
|------|-------|-----------|------------|
| **Curioso** | 30 min | Entende a ideia | Quer saber se vale a pena |
| **Prático** | 1-2 horas | Sabe usar | Quer começar agora |
| **Específico** | 1 hora | Sabe aplicar | Já tem caso em mente |

## 🚀 Fluxo Rápido de Início

### Passo 1: Leia README (5 min)
```
otimizacao-de-contexto/README.md
```

### Passo 2: Escolha seu caso de uso (1 min)
- [ ] Pessoal (autodesenvolvimento, saúde)
- [ ] Pesquisa (acadêmica, profissional)
- [ ] Livros (wiki companheiro)
- [ ] Equipe (wiki interno)
- [ ] Outro

### Passo 3: Leia o caso de uso correspondente (30-55 min)
```
otimizacao-de-contexto/03-casos-de-uso/[seu-caso].md
```

### Passo 4: Configure ferramentas (30 min, opcional)
```
otimizacao-de-contexto/04-ferramentas/obsidian.md
```

### Passo 5: Comece pequeno!
```
1. Adicione 1 fonte ao wiki
2. Deixe o LLM processar
3. Faça 1 pergunta
4. Expanda gradualmente
```

## 💡 Dicas de Uso

### Para Começar

1. **Comece pequeno**: 1-2 fontes, não tente processar tudo de uma vez
2. **Seja consistente**: Processar 1 fonte por dia é melhor que 10 fontes de uma vez
3. **Revisar**: Sempre revise o que o LLM cria, ajuste se necessário
4. **Iterar**: O schema (CLAUDE.md/AGENTS.md) evolui com você

### Para Crescer

1. **Automatize**: Quando o fluxo estiver estabelecido, automatize ingestão
2. **Manutenção**: Faça health-check periódico (mensalmente ou trimestralmente)
3. **Ferramentas**: Adicione ferramentas (qmd, Dataview) conforme o wiki cresce
4. **Padrões**: Desenvolva seus próprios padrões de organização

### Para Otimizar

1. **Busca eficiente**: Use qmd quando wiki for > 500 páginas
2. **Apresentações**: Use Marp para transformar wiki em slides
3. **Análises**: Use Dataview para queries dinâmicas
4. **Compartilhar**: Considere compartilhar o wiki com a equipe

## 📚 Próximos Passos

### Após Ler os Conceitos (Rota 1)

**Se a ideia faz sentido para você**:
- Vá para Rota 2 (Prático) ou Rota 3 (Específico)
- Comece com 1 fonte no wiki
- Veja como funciona na prática

**Se a ideia NÃO faz sentido**:
- Releia `01-conceitos/diferenciais.md` (comparações com RAG)
- Considere casos de uso em `03-casos-de-uso/` (exemplos reais)
- Pergunte: "Para qual caso de uso isso é útil?"

### Após Ler a Implementação (Rota 2)

**Se está pronto para começar**:
- Configure Obsidian (`04-ferramentas/obsidian.md`)
- Adicione 1 fonte ao `raw/`
- Peça ao LLM para processar

**Se precisa de mais exemplos**:
- Vá para Rota 3 (Específico)
- Escolha um caso de uso relevante
- Veja exemplos detalhados

### Após Ler Casos de Uso (Rota 3)

**Se encontrou seu caso**:
- Siga o fluxo de trabalho do caso escolhido
- Adapte para suas necessidades
- Comece pequeno, expanda gradualmente

**Se NÃO encontrou seu caso**:
- Combine múltiplos casos (ex: Pessoal + Pesquisa)
- Adapte exemplos para seu contexto
- O LLM pode ajudar a adaptar

## 🔗 Conexões Entre Seções

### Conceitos ↔ Implementação

```
01-conceitos/ideia-central.md
    ↓ Explica a ideia
02-implementacao/fluxo-ingestao.md
    ↓ Como aplicar
03-casos-de-uso/[seu-caso].md
    ↓ Exemplos reais
```

### Implementação ↔ Ferramentas

```
02-implementacao/fluxo-ingestao.md
    ↓ Precisa de ferramentas
04-ferramentas/obsidian.md
    ↓ Ferramenta principal
04-ferramentas/[outras].md
    ↓ Ferramentas adicionais
```

### Casos de Uso ↔ Ferramentas

```
03-casos-de-uso/pessoal.md
    ↓ Pode usar
04-ferramentas/dataview.md
    ← Para queries de saúde/progresso

03-casos-de-uso/equipe-negocio.md
    ↓ Pode usar
04-ferramentas/marp.md
    ← Para apresentações internas
```

## ⚡ Comandos Rápidos de Referência

### Ingestão de Fonte
```
"Adicione [arquivo] ao wiki e processe"
```

### Consulta ao Wiki
```
"Como [X] se relaciona com [Y]?"
"Quais são os trade-offs de [X]?"
"Como [X] evoluiu ao longo do tempo?"
```

### Manutenção
```
"Faça um health-check do wiki"
"Identifique páginas órfãs"
"Quais contradições existem?"
```

### Ferramentas
```
"Configure o Obsidian para wiki LLM"
"Crie uma query Dataview para [X]"
"Crie uma apresentação Marp sobre [Y]"
"Use qmd para buscar [Z] no wiki"
```

## 📊 Métricas de Progresso

### Semanal

- [ ] Fontes adicionadas: ___
- [ ] Consultas feitas: ___
- [ ] Páginas criadas/atualizadas: ___
- [ ] Health-check realizado: [ ] Sim [ ] Não

### Mensal

- [ ] Wiki cresceu: [ ] Sim [ ] Não
- [ ] Ferramentas configuradas: [ ] Sim [ ] Não
- [ ] Manutenção realizada: [ ] Sim [ ] Não
- [ ] Satisfação com wiki: ___/10

### Trimestral

- [ ] Wiki está maduro: [ ] Sim [ ] Não
- [ ] Precisa de reestruturação: [ ] Sim [ ] Não
- [ ] Valor agregado: [ ] Alto [ ] Médio [ ] Baixo
- [ ] Recomendaria para outros: [ ] Sim [ ] Não

## 🎓 Recursos Adicionais

### Fonte Original

**Wiki LLM por Andrej Karpathy**
- Link: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- Data: 4 de abril de 2026
- Tradução: `01-conceitos/ideia-central.md`

### Ferramentas

1. **Obsidian**: https://obsidian.md/
2. **qmd**: https://github.com/tobi/qmd
3. **Marp**: https://marp.app/
4. **Dataview**: https://blacksmithgu.github.io/obsidian-dataview/

### Documentação

- Obsidian: https://help.obsidian.md/
- Obsidian Graph View: https://help.obsidian.md/Plugins/Graph+view
- Obsidian Dataview: https://blacksmithgu.github.io/obsidian-dataview/query/queries/

---

## ✅ Checklist Inicial

Antes de começar:

- [ ] Li `README.md` e entendi a ideia
- [ ] Escolhi um caso de uso (pessoal, pesquisa, livros, equipe)
- [ ] Li o caso de uso correspondente em `03-casos-de-uso/`
- [ ] Configurei o Obsidian (ou outro editor markdown)
- [ ] Criei estrutura de pastas `raw/`, `wiki/`, `schema.md`
- [ ] Adicionei 1 fonte em `raw/`
- [ ] Pedi ao LLM para processar
- [ ] Fiz 1 pergunta ao wiki
- [ ] Revisei o resultado

**Se tudo isso está marcado, você está pronto para expandir!**

---

**Pronto para começar?**

Escolha sua rota:
1. **Curioso** → `01-conceitos/ideia-central.md`
2. **Prático** → `02-implementacao/fluxo-ingestao.md`
3. **Específico** → `03-casos-de-uso/[seu-caso].md`

Ou retorne ao README para começar do zero: `README.md`

---

**Criado em**: 2026-04-21
**Baseado em**: Wiki LLM por Andrej Karpathy
**Estrutura otimizada para estudos**