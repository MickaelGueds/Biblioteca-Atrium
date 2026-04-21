# Manutenção do Wiki

## Visão Geral

Manutenção é o processo periódico de health-check do wiki. O LLM identifica contradições, páginas órfãs, lacunas de conhecimento e sugere melhorias.

## Quando Fazer Manutenção

### Disparadores Automáticos

- [ ] Após adicionar 10 novas fontes
- [ ] Após 50 perguntas ao wiki
- [ ] Semanalmente (se wiki ativo diariamente)
- [ ] Mensalmente (se uso moderado)
- [ ] Trimestralmente (se uso esporádico)

### Disparadores Manuais

- [ ] Quando sentir que respostas estão inconsistentes
- [ ] Ao notar links quebrados
- [ ] Ao perceber lacunas óbvias de conhecimento
- [ ] Antes de começar um novo projeto que depende do wiki

## Fluxo de Manutenção

```
1. Solicitar health-check
   ↓
2. LLM verifica consistência
   ↓
3. LLM identifica páginas órfãs
   ↓
4. LLM detecta lacunas de conhecimento
   ↓
5. LLM sugere novas fontes
   ↓
6. LLM propõe reestruturação
   ↓
7. Você revisa e aprova alterações
   ↓
8. LLM implementa alterações
```

## Comando de Manutenção

### Health-Check Básico

```
Por favor, faça um health-check do wiki.

Verifique:
1. Contradições entre páginas
2. Páginas sem links de entrada (órfãs)
3. Links quebrados
4. Conceitos mencionados mas sem página própria
5. Páginas desatualizadas (fontes antigas sem atualizações recentes)
```

### Health-Check Completo

```
Por favor, faça um health-check completo do wiki.

Verifique:

1. Consistência
   - Contradições entre páginas
   - Afirmativas conflitantes sobre o mesmo conceito
   - Dados inconsistentes em tabelas comparativas

2. Integridade
   - Páginas órfãs (sem links de entrada)
   - Links quebrados (apontam para páginas inexistentes)
   - Conceitos mencionados mas sem página própria

3. Atualização
   - Fontes antigas sem atualizações recentes (> 6 meses)
   - Páginas com dados desatualizados
   - Descobertas recentes não refletidas

4. Estrutura
   - Páginas que deveriam ser separadas mas estão juntas
   - Tópicos relacionados que deveriam estar conectados
   - Hierarquia inconsistente

5. Cobertura
   - Lacunas óbvias de conhecimento
   - Conceitos importantes mencionados mas não explorados
   - Fontes faltantes para completar um tópico

6. Oportunidades
   - Conexões não óbvias entre páginas
   - Sínteses que poderiam ser criadas
   - Perguntas que o wiki poderia responder mas não está estruturado para

Gere um relatório detalhado com:
- Problemas encontrados (categorizados por severidade)
- Recomendações de ação
- Estimativa de esforço para cada ação
```

## Relatório de Health-Check

### Exemplo de Relatório

