# Fluxo de Ingestão

## Visão Geral

Ingestão é o processo de adicionar novas fontes ao wiki. O LLM lê a fonte, extrai informações-chave e as integra ao conhecimento existente.

## Fluxo Completo

```
1. Adicionar Fonte
   ↓
2. Processamento pelo LLM
   ↓
3. Discussão com Você
   ↓
4. Criação/Atualização de Páginas
   ↓
5. Cruzamento de Referências
   ↓
6. Atualização de Index e Log
   ↓
7. Revisão e Ajustes
```

## Passo 1: Adicionar Fonte

### Locais de Origem

```bash
# Artigos científicos
raw/papers/novo-paper.pdf

# Posts de blog
raw/articles/artigo-importante.md

# Documentação técnica
raw/docs/api-reference.md

# Imagens e diagramas
raw/images/arquitetura.png

# Transcrições de áudio
raw/audio/entrevista.md
```

### Ferramentas de Captura

**Obsidian Web Clipper** (recomendado)
```
1. Instale a extensão do navegador
2. No artigo que deseja salvar: clique no ícone do Obsidian
3. Escolha a pasta de destino (ex: raw/articles/)
4. Pressione hotkey (Ctrl+Shift+D) para baixar imagens
```

**Manual**
```bash
# Arquivo já em markdown
cp ~/Downloads/artigo.md raw/articles/

# PDF de paper
cp ~/Downloads/paper.pdf raw/papers/

# Converta HTML para markdown se necessário
pandoc -t markdown artigo.html -o raw/articles/artigo.md
```

## Passo 2: Processamento pelo LLM

### Comando ao LLM

```
Adicione a nova fonte ao wiki:

Fonte: raw/papers/novo-paper.pdf
Tipo: Paper científico

Por favor:
1. Leia o documento completo
2. Identifique os conceitos-chave
3. Extraia entidades mencionadas
4. Notifique se há contradições com conhecimento existente
```

### O que o LLM Faz Internamente

```python
# Pseudocódigo do fluxo do LLM

def process_source(source_path):
    # 1. Leitura completa
    content = read_file(source_path)

    # 2. Extração de entidades
    entities = extract_entities(content)
    # Ex: ["Transformer", "Attention", "Feed-Forward"]

    # 3. Extração de conceitos
    concepts = extract_concepts(content)
    # Ex: ["Self-Attention", "Multi-Head Attention", "Positional Encoding"]

    # 4. Identificação de temas
    themes = identify_themes(content)
    # Ex: ["Neural Networks", "Sequence Modeling", "Attention Mechanisms"]

    # 5. Análise de contradições
    contradictions = check_against_wiki(content)
    # Ex: []

    return {
        "entities": entities,
        "concepts": concepts,
        "themes": themes,
        "contradictions": contradictions
    }
```

## Passo 3: Discussão com Você

### O LLM Apresenta

```
Acabei de ler o novo paper. Aqui está o que encontrei:

**Conceitos principais:**
- Self-Attention (já existe no wiki)
- Multi-Head Attention (já existe no wiki)
- Positional Encoding (já existe no wiki)
- NEW: Relative Positional Encoding (novo conceito!)

**Entidades mencionadas:**
- Google Brain (nova organização)
- Vaswani, Ashish (novo autor)

**Possíveis contradições:**
- Nenhuma

**Próximos passos:**
1. Criar página para Relative Positional Encoding
2. Atualizar Self-Attention com insights do paper
3. Criar páginas para Google Brain e Vaswani
4. Adicionar ao index

Quer que eu prossiga?
```

### Você Responde

```
Sim, prossiga.
Para Relative Positional Encoding, foque em:
- Diferença em relação ao Positional Encoding absoluto
- Trade-offs de performance
- Quando é preferível usar um ou outro
```

## Passo 4: Criação/Atualização de Páginas

### Páginas Criadas

#### Nova Página de Conceito

