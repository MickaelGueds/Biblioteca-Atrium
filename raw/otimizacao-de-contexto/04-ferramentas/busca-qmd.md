# Busca qmd - Local Search Engine

## Visão Geral

qmd é um motor de busca local para arquivos markdown com busca híbrida BM25/vetorial e re-ranking por LLM. Roda no seu computador, sem enviar dados para a nuvem.

## Por que Usar?

### Busca em Arquivos vs Busca em Index

**Pequeno wiki (50-100 páginas)**:
```
wiki/index.md é suficiente
→ LLM lê index, encontra páginas relevantes
→ Funciona bem
```

**Wiki médio (100-500 páginas)**:
```
wiki/index.md começa a ficar lento
→ LLM precisa ler muito para encontrar
→ qmd ajuda (opcional)
```

**Wiki grande (500+ páginas)**:
```
wiki/index.md é insuficiente
→ LLM precisa ler centenas de páginas
→ qmd é essencial
```

### qmd vs Busca do Obsidian

| Aspecto | Obsidian Search | qmd |
|---------|----------------|-----|
| Busca vetorial | Não | Sim |
| Re-ranking LLM | Não | Sim |
| CLI para LLM usar | Não | Sim |
| API/MCP server | Não | Sim |
| Busca semântica | Não | Sim |
| Busca BM25 (palavras-chave) | Sim | Sim |

**qmd é melhor quando**:
- Wiki é grande (500+ páginas)
- Precisa de busca semântica (não só palavras-chave)
- LLM precisa fazer buscas programaticamente (CLI)
- Precisa de re-ranking inteligente

## Instalação

### Via pip (recomendado)

```bash
pip install qmd
```

### Via pipx (para isolamento)

```bash
pipx install qmd
```

### Verificar instalação

```bash
qmd --version
# Saída esperada: qmd 0.x.x
```

## Configuração Inicial

### 1. Criar Configuração

Crie arquivo `qmd_config.json` na raiz do seu wiki:

```json
{
  "index_path": ".qmd_index",
  "files": [
    "wiki/**/*.md"
  ],
  "exclude": [
    "wiki/log.md",
    "wiki/.obsidian/**"
  ],
  "embedding_model": "all-MiniLM-L6-v2",
  "rerank": true,
  "rerank_model": "cross-encoder"
}
```

### 2. Indexar Wiki

```bash
qmd index --config qmd_config.json
```

**Saída esperada**:
```
Indexing wiki/**/*.md...
Found 147 files
Indexing: 100%|████████████| 147/147 [00:15<00:00]
Index saved to .qmd_index
```

### 3. Testar Busca

```bash
qmd search --config qmd_config.json "positional encoding"
```

**Saída esperada**:
```
Top 5 results for "positional encoding":
1. wiki/concepts/positional-encoding.md (score: 0.92)
   Relative Positional Encoding is a variation...
2. wiki/concepts/relative-positional-encoding.md (score: 0.88)
   Absolute Positional Encoding is the standard...
3. wiki/synthesis/positional-encoding-comparison.md (score: 0.85)
   Comparison of Absolute and Relative...
4. wiki/comparisons/positional-encoding-variants.md (score: 0.82)
   Trade-offs between different approaches...
5. wiki/sources/attention-is-all-you-need.md (score: 0.79)
   The original paper that introduced...
```

## Uso via CLI

### Busca Simples

```bash
qmd search --config qmd_config.json "positional encoding"
```

### Busca com N resultados

```bash
qmd search --config qmd_config.json "positional encoding" --top 10
```

### Busca em modo verbose

```bash
qmd search --config qmd_config.json "positional encoding" --verbose
```

### Re-indexar (após mudanças no wiki)

```bash
# Opção 1: Re-indexar tudo
qmd index --config qmd_config.json --force

# Opção 2: Indexar apenas arquivos modificados
qmd index --config qmd_config.json
```

### Busca com filtros

```bash
# Apenas em pasta específica
qmd search --config qmd_config.json "attention" --filter "wiki/concepts"

# Apenas por tipo (usa frontmatter YAML)
qmd search --config qmd_config.json "attention" --filter "type:concept"
```

## Uso via API Python

### Configuração

```python
from qmd import QMD

qmd = QMD(config_path="qmd_config.json")
qmd.index()  # Indexar se necessário
```

### Busca Simples

```python
results = qmd.search("positional encoding")

for result in results:
    print(f"{result['path']}: {result['score']}")
    print(f"  {result['snippet'][:100]}...")
```

### Busca com Parâmetros

```python
results = qmd.search(
    query="positional encoding",
    top_k=10,           # Retornar top 10 resultados
    rerank=True,        # Usar re-ranking (padrão: True)
    filters={"type": "concept"}  # Filtrar por tipo
)
```

### Busca com Contexto

```python
results = qmd.search(
    query="positional encoding",
    return_context=True  # Incluir contexto completo
)

for result in results:
    print(f"File: {result['path']}")
    print(f"Score: {result['score']}")
    print(f"Context:")
    print(result['context'])
```

