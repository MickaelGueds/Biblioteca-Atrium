# Casos de Uso Pessoais

## Visão Geral

O wiki LLM pode ser usado para construir conhecimento pessoal sobre si mesmo, seus objetivos, saúde e desenvolvimento.

## Caso 1: Autodesenvolvimento

### Objetivo

Acompanhar progresso pessoal, identificar padrões, e construir um sistema de autoconhecimento estruturado.

### Fontes de Dados

```
raw/pessoal/
├── diario/
│   ├── 2026-04-01.md
│   ├── 2026-04-02.md
│   └── ...
├── anotacoes-podcasts/
│   ├── mindfulness-podcast.md
│   ├── habit-forming.md
│   └── ...
├── artigos-saude/
│   ├── sono-otimizacao.md
│   ├── meditacao-beneficios.md
│   └── ...
├── metas-okrs/
│   ├── 2026-q1.md
│   ├── 2026-q2.md
│   └── ...
└── reflexoes/
    ├── semanais/
    ├── mensais/
    └── trimestrais/
```

### Estrutura do Wiki

```
wiki/pessoal/
├── entidades/
│   ├── habitos.md (hábitos atuais e passados)
│   ├── objetivos.md (metas por período)
│   ├── projetos.md (projetos pessoais)
│   └── relacionamentos.md (pessoas-chave)
├── conceitos/
│   ├── mindfulness.md (prática e benefícios)
│   ├── habit-forming.md (teoria e técnicas)
│   ├── productividade.md (estratégias)
│   └── autoconhecimento.md (práticas)
├── padroes/
│   ├── padroes-comportamentais.md (padrões identificados)
│   ├── triggers-emocionais.md (gatilhos e reações)
│   └── ciclos-de-energia.md (ritmos diários/semanais)
└── sintese/
    ├── evolucao-pessoal.md (linha do tempo)
    ├── aprendizados-chave.md (lições principais)
    └── areas-para-melhoria.md (lacunas identificadas)
```

### Exemplo de Uso

```
Você: "Quais hábitos eu tentei formar e quais funcionaram?"

LLM processa:
1. Busca "hábitos" em index.md
2. Lê wiki/pessoal/entidades/habitos.md
3. Filtra por "funcionou: true"
4. Sintetiza resposta

Resposta:
Hábitos que funcionaram para você:

1. **Meditação matinal** (funcionou)
   - Iniciado: 2025-11-15
   - Duração: 10 minutos
   - Frequência: Todos os dias
   - Benefícios observados:
     - Menos ansiedade
     - Maior foco ao longo do dia
     - Melhor qualidade de sono
   - Fontes:
     - diario/2025-11-20.md (notou primeira melhoria)
     - diario/2025-12-15.md (consequência de 30 dias)
     - reflexoes/mensais/2025-12.md (síntese)

2. **Leitura diária** (funcionou)
   - Iniciado: 2025-09-01
   - Duração: 30 minutos
   - Frequência: 6x/semana
   - Benefícios observados:
     - Maior vocabulário
     - Mais ideias para projetos
     - Melhor capacidade de escrita
   - Fontes:
     - diario/2025-09-15.md (notou mudança)
     - reflexoes/mensais/2025-10.md (resumo)

3. **Exercício físico** (parcialmente funcionou)
   - Iniciado: 2025-10-01
   - Duração: 45 minutos
   - Frequência: 4x/semana (meta: 5x/semana)
   - Benefícios observados:
     - Mais energia
     - Melhor sono
     - Melhor humor
   - Desafios:
     - Difícil manter frequência consistente
     - Falta de motivação em dias frios
   - Fontes:
     - diario/2025-10-20.md (desafios)
     - diario/2025-12-01.md (ajustes)

Hábitos que não funcionaram:
1. **Acordar às 5h** (tentou 3x, desistiu)
   - Problema: não era um night owl
   - wiki/pessoal/padroes/ciclos-de-energia.md revela que seu pico de energia é às 10h
2. **Diário alimentar** (tentou 2x, desistiu)
   - Problema: muito burocrático
   - Solução alternativa: fotos de refeições (menos trabalho)

Padrões identificados:
- Você é mais consistente com hábitos curtos (10-30 min)
- Hábitos pela manhã funcionam melhor (energia alta)
- Tracking detalhado desmotiva (prefere tracking simples)

Recomendações:
- Para exercício: tente 20 min vs 45 min (consistência > intensidade)
- Para acordar cedo: tente 6h30 vs 5h (mais realista)
- Para tracking: use sistema simples vs detalhado
```

