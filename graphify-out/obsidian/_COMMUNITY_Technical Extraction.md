---
type: community
cohesion: 0.67
members: 3
---

# Technical Extraction

**Cohesion:** 0.67 - moderately connected
**Members:** 3 nodes

## Members
- [[AST Extraction]] - document - raw/practices/continuous-graph-maintenance.md
- [[Incremental Updates]] - document - raw/practices/continuous-graph-maintenance.md
- [[SHA256 Cache]] - document - raw/practices/continuous-graph-maintenance.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Technical_Extraction
SORT file.name ASC
```
