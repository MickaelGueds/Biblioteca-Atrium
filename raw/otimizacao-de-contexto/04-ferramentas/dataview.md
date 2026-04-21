# Dataview - Queries Dinâmicas

## Visão Geral

Dataview é um plugin do Obsidian que permite fazer queries dinâmicas sobre frontmatter YAML das páginas do wiki. Útil para visões organizadas e análises de dados.

## Por que Usar?

### Queries Estáticas vs Dinâmicas

**Queries estáticas (manual)**:
```markdown
## Conceitos
- [[Positional Encoding]]
- [[Relative Positional Encoding]]
- [[Self-Attention]]
```

**Problemas**:
- Precisa atualizar manualmente a cada novo conceito
- Esquece de adicionar conceitos novos
- Não filtra ou ordena automaticamente

**Queries dinâmicas (Dataview)**:
```dataview
TABLE file.link as "Conceito"
FROM "wiki/concepts"
WHERE type = "concept"
SORT last_updated DESC
```

**Benefícios**:
- Automático (não precisa atualizar)
- Filtra (apenas conceitos)
- Ordena (últimos atualizados primeiro)

### Casos de Uso

- **Visões organizadas**: Listas automáticas por tipo, tag, data
- **Análises**: Tabelas comparativas, métricas
- **Dashboards**: Visões de status, progresso
- **Discovery**: Encontrar páginas desatualizadas, órfãs, etc.

## Instalação

### Via Obsidian Community Plugins

```
Settings → Community Plugins → Browse → Search "Dataview"
→ Install → Enable
```

### Verificar instalação

Crie página teste:
```markdown
```dataview
TABLE file.link as "Nome"
FROM "wiki"
LIMIT 5
```
```

Se funcionar, Dataview está instalado.

## Sintaxe Básica

### Query Simples

```dataview
TABLE file.link as "Nome", type as "Tipo"
FROM "wiki/concepts"
LIMIT 10
```

**Saída**:
| Nome | Tipo |
|------|------|
| [[Positional Encoding]] | concept |
| [[Relative Positional Encoding]] | concept |
| [[Self-Attention]] | concept |

### Query com Filtros

```dataview
TABLE file.link as "Conceito", difficulty as "Dificuldade"
FROM "wiki/concepts"
WHERE type = "concept" AND difficulty = "advanced"
```

**Saída**: Apenas conceitos avançados

### Query com Ordenação

```dataview
TABLE file.link as "Conceito", last_updated as "Atualizado"
FROM "wiki/concepts"
WHERE type = "concept"
SORT last_updated DESC
LIMIT 5
```

**Saída**: Últimos 5 conceitos atualizados

### Query com Cálculos

```dataview
TABLE file.link as "Fonte", sources_count as "Citações", (sources_count * 10) as "Pontos"
FROM "wiki/sources"
SORT sources_count DESC
```

**Saída**: Fontes com mais citações (e pontos calculados)

## Queries Avançadas

### Query com Tags

```dataview
LIST
FROM "wiki"
WHERE contains(tags, "attention")
```

**Saída**: Lista de todas as páginas com tag "attention"

### Query com Data

```dataview
TABLE file.link as "Fonte", original_date as "Data"
FROM "wiki/sources"
WHERE original_date >= date(2017) AND original_date <= date(2019)
SORT original_date ASC
```

**Saída**: Fontes entre 2017 e 2019

### Query com Links

```dataview
LIST
FROM "wiki/concepts"
WHERE -contains(file.outlinks.path, "wiki/synthesis")
```

**Saída**: Conceitos sem links para sínteses (órfãos de síntese)

### Query com Comprimento

```dataview
TABLE file.link as "Página", length(file.content) as "Caracteres"
FROM "wiki"
SORT length(file.content) DESC
LIMIT 5
```

**Saída**: Páginas mais longas

## Categorias de Queries

### 1. Listas por Tipo

#### Todos os Conceitos

```dataview
TABLE file.link as "Conceito", difficulty as "Nível"
FROM "wiki/concepts"
WHERE type = "concept"
SORT concept_name ASC
```

#### Todas as Entidades

```dataview
TABLE file.link as "Entidade"
FROM "wiki/entities"
WHERE type = "entity"
SORT file.name ASC
```

#### Todas as Fontes

```dataview
TABLE file.link as "Fonte", original_date as "Data"
FROM "wiki/sources"
WHERE type = "source"
SORT original_date DESC
```

