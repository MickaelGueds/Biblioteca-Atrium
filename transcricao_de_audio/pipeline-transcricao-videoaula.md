---
source: "múltiplas — ver [[fontes-transcricao]]"
captured_at: 2026-10-01
tags: [transcricao, asr, whisper, pipeline, videoaula]
type: study-note
---

# Pipeline de transcrição de videoaula: áudio → Whisper → texto revisado

## TL;DR
Transcrever aula longa não é "rodar o Whisper": é um pipeline de 5 estágios (extrair áudio → VAD → ASR em janelas → alinhamento/falantes → pós-correção), e cada estágio existe pra tapar um buraco do anterior.

## Intuição (Feynman)
Pensa numa linha de montagem de estenógrafo: alguém corta a gravação só nos trechos com fala, o estenógrafo escreve trecho por trecho, um assistente marca quem falou e em que segundo, e um revisor arruma pontuação e termos técnicos. O Whisper é só o estenógrafo — muito bom, mas que inventa frase quando ouve silêncio e não sabe quem está falando.

## Como funciona (técnico)

### Estágios
| # | Estágio | Ferramenta típica | Resolve |
|---|---|---|---|
| 1 | Extração de áudio | `ffmpeg -i aula.mp4 -ac 1 -ar 16000 aula.wav` | Whisper espera 16 kHz mono |
| 2 | VAD (detecção de voz) | Silero VAD, pyannote VAD | Silêncio → alucinação; também acelera |
| 3 | ASR | Whisper (large-v3 / turbo) via faster-whisper | Áudio → texto + timestamps de segmento |
| 4 | Alinhamento + diarização | WhisperX (wav2vec2 + pyannote) | Timestamp por palavra, "quem falou" |
| 5 | Pós-correção | LLM com glossário da disciplina | Pontuação, parágrafos, jargão, filler words |

Opcional entre 4 e 5: classificador ([[jev-modelo-de-decisao]]) marcando trechos que precisam de revisão.

### Restrições que moldam o design
- Whisper só enxerga **30 s por vez** → áudio de 1 h vira ~120 janelas costuradas. Ver [[whisper-arquitetura]].
- Costura de janelas gera **alucinação, loops e perda de contexto** na fronteira. Ver [[whisper-audio-longo-e-alucinacao]].
- Whisper não faz diarização nem timestamp confiável por palavra. Ver [[diarizacao-e-timestamps-whisperx]].
- Saída crua não é "texto de estudo": sem parágrafo, com "né", "então", repetição. Ver [[pos-correcao-de-transcricao-com-llm]].

### Formatos de saída úteis
- `.srt` / `.vtt` — legenda (precisa timestamps).
- `.json` com segmentos `{start, end, speaker, text}` — fonte da verdade, gera o resto.
- `.md` revisado — material de estudo.

## Conceitos relacionados
- [[whisper-arquitetura]] — o motor do estágio 3
- [[whisper-audio-longo-e-alucinacao]] — por que estágio 2 é obrigatório
- [[diarizacao-e-timestamps-whisperx]] — estágio 4
- [[pos-correcao-de-transcricao-com-llm]] — estágio 5
- [[jev-modelo-de-decisao]] — triagem de trechos por confiança
- [[fontes-transcricao]] — lista completa de leitura

## Quando aplicar
- Aula gravada (offline, batch) → pipeline completo, prioriza qualidade sobre latência.
- Aula com 1 professor só → diarização pode ser pulada.
- Aula com perguntas de alunos → diarização vale a pena.
- Disciplina com muito jargão → glossário no estágio 5 (e `initial_prompt` no estágio 3).

## Perguntas de revisão
1. Por que rodar VAD **antes** do Whisper e não depois?
2. Se a aula tem só o professor falando, quais estágios dá pra cortar e qual o risco?
3. Por que guardar o `.json` de segmentos em vez de só o texto final?
4. Em que estágio entra o glossário de termos técnicos, e por que em dois lugares?

## Fonte
Síntese das fontes em [[fontes-transcricao]].
