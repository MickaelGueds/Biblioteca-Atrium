---
source: https://flaviocopes.com/jev/
captured_at: 2026-10-01
tags: [jev, typesafe, classificador, system-one, roteamento]
type: study-note
---

# Jev (TypeSafe): modelo que escolhe entre opções tipadas, não gera texto

## TL;DR
Jev recebe um estado (texto/registro) + perguntas tipadas e devolve escolha, probabilidade e confiança em ~100 ms, por fração do custo de um LLM; serve pra decidir, não pra escrever.

## Intuição (Feynman)
LLM é o funcionário que redige; Jev é o porteiro que, num relance, diz "isso vai pro financeiro, com 92% de certeza". Como ele só aponta pra uma das portas que você desenhou, não tem como inventar uma porta nova — e o "quão certo" vem calibrado, não escrito no chute.

## Como funciona (técnico)

### Tipos de pergunta
| Tipo | Pergunta | Retorno |
|---|---|---|
| **Noul** (`boolean` no AI SDK) | É verdade? | probabilidade 0–1 |
| **Choice** | Qual opção? | `choice`, `probabilities`, `confidence` |
| **Score** | Onde na escala? | `score`, `legend`, `probabilities`, `confidence` |

- Cada pergunta: ID (só pro seu código — não vai ao modelo), `type`, `instructions` (pergunta completa), `criteria` (opções).
- Várias perguntas no mesmo request (fan-out).

```bash
curl -s https://api.typesafe.ai/v1/systemone \
  -H "Authorization: Bearer $TYPESAFE_API_KEY" -H "Content-Type: application/json" \
  -d '{"model":"jev-latest","state":{"texto":"..."},
       "questions":{"precisa_revisao":{"type":"noul",
         "instructions":"`texto` contém termo técnico possivelmente mal transcrito?"}}}'
```

### Números (out/2026)
- US$ 0,042 / 1M tokens de entrada, saída grátis.
- 70–500 ms (maioria ~100 ms), medido da costa oeste dos EUA.
- Limites: 250k tokens/s, 1.200 req/min (early access).
- Lançado 15/09/2026; OpenAI respondeu com Decision API (DevDay, 29/09/2026).

### Confidence-gated routing
- Alta → age automático. Média → pede confirmação/revisão. Baixa → humano ou modelo mais lento.
- Exemplos da doc: 0,5 piso de revisão, 0,9 antes de ação destrutiva (exemplos, não defaults).

### Diferença pra alternativas
- Regra/regex: rápido, frágil com significado.
- Classificador treinado: rápido, mas precisa de dados rotulados + 1 modelo por tarefa.
- LLM com JSON: flexível, mas gera token a token, pode falhar o schema, probabilidade "escrita" não é calibrada.
- Jev: perguntas definidas em runtime (como LLM) + distribuição de probabilidade restrita (como classificador).

### Jev + Whisper (o que existe)
- **jev-voice**: `mic → VAD → whisper.cpp (~100 ms) → Jev (~250 ms) → ação macOS`. Código gera candidatos, Jev seleciona.
- **jev-on-air**: YouTube → faster-whisper → Jev.
- Nenhuma fonte usa Jev pra melhorar a transcrição em si — ele atua **depois** do texto pronto.

### Encaixes possíveis no [[pipeline-transcricao-videoaula]] (hipóteses, sem fonte)
- Noul por segmento: "precisa revisão humana?" → manda só os duvidosos pro LLM/pessoa.
- Choice por bloco: tópico da aula (pra gerar sumário/capítulos).
- Noul: "segmento é alucinação típica (agradecimento, legenda)?" → filtro pós-ASR.

## Conceitos relacionados
- [[pos-correcao-de-transcricao-com-llm]] — Jev decide *o que* vai pra correção
- [[whisper-audio-longo-e-alucinacao]] — filtro de alucinação como pergunta Noul
- [[pipeline-transcricao-videoaula]] — onde encaixa

## Quando aplicar
- Decisão repetida em volume alto sobre texto (rotear, filtrar, rotular) → Jev.
- Precisa gerar/reescrever texto → LLM, não Jev.
- Opções não enumeráveis de antemão → LLM.

## Perguntas de revisão
1. Por que a "confiança" do Jev é mais útil que um LLM respondendo "tenho 90% de certeza"?
2. No jev-voice, por que o código gera candidatos e o Jev só escolhe?
3. Em qual estágio do pipeline de aula o Jev **não** ajuda, e por quê?
4. Como você escolheria os limiares de confiança pra mandar trecho pra revisão?

## Fonte
- Flavio Copes, *A deep dive into Jev* — https://flaviocopes.com/jev/
- jev-voice — https://github.com/kevinbadi/jev-voice
- Sebastian Raschka, *From Bag-of-Words to Jev* — https://magazine.sebastianraschka.com/p/classifier-history-and-jev