## Integração com LLM

### Opção 1: LLM usa CLI direto

**No schema (CLAUDE.md / AGENTS.md)**:

```markdown
## Como Fazer Buscas

Para fazer buscas no wiki, use qmd CLI:

```bash
qmd search --config qmd_config.json "[QUERY]" --top 5
```

Exemplo:
```bash
qmd search --config qmd_config.json "positional encoding" --top 5
```

Analise os resultados e leia os arquivos relevantes antes de responder.
```

**Quando usar**: CLI é suficiente, não precisa de re-ranking avançado

### Opção 2: LLM usa API Python via subprocess

**No schema**:

```markdown
## Como Fazer Buscas

Para fazer buscas no wiki, use qmd via Python script:

```python
import subprocess
import json

def search_wiki(query, top_k=5):
    cmd = f"""python3 <<'EOF'
import qmd
qmd_search = qmd.QMD(config_path="qmd_config.json")
results = qmd_search.search(query, top_k=top_k)
for r in results:
    r['content'] = open(r['path']).read()
print(json.dumps(results))
EOF"""
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)
    return json.loads(result.stdout)
```

Use assim:
```python
results = search_wiki("positional encoding", top_k=5)
for r in results:
    print(f"{r['path']}: {r['score']}")
    print(r['content'][:200] + "...")
```

Analise os resultados e o conteúdo dos arquivos antes de responder.
```

**Quando usar**: Precisa de conteúdo completo dos arquivos (não só snippet)

### Opção 3: LLM usa API Python nativa

**No schema**:

```markdown
## Como Fazer Buscas

Para fazer buscas no wiki, use qmd API Python:

```python
from qmd import QMD

# Inicializar
qmd = QMD(config_path="qmd_config.json")
qmd.index()  # Indexar se necessário

# Buscar
results = qmd.search(
    query="positional encoding",
    top_k=5,
    rerank=True,
    filters={"type": "concept"}
)

# Ler conteúdo
for result in results:
    result['content'] = open(result['path']).read()

# Agora você tem: path, score, content, snippet
```

Use assim:
```python
results = qmd.search("positional encoding", top_k=5)
for r in results:
    print(f"=== {r['path']} (score: {r['score']}) ===")
    print(r['content'])
```

Analise os resultados e o conteúdo dos arquivos antes de responder.
```

**Quando usar**: Mais controle, melhor performance, re-ranking avançado

## Exemplo de Integração Completa

### Fluxo de Consulta com qmd

**Schema**:

```markdown
## Fluxo de Consulta ao Wiki

Quando receber uma pergunta:

1. **Identificar termos-chave**
   - Extraia 3-5 termos da pergunta
   - Exemplo: "positional encoding", "attention", "trade-offs"

2. **Buscar com qmd**
   ```python
   results = qmd.search(query="positional encoding attention trade-offs", top_k=10)
   ```

3. **Ler conteúdo relevante**
   - Para cada resultado com score > 0.7:
   ```python
   content = open(result['path']).read()
   ```

4. **Sintetizar resposta**
   - Use conteúdo dos arquivos relevantes
   - Cite fontes com formato [[Nome da Fonte]] (raw/path/to/source.md)

5. **Cruzar referências**
   - Se uma página cita outra, leia também
   - Use links bidirecionais para contexto

Exemplo completo:
```python
from qmd import QMD

# 1. Buscar
qmd = QMD(config_path="qmd_config.json")
results = qmd.search("positional encoding trade-offs", top_k=10)

# 2. Filtrar por score
relevant = [r for r in results if r['score'] > 0.7]

# 3. Ler conteúdo
for r in relevant:
    r['content'] = open(r['path']).read()

# 4. Sintetizar (você faz isso)
# [sua lógica de síntese]
```

Sempre cite as fontes usadas na resposta.
```

### LLM Seguindo o Fluxo

```
Você: "Quais são os trade-offs entre Absolute e Relative Positional Encoding?"

LLM processa:

1. **Identificar termos-chave**:
   - "positional encoding"
   - "absolute"
   - "relative"
   - "trade-offs"

2. **Buscar com qmd**:
   ```python
   results = qmd.search("positional encoding absolute relative trade-offs", top_k=10)
   ```

   Resultados:
   - wiki/concepts/positional-encoding.md (score: 0.94)
   - wiki/concepts/relative-positional-encoding.md (score: 0.91)
   - wiki/comparisons/positional-encoding-variants.md (score: 0.89)
   - wiki/synthesis/positional-encoding-comparison.md (score: 0.87)

3. **Ler conteúdo relevante**:
   - Ler wiki/concepts/positional-encoding.md
   - Ler wiki/concepts/relative-positional-encoding.md
   - Ler wiki/comparisons/positional-encoding-variants.md
   - Ler wiki/synthesis/positional-encoding-comparison.md

4. **Sintetizar resposta**:
   [Resposta detalhada com comparação e trade-offs]

5. **Citar fontes**:
   - [[Positional Encoding]] (wiki/concepts/positional-encoding.md)
   - [[Relative Positional Encoding]] (wiki/concepts/relative-positional-encoding.md)
   - [[Positional Encoding Variants Comparison]] (wiki/comparisons/positional-encoding-variants.md)
```

