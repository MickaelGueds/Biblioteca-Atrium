# Casos de Uso: Equipe e Negócios

## Visão Geral

Wiki interno mantido por LLMs, alimentado por threads do Slack, transcrições de reuniões, documentos de projeto, chamadas de clientes. O wiki fica atualizado porque o LLM faz a manutenção que ninguém na equipe quer fazer.

## Fontes de Dados

```
raw/negocios/
├── slack/
│   ├── canais/
│   │   ├── geral/
│   │   │   ├── 2026-04-21.md
│   │   │   └── ...
│   │   ├── engenharia/
│   │   ├── produto/
│   │   ├── design/
│   │   └── clientes/
│   └── dms/
│       └── [usuario]/[data]/
├── reunioes/
│   ├── diarias/
│   ├── semanais/
│   ├── mensais/
│   └── revisoes-projeto/
├── clientes/
│   ├── chamadas/
│   ├── tickets/
│   └── feedback/
├── projetos/
│   ├── [projeto-1]/
│   │   ├── requisitos.md
│   │   ├── prs/
│   │   └── releases/
│   └── [projeto-2]/
├── documentacao/
│   ├── arquitetura/
│   ├── apis/
│   └── guias/
└── noticias/
    ├── concorrentes/
    ├── mercado/
    └── tendencias/
```

## Estrutura do Wiki

```
wiki/negocios/
├── entidades/
│   ├── clientes.md
│   ├── parceiros.md
│   ├── fornecedores.md
│   ├── membros-equipe.md
│   ├── concorrentes.md
│   └── stakeholders.md
├── projetos/
│   ├── [projeto-1]/
│   │   ├── visao.md
│   │   ├── roadmap.md
│   │   ├── status.md
│   │   ├── decisoes.md
│   │   ├── riscos.md
│   │   └── aprendizados.md
│   └── [projeto-2]/
├── produtos/
│   ├── [produto-1]/
│   │   ├── features.md
│   │   ├── roadmap.md
│   │   ├── feedback-clientes.md
│   │   ├── bugs-conhecidos.md
│   │   └── metricas.md
│   └── [produto-2]/
├── processos/
│   ├── onboard.md
│   ├── code-review.md
│   ├── release.md
│   ├── comunicacao-cliente.md
│   └── gerenciamento-crise.md
├── metricas/
│   ├── kpis.md
│   ├── okrs.md
│   ├── dashboards.md
│   └── analises-customizadas.md
├── conhecimento/
│   ├── arquitetura.md
│   ├── stacks-tecnicas.md
│   ├── decisoes-arquiteturais.md
│   ├── padroes.md
│   └── anti-padroes.md
├── sintese/
│   ├── estado-da-empresa.md
│   ├── tendencia-mensal.md
│   ├── aprendizados-trimestrais.md
│   ├── oportunidades.md
│   └── riscos.md
└── index.md
```

## Fluxo de Trabalho

### Ingestão Automatizada

```bash
# Script que roda diariamente
1. Exporta threads do Slack (últimas 24h)
   → raw/negocios/slack/canais/*/YYYY-MM-DD.md

2. Exporta transcrições de reuniões (últimas 24h)
   → raw/negocios/reunioes/*/YYYY-MM-DD.md

3. Exporta chamadas de clientes (últimas 24h)
   → raw/negocios/clientes/chamadas/YYYY-MM-DD.md

4. Executa: "/graphify raw/negocios --update"
   → LLM processa novos arquivos e atualiza wiki

# Resultado: Wiki atualizado automaticamente diariamente
```

### Ingestão Manual

```
Evento ocorre (ex: grande decisão, crise, novo cliente)
    ↓
Adiciona notas a raw/negocios/projetos/[projeto]/decisoes.md
    ↓
Executa: "/graphify raw/negocios --update"
    ↓
LLM processa e atualiza wiki
    ↓
Equipe pode consultar wiki atualizado
```

## Exemplo de Consulta