```markdown
# Health-Check Report

**Data**: 2026-04-21
**Páginas analisadas**: 147
**Conceitos identificados**: 89
**Entidades identificadas**: 34

## 🔴 Crítico (requer ação imediata)

### 1. Contradição em Positional Encoding

**Localização**:
- wiki/concepts/positional-encoding.md: "custo computacional O(1)"
- wiki/concepts/relative-positional-encoding.md: "custo computacional O(n²)"

**Problema**: Ambos os conceitos são citados na mesma tabela comparativa em
wiki/comparisons/positional-encoding-variants.md com custo computacional O(1),
o que está incorreto para Relative Positional Encoding.

**Ação recomendada**: Atualizar tabela em wiki/comparisons/positional-encoding-variants.md

**Severidade**: Alta - dados incorretos podem levar a decisões erradas

**Esforço estimado**: 5 minutos

---

### 2. Link Quebrado em Self-Attention

**Localização**: wiki/concepts/self-attention.md

**Link quebrado**: [[Multi-Head Attention Variants]] → página não existe

**Ação recomendada**:
- Remover link ou criar página faltante
- Verificar se conteúdo deveria estar em outra página

**Severidade**: Média - afeta navegação

**Esforço estimado**: 10 minutos (criar página) ou 2 minutos (remover link)

---

## 🟡 Importante (deve ser feito em breve)

### 3. Páginas Órfãs

**Páginas sem links de entrada**:
- wiki/concepts/feed-forward-gating.md (criada há 3 meses, nunca citada)
- wiki/entities/openai-research.md (criada há 2 meses, 1 link de entrada)
- wiki/synthesis/early-attention-papers.md (criada há 5 meses, nunca citada)

**Ação recomendada**:
- wiki/concepts/feed-forward-gating.md: integrar em página de Feed-Forward
  ou criar link de wiki/concepts/feed-forward-layer.md
- wiki/entities/openai-research.md: está bem, tem 1 link (pode aumentar)
- wiki/synthesis/early-attention-papers.md: criar link de
  wiki/synthesis/attention-mechanism-evolution.md

**Severidade**: Média - conhecimento existente mas não acessível

**Esforço estimado**: 15 minutos

---

### 4. Fontes Desatualizadas

**Páginas com fontes antigas (> 6 meses)**:
- wiki/concepts/positional-encoding.md: última atualização 2025-11-15 (5 meses)
- wiki/concepts/layer-normalization.md: última atualização 2025-10-22 (6 meses)

**Ação recomendada**: Buscar fontes recentes em:
- ArXiv (últimos 3 meses)
- Conferências recentes (ICML, NeurIPS, ICLR 2026)
- Blogs de research (Google AI, OpenAI, Anthropic)

**Severidade**: Baixa - conhecimento válido mas pode estar incompleto

**Esforço estimado**: 30 minutos (busca + ingestão)

---

## 🟢 Sugestões (oportunidades de melhoria)

### 5. Conexão Não Óbvia

**Conexão identificada**:
- wiki/concepts/feed-forward-gating.md (órfã) está diretamente relacionada a
  wiki/concepts/efficient-transformers.md (ativas)

**Relação**: Gating é uma técnica de optimization usada em Efficient Transformers,
mas nunca foi conectada.

**Ação recomendada**: Criar link bidirecional entre as páginas

**Severidade**: Baixa - melhoria de descoberta

**Esforço estimado**: 5 minutos

---

### 6. Síntese Faltante

**Pergunta que o wiki poderia responder mas não está estruturado**:
"Qual o melhor positional encoding para meu caso de uso específico?"

**Ação recomendada**: Criar página wiki/synthesis/positional-encoding-decision-tree.md
com um decision tree baseado em:
- Comprimento de sequência
- Variabilidade de comprimento
- Custo computacional disponível
- Necessidade de generalização

**Severidade**: Baixa - melhoria de usabilidade

**Esforço estimado**: 20 minutos

---

## 📊 Estatísticas Gerais

### Cobertura
- Conceitos com página própria: 76/89 (85%)
- Entidades com página própria: 32/34 (94%)
- Fontes processadas: 47

### Qualidade
- Contradições encontradas: 1
- Links quebrados: 1
- Páginas órfãs: 3
- Páginas desatualizadas: 2

### Oportunidades
- Conexões não óbvias: 1
- Sínteses que poderiam ser criadas: 3
- Perguntas sem resposta estruturada: 2

## 🎯 Prioridades

### Imediato (esta semana)
1. [ ] Corrigir contradição em Positional Encoding (5 min)
2. [ ] Corrigir link quebrado em Self-Attention (10 min)

### Curto prazo (próximas 2 semanas)
3. [ ] Integrar páginas órfãs (15 min)
4. [ ] Atualizar fontes desatualizadas (30 min)

### Médio prazo (próximo mês)
5. [ ] Criar conexões não óbvias (5 min)
6. [ ] Criar sínteses faltantes (20 min)

## 💡 Sugestões de Novas Fontes

Baseado em lacunas identificadas:

1. **Positional Encoding (2026)**:
   - Buscar papers recentes em ArXiv com "positional encoding 2026"
   - Conferência ICML 2026 proceedings
   - Blog posts recentes sobre positional encoding

2. **Layer Normalization (2026)**:
   - Buscar papers com "layer normalization 2026"
   - Verificar se há novas variantes (Pre-LN 2.0?)
   - Conferência NeurIPS 2025 proceedings

## 🔄 Sugestões de Reestruturação

### Proposta 1: Consolidar Pages

**Páginas a consolidar**:
- wiki/concepts/feed-forward-gating.md → wiki/concepts/feed-forward-layer.md

**Motivo**: Feed-Forward Gating é uma variação específica, não um conceito separado.
Conteúdo deve ser seção em Feed-Forward Layer.

**Esforço**: 10 minutos

---

### Proposta 2: Criar Nova Hierarquia

**Nova estrutura proposta**:
```
wiki/concepts/attention/
  ├── mechanisms/
  │   ├── self-attention.md
  │   ├── multi-head-attention.md
  │   └── sparse-attention.md
  └── optimization/
      ├── efficient-attention.md
      ├── linear-attention.md
      └── [outros...]