### Consultas Poderosas

```
"Quais padrões de energia eu tenho?"
→ wiki/pessoal/padroes/ciclos-de-energia.md

"Como meu humor mudou ao longo dos últimos 6 meses?"
→ wiki/pessoal/sintese/evolucao-pessoal.md (com dados de diario/)

"Quais técnicas de mindfulness funcionaram melhor para mim?"
→ wiki/pessoal/conceitos/mindfulness.md (com evidências de diario/)

"Quais gatilhos causam procrastinação?"
→ wiki/pessoal/padroes/triggers-emocionais.md

"Como meu sono afeta minha produtividade?"
→ wiki/pessoal/sintese/sono-efetividade.md (correlação de diario/)
```

## Caso 2: Gestão de Saúde

### Objetivo

Acompanhar saúde, identificar correlações, e tomar decisões informadas baseadas em dados.

### Fontes de Dados

```
raw/saude/
├── diario-sintomas/
│   ├── 2026-04-01.md (dores, energia, humor, sono)
│   └── ...
├── exames-medicos/
│   ├── hemograma-2026-01-15.md
│   ├── colesterol-2026-03-20.md
│   └── ...
├── prescricoes/
│   ├── vitamina-d.md
│   └── ...
└── dieta/
    ├── diario-alimentar.md
    └── receitas-testadas.md
```

### Estrutura do Wiki

```
wiki/saude/
├── condicoes/
│   ├── insomnio.md (sintomas, tratamentos, eficácia)
│   ├── fadiga-cronica.md (diagnóstico, progresso)
│   └── alergias.md (gatilhos, sintomas, tratamentos)
├── tratamentos/
│   ├── suplementos.md (o que funciona, o que não funciona)
│   ├── terapias.md (fisioterapia, psicologia)
│   └── mudancas-estilo-vida.md (dieta, exercício, sono)
├── metricas/
│   ├── sono.md (qualidade, duração, padrões)
│   ├── energia.md (níveis ao longo do dia)
│   └── humor.md (variações e correlações)
└── sintese/
    ├── correlacoes.md (sono ↔ humor ↔ energia ↔ dieta)
    ├── progresso-tratamentos.md (o que está funcionando)
    └── areas-para-investigacao.md (sintomas inexplicados)
```

### Exemplo de Uso