```
Você: "Quais foram as principais decisões este mês?"

LLM processa:
1. Busca "decisões" em wiki/negocios/index.md
2. Lê wiki/negocios/sintese/tendencia-mensal.md
3. Lê wiki/negocios/projetos/*/decisoes.md
4. Sintetiza resposta

Resposta:
Principais decisões tomadas em abril de 2026:

## 1. Migração para Microserviços (Projeto: Monolith-to-Microservices)

**Decisão**: Aprovar migração gradual da monolito para microserviços

**Quando**: 2026-04-15

**Quem decidiu**: CTO, Lead de Engenharia, Arquiteto

**Contexto**:
- Monolito atual: 200k linhas de código, deploy 2h
- Problemas: deploy quebra funcionalidades não relacionadas, dificuldade de escala
- Proposta: Migrar para 5 microserviços em 6 meses
- Fontes:
  - raw/reunioes/mensais/2026-04-15.md (decisão final)
  - raw/slack/canais/engenharia/2026-04-10.md (discussão prévia)
  - wiki/negocios/projetos/monolith-to-microservices/decisoes.md

**Trade-offs**:
| Aspecto | Monolito | Microserviços |
|---------|----------|---------------|
| Deploy | 2h (tudo) | 5-10min (individual) |
| Escala | Difícil (escala tudo) | Fácil (escala apenas necessário) |
| Manutenção | Simples (um repo) | Complexo (vários repos) |
| Latência entre serviços | N/A | +10-20ms |

**Riscos**:
- Complexidade operacional (monitoramento, tracing)
- Latência adicional entre serviços
- Curva de aprendizado da equipe
- Fonte: wiki/negocios/projetos/monolith-to-microservices/riscos.md

**Timeline**:
- Fase 1 (Abril-Junho): Separar serviço de usuários
- Fase 2 (Julho-Setembro): Separar serviço de pagamentos
- Fase 3 (Outubro-Dezembro): Separar serviços restantes
- Fonte: wiki/negocios/projetos/monolith-to-microservices/roadmap.md

**Status**: Em andamento, fase 1 (35% concluída)

---

## 2. Contrato com Cliente Enterprise (Cliente: Acme Corp)

**Decisão**: Fechar contrato com Acme Corp por $500k/ano

**Quando**: 2026-04-08

**Quem decidiu**: CEO, Head de Vendas, CFO

**Contexto**:
- Acme Corp: Cliente enterprise (Fortune 500)
- Proposta: $500k/ano, 3 anos,条款 SLA 99.9%
- Negociação: 2 semanas, 3 iterações
- Fontes:
  - raw/clientes/chamadas/2026-03-25-acme.md (primeira chamada)
  - raw/clientes/chamadas/2026-04-05-acme.md (negociação final)
  - wiki/negocios/entidades/clientes.md#acme-corp

**Termos**:
- Valor: $500k/ano, 3 anos (total: $1.5M)
- Pagamento: Trimestral
- SLA: 99.9% uptime
- Suporte: 24/7 (necessita contratar +2 SRE)
- Customização: Features customizadas para Acme (~2 meses trabalho)

**Impacto**:
- Receita anual: +$500k (+20% do total)
- Custos: +$120k/ano (2 SREs + infraestrutura)
- Lucro líquido: +$380k/ano
- Capacidade: -15% (equipe vai focar em customização por 2 meses)
- Fonte: wiki/negocios/metricas/analises-customizadas.md#acme-corp-impacto

**Riscos**:
- SLA 99.9% é agressivo (atual: 99.5%)
- Customização pode criar "fornecedor lock-in"
- Acme pode exigir features que não beneficiam outros clientes
- Fonte: wiki/negocios/projetos/acme-corp-onboarding/riscos.md

**Status**: Assinado, onboarding em andamento (fase 1 de 3)

---

## 3. Adoção de AI Copilot para Desenvolvimento

**Decisão**: Comprar licenças de GitHub Copilot para todos os desenvolvedores

**Quando**: 2026-04-01

**Quem decidiu**: CTO, Lead de Engenharia, CFO

**Contexto**:
- Tamanho da equipe: 20 desenvolvedores
- Custo: $10/dev/mês = $200/mês = $2.400/ano
- Teste piloto: 2 desenvolvedores, 1 mês, +30% produtividade
- Fontes:
  - raw/slack/canais/engenharia/2026-03-20.md (pilot results)
  - wiki/negocios/processos/code-review.md (productivity metrics)

**Benefícios esperados**:
- Produtividade: +25-30% (baseado em piloto)
- Qualidade: Menos bugs (Copilot gera código padrão)
- Onboarding: Novos desenvolvedores aprendem stack mais rápido
- Moral: Desenvolvedores pediram (satisfação ↑)

**Custo-benefício**:
- Custo anual: $2.400
- Benefício anual (produtividade): +25% de 20 devs = +5 devs equivalentes
- Valor de 1 dev: $100k/ano (conservador)
- Benefício em valor: $500k/ano
- ROI: 20.800% (extremamente positivo)
- Fonte: wiki/negocios/metricas/analises-customizadas.md#copilot-roi

**Riscos**:
- Dependência de AI: Código pode não ser entendido se Copilot mudar
- Licenciamento: GitHub pode aumentar preços no futuro
- Qualidade: Copilot pode gerar código inseguro
- Fonte: wiki/negocios/conhecimento/anti-padroes.md#ai-dependencia

**Status**: Licenças compradas, em uso desde 2026-04-15

---

## Resumo Tendencial

**Padrões de decisão em abril 2026**:
1. **Investimento em tecnologia**: Migração microserviços, AI Copilot
2. **Foco em receita enterprise**: Acme Corp ($500k/ano)
3. **Risco calculado**: Microserviços aumenta complexidade, mas benefícios superam riscos

**Mudança vs março 2026**:
- Mais decisões técnicas (2 vs 0 em março)
- Menos decisões de produto (0 vs 2 em março)
- Foco em infraestrutura para escalar (necessário para crescimento)
- Fonte: wiki/negocios/sintese/tendencia-mensal.md

**Próximas decisões esperadas**:
- Contratação de +2 SREs (para Acme SLA)
- Escolha de framework de frontend (debate em andamento no Slack)
- Expansão para mercado europeu (em discussão)
- Fonte: wiki/negocios/sintese/estado-da-empresa.md#roadmap-decisoes

Fontes principais:
- raw/reunioes/mensais/2026-04-15.md
- raw/clientes/chamadas/2026-04-05-acme.md
- raw/slack/canais/engenharia/2026-03-20.md
- wiki/negocios/sintese/tendencia-mensal.md
```

