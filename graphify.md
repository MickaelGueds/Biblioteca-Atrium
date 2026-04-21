# Graphify — Guia Básico (para estruturar e linkar `.md`)

Graphify transforma qualquer pasta em um **grafo de conhecimento navegável**. Aqui o foco é usá-lo **apenas sobre conteúdos em markdown** — sem código — para descobrir conexões entre notas, agrupar temas e gerar um wiki linkado automaticamente.

---

## 1. Instalação

```bash
pip install graphifyy
```

Se der erro de "externally managed environment":

```bash
pip install graphifyy --break-system-packages
# ou, recomendado:
pipx install graphifyy
```

Verificar:

```bash
graphify --help
```

---

## 2. Adicionando aos agentes

### Claude Code

```bash
graphify claude install
```

Adiciona seção `## graphify` ao `CLAUDE.md`, fazendo o Claude consultar o grafo antes de responder e rebuildar após mudanças. A skill `/graphify` também já está disponível globalmente.

Remover:

```bash
graphify claude uninstall
```

### OpenCode

No `opencode.json` do projeto:

```json
{
  "commands": {
    "graphify": "graphify ."
  }
}
```

Ou rodar direto no shell integrado — o binário `graphify` está no PATH.

### Codex (OpenAI CLI)

No `~/.codex/config.toml` ou no prompt do projeto:

```toml
[project]
instructions = """
Antes de responder, leia graphify-out/GRAPH_REPORT.md.
Após adicionar/editar .md, rode: graphify update .
"""
```

---

## 3. Usando só com markdown

Graphify detecta `.md` como `docs` e extrai:

- **Conceitos nomeados** viram nós
- **Links `[[wiki]]` e menções** viram arestas `EXTRACTED`
- **Similaridade semântica** entre notas vira arestas `INFERRED`
- **Citações e referências** cruzadas viram arestas de citação
- **Comunidades temáticas** emergem automaticamente (clustering Louvain)

Basta organizar seus `.md` em pastas e rodar:

```bash
graphify .
```

Estrutura sugerida:

```
conhecimentos_tecnicos/
  otimizacao_de_contexto/
    nota1.md
    nota2.md
  outro_tema/
    ...
```

---

## 4. Comandos básicos

### Construir / atualizar

```bash
graphify .                         # pipeline completo
graphify . --wiki                  # + wiki navegável (index.md por comunidade)
graphify . --update                # incremental (só re-extrai .md novos/alterados)
graphify . --mode deep             # mais arestas inferidas (mais tokens)
graphify . --no-viz                # sem HTML, só relatório + JSON
```

### Consultar

```bash
graphify query "o que conecta otimização de contexto a RAG?"
graphify query "caminho entre nota A e nota B" --dfs
graphify path "Contexto" "Embeddings"
graphify explain "Otimização de Contexto"
```

### Adicionar fontes externas como `.md`

```bash
graphify add https://arxiv.org/abs/2301.00001      # abstract vira .md em ./raw
graphify add https://exemplo.com/artigo            # webpage convertida em markdown
```

---

## 5. Como funciona (só markdown)

1. **Detect** — classifica arquivos como `docs`.
2. **Extract (semantic)** — subagentes leem cada `.md` e extraem conceitos, citações, relações.
3. **Build + Cluster** — grafo NetworkX, detecção de comunidades temáticas.
4. **Analyze** — identifica *god nodes* (notas centrais) e *surprising connections* (pontes entre temas).
5. **Export** — `graphify-out/` com HTML, JSON, relatório e wiki.

Cada aresta é marcada como `EXTRACTED` (explícita no texto), `INFERRED` (inferida por similaridade) ou `AMBIGUOUS` (incerta) — sem invenção cega.

---

## 6. Saídas (`graphify-out/`)

| Arquivo | Uso |
|---|---|
| `GRAPH_REPORT.md` | Leia primeiro: god nodes, comunidades, perguntas sugeridas |
| `graph.html` | Exploração visual no navegador |
| `graph.json` | Dados brutos para GraphRAG / outros agentes |
| `wiki/index.md` | Ponto de entrada linkado por tema (com `--wiki`) |
| `cost.json` | Tracker de tokens gastos |

---

## 7. Fluxo recomendado para base de `.md`

```bash
# Primeira vez
graphify . --wiki

# Sempre que adicionar/editar notas
graphify . --update

# Explorar
graphify query "quais notas falam sobre X?"
graphify explain "Nome da Nota"
```