```
Você: "O que afeta minha qualidade de sono?"

LLM processa:
1. Busca "sono" em index.md
2. Lê wiki/saude/metricas/sono.md
3. Lê wiki/saude/sintese/correlacoes.md
4. Lê dados brutos de raw/saude/diario-sintomas/
5. Sintetiza resposta

Resposta:
Identifiquei 5 fatores que afetam sua qualidade de sono (baseado em 180 dias de dados):

1. **Cafeína após 14h** (correlação forte: 0.82)
   - Consumo de cafeína após 14h → qualidade do sono cai de 7.2/10 para 5.8/10
   - Padrão consistente: 23 de 26 dias com cafeína tarde → sono ruim
   - Recomendação: limite cafeína até 14h
   - Fontes:
     - diario-sintomas/2026-01-15.md (primeira observação)
     - diario-sintomas/2026-02-28.md (padrão confirmado)
     - wiki/saude/sintese/correlacoes.md (análise)

2. **Exercício após 19h** (correlação moderada: 0.65)
   - Exercício vigoroso após 19h → demora mais para dormir (+45min)
   - Exercício leve (caminhada) após 19h → sem impacto
   - Recomendação: exercício vigoroso até 18h, leve OK após 19h
   - Fontes:
     - diario-sintomas/2026-02-10.md (primeira observação)
     - wiki/saude/tratamentos/exercicio.md (guidelines)

3. **Telas antes de dormir** (correlação forte: 0.78)
   - Uso de telas até 30min antes de dormir → sono mais leve
   - Uso de telas até 1h antes de dormir → sonhos mais vívidos, acordar cansado
   - Recomendação: sem telas 1h antes de dormir
   - Fontes:
     - diario-sintomas/2026-03-05.md (padrão observado)
     - wiki/saude/condicoes/insomnio.md (trigger)

4. **Suplemento de Magnésio** (correlação positiva: 0.71)
   - 400mg magnésio antes de dormir → qualidade do sono melhora de 6.5/10 para 7.8/10
   - Padrão: 31 de 35 dias com magnésio → sono bom
   - Recomendação: continue tomando magnésio antes de dormir
   - Fontes:
     - diario-sintomas/2026-01-20.md (primeiro teste)
     - prescricoes/magnesio.md (dosagem e timing)
     - exames-medicos/2026-03-20.md (níveis de magnésio confirmaram deficiência)

5. **Alimentação pesada à noite** (correlação moderada: 0.58)
   - Refeição pesada (carne vermelha, carboidratos) → sono agitado
   - Refeição leve (sopa, salada) → sono tranquilo
   - Recomendação: jantar leve, finalizar 3h antes de dormir
   - Fontes:
     - diario-sintomas/2026-02-22.md (padrão observado)
     - dieta/diario-alimentar.md (análise de refeições)

Fatores que NÃO afetam seu sono:
- Temperatura do quarto (testou: 18°C, 20°C, 22°C → sem diferença)
- Ruído branco (testou: com/sem → sem diferença)
- Horário de dormir (testou: 22h, 23h, 00h → mesma qualidade, apenas horário de acordar muda)

Correlações interessantes (wiki/saude/sintese/correlacoes.md):
- Sono ruim → humor ruim no dia seguinte (correlação: 0.85)
- Sono ruim → menos energia (correlação: 0.79)
- Sono bom → mais foco (correlação: 0.73)

Recomendações consolidadas:
1. **Rotina ideal**:
   - Café da manhã: 8h
   - Última cafeína: 14h
   - Jantar leve: 18h
   - Exercício vigoroso: 17h-18h
   - Caminhada leve: 19h-19h30
   - Última tela: 21h
   - Magnésio: 21h30 (400mg)
   - Dormir: 22h-22h30

2. **Testes futuros**:
   - Melatonina (0.5mg ou 1mg)
   - Temperatura do quarto mais baixa (16°C)
   - Aromaterapia (lavanda)

3. **Áreas para investigação**:
   - Por que você acordou cansado em 2026-03-15 (não há correlação óbvia)
   - O que causou o "sono incrível" de 2026-02-28 (fatores não documentados)

Respostas para essas perguntas podem requerer mais dados ou investigação adicional.
```

## Caso 3: Aprendizado e Hobbies

### Objetivo

Acompanhar progresso em áreas de interesse, conectar conceitos, e construir conhecimento profundo.

### Fontes de Dados

```
raw/aprendizado/
├── programacao/
│   ├── python-basico.md
│   ├── python-avancado.md
│   └── projetos/
├── guitarra/
│   ├── aulas/
│   ├── pratica-diaria.md
│   └── musicas-aprendidas.md
├── fotografia/
│   ├── tutoriais/
│   ├── galeria-testes.md
│   └── feedback.md
└── outros-hobbies/
    ├── cozinhar.md
    └── jardinagem.md
```

### Estrutura do Wiki