## Casos de Uso Específicos

### 1. Onboarding de Novos Membros

**Problema**: Novo desenvolvedor chega, precisa aprender stack, projetos, processos

**Tradicional**:
- Documentação estática (freq desatualizada)
- Ask colegas (interrupções)
- 2-3 semanas para ser produtivo

**Com Wiki LLM**:

```
Novo desenvolvedor: "Quais são os projetos ativos e qual devo começar?"

LLM responde (instantaneamente):
Projeto: Monolith-to-Microservices
- Prioridade: Alta (decisão de abril 2026)
- Status: Fase 1, 35% concluída
- Stack: Node.js, TypeScript, Kubernetes
- Responsável: João Silva (Lead)
- Recursos para aprender:
  - wiki/negocios/conhecimento/arquitetura.md (visão geral)
  - wiki/negocios/projetos/monolith-to-microservices/visao.md (detalhes)
  - wiki/negocios/processos/code-review.md (processo)
  - wiki/negocios/membros-equipe.md#joao-silva (quem perguntar)

Próximos passos:
1. Leia wiki/negocios/conhecimento/arquitetura.md (30min)
2. Converse com João Silva (15min)
3. Leia wiki/negocios/projetos/monolith-to-microservices/visao.md (1h)
4. Comece com tickets pequenos (ver wiki/negocios/projetos/monolith-to-microservices/roadmap.md)

Tempo estimado para contribuir: 1-2 dias (vs 2-3 semanas tradicional)
```