### 2. Listas por Tag

#### Todos os itens com tag "attention"

```dataview
TABLE file.link as "Item", type as "Tipo"
FROM "wiki"
WHERE contains(tags, "attention")
SORT type, file.name
```

#### Todos os itens com tag "optimization"

```dataview
TABLE file.link as "Item"
FROM "wiki"
WHERE contains(tags, "optimization")
SORT file.name ASC
```

### 3. Listas por Data

#### Atualizados recentemente (últimos 7 dias)

```dataview
TABLE file.link as "Página", last_updated as "Atualizado"
FROM "wiki"
WHERE last_updated >= date(today) - dur(7 days)
SORT last_updated DESC
```

#### Não atualizados há muito tempo (> 30 dias)

```dataview
TABLE file.link as "Página", last_updated as "Atualizado"
FROM "wiki"
WHERE last_updated < date(today) - dur(30 days)
SORT last_updated ASC
```

#### Fontes por ano

```dataview
TABLE original_date.year as "Ano", count(rows) as "Quantidade"
FROM "wiki/sources"
WHERE original_date
GROUP BY original_date.year
SORT original_date.year DESC
```

### 4. Listas por Relacionamento

#### Conceitos relacionados a X

```dataview
LIST
FROM "wiki/concepts"
WHERE contains(file.outlinks.path, "wiki/concepts/self-attention.md")
OR contains(related_concepts, "Self-Attention")
```

#### Páginas que linkam para X (backlinks)

```dataview
LIST
FROM "wiki"
WHERE -contains(file.inlinks.path, "wiki/concepts/positional-encoding.md")
```

#### Conexões mútuas (A e B linkam entre si)

```dataview
TABLE file.link as "Página"
FROM "wiki"
WHERE contains(file.outlinks.path, "wiki/concepts/self-attention.md")
AND contains(file.inlinks.path, "wiki/concepts/self-attention.md")
```

### 5. Listas por Status

#### Conclusos vs Em Progresso (para projetos)

```dataview
TABLE file.link as "Projeto", status as "Status"
FROM "wiki/projetos"
WHERE type = "project"
SORT status DESC, file.name ASC
```

#### Bug Conhecidos vs Resolvidos

```dataview
TABLE file.link as "Bug", resolution as "Status"
FROM "wiki/bugs"
WHERE type = "bug"
SORT resolution ASC, file.name ASC
```

### 6. Análises

#### Páginas mais citadas

```dataview
TABLE file.link as "Página", length(file.inlinks) as "Links de Entrada"
FROM "wiki"
SORT length(file.inlinks) DESC
LIMIT 10
```

#### Conceitos por dificuldade

```dataview
TABLE difficulty as "Dificuldade", count(rows) as "Quantidade"
FROM "wiki/concepts"
WHERE type = "concept"
GROUP BY difficulty
SORT count(rows) DESC
```

#### Fontes por número de citações

```dataview
TABLE file.link as "Fonte", sources_count as "Citações"
FROM "wiki/sources"
WHERE type = "source"
SORT sources_count DESC
LIMIT 10
```

## Queries Específicas para Wiki LLM

### 1. Health-Check

#### Páginas sem frontmatter

```dataview
LIST
FROM "wiki"
WHERE !type
```

**Explicação**: Páginas sem campo `type` no frontmatter

#### Páginas órfãs (sem links de entrada)

```dataview
LIST
FROM "wiki"
WHERE length(file.inlinks) = 0 AND file.path != "wiki/index.md"
```

**Explicação**: Páginas que ninguém linka

#### Links quebrados (páginas que linkam para arquivos inexistentes)

```dataview
LIST
FROM "wiki"
WHERE any(file.outlinks.path, (p) => !fileexists(p))
```

**Explicação**: Páginas com links para arquivos que não existem

### 2. Manutenção

#### Páginas desatualizadas (> 60 dias sem atualização)

```dataview
TABLE file.link as "Página", last_updated as "Última Atualização"
FROM "wiki"
WHERE last_updated < date(today) - dur(60 days)
SORT last_updated ASC
```

**Explicação**: Páginas que precisam de revisão

#### Páginas com poucas fontes (< 2)

```dataview
TABLE file.link as "Página", sources_count as "Citações"
FROM "wiki"
WHERE sources_count < 2
SORT sources_count ASC
```