```
wiki/aprendizado/
├── programacao/
│   ├── conceitos/
│   │   ├── orientacao-objetos.md
│   │   ├── funcional.md
│   │   └── sistemas-distribuidos.md
│   ├── sintaxe/
│   │   ├── python.md
│   │   ├── javascript.md
│   │   └── rust.md
│   ├── padroes/
│   │   ├── design-patterns.md
│   │   └── arquitetura.md
│   └── progresso/
│       ├── python.md (nível atual, objetivos, roadmap)
│       ├── guitarra.md (técnicas dominadas, músicas aprendidas)
│       └── fotografia.md (técnicas, composições, equipamento)
├── guitarra/
│   ├── teoria/
│   │   ├── escalas.md
│   │   ├── acordes.md
│   │   └── harmonia.md
│   ├── tecnica/
│   │   ├── digitacao.md
│   │   ├── palheta.md
│   │   └── ritmo.md
│   └── musicas/
│       ├── classificadas-por-dificuldade.md
│       └── aprendidas-recentemente.md
└── fotografia/
    ├── tecnica/
    │   ├── composicao.md
    │   ├── exposicao.md
    │   └── edicao.md
    ├── equipamento/
    │   ├── camera.md
    │   ├── lentes.md
    │   └── acessorios.md
    └── galeria/
        ├── por-tema.md
        └── por-tecnica.md
```

### Exemplo de Uso

