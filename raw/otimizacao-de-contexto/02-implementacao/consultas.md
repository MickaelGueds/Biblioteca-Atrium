# Consultas ao Wiki

## Visão Geral

Consultas são perguntas feitas ao wiki. O LLM busca páginas relevantes, as lê e sintetiza respostas com citações. Respostas valiosas podem ser arquivadas no wiki.

## Fluxo de Consulta

```
1. Você faz uma pergunta
   ↓
2. LLM busca no index
   ↓
3. LLM lê páginas relevantes
   ↓
4. LLM segue links conforme necessário
   ↓
5. LLM sintetiza resposta com citações
   ↓
6. (Opcional) Resposta é arquivada no wiki
   ↓
7. Você revisa e dá feedback
```

## Tipos de Consultas

### 1. Consultas Focadas (Factual)

**Exemplo**: "O que é Relative Positional Encoding?"

```
Você: "O que é Relative Positional Encoding?"

LLM processa:
1. Busca em index.md → encontra "Relative Positional Encoding"
2. Lê wiki/concepts/relative-positional-encoding.md
3. Sintetiza resposta

Resposta:
Relative Positional Encoding é uma variação de positional encoding que
representa posições relativas em vez de absolutas, permitindo maior
generalização para comprimentos de sequência não vistos durante
treinamento.

Principais características:
- Usa distâncias entre tokens em vez de posições absolutas
- Melhora generalização para sequências mais longas
- Trade-off: maior complexidade computacional (O(n²) vs O(1))

Quando usar:
- Sequências muito longas (> 2048 tokens)
- Comprimento variável de sequência
- Quando generalização é mais importante que performance absoluta

Fontes:
1. Self-Attention with Relative Position Representations
   (raw/papers/relative-positional-encoding.pdf)

Ver também:
- Positional Encoding (versão absoluta)
- Self-Attention (mecanismo base)
```

### 2. Consultas Relacionais (Conexões)

**Exemplo**: "Qual a relação entre Relative e Absolute Positional Encoding?"

```
Você: "Qual a relação entre Relative e Absolute Positional Encoding?"

LLM processa:
1. Busca em index.md → encontra ambos os conceitos
2. Lê ambas as páginas
3. Identifica seções de comparação
4. Sintetiza resposta

Resposta:
Ambas são técnicas de positional encoding usadas em Transformers, mas
com abordagens diferentes:

Absolute Positional Encoding:
- Representa posição como número absoluto (0, 1, 2, ...)
- Custo: O(1)
- Limitações: generalização pobre para sequências mais longas
- Usado no Transformer original

Relative Positional Encoding:
- Representa posição como distância relativa entre tokens
- Custo: O(n²)
- Vantagens: melhor generalização
- Usado quando comprimento de sequência varia muito

Conexão:
Relative é uma variação de Absolute, projetada para superar suas
limitações de generalização.

Comparação detalhada:
- wiki/concepts/relative-positional-encoding.md#trade-offs
- wiki/concepts/positional-encoding.md#variações

Fontes:
1. Attention Is All You Need (original)
2. Self-Attention with Relative Position Representations (variação)
```

### 3. Consultas Evolutivas (Histórico)

**Exemplo**: "Como a ideia de positional encoding evoluiu?"

```
Você: "Como a ideia de positional encoding evoluiu?"

LLM processa:
1. Busca "positional encoding" em index.md
2. Lê página principal
3. Segue links para variações
4. Sintetiza linha do tempo

Resposta:
A ideia de positional encoding evoluiu em 3 fases principais:

Fase 1: Absolute Positional Encoding (2017)
- Paper seminal: Attention Is All You Need
- Abordagem: seno e cosseno com frequências variadas
- Limitações: não generaliza bem para sequências mais longas

Fase 2: Learned Positional Encoding (2018)
- Paper: BERT
- Abordagem: embeddings aprendidos
- Limitações: fixo ao comprimento máximo de treinamento

Fase 3: Relative Positional Encoding (2020-2024)
- Papers: Various
- Abordagem: distâncias relativas entre tokens
- Vantagens: generalização para qualquer comprimento

Linha do tempo detalhada:
- wiki/synthesis/positional-encoding-evolution.md

Fontes por ordem:
1. raw/papers/attention-is-all-you-need.pdf (2017)
2. raw/papers/bert.pdf (2018)
3. raw/papers/relative-positional-encoding.pdf (2020)
[mais papers...]
```

### 4. Consultas Comparativas (Trade-offs)

**Exemplo**: "Compare Relative e Absolute Positional Encoding"

```
Você: "Compare Relative e Absolute Positional Encoding"

LLM processa:
1. Busca ambos os conceitos
2. Lê páginas e seções de trade-offs
3. Cria tabela comparativa
4. Sintetiza recomendações

Resposta:
Comparação entre Absolute e Relative Positional Encoding:

| Aspecto | Absolute | Relative |
|---------|----------|----------|
| Generalização | Pobre | Excelente |
| Complexidade | O(1) | O(n²) |
| Treinamento | Simples | Moderado |
| Performance no mesmo comprimento | 100% | ~98% |
| Performance em sequências mais longas | Degrada significativamente | Mantém ~95% |

Quando usar Absolute:
- Sequências de comprimento fixo
- Performance é crítica
- Custo computacional é preocupação
- Casos de uso simples

Quando usar Relative:
- Sequências de comprimento variável
- Generalização é importante
- Custo computacional não é crítico
- Casos de uso complexos

Recomendação:
Para produção, comece com Absolute (simples e rápido). Se precisar de
generalização, considere Relative ou abordagens híbridas.

Tabela detalhada:
- wiki/comparisons/positional-encoding-variants.md

Fontes:
- raw/papers/attention-is-all-you-need.pdf
- raw/papers/relative-positional-encoding.pdf
- raw/papers/hybrid-positional-encoding.pdf
```