**Explicação**: Páginas com pouca evidência de fontes

#### Páginas sem tags

```dataview
LIST
FROM "wiki"
WHERE length(tags) = 0
```

**Explicação**: Páginas difíceis de categorizar

### 3. Descoberta

#### Conceitos populares (muitos links de entrada)

```dataview
TABLE file.link as "Conceito", length(file.inlinks) as "Links"
FROM "wiki/concepts"
WHERE length(file.inlinks) > 5
SORT length(file.inlinks) DESC
```

**Explicação**: Conceitos que são hubs (conectados a muitas outras páginas)

#### Padrões de tags frequentes

```dataview
TABLE tags as "Tag", count(rows) as "Quantidade"
FROM "wiki"
GROUP BY tags
FLATTEN tags
SORT count(rows) DESC
LIMIT 20
```

**Explicação**: Tags mais comuns (temas populares)

#### Conexões fortes (A e B se citam mutuamente)

```dataview
TABLE file.link as "Página A", filter(file.outlinks, (l) => contains(file.inlinks, l)) as "Conexões Mútuas"
FROM "wiki"
WHERE length(filter(file.outlinks, (l) => contains(file.inlinks, l))) > 0
```

**Explicação**: Páginas com múltiplas conexões bidirecionais

### 4. Dashboards

#### Status do Wiki

```dataview
TABLE "Total" as "Métrica", count(rows) as "Quantidade"
FROM "wiki"
GROUP BY "Total"
```

**Explicação**: Total de páginas no wiki

#### Por Tipo

```dataview
TABLE type as "Tipo", count(rows) as "Quantidade"
FROM "wiki"
GROUP BY type
SORT count(rows) DESC
```

**Explicação**: Quantidade de páginas por tipo (concepts, entities, etc.)

#### Atividade Recente

```dataview
TABLE file.link as "Página", last_updated as "Atualizado"
FROM "wiki"
WHERE last_updated >= date(today) - dur(7 days)
SORT last_updated DESC
LIMIT 20
```

**Explicação**: Últimas 20 páginas atualizadas

#### Progresso por Projeto

```dataview
TABLE file.link as "Projeto", status as "Status", progress as "Progresso"
FROM "wiki/projetos"
WHERE type = "project"
SORT status DESC, progress DESC
```

**Explicação**: Status de todos os projetos

## Uso com LLM

### Pedir ao LLM para criar queries

**Comando ao LLM**:
```
Crie uma query Dataview para mostrar todos os conceitos que não foram atualizados nos últimos 30 dias.

Adicione:
- Nome do conceito
- Data da última atualização
- Ordenar por data (mais antigos primeiro)

Salve a query em wiki/dashboards/conceitos-desatualizados.md
```

**Resultado**:
```markdown
# Conceitos Desatualizados

```dataview
TABLE file.link as "Conceito", last_updated as "Última Atualização", (date(today) - last_updated).days as "Dias Sem Atualização"
FROM "wiki/concepts"
WHERE type = "concept" AND last_updated < date(today) - dur(30 days)
SORT last_updated ASC
```

**Gerado em**: 2026-04-21
```

### LLM usando Dataview para análise

**Comando ao LLM**:
```
Use Dataview para analisar o wiki e responder:

1. Quantos conceitos temos?
2. Quantos estão desatualizados (> 30 dias)?
3. Quais são os 5 conceitos mais conectados (mais links de entrada)?
4. Quais são as tags mais populares?

Para cada pergunta, mostre a query Dataview que usou e a resposta.
```

