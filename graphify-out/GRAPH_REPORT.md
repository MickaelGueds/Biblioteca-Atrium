# Graph Report - raw  (2026-04-21)

## Corpus Check
- Corpus is ~2,074 words - fits in a single context window. You may not need a graph.

## Summary
- 26 nodes · 27 edges · 5 communities detected
- Extraction: 85% EXTRACTED · 15% INFERRED · 0% AMBIGUOUS · INFERRED: 4 edges (avg confidence: 0.88)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Knowledge Output|Knowledge Output]]
- [[_COMMUNITY_Maintenance Practices|Maintenance Practices]]
- [[_COMMUNITY_Navigation & Discovery|Navigation & Discovery]]
- [[_COMMUNITY_Core Concepts|Core Concepts]]
- [[_COMMUNITY_Technical Extraction|Technical Extraction]]

## God Nodes (most connected - your core abstractions)
1. `Graphify` - 5 edges
2. `Knowledge Graph` - 5 edges
3. `Continuous Graph Maintenance` - 4 edges
4. `GRAPH_REPORT.md` - 4 edges
5. `Git Hooks` - 3 edges
6. `Onboarding` - 3 edges
7. `Wiki` - 3 edges
8. `Queries` - 3 edges
9. `Repository Pattern` - 2 edges
10. `Queries` - 2 edges

## Surprising Connections (you probably didn't know these)
- `Graphify` --requires--> `Continuous Graph Maintenance`  [INFERRED]
  raw/patterns/graphify-as-knowledge-center.md → raw/practices/continuous-graph-maintenance.md
- `Queries` --same_concept_as--> `Queries`  [INFERRED]
  raw/patterns/graphify-as-knowledge-center.md → raw/tutorials/onboarding.md
- `Wiki` --same_concept_as--> `Wiki`  [INFERRED]
  raw/patterns/graphify-as-knowledge-center.md → raw/tutorials/onboarding.md

## Communities

### Community 0 - "Knowledge Output"
Cohesion: 0.33
Nodes (6): Continuous Documentation, Graphify, Repository Pattern, Wiki, Obsidian, Wiki

### Community 1 - "Maintenance Practices"
Cohesion: 0.4
Nodes (6): Atomic Commits, Cache Hit Rate, Continuous Graph Maintenance, Continuous Integration, Git Hooks, Synchronization

### Community 2 - "Navigation & Discovery"
Cohesion: 0.4
Nodes (6): Queries, GRAPH_REPORT.md, Onboarding, Queries, Suggested Questions, Surprising Connections

### Community 3 - "Core Concepts"
Cohesion: 0.4
Nodes (5): Communities (Comunidades), Edges (Arestas), God Nodes (Nós de Deus), Knowledge Graph, Nodes (Nós)

### Community 4 - "Technical Extraction"
Cohesion: 0.67
Nodes (3): AST Extraction, Incremental Updates, SHA256 Cache

## Knowledge Gaps
- **12 isolated node(s):** `Nodes (Nós)`, `Edges (Arestas)`, `Communities (Comunidades)`, `God Nodes (Nós de Deus)`, `Continuous Documentation` (+7 more)
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Graphify` connect `Knowledge Output` to `Maintenance Practices`, `Navigation & Discovery`, `Core Concepts`?**
  _High betweenness centrality (0.572) - this node is a cross-community bridge._
- **Why does `Continuous Graph Maintenance` connect `Maintenance Practices` to `Knowledge Output`?**
  _High betweenness centrality (0.307) - this node is a cross-community bridge._
- **Why does `Knowledge Graph` connect `Core Concepts` to `Knowledge Output`?**
  _High betweenness centrality (0.260) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `Continuous Graph Maintenance` (e.g. with `Synchronization` and `Graphify`) actually correct?**
  _`Continuous Graph Maintenance` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Nodes (Nós)`, `Edges (Arestas)`, `Communities (Comunidades)` to the rest of the system?**
  _12 weakly-connected nodes found - possible documentation gaps or missing edges._