```markdown
---
type: concept
tags: [attention, positional-encoding, optimization]
sources_count: 1
last_updated: 2026-04-21
related_concepts: [Positional Encoding, Self-Attention]
---

# Relative Positional Encoding

## Definição
Variação de positional encoding que representa posições relativas em vez de absolutas, permitindo maior generalização para comprimentos de sequência não vistos durante treinamento.

## Como Funciona
[Diferenças em relação ao Positional Encoding absoluto]

## Trade-offs
| Aspecto | Absoluto | Relativo |
|---------|----------|----------|
| Generalização | Pobre para sequências mais longas | Melhor generalização |
| Complexidade | Simples | Mais complexo |
| Performance | Boa em curto prazo | Similar no mesmo comprimento |

## Quando Usar
- Sequências muito longas (> 2048 tokens)
- Comprimento variável de sequência
- Quando generalização é mais importante que performance absoluta

## Fontes
1. [[Self-Attention with Relative Position Representations]] (raw/papers/relative-positional-encoding.pdf)

## Ver Também
- [[Positional Encoding]] (versão absoluta)
- [[Self-Attention]] (mecanismo base)
```

#### Nova Página de Entidade

```markdown
---
type: entity
tags: [organization, research]
sources_count: 1
last_updated: 2026-04-21
related_entities: [Google, OpenAI, Facebook AI Research]
---

# Google Brain

## Definição
Equipe de pesquisa de IA do Google, responsável por avanços significativos em aprendizado profundo.

## Principais Contribuições
- Attention Is All You Need (2017)
- BERT (2018)
- TensorFlow (2015)
- [outras contribuições]

## Pessoas-Chave
- [[Vaswani, Ashish]] - Autor principal do Transformer
- [[Devlin, Jacob]] - Autor principal do BERT
- [outras]

## Fontes
1. [[Google Brain - Publications]] (raw/articles/google-brain-publications.md)
2. [[Self-Attention with Relative Position Representations]] (raw/papers/relative-positional-encoding.pdf)

## Ver Também
- [[Google]] (empresa mãe)
- [[DeepMind]] (outra equipe de pesquisa do Google)
```

### Páginas Atualizadas

#### Atualização de Página Existente

```markdown
---
type: concept
tags: [attention, neural-networks]
sources_count: 3  # ATUALIZADO: era 2, agora 3
last_updated: 2026-04-21  # ATUALIZADO
related_concepts: [Positional Encoding, Multi-Head Attention, Relative Positional Encoding]  # ATUALIZADO
---

# Positional Encoding

[conteúdo anterior... mantido]

## Variações

### Positional Encoding Absoluto (Padrão)
[descrição original mantida...]

### Positional Encoding Relativo (NOVA SEÇÃO)
Representa posições de forma relativa, oferecendo melhor generalização para sequências mais longas.

Ver [[Relative Positional Encoding]] para detalhes.

[resto do conteúdo... mantido]
```

## Passo 5: Cruzamento de Referências

### Links Bidirecionais

```markdown
# Relative Positional Encoding

## Relacionamentos
- [[Positional Encoding]] → é uma variação de
- [[Self-Attention]] → é aplicado em
```

```markdown
# Positional Encoding

## Relacionamentos
- [[Self-Attention]] → é usado em
- [[Relative Positional Encoding]] ← variação deste
- [[Multi-Head Attention]] → é usado em
```

### Atualização de Síntese

```markdown
# Transformer Architecture Overview

## Posicional Encoding

Existem duas abordagens principais:

1. **Positional Encoding Absoluto** (padrão)
   - Usado no Transformer original
   - Desempenho bom em sequências de comprimento fixo
   - Limitações em generalização para sequências mais longas

2. **Positional Encoding Relativo** (variação)
   - Melhor generalização
   - Usado quando comprimento de sequência varia muito
   - Ver [[Relative Positional Encoding]]

Comparação detalhada: [[Positional Encoding Variants Comparison]]
```

## Passo 6: Atualização de Index e Log

### Atualização de index.md

```markdown
# Wiki Index

## Conceitos
- [[Positional Encoding]] - Codificação posicional em Transformers
- [[Relative Positional Encoding]] - Codificação posicional relativa (NOVO)
- [[Self-Attention]] - Mecanismo de atenção autodirecionada

## Entidades
- [[Google Brain]] - Equipe de pesquisa de IA do Google (NOVO)
- [[Vaswani, Ashish]] - Autor principal do Transformer (NOVO)

## Fontes
- [[Attention Is All You Need]] - Paper original do Transformer
- [[Self-Attention with Relative Position Representations]] - Paper sobre positional encoding relativo (NOVO)

[resto do index...]
```

### Adição a log.md