**Resposta do LLM**:
```
## 1. Quantos conceitos temos?

**Query**:
```dataview
TABLE count(rows) as "Total"
FROM "wiki/concepts"
WHERE type = "concept"
```

**Resposta**: 89 conceitos

---

## 2. Quantos estão desatualizados (> 30 dias)?

**Query**:
```dataview
TABLE count(rows) as "Desatualizados"
FROM "wiki/concepts"
WHERE type = "concept" AND last_updated < date(today) - dur(30 days)
```

**Resposta**: 12 conceitos desatualizados

---

## 3. Quais são os 5 conceitos mais conectados?

**Query**:
```dataview
TABLE file.link as "Conceito", length(file.inlinks) as "Links"
FROM "wiki/concepts"
WHERE type = "concept"
SORT length(file.inlinks) DESC
LIMIT 5
```

**Resposta**:
1. [[Self-Attention]]: 23 links
2. [[Positional Encoding]]: 19 links
3. [[Transformer]]: 17 links
4. [[Multi-Head Attention]]: 15 links
5. [[Feed-Forward Layer]]: 12 links

---

## 4. Quais são as tags mais populares?

**Query**:
```dataview
TABLE tags as "Tag", count(rows) as "Quantidade"
FROM "wiki"
GROUP BY tags
FLATTEN tags
SORT count(rows) DESC
LIMIT 10
```

**Resposta**:
1. attention: 23
2. transformer: 19
3. optimization: 15
4. neural-network: 12
5. positional-encoding: 10
6. sequence-modeling: 8
7. deep-learning: 7
8. nlp: 6
9. architecture: 5
10. performance: 4
```

## Boas Práticas

### 1. Usar TABLE para dados tabulares

**Bom**:
```dataview
TABLE file.link as "Nome", type as "Tipo"
FROM "wiki"
```

**Ruim** (para dados tabulares):
```dataview
LIST
FROM "wiki"
```

### 2. Usar LIST para dados simples

**Bom**:
```dataview
LIST
FROM "wiki/concepts"
WHERE contains(tags, "attention")
```

**Ruim** (para lista simples):
```dataview
TABLE file.link as "Nome"
FROM "wiki/concepts"
```

### 3. Filtrar sempre que possível

**Bom**:
```dataview
TABLE file.link as "Conceito"
FROM "wiki/concepts"
WHERE type = "concept"
```

**Ruim** (sem filtro):
```dataview
TABLE file.link as "Página"
FROM "wiki"
```

### 4. Ordenar resultados

**Bom**:
```dataview
TABLE file.link as "Conceito", last_updated as "Atualizado"
FROM "wiki/concepts"
WHERE type = "concept"
SORT last_updated DESC
```

**Ruim** (sem ordenação):
```dataview
TABLE file.link as "Conceito"
FROM "wiki/concepts"
WHERE type = "concept"
```

### 5. Limitar resultados para queries grandes

**Bom**:
```dataview
TABLE file.link as "Página"
FROM "wiki"
LIMIT 100
```

**Ruim** (sem limite, wiki grande pode travar):
```dataview
TABLE file.link as "Página"
FROM "wiki"
```

## Troubleshooting

### Problema: Query retorna resultados vazios

**Causa 1**: Filtro incorreto
**Solução**: Verifique filtros
```dataview
# Ruim (type errado)
WHERE type = "conceptual"

# Bom (type correto)
WHERE type = "concept"
```

**Causa 2**: Caminho incorreto
**Solução**: Verifique FROM
```dataview
# Ruim (caminho errado)
FROM "wikis/concepts"

# Bom (caminho correto)
FROM "wiki/concepts"
```

**Causa 3**: Dados não existem
**Solução**: Verifique se há dados
```dataview
# Teste se há dados
TABLE count(rows) as "Total"
FROM "wiki/concepts"
```

### Problema: Query muito lenta

**Causa 1**: Wiki muito grande (500+ páginas)
**Solução**: Limite resultados
```dataview
TABLE file.link as "Página"
FROM "wiki"
LIMIT 50  ← Limite
```

**Causa 2**: Muitos filtros complexos
**Solução**: Simplifique filtros
```dataview
# Ruim (múltiplos filtros complexos)
WHERE type = "concept" AND contains(tags, "attention") AND last_updated >= date(2026) AND difficulty = "advanced"

# Bom (filtros simples)
WHERE type = "concept"
```

**Causa 3**: Dataview desativado
**Solução**: Ative Dataview
```
Settings → Dataview → Enable Dataview queries
```

### Problema: Colunas não aparecem

**Causa**: TABLE sem colunas especificadas
**Solução**: Especifique colunas
```dataview
# Ruim (sem colunas)
TABLE
FROM "wiki"

# Bom (com colunas)
TABLE file.link as "Nome", type as "Tipo"
FROM "wiki"
```

### Problema: Ordenação não funciona

**Causa**: Campo não existe ou não é numérico/data
**Solução**: Verifique campo
```dataview
# Ruim (last_updated não existe)
SORT last_updated DESC

# Bom (last_updated existe)
SORT last_updated DESC
```

---

**Próximo**: Resumo Final da Estrutura