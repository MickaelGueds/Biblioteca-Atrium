# Arquitetura do Wiki LLM

## Três Camadas

```
┌─────────────────────────────────────────────────────────────┐
│                    Fontes Originais (raw/)                    │
│  Artigos, papers, imagens, arquivos de dados                 │
│  IMUTÁVEIS - o LLM lê mas nunca modifica                     │
│  Sua fonte de verdade                                         │
└──────────────────────┬──────────────────────────────────────┘
                       ↓ (leitura e extração)
┌─────────────────────────────────────────────────────────────┐
│                       Wiki (/wiki)                            │
│  Markdown gerado pelo LLM:                                   │
│  • Resumos                                                   │
│  • Páginas de entidades                                      │
│  • Páginas de conceitos                                      │
│  • Comparações                                               │
│  • Visão geral                                               │
│  • Síntese                                                   │
│  PROPRIEDADE DO LLM - ele cria, atualiza e mantém            │
└──────────────────────┬──────────────────────────────────────┘
                       ↑ (instruções e convenções)
┌─────────────────────────────────────────────────────────────┐
│                    Schema (CLAUDE.md / AGENTS.md)           │
│  Arquivo de configuração que diz ao LLM:                     │
│  • Como o wiki está estruturado                              │
│  • Quais são as convenções                                   │
│  • Quais fluxos de trabalho seguir                          │
│  CO-EVOLUI com você conforme descobre o que funciona        │
└─────────────────────────────────────────────────────────────┘
```

## Detalhe de Cada Camada

### 1. Fontes Originais (`raw/`)

**Propósito**: Coleção curada de documentos fonte

**O que contém**:
- Artigos científicos
- Posts de blog
- Relatórios técnicos
- Imagens e diagramas
- Arquivos de dados
- Transcrições de áudio

**Regras**:
- **Imutáveis**: nunca modificar
- **Verdade absoluta**: o LLM sempre retorna aqui para verificar
- **Organização por tipo**: `raw/papers/`, `raw/articles/`, `raw/images/`

**Fluxo de adição**:
```bash
# 1. Adicione a fonte
cp novo-paper.pdf raw/papers/

# 2. Informe o LLM
"Adicione raw/papers/novo-paper.pdf ao wiki"

# 3. LLM processa
# → Lê o arquivo
# → Extrai conceitos
# → Cria/atualiza páginas do wiki
# → Atualiza index.md
# → Registra em log.md
```

### 2. Wiki (`wiki/`)

**Propósito**: Markdown estruturado e interligado gerado pelo LLM

**O que contém**:

#### Páginas de Entidades
```markdown
# Attention Mechanism

## Definição
[Descrição concisa]

## Componentes
- Query
- Key
- Value
- [etc]

## Aplicações
- Transformers
- Vision models
- [etc]

## Fontes
- [Attention Is All You Need](raw/papers/attention.md)
- [Annotated Transformer](raw/articles/transformer.md)

## Relacionamentos
- [[Self-Attention]] (especializa)
- [[Feed-Forward Layer]] (complementa)
- [[Positional Encoding]] (depende)
```

#### Páginas de Conceitos
```markdown
# Token Optimization

## Visão Geral
[Resumo sintético]

## Técnicas Principais
1. Context Window Extension
2. RAG (Retrieval-Augmented Generation)
3. Knowledge Graph Compression
4. Dynamic Pruning

## Trade-offs
[Comparação de técnicas]

## Estado da Arte
[O que funciona hoje]

## Questões em Aberto
[Perguntas para investigação futura]
```

#### Páginas de Síntese
```markdown
# Comparative Analysis: RAG vs Graph RAG

## Contexto
[Por que essa comparação importa]

## Critérios de Avaliação
- Custo de latência
- Custo de tokens
- Fidelidade ao conhecimento
- Capacidade de generalização

## Tabela Comparativa
| Aspecto | RAG | Graph RAG |
|---------|-----|-----------|
| [fill] | ... | ... |

## Recomendação
[Quando usar cada um]
```