### 2. Comunicação com Clientes

**Problema**: Cliente pergunta sobre status, roadmaps, features. Precisa respostas consistentes.

**Tradicional**:
- Procurar em emails, docs, Slack
- Perguntar time (interrupções)
- Risco de respostas inconsistentes

**Com Wiki LLM**:

```
Cliente: "Quando feature X estará disponível?"

Equipe usa wiki LLM para gerar resposta:

LLM:
Status da feature X:
- Planejado: Q2 2026
- Prioridade: Alta (solicitado por 3 clientes enterprise)
- Bloqueadores: Dependência de migração microserviços (Fase 1 concluída em junho 2026)
- Estimativa: Disponível julho-agosto 2026
- Fontes:
  - wiki/negocios/produtos/[produto]/features.md (status)
  - wiki/negocios/produtos/[produto]/roadmap.md (timeline)
  - wiki/negocios/clientes/feedback.md (solicitações)

Draft de resposta para cliente:
"Feature X está planejada para Q2 2026. Estimamos disponibilizá-la em julho-agosto de 2026. Atualmente, estamos trabalhando na migração para microserviços, que é um pré-requisito. A feature foi solicitada por 3 clientes enterprise, incluindo você, por isso tem alta prioridade. Vamos te avisar assim que estiver disponível para beta testing."

Fonte: wiki/negocios/processos/comunicacao-cliente.md (guideline de comunicação)
```

### 3. Gerenciamento de Crise

**Problema**: Crise acontece (outage, bug crítico, PR desfavorável). Precisa contexto rápido.

**Tradicional**:
- Procurar docs, emails, Slack (demorado)
- Perguntar time (interrupções)
- Risco de informações incompletas

**Com Wiki LLM**:

```
Crise: Outage de 2h, clientes afetados

Você (CTO): "O que aconteceu, quais foram as causas raiz, quais clientes foram afetados?"

LLM responde (instantaneamente):

**O que aconteceu**:
- Outage: 2026-04-21 10:00-12:00 UTC (2h)
- Impacto: 75% dos clientes, 95% de tráfego
- Status: Resolvido, investigação em andamento
- Fontes:
  - raw/reunioes/gestao-crise/2026-04-21-10h15.md (incident report inicial)
  - raw/slack/canais/engenharia/2026-04-21.md (investigação em tempo real)

**Causas raiz**:
1. Primary: Deploy de microserviço de usuários (Fase 1) causou conflito com monolito
   - Detalhe: Nova versão de microserviço não foi testada com monolito em produção
2. Secondary: Rollback automático falhou (bug no script)
   - Detalhe: Script de rollback não considera casos de cross-service deployment
3. Contributing: Monitoramento não detectou degradamento inicialmente
   - Detalhe: Alertas configurados para monolito, não para cross-service
- Fontes:
  - raw/reunioes/gestao-crise/2026-04-21-12h30.md (post-mortem parcial)
  - wiki/negocios/projetos/monolith-to-microservices/riscos.md (risco previsto!)

**Clientes afetados**:
- Total: 75% de clientes (15 de 20)
- Enterprise: 3 de 5 (Acme Corp, Beta Corp, Gamma Corp)
- SLA impactado: 99.9% (Acme Corp) - risco de violação
- Clientes não afetados: 5 (Staging environment, clientes on-premise)
- Fontes:
  - raw/clientes/chamadas/2026-04-21.md (reclamações clientes)
  - wiki/negocios/entidades/clientes.md

**Ações tomadas**:
1. 10:15: Incident declarado, engenharia convocada
2. 10:30: Rollback manual executado (script automático falhou)
3. 10:45: Serviço restaurado parcialmente (80%)
4. 11:30: Serviço restaurado completamente
5. 12:00: Incident declarado resolvido
- Fonte: raw/reunioes/gestao-crise/2026-04-21.md (timeline completa)

**Comunicação com clientes**:
- 10:20: Email enviado para todos os clientes (notificação inicial)
- 11:00: Atualização para clientes enterprise (Acme, Beta, Gamma)
- 12:15: Email final (resolvido)
- Draft de email: wiki/negocios/processos/gerenciamento-crise.md#template-outage

**Próximos passos**:
1. Post-mortem completo (amanhã, 10h)
2. Comunicar com Acme Corp (SLA)
3. Atualizar wiki/negocios/projetos/monolith-to-microservices/riscos.md (cross-service deployment)
4. Atualizar wiki/negocios/processos/release.md (rollback testing)
5. Atualizar wiki/negocios/processos/monitoramento.md (cross-service alerting)

**Aprendizados**:
1. Cross-service deployment precisa de pipeline dedicado
2. Rollback scripts precisam ser testados para cross-service casos
3. Monitoramento precisa cobrir cross-service interações
4. Comunicação com clientes enterprise precisa ser mais rápida (10min vs 20min)
- Fonte: wiki/negocios/projetos/monolith-to-microservices/aprendizados.md (adicionar post-mortem)

**Contexto adicional**:
- Este risco foi previsto em wiki/negocios/projetos/monolith-to-microservices/riscos.md (#3)
- Risco foi discutido mas mitigação não foi priorizada (decisão de 2026-04-15)
- Fonte: raw/reunioes/mensais/2026-04-15.md (decisão migração)

Tempo para resposta completa: < 30 segundos (vs 2-3 horas tradicional)
```

