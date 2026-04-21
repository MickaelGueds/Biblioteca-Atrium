# Marp - Slides em Markdown

## Visão Geral

Marp é um framework para criar apresentações (slides) usando Markdown. Permite gerar apresentações a partir do conteúdo do seu wiki LLM.

## Por que Usar?

### Slides do Wiki → Apresentações Rápidas

**Sem Marp**:
```
Quer apresentar sobre "Transformer Architecture"?
1. Copia conteúdo do wiki
2. Cola no PowerPoint
3. Ajusta formatação manualmente
4. 2-3 horas de trabalho
```

**Com Marp**:
```
Quer apresentar sobre "Transformer Architecture"?
1. Adiciona frontmatter Marp no wiki
2. Exporta para PDF
3. 10 minutos de trabalho
```

### Uso Cases

- Apresentações internas (equipe, stakeholders)
- Conferências e meetups
- Documentação visual
- Tutoriais e guias
- Sínteses para consulta rápida

## Instalação

### Via npm (recomendado)

```bash
npm install -g @marp-team/marp-cli
```

### Verificar instalação

```bash
marp --version
# Saída esperada: marp-cli v.x.x
```

## Configuração Básica

### Frontmatter Obrigatório

```markdown
---
marp: true
theme: gaia
paginate: true
---

# Título da Apresentação
```

**O que cada opção faz**:
- `marp: true` → Ativa Marp (obrigatório)
- `theme: gaia` → Usa tema Gaia (padrão)
- `paginate: true` → Mostra números de página

## Temas

### Temas Integrados

1. **Gaia** (padrão)
   - Minimalista, moderno
   - Bom para apresentações de tecnologia

2. **Default**
   - Simples, clean
   - Bom para apresentações gerais

3. **Uncover**
   - Fundo escuro, texto claro
   - Bom para ambientes escuros

### Usar Tema

```markdown
---
marp: true
theme: uncover
paginate: true
---

# Título
```

## Criação de Slides

### Slide de Título

```markdown
---
marp: true
theme: gaia
paginate: true
---

# Transformer Architecture

## Uma introdução aos modelos de sequência baseados em attention

**Apresentador**: Seu Nome
**Data**: 2026-04-21
```

### Slide de Conteúdo

```markdown
---

# What is a Transformer?

- **Attention Is All You Need** (2017)
  - Introduziu arquitetura Transformer
  - Base para GPT, BERT, T5

- **Características principais**
  - Baseado puramente em attention
  - Sem recorrência (RNNs) ou convolução (CNNs)
  - Paralelização completa

**Fonte**: [[Attention Is All You Need]] (raw/papers/attention-is-all-you-need.pdf)
```

### Slide com Lista

```markdown
---

# Components

## Main Architecture

1. **Encoder**
   - Self-attention layer
   - Feed-forward network

2. **Decoder**
   - Self-attention layer
   - Cross-attention layer
   - Feed-forward network

3. **Positional Encoding**
   - Adiciona informação de posição

**Ver também**: [[Transformer Architecture]] (wiki/concepts/transformer-architecture.md)
```

### Slide com Código

```markdown
---

# Self-Attention

## Implementation

```python
def scaled_dot_product_attention(Q, K, V):
    """
    Q: Queries (batch_size, seq_len, d_k)
    K: Keys (batch_size, seq_len, d_k)
    V: Values (batch_size, seq_len, d_v)
    """
    # Calcula scores
    scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)

    # Softmax
    attention_weights = F.softmax(scores, dim=-1)

    # Valores ponderados
    output = torch.matmul(attention_weights, V)

    return output, attention_weights
```

**Fonte**: [[Annotated Transformer]] (raw/articles/annotated-transformer.md)
```

### Slide com Imagem

```markdown
---

# Transformer Architecture

## Diagram

![width:900px](raw/assets/transformer-architecture.png)

**Componentes**: Encoder (esquerda), Decoder (direita)
**Data**: [[Attention Is All You Need]] (2017)
```

### Slide com Tabela

```markdown
---

# Positional Encoding: Comparison

| Aspect | Absolute | Relative |
|--------|----------|----------|
| Generalização | Pobre | Excelente |
| Complexidade | O(1) | O(n²) |
| Quando usar | Sequências de comprimento fixo | Sequências de comprimento variável |

**Fonte**: [[Positional Encoding Variants Comparison]] (wiki/comparisons/positional-encoding-variants.md)
```

### Slide com Citações

```markdown
---

# Key Insights

## Why Transformers Work

> "The Transformer allows for significantly more parallelization and can reach a new state of the art in translation quality after being trained for as little as twelve hours on eight P100s."

— Vaswani et al., 2017

**Fonte**: [[Attention Is All You Need]] (raw/papers/attention-is-all-you-need.pdf)
```

### Slide de Conclusão