```

**Motivo**: Páginas de attention estão misturadas com páginas de optimization.
Separar em sub-pastas melhoraria organização.

**Esforço**: 30 minutos

---

## ✅ Status Geral

**Qualidade do wiki**: Boa (8.2/10)
- Poucas contradições
- Alta cobertura de conceitos
- Algumas páginas órfãs
- Oportunidades de melhoria identificadas

**Próximo health-check**: 2026-06-21 (em 2 meses)

---

**Comando para implementar correções**:
"Por favor, implemente as correções de severidade Alta (1 e 2) do relatório."
```

## Implementação de Correções

### Após Revisar Relatório

```
Por favor, implemente as correções de severidade Alta:

1. Corrigir contradição em Positional Encoding
2. Corrigir link quebrado em Self-Attention

Para cada correção:
- Explique o que vai fazer
- Faça a alteração
- Confirme que foi resolvida
```

### LLM Implementa

```
**Correção 1: Contradição em Positional Encoding**

Vou atualizar a tabela comparativa em wiki/comparisons/positional-encoding-variants.md

[LLM lê a página]
[LLM identifica o erro]
[LLM corrige o custo computacional de O(1) para O(n²) para Relative Positional Encoding]
[LLM salva a página]

✅ Contradição corrigida. Tabela agora mostra corretamente:
- Absolute Positional Encoding: O(1)
- Relative Positional Encoding: O(n²)

---

**Correção 2: Link Quebrado em Self-Attention**

Vou verificar o link quebrado [[Multi-Head Attention Variants]] em wiki/concepts/self-attention.md

[LLM lê a página]
[LLM verifica se a página existe]
[LLM determina que o conteúdo deveria estar em wiki/concepts/multi-head-attention.md]
[LLM atualiza o link]

✅ Link quebrado corrigido. Agora aponta para [[Multi-Head Attention]]
```

## Manutenção Contínua

### Checklist Semanal Rápido

```
Por favor, faça um health-check rápido do wiki (5 minutos):

- Verifique se há contradições óbvias
- Identifique links quebrados
- Liste páginas órfãs criadas esta semana
- Sugira 1-2 fontes novas baseadas em lacunas
```

### Checklist Mensal Detalhado

```
Por favor, faça um health-check detalhado do wiki (30 minutos):

[Inclua todas as verificações do health-check completo]
```

## Prevenção de Problemas

### Boas Práticas

1. **Sempre crie links bidirecionais**
   - Se cria link A → B, também crie B → A
   - O LLM deve fazer isso automaticamente

2. **Cite fontes explicitamente**
   - Cada afirmação deve ter uma fonte
   - Use formato [[Nome da Fonte]] com caminho em raw/

3. **Use metadata YAML consistentemente**
   - Todas as páginas devem ter frontmatter
   - Tags, last_updated, sources_count devem ser mantidos

4. **Atualize log.md**
   - Cada alteração significativa deve ser registrada
   - Use formato consistente: `## [YYYY-MM-DD] update | descrição`

5. **Revise páginas periodicamente**
   - Verifique se conteúdo está atualizado
   - Busque fontes recentes se necessário

---

**Próximo**: Índice e Log