```markdown
## [2026-04-21] ingest | Self-Attention with Relative Position Representations

**Fonte**: raw/papers/relative-positional-encoding.pdf

**Conceitos extraídos**:
- Relative Positional Encoding (novo)
- [outros conceitos...]

**Entidades extraídas**:
- Google Brain (novo)
- Vaswani, Ashish (novo)

**Páginas criadas**:
- wiki/concepts/relative-positional-encoding.md
- wiki/entities/google-brain.md
- wiki/entities/vaswani-ashish.md

**Páginas atualizadas**:
- wiki/concepts/positional-encoding.md
- wiki/synthesis/transformer-architecture.md

**Contradições**: Nenhuma
```

## Passo 7: Revisão e Ajustes

### Você Revisa

```
Parece bom! Mas em Relative Positional Encoding,
poderia adicionar uma seção sobre complexidade computacional?

E em Google Brain, talvez adicionar uma linha do tempo das contribuições?
```

### LLM Ajusta

```markdown
# Relative Positional Encoding

[conteúdo existente...]

## Complexidade Computacional

| Variante | Complexidade | Notas |
|----------|--------------|-------|
| Absoluto | O(1) | Cálculo direto |
| Relativo | O(n²) | Requer cálculo de distâncias |
| Híbrido | O(n) | Balance entre precisão e custo |

[resto do conteúdo...]
```

```markdown
# Google Brain

[conteúdo existente...]

## Linha do Tempo de Contribuições

| Ano | Contribuição | Impacto |
|-----|--------------|---------|
| 2015 | TensorFlow | Framework de ML |
| 2017 | Attention Is All You Need | Paper seminal do Transformer |
| 2018 | BERT | State-of-the-art em NLP |

[resto do conteúdo...]
```

## Ingestão em Batch

### Quando Usar

- Muitas fontes relacionadas de uma vez
- Fontes de uma conferência inteira
- Série de artigos de um autor específico

### Fluxo Adaptado

```
Comando ao LLM:
Adicione estas fontes ao wiki:
- raw/papers/neurips-2026/*.pdf (15 papers)

Por favor:
1. Leia todos os papers
2. Identifique temas comuns
3. Crie uma página de síntese para NeurIPS 2026
4. Crie/atualize páginas individuais conforme necessário
5. Foque em descobrir conexões entre papers
```

### Resultado

```markdown
## [2026-04-21] ingest | NeurIPS 2026 Conference (batch)

**Fontes**: 15 papers em raw/papers/neurips-2026/

**Conceitos extraídos**:
- [lista completa...]

**Temas comuns identificados**:
- Efficient Transformers (7 papers)
- Multimodal Learning (5 papers)
- Few-shot Learning (3 papers)

**Páginas criadas**:
- wiki/synthesis/neurips-2026-overview.md
- wiki/concepts/efficient-transformers.md
- wiki/concepts/multimodal-learning.md
- [mais 20 páginas...]

**Conexões surpreendentes encontradas**:
- 2 papers de Efficient Transformers citam o mesmo conceito mas com nomes diferentes
- 1 paper de Multimodal Learning usa uma técnica de Few-shot Learning

**Revisão necessária**: Síntese de Efficient Transformers pode precisar de refinamento
```

## Checklist de Ingestão

### Para Cada Nova Fonte

- [ ] Fonte adicionada em `raw/` com nome descritivo
- [ ] LLM leu a fonte completa
- [ ] Conceitos-chave identificados
- [ ] Entidades extraídas
- [ ] Contradições verificadas com wiki existente
- [ ] Páginas de conceito criadas/atualizadas
- [ ] Páginas de entidade criadas/atualizadas
- [ ] Links bidirecionais estabelecidos
- [ ] Síntese atualizada (se relevante)
- [ ] Index atualizado
- [ ] Log atualizado com timestamp
- [ ] Você revisou as alterações
- [ ] Ajustes finais feitos

### Checklist de Quality Assurance

- [ ] Todas as páginas têm frontmatter YAML
- [ ] Todas as citações apontam para fontes em `raw/`
- [ ] Não há links quebrados
- [ ] Contradições foram resolvidas ou notadas
- [ ] Síntese reflete todas as fontes relevantes
- [ ] Index está atualizado
- [ ] Log está cronologicamente correto

---

**Próximo**: Consultas ao Wiki