**Regras**:
- **Propriedade do LLM**: você lê, ele escreve
- **Referências cruzadas**: links bidirecionais automáticos
- **Citações**: cada afirmação aponta para a fonte em `raw/`
- **Atualização contínua**: novas fontes enriquecem páginas existentes

**Estrutura sugerida**:
```
wiki/
├── entities/           # Pessoas, organizações, tecnologias
├── concepts/           # Ideias abstratas, padrões, teorias
├── sources/            # Resumos de fontes individuais
├── comparisons/        # Análises comparativas
├── synthesis/          # Sínteses cruzadas
├── index.md            # Catálogo de tudo
└── log.md              # Histórico cronológico
```

### 3. Schema (`CLAUDE.md` / `AGENTS.md`)

**Propósito**: Instruções e convenções para o LLM

**O que contém**:

#### Estrutura do Wiki
```markdown
## Estrutura de Pastas

### Fontes Originais
- `raw/papers/` - Artigos científicos (.pdf)
- `raw/articles/` - Posts e blogs (.md)
- `raw/images/` - Diagramas e imagens (.png, .jpg)
- `raw/audio/` - Transcrições de áudio (.md)
```

#### Convenções de Página
```markdown
## Formato de Páginas de Entidades

```yaml
---
type: entity
tags: [person, organization, technology]
sources_count: 3
last_updated: 2026-04-21
---

# [Nome da Entidade]

## Definição
[1-2 frases concisas]

## Componentes/Características
- [lista]

## Aplicações
- [lista]

## Fontes
1. [[Nome da Fonte]] (raw/path/to/source.md)

## Relacionamentos
- [[Entidade Relacionada]] - [tipo de relação]
```

#### Fluxos de Trabalho
```markdown
## Ingestão de Novas Fontes

Ao receber uma nova fonte:

1. **Leitura completa**
   - Ler o documento inteiro
   - Identificar conceitos-chave
   - Extrair entidades mencionadas

2. **Criação/atualização de páginas**
   - Criar resumo da fonte em `wiki/sources/`
   - Criar/atualizar páginas de entidades em `wiki/entities/`
   - Criar/atualizar páginas de conceitos em `wiki/concepts/`

3. **Cruzamento de referências**
   - Adicionar links bidirecionais entre páginas relacionadas
   - Atualizar páginas de síntese se houver novas contradições

4. **Atualização de index**
   - Adicionar entrada em `wiki/index.md`
   - Registrar em `wiki/log.md` com timestamp

## Consultas ao Wiki

Ao receber uma pergunta:

1. **Busca no index**
   - Ler `wiki/index.md` primeiro
   - Identificar páginas relevantes

2. **Leitura profunda**
   - Ler as páginas relevantes
   - Seguir links conforme necessário

3. **Síntese com citações**
   - Gerar resposta
   - Citar fontes em `raw/`
   - Criar referências cruzadas para `wiki/`

4. **Arquivamento opcional**
   - Se a resposta for valiosa, criar nova página em `wiki/synthesis/`
```

## Por que essa Arquitetura Funciona

| Camada | Problema que Resolve | Benefício |
|--------|---------------------|-----------|
| **Raw/** | Fontes dispersas, difíceis de encontrar | Fonte de verdade centralizada |
| **Wiki/** | Conhecimento fragmentado, sem contexto | Conhecimento interligado e enriquecido |
| **Schema** | LLM sem direção, inconsistente | Comportamento disciplinado e previsível |

## Evolução do Schema

O schema não é estático. Ele **co-evolui com você**:

```markdown
## Evolução do Schema

### v1.0 (Inicial)
- Estrutura básica de pastas
- Convenções simples de markdown

### v1.1 (Após 10 fontes)
- Adicionado metadata YAML
- Padrões de citação refinados

### v2.0 (Após 50 fontes)
- Adicionadas páginas de comparação
- Sintaxe de consultas específica

### v2.1 (Atual)
- Adicionado health-check
- Integração com ferramentas externas
```

**Próxima iteração**: Documente o que funciona e o que não funciona. Ajuste o schema. Repita.