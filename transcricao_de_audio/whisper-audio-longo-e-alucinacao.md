---
source: https://dev.to/nareshipme/whisper-hallucination-on-silence-why-your-transcript-loops-the-same-phrase-2pg4
captured_at: 2026-10-01
tags: [whisper, alucinacao, vad, audio-longo]
type: study-note
---

# Whisper em áudio longo: janelas costuradas, alucinação em silêncio e VAD

## TL;DR
Whisper alucina ("Obrigado por assistir!", frase repetida em loop) quando silêncio longo chega ao decoder; a correção padrão é VAD antes do modelo + desligar o condicionamento no texto anterior.

## Intuição (Feynman)
O decoder é um modelo de linguagem: se o ouvido não ouve nada, ele "completa" com o que é estatisticamente comum no fim de vídeos do YouTube. E como cada janela lê o texto da anterior, um erro vira eco que se repete. Cortar o silêncio antes tira a tentação; cortar o eco impede o loop.

## Como funciona (técnico)

### Decodificação longa (paper)
Áudio > 30 s é processado em janelas sequenciais, deslocadas pelo último timestamp previsto. Pilha de heurísticas — cada uma vale 1–2 pts de WER, mas sem qualquer uma aparecem loops:
| Heurística | Parâmetro (openai-whisper) | Default |
|---|---|---|
| Beam search | `beam_size` | 5 |
| Temperature fallback | `temperature` | (0.0, 0.2, …, 1.0) |
| Gate de log-prob | `logprob_threshold` | -1.0 |
| Teto de compressão (detecta repetição) | `compression_ratio_threshold` | 2.4 |
| Limiar de não-fala | `no_speech_threshold` | 0.6 |
| Prompt com texto anterior | `condition_on_previous_text` | True |

Fallback: se a saída falha no gate (log-prob baixa ou texto muito compressível = repetitivo), redecodifica com temperatura maior.

### Causas de alucinação
- Silêncio longo / ruído / música na janela.
- `condition_on_previous_text=True` propaga erro de uma janela pras próximas → loop.
- Fronteira de janela cortando palavra no meio.

### Correções (faster-whisper)
```python
segments, info = model.transcribe(
    "aula.wav",
    language="pt",
    vad_filter=True,                    # Silero VAD antes do Whisper
    vad_parameters={"min_silence_duration_ms": 500},
    condition_on_previous_text=False,   # quebra o eco entre janelas
    initial_prompt="Aula de <disciplina>. Termos: ...",  # glossário
)
```
- VAD: manter pausas curtas (< ~1,5 s) e encurtar pausas longas pra 0,3–0,5 s preserva ritmo sem dar espaço pra alucinar.
- Pós-filtro: descartar segmento com `no_speech_prob` alto ou texto da lista negra ("Thanks for watching", "Legendas pela comunidade…").
- Trade-off: `condition_on_previous_text=False` reduz loop mas perde coerência de termos entre janelas → compense com `initial_prompt`.

### Chunking alternativo
WhisperX/batched: corta por VAD em pedaços ≤ 30 s e processa **em paralelo** (rápido), ao custo de erros na fronteira e sem contexto entre pedaços. Ver [[diarizacao-e-timestamps-whisperx]].

## Conceitos relacionados
- [[whisper-arquitetura]] — por que existe a janela de 30 s
- [[pipeline-transcricao-videoaula]] — estágio 2 e 3
- [[diarizacao-e-timestamps-whisperx]] — chunking por VAD em lote

## Quando aplicar
- Aula com pausas longas (exercício, quadro, intervalo) → `vad_filter=True` sempre.
- Transcrição com frase repetida em sequência → olhar `compression_ratio` e desligar `condition_on_previous_text`.
- Termos técnicos sumindo após desligar contexto → `initial_prompt` com glossário.

## Perguntas de revisão
1. Por que um modelo de ASR "inventa" texto se só deveria transcrever?
2. O que `compression_ratio` alto indica sobre o texto gerado?
3. Qual o custo de desligar `condition_on_previous_text`, e como compensar?
4. Por que processar janelas em paralelo é mais rápido mas pior na fronteira?

## Fonte
- DEV — *Whisper Hallucination on Silence* — https://dev.to/nareshipme/whisper-hallucination-on-silence-why-your-transcript-loops-the-same-phrase-2pg4
- Paper Whisper, seção long-form — https://arxiv.org/pdf/2212.04356
- https://theneuralbase.com/whisper/learn/intermediate/reducing-hallucinations-with-vad/