```markdown
---

# Summary

## Takeaways

1. **Attention is powerful**
   - Substitui RNNs e CNNs para sequências

2. **Positional encoding is essential**
   - Adiciona informação de ordem

3. **Variations exist**
   - Relative vs Absolute
   - Sparse attention, Linear attention

## Thank You!

**Questions?**

**Links**:
- [[Transformer Architecture]] (wiki/concepts/transformer-architecture.md)
- [[Attention Mechanism]] (wiki/concepts/attention-mechanism.md)
```

## Layout Avançado

### Dois Colunas

```markdown
---

# Split Layout

<div class="columns">
<div>

## Encoder

- Self-attention
- Position-wise feed-forward
- Residual connections

</div>
<div>

## Decoder

- Self-attention
- Cross-attention
- Position-wise feed-forward

</div>
</div>

**Arquitetura completa**: [[Transformer Architecture]] (wiki/concepts/transformer-architecture.md)
```

### Slide com Notas (Speaker Notes)

```markdown
---

# Attention Mechanism

## Key Idea

Attention computes weighted sums of values based on queries and keys.

<!--
NOTAS PARA O APRESENTADOR:
- Explique a analogia de queries/keys/values
- Mostre o exemplo de busca em banco de dados
- Destaque a importância do scaling factor
-->
```

### Slide com Highlight

```markdown
---

# Self-Attention: Key Equation

<div class="highlight">

$$ \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V $$

</div>

**Componentes**:
- Q (Queries): O que estou buscando?
- K (Keys): O que cada token representa?
- V (Values): O conteúdo a ser retornado?

**Fonte**: [[Attention Mechanism]] (wiki/concepts/attention-mechanism.md)
```

## Exportação

### Exportar para PDF

```bash
marp apresentacao.md -o apresentacao.pdf
```

### Exportar para HTML (interativo)

```bash
marp apresentacao.md -o apresentacao.html
```

### Exportar para PowerPoint

```bash
marp apresentacao.md -o apresentacao.pptx
```

### Exportar para Imagens (PNG)

```bash
marp apresentacao.md -o apresentacao-%d.png
```

## Integração com Obsidian

### Plugin Marp for Obsidian

**Instalação**:
```
Settings → Community Plugins → Browse → Search "Marp for Obsidian"
```

**Uso**:
1. Adiciona frontmatter Marp no arquivo markdown
2. Clique no botão "Export" do plugin Marp
3. Escolha formato (PDF, PPTX, etc.)

### Exemplo no Wiki LLM

**Arquivo**: `wiki/presentations/transformer-architecture.md`

```markdown
---
marp: true
theme: gaia
paginate: true
type: presentation
---

# Transformer Architecture

## An Introduction to Attention-Based Sequence Models

**Date**: 2026-04-21
**Source**: [[Transformer Architecture]] (wiki/concepts/transformer-architecture.md)

---

# What is a Transformer?

[Conteúdo...]

---

[Outros slides...]
```

**Para exportar**:
1. Abra arquivo no Obsidian
2. Plugin Marp → Export → PDF

## Padrões de Uso

### 1. Apresentação de Conceito

```markdown
---
marp: true
theme: gaia
paginate: true
type: concept-presentation
---

# [Nome do Conceito]

[Slide 1: Introdução]
[Slide 2: Definição]
[Slide 3: Componentes]
[Slide 4: Como funciona]
[Slide 5: Exemplos]
[Slide 6: Conclusão]
```

### 2. Apresentação de Comparação

```markdown
---
marp: true
theme: gaia
paginate: true
type: comparison-presentation
---

# Comparison: [Conceito A] vs [Conceito B]

[Slide 1: Introdução]
[Slide 2: Conceito A]
[Slide 3: Conceito B]
[Slide 4: Tabela Comparativa]
[Slide 5: Trade-offs]
[Slide 6: Quando usar cada um]
[Slide 7: Conclusão]
```

### 3. Apresentação de Síntese

```markdown
---
marp: true
theme: gaia
paginate: true
type: synthesis-presentation
---

# Synthesis: [Tópico]

[Slide 1: Visão Geral]
[Slide 2: Estado da Arte]
[Slide 3: Evolução Temporal]
[Slide 4: Tendências Atuais]
[Slide 5: Direções Futuras]
[Slide 6: Conclusão]
```

### 4. Apresentação de Caso de Uso

```markdown
---
marp: true
theme: gaia
paginate: true
type: usecase-presentation
---

# Use Case: [Nome do Caso]

[Slide 1: Contexto]
[Slide 2: Problema]
[Slide 3: Solução]
[Slide 4: Implementação]
[Slide 5: Resultados]
[Slide 6: Lições Aprendidas]
[Slide 7: Conclusão]
```

## Criação Automática com LLM

### Pedir ao LLM para criar apresentação