```
Você: "Quais progressos fiz em guitarra nos últimos 3 meses?"

LLM processa:
1. Busca "guitarra" em index.md
2. Lê wiki/aprendizado/progresso/guitarra.md
3. Lê dados brutos de raw/aprendizado/guitarra/pratica-diaria.md
4. Lê wiki/aprendizado/guitarra/musicas/aprendidas-recentemente.md
5. Sintetiza resposta

Resposta:
Progresso em guitarra nos últimos 3 meses (2026-01-21 a 2026-04-21):

## Técnicas Dominadas

✅ **Acordes básicos** (dominado)
- A, Am, C, D, Dm, E, Em, G (7 acordes)
- Transições fluidas entre todos os acordes
- Tempo médio de transição: 0.5s (meta: < 1s)
- Fontes:
  - pratica-diaria/2026-02-15.md (primeiro dia sem erros)
  - wiki/aprendizado/guitarra/tecnica/acordes.md

✅ **Ritmo básico** (dominado)
- Downstroke em 4/4
- Upstroke em 4/4
- Downstroke em 3/4
- Praticou 45 dias consecutivos (2026-01-21 a 2026-03-07)
- Fontes:
  - pratica-diaria/2026-03-07.md (meta alcançada)
  - wiki/aprendizado/guitarra/tecnica/ritmo.md

🔄 **Palheta alternada** (em progresso)
- Começou: 2026-02-20
- Nível atual: moderado
- Meta: dominado até 2026-05-21
- Desafios:
  - Ainda confunde upstroke vs downstroke em tempos rápidos
  - Perde ritmo em acordes mais difíceis (F, Bm)
- Progresso:
  - Dia 1 (2026-02-20): 5 acordes/minuto, muitos erros
  - Dia 30 (2026-03-21): 15 acordes/minuto, poucos erros
  - Dia 60 (hoje): 25 acordes/minuto, erros ocasionais
- Fontes:
  - pratica-diaria/2026-02-20.md (início)
  - pratica-diaria/2026-03-21.md (progresso)
  - pratica-diaria/2026-04-20.md (hoje)
  - wiki/aprendizado/guitarra/tecnica/palheta.md

❌ **Fingerstyle** (ainda não começou)
- Programado para começar após dominar palheta alternada
- Estimativa de início: 2026-06-01

## Músicas Aprendidas

✅ **Wonderwall** (dominado)
- Dificuldade: Fácil
- Data que dominou: 2026-02-10
- Tempo para dominar: 21 dias
- Técnicas usadas: Acordes básicos, ritmo básico
- Fontes:
  - musicas-aprendidas.md (2026-02-10)

✅ **Hotel California** (dominado)
- Dificuldade: Intermediária
- Data que dominou: 2026-03-28
- Tempo para dominar: 47 dias
- Técnicas usadas: Acordes básicos, palheta alternada, ritmo intermediário
- Fontes:
  - musicas-aprendidas.md (2026-03-28)

🔄 **Stairway to Heaven** (em progresso)
- Dificuldade: Difícil
- Começou: 2026-03-15
- Progresso atual: 45%
- Seções dominadas:
  - Intro (100%)
  - Verso 1 (100%)
  - Refrão (100%)
- Seções em progresso:
  - Verso 2 (70%)
  - Solo (30%)
- Seções não começadas:
  - Ponte
  - Refrão final
- Desafios:
  - Solo muito rápido (não consegue manter ritmo)
  - Muda muito de dedilhado
- Estimativa de conclusão: 2026-06-15 (mais 2 meses)
- Fontes:
  - musicas-aprendidas.md (2026-03-15)
  - pratica-diaria/2026-04-20.md (progresso atual)

## Teoria Musical Aprendida

✅ **Escala maior** (entendida)
- Pode construir escala maior em qualquer tonalidade
- Pode identificar notas da escala de ouvido (50% de acerto)
- Fontes:
  - wiki/aprendizado/guitarra/teoria/escalas.md
  - aulas/escala-maior.md

✅ **Acordes básicos** (entendidos)
- Entende como acordes são construídos (terça, quinta)
- Pode derivar acordes desconhecidos a partir da escala
- Fontes:
  - wiki/aprendizado/guitarra/teoria/acordes.md

🔄 **Harmonia básica** (em progresso)
- Entende o conceito de I-IV-V
- Pode identificar progressões simples em músicas
- Próximo passo: progressões mais complexas (ii-V-I, vi-IV-I-V)
- Fontes:
  - wiki/aprendizado/guitarra/teoria/harmonia.md
  - aulas/harmonia-basica.md

## Estatísticas de Prática

- Total de dias de prática: 90 dias consecutivos (2026-01-21 a 2026-04-21)
- Tempo total de prática: ~45 horas (30 minutos/dia)
- Consistência: 100% (todos os dias sem falta)
- Dias mais longos: 60 minutos (sábados)
- Dias mais curtos: 15 minutos (dias de trabalho pesado)

## Padrões Identificados

- **Melhor horário para praticar**: 20h-21h (após jantar, antes de relaxar)
  - Fonte: pratica-diaria/ (análise de foco vs horário)
- **Consistência > intensidade**: Praticar todos os dias 30min é melhor que 3x/semana 90min
  - Fonte: pratica-diaria/ (comparação de fevereiro vs janeiro)
- **Repetição vs variação**: Praticar a mesma música é mais eficiente que variar muito
  - Fonte: pratica-diaria/2026-02-20.md vs 2026-03-10.md

## Objetivos Futuros

Curto prazo (próximos 3 meses):
- [ ] Dominar palheta alternada até 2026-05-21
- [ ] Completar Stairway to Heaven até 2026-06-15
- [ ] Aprender fingerstyle até 2026-07-15

Médio prazo (próximos 6 meses):
- [ ] Aprender 10 músicas de nível intermediário
- [ ] Entender harmonia avançada
- [ ] Começar improviso básico

Longo prazo (próximo ano):
- [ ] Ser capaz de improvisar sobre qualquer escala
- [ ] Aprender a tocar música por ouvido
- [ ] Compor uma música própria

## Áreas para Melhoria

1. **Teoria**: Precisa estudar mais sobre improvisação
   - Recomendação: aulas/improvisacao-basica.md
2. **Técnica**: Palheta alternada precisa de mais prática
   - Recomendação: continuar praticando 15min/dia apenas com palheta
3. **Leitura**: Não consegue ler tablatura bem
   - Recomendação: praticar leitura de tablatura 10min/dia

Fonte consolidada:
- wiki/aprendizado/progresso/guitarra.md (síntese completa)
```

## Padrões Comuns em Casos Pessoais

### 1. Consistência é mais importante que intensidade
- 30 minutos todos os dias > 3 horas 1x por semana
- Padrão observado em: hábitos, saúde, guitarra, programação

### 2. Feedback loops são essenciais
- Medir → analisar → ajustar → repetir
- Exemplo: sono → correlações → ajustes → verificar

### 3. Conexões não óbvias aparecem
- Sono ↔ humor ↔ produtividade (saúde)
- Hábitos ↔ energia ↔ foco (autodesenvolvimento)
- Técnica ↔ teoria ↔ progresso (aprendizado)

### 4. O valor aumenta com o tempo
- Primeiro mês: poucas conexões
- Sexto mês: muitas conexões não óbvias
- Ano: sistema de conhecimento profundo

---

**Próximo**: Casos de Uso: Pesquisa Acadêmica