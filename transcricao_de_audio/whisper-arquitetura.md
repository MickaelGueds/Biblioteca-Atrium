---
source: https://arxiv.org/pdf/2212.04356
captured_at: 2026-10-01
tags: [whisper, asr, transformer, openai]
type: study-note
---

# Whisper: encoder-decoder sobre janelas de 30 s, tarefas como tokens

## TL;DR
Whisper é um Transformer encoder-decoder comum; a força vem de 680 mil horas de áudio "sujo" da web e de controlar a tarefa (transcrever, traduzir, idioma, timestamp) por tokens especiais no decoder.

## Intuição (Feynman)
O encoder "escuta" 30 segundos e transforma em uma representação; o decoder é um mini-LLM que escreve o texto olhando pra essa representação. Em vez de um modelo por tarefa, você diz no começo da frase o que quer — "português, transcrever, com timestamps" — e ele segue.

## Como funciona (técnico)

### Entrada
- Áudio 16 kHz mono → janela fixa de **30 s** (preenche com silêncio se menor).
- Log-Mel spectrogram: janela 25 ms, hop 10 ms → **3000 frames**. 80 bins (até v2), **128 bins no large-v3**.

### Encoder
- 2 convoluções 1D (largura 3, a segunda com stride 2) + GELU → 1500 frames.
- Positional embedding senoidal → blocos Transformer.
- Roda **uma vez** por janela.

### Decoder
- Autoregressivo, cross-attention nos estados do encoder.
- Perda: `L(θ) = -Σ log p(y_t | y_<t, Mel(x))`.
- Sequência alvo mistura tokens de controle:
  `<|startoftranscript|> <|pt|> <|transcribe|> <|0.00|> texto... <|4.20|> ...`
- `<|nospeech|>` para janela sem fala; `<|notimestamps|>` desliga timestamps.
- Prompt de texto anterior (até ~224 tokens) pode condicionar a janela atual — é assim que funciona `initial_prompt` / `condition_on_previous_text`.

### Variantes relevantes (2024–2026)
| Modelo | Params | Nota |
|---|---|---|
| large-v3 | 1.55B | Referência de qualidade |
| large-v3-turbo | 809M | Decoder de 32 → **4 camadas**; 2–5× mais rápido; **não traduz** |
| distil-whisper | menor | Destilação; inspirou o turbo |
| faster-whisper | — | Não é modelo: reimplementação em CTranslate2 (INT8/FP16), até 4× mais rápido, menos memória |

Turbo = encoder pesado + decoder leve → ganha muito com GPU.

### Limites conhecidos
- Alucinação e loops em silêncio/ruído → [[whisper-audio-longo-e-alucinacao]].
- Sem diarização → [[diarizacao-e-timestamps-whisperx]].
- Language ID fraco (64,5% no FLEURS) — fixe o idioma (`language="pt"`).
- Timestamps por segmento, não por palavra confiável.

## Conceitos relacionados
- [[pipeline-transcricao-videoaula]] — onde o Whisper entra
- [[whisper-audio-longo-e-alucinacao]] — o que quebra em áudio longo
- [[rag-vs-wiki]] — mesma ideia de "tarefa como prompt", outro domínio

## Quando aplicar
- Transcrição offline multilíngue sem treino → Whisper direto.
- GPU disponível + volume alto → large-v3-turbo em faster-whisper.
- Precisa traduzir pra inglês na mesma passada → large-v3 (turbo não traduz).
- Vocabulário muito específico e muitas horas de dados → fine-tune ([guia HF](https://huggingface.co/blog/fine-tune-whisper)).

## Perguntas de revisão
1. Por que a janela fixa de 30 s simplifica o treino mas complica a inferência de áudio longo?
2. O que o turbo cortou e por que isso quase não piora o WER?
3. Como o mesmo modelo faz transcrição e tradução sem "cabeças" separadas?
4. Por que fixar `language` em vez de deixar o modelo detectar?

## Fonte
- Radford et al., *Robust Speech Recognition via Large-Scale Weak Supervision* (OpenAI, 2022) — https://arxiv.org/pdf/2212.04356
- Resumo: https://github.com/zhaoyang97/awesome-papers/blob/main/docs_en/era4_foundation_models/2022_whisper.md
- Turbo: https://huggingface.co/openai/whisper-large-v3-turbo
