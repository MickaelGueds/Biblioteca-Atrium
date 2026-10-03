---
source: https://arxiv.org/abs/2607.17237
captured_at: 2026-10-01
tags: [pos-processamento, llm, transcricao, revisao]
type: study-note
---

# Pós-correção de transcrição com LLM: legível ≠ fiel

## TL;DR
Um LLM transforma transcrição crua em texto de estudo (pontuação, parágrafos, jargão), mas sem ouvir o áudio ele pode "embelezar" e mudar o sentido — precisa de chunking, glossário e checagem.

## Intuição (Feynman)
É um revisor de texto que nunca assistiu à aula. Ele arruma vírgula e corrige "rede neural convulsional" pra "convolucional" porque conhece o assunto — mas, se uma frase estiver ambígua, ele vai escolher a versão que soa melhor, não necessariamente a que o professor disse.

## Como funciona (técnico)

### O que corrigir
- Pontuação, maiúsculas, quebra em parágrafos/seções.
- Filler words e repetições ("né", "então, então").
- Jargão mal transcrito (via glossário da disciplina).
- **Não** reescrever conteúdo, **não** resumir na mesma passada.

### Padrão de pipeline
1. Chunk do texto por tempo ou por segmento (ex.: blocos de ~3 min), com sobreposição curta pra não cortar frase.
2. Prompt de revisor: "corrija apenas forma; preserve conteúdo; use o glossário; marque `[??]` onde não tiver certeza".
3. Manter `start/end` de cada bloco pra rastrear de volta ao vídeo.
4. Passadas separadas: (a) limpeza fiel → (b) versão "nota de estudo" opcional.

### Evidência (AI_LectureNote, 2026)
- Aulas de medicina coreano-inglês; post-processing subiu taxa de termos corretos em script latino de **0,39 → 0,71** (whisper-1) e **0,26 → 0,65** (gpt-4o-transcribe em chunks de 3 min).
- Porém: **renderizar o termo certo não implicou fidelidade semântica** — houve *semantic drift*. Lição: medir fidelidade, não só legibilidade.

### Limite estrutural
LLM sem acesso ao áudio não corrige nome próprio/jargão que o ASR errou de forma plausível. Mitigação: glossário também no `initial_prompt` do Whisper ([[whisper-audio-longo-e-alucinacao]]), e revisão humana dos trechos de baixa confiança ([[jev-modelo-de-decisao]]).

## Conceitos relacionados
- [[pipeline-transcricao-videoaula]] — estágio 5
- [[whisper-audio-longo-e-alucinacao]] — `initial_prompt` como glossário na origem
- [[jev-modelo-de-decisao]] — triagem do que vai pra revisão

## Quando aplicar
- Transcrição pra leitura/estudo → sim, com prompt "só forma".
- Legenda sincronizada → cuidado: reescrita desalinha timestamps.
- Conteúdo crítico (medicina, jurídico) → passada fiel + checagem humana amostral.

## Perguntas de revisão
1. Por que um texto mais legível pode ser menos fiel?
2. Por que separar "limpeza" de "resumo" em passadas diferentes?
3. Que erro do ASR o LLM nunca consegue corrigir sozinho?
4. Como medir se a pós-correção mudou o sentido?

## Fonte
- Lee et al., *AI_LectureNote* (2026) — https://arxiv.org/abs/2607.17237
- LectureScribe-AI — https://github.com/GraduationGroup101/LectureScribe-AI
- LM-Kit guide — https://docs.lm-kit.com/lm-kit-net/guides/how-to/transcribe-and-reformat-audio-with-llm.html
