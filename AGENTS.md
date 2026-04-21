# Agent Instructions

## Graphify Knowledge Graph

Este projeto usa **graphify** para criar uma rede de conhecimento interconectada.

### 📊 Como funciona

Graphify lê os arquivos em `raw/`, extrai conceitos e relacionamentos, e constrói um grafo de conhecimento.

**IMPORTANTE:** Antes de responder perguntas arquiteturais ou sobre o códigobase:
1. Verifique se existe `graphify-out/GRAPH_REPORT.md`
2. Leia este arquivo primeiro
3. Use-o como mapa de navegação
4. Prefira a estrutura do grafo ao invés de pesquisar arquivos cru

### 🎯 Arquivos importantes

- `graphify-out/GRAPH_REPORT.md` - Resumo executivo (SEMPRE comece aqui!)
  - Nós de Deus: conceitos centrais
  - Conexões Surpreendentes: relações não óbvias
  - Perguntas Sugeridas: perguntas que o grafo pode responder

- `graphify-out/wiki/index.md` - Wiki navegável por comunidade

- `graphify-out/graph.json` - Grafo persistente para queries avançadas

### 🔍 Como navegar o conhecimento

**Para perguntas gerais:**
1. Leia `GRAPH_REPORT.md` primeiro
2. Identifique as comunidades relevantes
3. Explore a wiki em `graphify-out/wiki/`

**Para perguntas específicas:**
```bash
/graphify query "como X se conecta a Y?"
/graphify query "quais padrões influenciam Z?"
/graphify path "Conceito A" "Conceito B"
/graphify explain "Conceito C"
```

### 📁 Estrutura de conteúdo

- `raw/patterns/` - Padrões de design e arquitetura
- `raw/practices/` - Práticas recomendadas
- `raw/docs/` - Documentação técnica
- `raw/guidelines/` - Diretrizes e padrões de equipe
- `raw/tutorials/` - Tutoriais e guias
- `raw/media/` - Imagens, diagramas, vídeos, PDFs

### 🔄 Atualização

Quando o conteúdo muda, execute:
```bash
/graphify ./raw --update
```

Para recriar do zero:
```bash
rm -rf graphify-out/cache/
/graphify ./raw
```

### 💡 Padrões de uso

**Estudo:**
"Quais são os padrões que conectam autenticação e autorização?"
→ Consulte o grafo primeiro, use caminhos traçados

**Descoberta:**
"Existem práticas não óbvias que afetam performance?"
→ Use as "Conexões Surpreendentes" do GRAPH_REPORT.md

**Onboarding:**
"Como começar a estudar este tópico?"
→ Comece pelos nós de Deus em GRAPH_REPORT.md

### 🎯 Princípios de design da base de conhecimento

1. **Conexões sobre conteúdo**: O valor está nas relações, não apenas no conteúdo
2. **Contexto em camadas**: Grafo → Wiki → Conteúdo detalhado
3. **Descoberta ativa**: O grafo revela conexões que você nem sabia que existiam
4. **Evolução contínua**: Cada novo arquivo pode revelar novas relações

### 🚨 Não faça

- ❌ Não leia todos os arquivos crus para responder perguntas arquiteturais
- ❌ Não adivinhe relações - use o grafo
- ❌ Não ignore o GRAPH_REPORT.md
- ❌ Não faça grep massivo quando o grafo tem a resposta

### ✅ Faça sempre

- ✅ Comece lendo GRAPH_REPORT.md para perguntas arquiteturais
- ✅ Use `/graphify query` para perguntas específicas
- ✅ Trace caminhos no grafo (`/graphify path`)
- ✅ Consulte o grafo antes de sugerir mudanças estruturais

---

**Lembre-se:** Esta é uma rede de conhecimento, não apenas um repositório de documentos. As conexões são tão importantes quanto o conteúdo!