## Comparação: qmd vs wiki/index.md

### wiki/index.md (Pequeno Wiki)

**Vantagens**:
- Simples, sem configuração
- LLM já lê markdown (não precisa de ferramenta externa)
- Rápido para wikis pequenos (50-100 páginas)

**Desvantagens**:
- Lento para wikis grandes (500+ páginas)
- Não tem busca semântica
- Não tem re-ranking

**Quando usar**: Wiki pequeno (50-100 páginas)

### qmd (Médio/Grande Wiki)

**Vantagens**:
- Rápido mesmo para wikis grandes (1000+ páginas)
- Busca semântica (vetorial)
- Re-ranking por LLM
- CLI/API para integração

**Desvantagens**:
- Requer instalação e configuração
- Requer re-indexar após mudanças
- Curva de aprendizado

**Quando usar**: Wiki médio (100-500 páginas) ou grande (500+ páginas)

## Boas Práticas

### 1. Re-indexar Após Mudanças Importantes

**Quando**:
- Após adicionar 10+ novas fontes
- Após grandes reestruturações do wiki
- Após criar/alterar muitas páginas

**Comando**:
```bash
qmd index --config qmd_config.json --force
```

### 2. Usar Filtros para Buscas Específicas

**Exemplo**: Buscar apenas em conceitos
```bash
qmd search --config qmd_config.json "attention" --filter "wiki/concepts"
```

**Exemplo**: Buscar apenas por tipo (frontmatter)
```bash
qmd search --config qmd_config.json "attention" --filter "type:concept"
```

### 3. Usar Re-ranking para Resultados Melhores

**Sem re-ranking**:
```bash
qmd search --config qmd_config.json "positional encoding" --no-rerank
```

**Com re-ranking** (padrão):
```bash
qmd search --config qmd_config.json "positional encoding"
```

**Quando usar re-ranking**:
- Precisa de alta precisão
- Query é ambígua
- Wiki é grande

### 4. Ajustar Top-K Conforme Necessidade

**Wiki pequeno**: `--top 5` (padrão)
**Wiki médio**: `--top 10`
**Wiki grande**: `--top 20`

```bash
qmd search --config qmd_config.json "attention" --top 20
```

### 5. Monitorar Performance

**Verificar tempo de indexação**:
```bash
time qmd index --config qmd_config.json
```

**Verificar tempo de busca**:
```bash
time qmd search --config qmd_config.json "positional encoding"
```

**Se estiver lento**:
- Aumentar `embedding_model` (modelo mais rápido)
- Diminuir `top_k`
- Usar filtros para reduzir escopo

## Troubleshooting

### Problema: "Index corrupted"

**Sintoma**: Erro ao buscar: "Index corrupted"

**Causa**: Arquivos deletados ou movidos após indexação

**Solução**:
```bash
qmd index --config qmd_config.json --force
```

### Problema: Busca retorna resultados irrelevantes

**Sintoma**: Top resultados não têm relação com query

**Causa 1**: Query muito genérica
**Solução**: Seja mais específico
```bash
# Ruim
qmd search "transformer"

# Bom
qmd search "transformer attention mechanism positional encoding"
```

**Causa 2**: Re-ranking desativado
**Solução**: Ative re-ranking
```bash
qmd search --config qmd_config.json "positional encoding" --rerank
```

**Causa 3**: Wiki precisa ser re-indexado
**Solução**: Re-indexe
```bash
qmd index --config qmd_config.json --force
```

### Problema: qmd não encontra arquivos

**Sintoma**: qmd retorna 0 resultados quando deveria retornar

**Causa 1**: Configuração de `files` incorreta
**Solução**: Verifique `qmd_config.json`
```json
{
  "files": ["wiki/**/*.md"]  ← Caminho correto?
}
```

**Causa 2**: Arquivos excluídos
**Solução**: Verifique `exclude` em `qmd_config.json`
```json
{
  "exclude": [
    "wiki/log.md",
    "wiki/.obsidian/**"
  ]  ← Não está excluindo algo que não deveria?
}
```

**Causa 3**: Arquivos não foram indexados
**Solução**: Indexe novamente
```bash
qmd index --config qmd_config.json --force
```

### Problema: qmd está lento

**Sintoma**: Indexação ou busca demoram minutos

**Causa 1**: Modelo de embedding muito pesado
**Solução**: Use modelo mais leve
```json
{
  "embedding_model": "all-MiniLM-L6-v2"  ← Modelo leve
}
```

**Causa 2**: Wiki muito grande (2000+ páginas)
**Solução**: Considere particionar wiki em múltiplos índices
```json
{
  "files": ["wiki/concepts/**/*.md"]  ← Apenas conceitos
}
```

**Causa 3**: Hardware limitado
**Solução**: Diminua top_k, use re-ranking apenas quando necessário

---

**Próximo**: Ferramentas: Marp