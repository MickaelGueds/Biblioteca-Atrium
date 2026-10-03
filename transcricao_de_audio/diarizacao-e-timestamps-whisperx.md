---
source: https://github.com/m-bain/whisperX
captured_at: 2026-10-01
tags: [whisperx, diarizacao, pyannote, alinhamento, timestamps]
type: study-note
---

# WhisperX: timestamp por palavra (alinhamento forçado) + quem falou (diarização)

## TL;DR
WhisperX envolve o Whisper com três peças: VAD pra cortar e paralelizar, wav2vec2 pra alinhar cada palavra no tempo, e pyannote pra rotular falantes.

## Intuição (Feynman)
Whisper sabe *o que* foi dito, mas só sabe "mais ou menos quando". Um segundo modelo, que é ótimo em ligar sons a letras, pega o texto pronto e acha o milissegundo de cada palavra. Um terceiro agrupa trechos de voz parecida e diz "isso é a pessoa A, isso é a B".

## Como funciona (técnico)

### Etapas
1. **VAD** (pyannote ou Silero) → corta áudio em pedaços ≤ 30 s nas pausas.
2. **ASR em lote** com faster-whisper → texto por pedaço (paralelo, rápido).
3. **Alinhamento forçado** com wav2vec2 (CTC, modelo por idioma) → `start`/`end` por palavra.
4. **Diarização** com pyannote → intervalos `SPEAKER_00`, `SPEAKER_01`…
5. **Atribuição**: cada palavra recebe o falante cujo intervalo mais se sobrepõe.

```bash
whisperx aula.wav --model large-v3 --language pt \
  --diarize --hf_token $HF_TOKEN --output_format all
```
pyannote exige token Hugging Face + aceitar termos do modelo.

### Limites
- Rótulo de falante pode vazar na fronteira de chunk (um rótulo cobre trecho com 2 vozes).
- **Speaker drift**: mesma pessoa vira `SPEAKER_00` e `SPEAKER_02` em partes diferentes de aula longa.
- Sem contexto entre chunks → pontuação/termos inconsistentes.
- Fala sobreposta (dois ao mesmo tempo) continua ruim.

### Para aula
- Professor dominante → diarização às vezes desnecessária; `--min_speakers/--max_speakers` ajudam quando há alunos.
- Timestamp por palavra é o que permite gerar legenda `.srt` bem sincronizada e "clicar na frase e pular pro vídeo".

## Conceitos relacionados
- [[pipeline-transcricao-videoaula]] — estágio 4
- [[whisper-audio-longo-e-alucinacao]] — VAD e chunking
- [[whisper-arquitetura]] — por que Whisper sozinho não dá timestamp por palavra

## Quando aplicar
- Precisa de legenda sincronizada → alinhamento forçado.
- Aula com perguntas/debate → diarização.
- Só texto corrido de 1 professor → pule diarização, mantenha VAD.

## Perguntas de revisão
1. Por que usar um segundo modelo (wav2vec2) pra timestamps em vez de confiar no Whisper?
2. O que é speaker drift e por que piora em áudio longo?
3. Como a atribuição palavra→falante pode errar na fronteira de chunk?

## Fonte
- WhisperX — https://github.com/m-bain/whisperX
- Forasoft deep-dive — https://www.forasoft.com/learn/ai-for-video-engineering/articles-ai/whisperx-diarization-word-level-timestamps
- WhisperAlign (paper) — https://arxiv.org/html/2603.04809v1
- *From Lectures to a Book* (Medium) — https://medium.com/@Lakshay-13/from-lectures-to-a-book-building-a-reliable-diarized-transcription-system-782e3a1a0604