### 5. Consultas Exploratórias (Descoberta)

**Exemplo**: "Quais padrões de optimization são usados em Transformers?"

```
Você: "Quais padrões de optimization são usados em Transformers?"

LLM processa:
1. Busca "optimization" e "transformer" em index.md
2. Lê páginas relevantes
3. Identifica padrões
4. Agrupa por categoria

Resposta:
Identifiquei 5 padrões principais de optimization em Transformers:

1. **Positional Encoding Optimization**
   - Absolute → Relative → Híbrido
   - Trade-off: generalização vs complexidade
   - wiki/concepts/positional-encoding.md

2. **Attention Mechanism Optimization**
   - Standard → Sparse → Linear
   - Trade-off: fidelidade vs custo
   - wiki/concepts/attention-mechanism.md

3. **Layer Normalization**
   - Pre-norm vs Post-norm
   - Trade-off: estabilidade vs convergência
   - wiki/concepts/layer-normalization.md

4. **Position-wise Feed-Forward**
   - Standard → Gated → ReLU → GeLU
   - Trade-off: expressividade vs custo
   - wiki/concepts/feed-forward-layer.md

5. **Training Techniques**
   - Warmup → Cosine scheduling → AdamW
   - Trade-off: estabilidade vs velocidade
   - wiki/synthesis/transformer-training.md

Padrões não óbvios:
- 3 dos 5 padrões têm abordagens "híbridas" que buscam equilíbrio
- Sparse Attention e Relative Positional Encoding têm custos similares (O(n²))
- Pre-norm e Post-norm foram usados em períodos diferentes (2017-2022)

Para explorar mais:
- wiki/synthesis/transformer-optimization-patterns.md
- wiki/concepts/[cada padrão acima]
```

## Arquivamento de Respostas

### Quando Arquivar

✅ **Arquivar se**:
- A resposta é um resumo valioso
- Cria nova conexão não documentada
- Responde uma pergunta complexa que pode ser feita novamente
- Síntese de múltiplas fontes
- Tabela comparativa útil

❌ **Não arquivar se**:
- A resposta é simples e óbvia
- Já existe página similar
- É uma pergunta única que não será repetida

### Como Arquivar

**Comando ao LLM**:
```
Arquive essa resposta no wiki em uma página de síntese.

Página: wiki/synthesis/positional-encoding-summary.md

Inclua:
- A pergunta original
- A resposta completa
- Citações de fontes
- Links para páginas relacionadas
- Data de criação
```

**Resultado**:
```markdown
---
type: synthesis
tags: [positional-encoding, summary, comparison]
sources_count: 3
last_updated: 2026-04-21
related_concepts: [Positional Encoding, Relative Positional Encoding]
---

# Summary: Comparison of Positional Encoding Approaches

## Pergunta Original
"Compare Relative e Absolute Positional Encoding"

## Resumo
[texto da resposta...]

## Comparação Detalhada
[tabela...]

## Recomendações
[texto...]

## Fontes
1. [[Attention Is All You Need]]
2. [[Self-Attention with Relative Position Representations]]
3. [[Hybrid Positional Encoding]]

## Ver Também
- [[Positional Encoding]]
- [[Relative Positional Encoding]]
- [[Positional Encoding Variants Comparison]]

## Metadata
- Criado: 2026-04-21
- Baseado em: 3 fontes
- Pergunta repetida: 2 vezes até agora
```

## Padrões de Consulta Eficientes

### Seja Específico

❌ Ruim: "Fale sobre Transformers"
✅ Bom: "Como o self-attention mechanism lida com dependências de longo alcance?"

### Use Termos do Wiki

❌ Ruim: "O que é a coisa de posição relativa?"
✅ Bom: "Quais as vantagens do Relative Positional Encoding em relação ao Absolute?"

### Peça Comparações

❌ Ruim: "Fale sobre positional encoding"
✅ Bom: "Compare Absolute, Relative e Híbrid Positional Encoding"

### Peça Evolução

❌ Ruim: "Quais tipos de positional encoding existem?"
✅ Bom: "Como a ideia de positional encoding evoluiu de 2017 até hoje?"

### Peça Recomendações

❌ Ruim: "Qual positional encoding usar?"
✅ Bom: "Quando devo usar Relative vs Absolute Positional Encoding?"

## Formatos de Resposta

Além de markdown, o LLM pode gerar:

### Tabelas
```
Por favor, gere uma tabela comparativa de todas as variações de positional encoding.
→ wiki/comparisons/positional-encoding-table.md
```

### Slides (Marp)
```
Crie uma apresentação sobre a evolução do positional encoding.
→ wiki/presentations/positional-encoding-evolution.md
```

### Gráficos
```
Gere um gráfico mostrando a trade-off de performance vs complexidade
entre Absolute e Relative Positional Encoding.
→ wiki/charts/positional-encoding-tradeoff.png
```

### Canvases
```
Crie um canvas visual conectando todos os padrões de optimization em Transformers.
→ wiki/canvases/transformer-optimization.canvas
```

---

**Próximo**: Manutenção do Wiki