# Graph Report - .  (2026-04-21)

## Corpus Check
- Corpus is ~3,921 words - fits in a single context window. You may not need a graph.

## Summary
- 32 nodes · 48 edges · 5 communities detected
- Extraction: 88% EXTRACTED · 12% INFERRED · 0% AMBIGUOUS · INFERRED: 6 edges (avg confidence: 0.76)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Graphify Pipeline e Outputs|Graphify Pipeline e Outputs]]
- [[_COMMUNITY_Skill Graphify-Study (Feynman + Notas)|Skill Graphify-Study (Feynman + Notas)]]
- [[_COMMUNITY_Padrao LLM Wiki (Karpathy)|Padrao LLM Wiki (Karpathy)]]
- [[_COMMUNITY_Schema do Wiki (Convencoes para LLM)|Schema do Wiki (Convencoes para LLM)]]
- [[_COMMUNITY_RAG vs Wiki Persistente|RAG vs Wiki Persistente]]

## God Nodes (most connected - your core abstractions)
1. `LLM como mantenedor de wiki pessoal` - 11 edges
2. `Wiki persistente mantido por LLM` - 7 edges
3. `Skill graphify-study` - 6 edges
4. `Graphify - Guia Basico` - 6 edges
5. `RAG vs Wiki persistente` - 5 edges
6. `Schema do Wiki (CLAUDE.md / AGENTS.md)` - 4 edges
7. `Schema (CLAUDE.md / AGENTS.md)` - 4 edges
8. `Metodo Feynman` - 4 edges
9. `Pipeline do graphify (detect-extract-build-analyze-export)` - 4 edges
10. `Por que funciona agora: LLM resolve bookkeeping` - 3 edges

## Surprising Connections (you probably didn't know these)
- `Wiki navegavel (wiki/index.md)` --semantically_similar_to--> `Wiki persistente mantido por LLM`  [INFERRED] [semantically similar]
  graphify.md → conhecimentos_tecnicos/ia/otimizacao_de_contexto/llm-wiki-pattern.md
- `Schema (CLAUDE.md / AGENTS.md)` --semantically_similar_to--> `Skill graphify-study`  [INFERRED] [semantically similar]
  conhecimentos_tecnicos/ia/otimizacao_de_contexto/schema-de-wiki.md → skills/graphify-study/SKILL.md
- `Conectar ao inves de arquivar` --semantically_similar_to--> `Wiki persistente mantido por LLM`  [INFERRED] [semantically similar]
  skills/graphify-study/SKILL.md → conhecimentos_tecnicos/ia/otimizacao_de_contexto/llm-wiki-pattern.md
- `Metodo Feynman` --semantically_similar_to--> `Divisao de trabalho humano-LLM`  [INFERRED] [semantically similar]
  skills/graphify-study/SKILL.md → conhecimentos_tecnicos/ia/otimizacao_de_contexto/llm-wiki-pattern.md
- `Arestas EXTRACTED / INFERRED / AMBIGUOUS` --semantically_similar_to--> `Obsidian graph view como diagnostico`  [INFERRED] [semantically similar]
  graphify.md → conhecimentos_tecnicos/ia/otimizacao_de_contexto/llm-wiki-pattern.md

## Hyperedges (group relationships)
- **** — llm_wiki_pattern_tres_camadas, llm_wiki_pattern_ingest_query_maintain, schema_de_wiki_schema [EXTRACTED 1.00]
- **** — skill_metodo_feynman, skill_notas_filhas, skill_active_recall, skill_template_study_note [EXTRACTED 1.00]
- **** — graphify_pipeline, graphify_god_nodes, graphify_comunidades_louvain, graphify_graph_report [EXTRACTED 1.00]

## Communities

### Community 0 - "Graphify Pipeline e Outputs"
Cohesion: 0.36
Nodes (8): Graphify - Guia Basico, Arestas EXTRACTED / INFERRED / AMBIGUOUS, Comunidades tematicas (Louvain), God nodes (notas centrais), GRAPH_REPORT.md, Pipeline do graphify (detect-extract-build-analyze-export), Wiki navegavel (wiki/index.md), Obsidian graph view como diagnostico

### Community 1 - "Skill Graphify-Study (Feynman + Notas)"
Cohesion: 0.43
Nodes (7): Skill graphify-study, Divisao de trabalho humano-LLM, Active recall (perguntas de revisao), Conectar ao inves de arquivar, Metodo Feynman, Notas filhas (decomposicao de conceitos), Template de study-note (frontmatter + secoes)

### Community 2 - "Padrao LLM Wiki (Karpathy)"
Cohesion: 0.43
Nodes (7): LLM como mantenedor de wiki pessoal, Por que funciona agora: LLM resolve bookkeeping, Loop Ingest-Query-Maintain, Andrej Karpathy (LLM Wiki gist), log.md append-only, Vannevar Bush Memex (1945), Wiki persistente mantido por LLM

### Community 3 - "Schema do Wiki (Convencoes para LLM)"
Cohesion: 0.5
Nodes (5): Schema do Wiki (CLAUDE.md / AGENTS.md), Tres camadas: raw sources, wiki, schema, Co-evolucao do schema com o usuario, Explicar o porque e nao so o que, Schema (CLAUDE.md / AGENTS.md)

### Community 4 - "RAG vs Wiki Persistente"
Cohesion: 0.5
Nodes (5): RAG vs Wiki persistente, Onde mora o custo do pensamento (query vs ingestao), Quando usar cada abordagem, RAG (Retrieval Augmented Generation), Stateful (wiki) vs Stateless (RAG)

## Knowledge Gaps
- **5 isolated node(s):** `Loop Ingest-Query-Maintain`, `log.md append-only`, `Quando usar cada abordagem`, `Co-evolucao do schema com o usuario`, `GRAPH_REPORT.md`
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `LLM como mantenedor de wiki pessoal` connect `Padrao LLM Wiki (Karpathy)` to `Graphify Pipeline e Outputs`, `Skill Graphify-Study (Feynman + Notas)`, `Schema do Wiki (Convencoes para LLM)`, `RAG vs Wiki Persistente`?**
  _High betweenness centrality (0.527) - this node is a cross-community bridge._
- **Why does `Wiki persistente mantido por LLM` connect `Padrao LLM Wiki (Karpathy)` to `Graphify Pipeline e Outputs`, `Skill Graphify-Study (Feynman + Notas)`, `RAG vs Wiki Persistente`?**
  _High betweenness centrality (0.329) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `Wiki persistente mantido por LLM` (e.g. with `Wiki navegavel (wiki/index.md)` and `Conectar ao inves de arquivar`) actually correct?**
  _`Wiki persistente mantido por LLM` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Loop Ingest-Query-Maintain`, `log.md append-only`, `Quando usar cada abordagem` to the rest of the system?**
  _5 weakly-connected nodes found - possible documentation gaps or missing edges._