### 4. Análise de Tendências

**Problema**: CEO quer saber tendências mês a mês, o que está funcionando, o que não está.

**Tradicional**:
- Procurar relatórios, emails, Slack
- Pedir a cada lead (interrupções)
- Risco de insights incompletos

**Com Wiki LLM**:

```
CEO: "Quais são as principais tendências de abril 2026? Compare com março 2026."

LLM responde:

**Tendências de abril 2026**:

1. **Investimento em tecnologia** (forte)
   - Decisão: Migração para microserviços ($100k investimento)
   - Decisão: Adoção de AI Copilot ($2.400/ano)
   - Motivo: Escalar para crescimento (+20% revenue planejado)
   - Fontes:
     - wiki/negocios/sintese/tendencia-mensal.md#abril-2026
     - raw/reunioes/mensais/2026-04-15.md

2. **Foco em receita enterprise** (forte)
   - Cliente: Acme Corp ($500k/ano, 3 anos)
   - Motivo: Revenue recorrente de alta qualidade
   - Trade-off: Customização para 1 cliente (+2 SREs necessários)
   - Fontes:
     - wiki/negocios/sintese/tendencia-mensal.md#abril-2026
     - wiki/negocios/entidades/clientes.md#acme-corp

3. **Complexidade operacional crescente** (moderado)
   - Microserviços → +complexidade monitoramento, tracing
   - AI Copilot → +dependência de ferramenta externa
   - Enterprise clientes → +customização, SLA estritos
   - Risco: Manutenção se torna gargalo
   - Fonte:
     - wiki/negocios/sintese/risco.md#complexidade-operacional

**Comparação com março 2026**:

| Aspecto | Março 2026 | Abril 2026 | Mudança |
|---------|------------|------------|---------|
| Decisões técnicas | 0 | 2 | ↑↑ |
| Decisões de produto | 2 | 0 | ↓↓ |
| Decisões de vendas | 1 | 1 | → |
| Complexidade operacional | Baixa | Moderada | ↑ |
| Revenue recorrente | $2.5M/ano | $3.0M/ano | ↑ 20% |
| Custos operacionais | $1.2M/ano | $1.4M/ano | ↑ 16.7% |
| Margem | 52% | 53% | ↑ 1pp |
| Cliente enterprise | 0 | 1 | ↑ |
| Riscos identificados | 3 | 5 | ↑ 67% |

**Análise**:
- **Positivo**: Revenue +20% com custo +16.7% → margem ↑ 1pp (bom)
- **Positivo**: Foco em clientes enterprise (receita de alta qualidade)
- **Preocupante**: Riscos ↑ 67% (complexidade operacional, dependências)
- **Preocupante**: Decisões de produto = 0 (estagnação de roadmap?)
- **Notável**: Decisões técnicas ↑ (foco em infraestrutura para escalar)

**Insights não óbvios**:
1. Decisões de produto = 0 em abril vs 2 em março: time de produto está muito ocupado com Acme Corp (customização)?
   - Fonte: raw/slack/canais/produto/2026-04-*.md (atividade baixa)
2. Riscos ↑ 67% mas margem ↑ 1pp: estratégia agressiva está funcionando, mas precisa mitigar riscos
3. Microserviços decisão (abril) + Copilot decisão (abril) = investimento coordenado em tecnologia
   - Ambas decisões conectadas a "escalar para crescimento" (raw/reunioes/mensais/2026-04-15.md)

**Recomendações**:
1. **Urgente**: Mitigar riscos de complexidade operacional
   - Contratar DevOps/Platform Engineer (já planejado para Q2)
   - Atualizar wiki/negocios/processos/monitoramento.md (cross-service alerting)
2. **Curto prazo**: Retomar roadmap de produto
   - Perguntar a Head of Product: "Por que 0 decisões de produto em abril?"
   - Revisar wiki/negocios/produtos/[produto]/roadmap.md (atualizar prioridades)
3. **Médio prazo**: Avaliar se complexidade operacional é sustentável
   - KPI: Tempo médio de deploy (atual: 2h monolito, 5-10min microserviço individual)
   - Meta: Manter < 1h para deployments completos (todos serviços)
4. **Longo prazo**: Considerar estratégia para customização de enterprise
   - Customização para 1 cliente (Acme) → pode ser ineficiente se muitos clientes enterprise
   - Considerar "plano enterprise" com features premium (em vez de customização única)
   - Fonte: wiki/negocios/produtos/[produto]/roadmap.md (adicionar "plano enterprise")

**Próximos passos**:
1. Reunião com Leads (amanhã, 14h): Discutir tendências, ajustes
2. Atualizar wiki/negocios/sintese/estado-da-empresa.md (com insights acima)
3. Criar action items em wiki/negocios/metricas/okrs.md (Q2 2026)
   - Mitigar riscos de complexidade operacional
   - Retomar roadmap de produto
   - Avaliar estratégia de customização

Tempo para análise completa: < 1 minuto (vs 4-8 horas tradicional)
```