**Comando ao LLM**:
```
Crie uma apresentação Marp sobre "Transformer Architecture".

Use wiki/concepts/transformer-architecture.md como conteúdo base.

Adicione:
- Frontmatter Marp completo
- 8-10 slides
- Código onde relevante
- Imagens se disponíveis
- Citações para o wiki

Salve em wiki/presentations/transformer-architecture.md
```

**Resultado**:
```markdown
---
marp: true
theme: gaia
paginate: true
type: presentation
title: Transformer Architecture
---

# Transformer Architecture

## An Introduction to Attention-Based Sequence Models

**Date**: 2026-04-21
**Source**: [[Transformer Architecture]] (wiki/concepts/transformer-architecture.md)

---

# What is a Transformer?

[Resto dos slides...]
```

### Pedir ao LLM para criar apresentação a partir de query

**Comando ao LLM**:
```
Crie uma apresentação Marp respondendo a: "Quais são as principais variações de positional encoding?"

Use wiki/concepts/positional-encoding.md e wiki/concepts/relative-positional-encoding.md como conteúdo.

Adicione:
- Tabela comparativa
- Quando usar cada um
- Recomendações

Salve em wiki/presentations/positional-encoding-variations.md
```

## Boas Práticas

### 1. Manter Slides Concisos

**Ruim** (muito texto):
```markdown
---

# Positional Encoding

## Absolute Positional Encoding

Absolute positional encoding is a technique used in transformers to add information about the position of tokens in a sequence. It uses sine and cosine functions of different frequencies to encode positional information, which allows the model to learn relationships between positions that are close in the sequence. The original paper "Attention Is All You Need" introduced this approach, and it has become the standard for many transformer models. The main advantage is that it's simple and works well for sequences of similar length to the training data, but it doesn't generalize well to longer sequences.
```

**Bom** (conciso):
```markdown
---

# Positional Encoding

## Absolute Positional Encoding

- **Technique**: Sine & cosine functions
- **Introduced**: Attention Is All You Need (2017)
- **Pros**: Simple, works well for similar lengths
- **Cons**: Doesn't generalize to longer sequences

**Source**: [[Positional Encoding]] (wiki/concepts/positional-encoding.md)
```

### 2. Usar Código Onde Relevante

**Quando usar código**:
- Para mostrar implementação
- Para explicar algoritmos
- Para ilustrar conceitos

**Quando NÃO usar código**:
- Para conceitos conceituais
- Para ideias abstratas
- Para comparações de alto nível

### 3. Adicionar Citações do Wiki

**Padrão**: `[[Nome do Conceito]] (wiki/path/to/concept.md)`

**Por que?**
- Rastreabilidade
- Facilita aprofundar após apresentação
- Conecta apresentação ao wiki

### 4. Usar Imagens Onde Possível

**Para criar diagrama**:
```markdown
---

# Self-Attention: Visualization

![width:800px](raw/assets/self-attention-visualization.png)

**How it works**:
1. Queries compare to all Keys
2. Softmax creates attention weights
3. Values are weighted and summed
```

**Para não criar diagrama**:
- Use Marp se tiver imagem pronta
- Use código se quiser mostrar implementação
- Use descrição textual se não tiver nem diagrama nem código

## Troubleshooting

### Problema: Marp não reconhece frontmatter

**Sintoma**: Slide aparece como markdown cru

**Causa**: Frontmatter não no início do arquivo ou formato incorreto

**Solução**: Verifique que frontmatter está nas primeiras 3 linhas
```markdown
---
marp: true
theme: gaia
---

# Título
```

### Problema: Tema não carrega

**Sintoma**: Slide usa tema padrão em vez do tema especificado

**Causa**: Nome de tema incorreto

**Solução**: Use nome de tema correto
```markdown
---
marp: true
theme: gaia  ← Tema correto (gaia, default, uncover)
---
```

### Problema: Imagem não aparece

**Sintoma**: `![alt](path)` aparece quebrado

**Causa**: Caminho incorreto ou imagem não existe

**Solução**: Verifique caminho
```markdown
![width:800px](raw/assets/nome-da-imagem.png)  ← Caminho correto
```

### Problema: Tabela muito larga

**Sintoma**: Tabela sai da página

**Causa**: Muitas colunas ou texto longo

**Solução 1**: Reduzir colunas
```markdown
# Antes (5 colunas)
| A | B | C | D | E |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

# Depois (3 colunas)
| A | B | C |
|---|---|---|
| ... | ... | ... |
```

**Solução 2**: Usar abreviações
```markdown
# Antes (texto longo)
| Absolute Positional Encoding | Relative Positional Encoding |
|------------------------------|------------------------------|

# Depois (abreviado)
| Absolute | Relative |
|----------|----------|
```

---

**Próximo**: Ferramentas: Dataview