## Benefícios

| Benefício | Tradicional | Com Wiki LLM |
|-----------|-------------|--------------|
| Onboarding | 2-3 semanas | 1-2 dias |
| Respostas a clientes | 2-4 horas | < 5 minutos |
| Gerenciamento de crise | 2-4 horas | < 1 minuto |
| Análise de tendências | 4-8 horas | < 1 minuto |
| Consistência de informação | Variável | Alta |
| Acesso a conhecimento | Limitado (quem perguntou) | Todos (wiki disponível) |
| Manutenção de documentação | Ninguém quer fazer | Automatizado pelo LLM |

## Configuração de Humans-in-the-Loop

O wiki LLM não substitui humanos, mas os capacita. Configure revisões:

### Revisão Obrigatória
```
LLM atualiza wiki →
Notifica equipe (Slack/email) →
Human revisa →
Aprova/rejeita →
Wiki atualizado (após aprovação)
```

**Quando usar**: Decisões importantes, comunicar com clientes, comunicar externamente

### Revisão Opcional
```
LLM atualiza wiki →
Wiki atualizado imediatamente →
Equipe pode revisar (assíncrono) →
Feedback para LLM (para aprender)
```

**Quando usar**: Atualizações de rotina, sínteses, análises internas

### Sem Revisão
```
LLM atualiza wiki →
Wiki atualizado imediatamente →
Equipe usa wiki como está
```

**Quando usar**: Index, log, sínteses de baixo risco

---

**Próximo**: Ferramentas: Obsidian