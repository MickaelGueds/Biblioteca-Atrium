# Fontes — Transcrição de videoaula com Whisper (+ Jev)

Levantamento feito em 2026-10-01. Objetivo: transcrever uma aula inteira (vídeo longo) e ajustar o texto.
Ordem sugerida de leitura: trilha 1 → 2 → 3 → 4, e Jev (5–6) em paralelo como curiosidade.

---

## 1. Whisper — fundamentos (como funciona por dentro)

- [Robust Speech Recognition via Large-Scale Weak Supervision (paper original)](https://arxiv.org/pdf/2212.04356) — a fonte primária.
- [Whisper explicado — Turing Post (2026)](https://www.turingpost.com/p/topic-15-inside-whisper-an-open-source-audio-model) — visão geral acessível.
- [Resumo comentado do paper (awesome-papers)](https://github.com/zhaoyang97/awesome-papers/blob/main/docs_en/era4_foundation_models/2022_whisper.md) — log-mel, janela de 30 s, tokens de controle.
- [Whisper: Speech Recognition Model Capable of Recognizing 99 Languages — Medium/axinc-ai](https://medium.com/axinc-ai/whisper-speech-recognition-model-capable-of-recognizing-99-languages-5b5cf0197c16)
- [Whisper Large-v3 Explained: Architecture, WER, and Limits (2026)](https://convertaudiototext.com/blog/whisper-large-v3-explained)
- [Wikipedia — Whisper](https://en.wikipedia.org/wiki/Whisper_(speech_recognition_system))

## 2. Whisper em produção — velocidade, variantes, alucinação

**Variantes / performance**
- [Whisper Large V3 Turbo — Medium/axinc-ai](https://medium.com/axinc-ai/whisper-large-v3-turbo-high-accuracy-and-fast-speech-recognition-model-be2f6af77bdc)
- [Discussão oficial do release turbo (GitHub openai/whisper)](https://github.com/openai/whisper/discussions/2363)
- [Model card whisper-large-v3-turbo (Hugging Face)](https://huggingface.co/openai/whisper-large-v3-turbo)
- [Distil-Whisper (paper)](https://arxiv.org/pdf/2311.00430)
- [faster-whisper: large-v3-turbo](https://theneuralbase.com/faster-whisper/learn/beginner/large-v3-turbo-fastest-high-quality/)
- [Deploy Whisper v3 Turbo em produção — Simplismart](https://www.simplismart.ai/blog/deploy-whisper-v3-turbo-using-vox-box)
- [Self-host de ASR em GPU (guia 2026) — Spheron](https://www.spheron.network/blog/whisper-v4-asr-gpu-cloud-production-guide/)

**Alucinação, silêncio e VAD (crítico pra aula longa)**
- [Whisper Hallucination on Silence — DEV](https://dev.to/nareshipme/whisper-hallucination-on-silence-why-your-transcript-loops-the-same-phrase-2pg4)
- [Whisper Keeps Repeating Itself — LocalAIMaster](https://localaimaster.com/blog/whisper-hallucination-fix)
- [Reducing hallucinations with VAD](https://theneuralbase.com/whisper/learn/intermediate/reducing-hallucinations-with-vad/)
- [Audio Pre-Processings For Better Results in the Transcription Pipeline — Medium](https://medium.com/@developerjo0517/audio-pre-processings-for-better-results-in-the-transcription-pipeline-bab1e8f63334)
- [Pré-processamento contra alucinação (GitHub discussion)](https://github.com/openai/whisper/discussions/2378)
- [Hallucination on audio with no speech (GitHub discussion)](https://github.com/openai/whisper/discussions/1606)
- [Reducing Hallucinated Transcripts in Whisper via Hallucination Space Projection (paper 2026)](https://arxiv.org/pdf/2609.04561)

## 3. Arquitetura pra áudio longo (aula inteira): chunking, timestamps, diarização

- ⭐ [From Lectures to a Book: Building a Reliable Diarized Transcription System — Medium](https://medium.com/@Lakshay-13/from-lectures-to-a-book-building-a-reliable-diarized-transcription-system-782e3a1a0604) — **mais próximo da sua task**.
- [WhisperX Deep-Dive — Diarização e timestamps por palavra (Forasoft)](https://www.forasoft.com/learn/ai-for-video-engineering/articles-ai/whisperx-diarization-word-level-timestamps)
- [Local Audio Transcription with Speaker Diarization — steeman.be](https://www.steeman.be/posts/local-whisper-transcription-with-speaker-diarization/)
- [MURMUR: Efficient Inference System for Long-Form ASR (paper 2026)](https://arxiv.org/pdf/2606.01483) — limites do chunking estilo WhisperX.
- [WhisperAlign: chunking respeitando fronteira de palavra + pyannote (paper)](https://arxiv.org/html/2603.04809v1)
- [WhisperX com Silero VAD (repo)](https://github.com/cnbeining/whisperX-silero)

**System design genérico de STT** (não achei post específico do ByteByteGo sobre transcrição)
- [Real-time speech-to-text: architecture of a live transcription feature — DEV](https://dev.to/pranjulrathour/real-time-speech-to-text-architecture-of-a-live-transcription-feature-d00)
- [Live Speech-to-Text Transcription Implementation — Medium](https://ryan-zheng.medium.com/live-speech-to-text-transcription-system-implementation-980b5dfe581f)
- [Speech-To-Text Software Design for Higher Education Learning (paper)](https://ceur-ws.org/Vol-3348/paper4.pdf) — STT pra contexto educacional.

## 4. "Ajustar" a transcrição — pós-processamento com LLM

- [AI_LectureNote: workflow pós-ASR pra aulas (paper 2026)](https://arxiv.org/pdf/2607.17237) — pipeline aula → Whisper → correção por LLM.
- [Whisper: Courtside Edition — LLM gerando contexto pra melhorar ASR (paper)](https://arxiv.org/pdf/2602.18966)
- [LectureScribe-AI (repo) — Whisper + LLM pra limpar áudio de aula](https://github.com/GraduationGroup101/LectureScribe-AI)
- [Transcribe and Reformat Audio with LLM Post-Processing — LM-Kit](https://docs.lm-kit.com/lm-kit-net/guides/how-to/transcribe-and-reformat-audio-with-llm.html)
- [Fine-tune Whisper (Hugging Face)](https://huggingface.co/blog/fine-tune-whisper) — se um dia precisar adaptar a vocabulário do domínio.

## 5. Jev (TypeSafe AI) — o que é

- [A deep dive into Jev — Flavio Copes](https://flaviocopes.com/jev/)
- [Language Models for Text Classification: From Bag-of-Words to Jev — Sebastian Raschka (Substack)](https://magazine.sebastianraschka.com/p/classifier-history-and-jev)
- [Jev vs. LLMs: When AI Moves from Generation to Decision-Making — Towards Data Science](https://towardsdatascience.com/jev-vs-llms-when-ai-moves-from-generation-to-decision-making/)
- [Jev: TypeSafe's System One Model Explained — DataCamp](https://www.datacamp.com/blog/system-one-models-jev)
- [How to Use Jev: guia prático — DEV](https://dev.to/valyuai/how-to-use-jev-a-practical-guide-to-typesafes-system-one-model-g5e)
- [Building a harness with Jev — LangChain](https://www.langchain.com/blog/building-a-harness-with-jev)
- [Jev Use Cases: 7 Patterns and 1,300+ Real Builds](https://www.ayautomate.com/blog/jev-use-cases)
- [jev-usecases — harnesses com decisão por confiança (repo)](https://github.com/kenhuangus/jev-usecases)
- [awesome-jev — diretório de projetos](https://github.com/hellogumbo/awesome-jev)
- Contexto de mercado: [The Register](https://www.theregister.com/devops/2026/09/23/shut-up-and-calculate-jevs-new-ai-primitives-for-coders/5298431) · [TechCrunch — Decision API da OpenAI](https://techcrunch.com/2026/09/30/openais-jev-clone-could-help-the-frontier-lab-stop-its-swarming-agents/)

## 6. Jev + Whisper — o que existe hoje

Não encontrei artigo/blog usando Jev **pra melhorar transcrição** em si. O que existe são projetos onde Whisper transcreve e Jev **decide** algo sobre o texto:

- [jev-voice — whisper.cpp local + 1 chamada Jev por comando (repo/README)](https://github.com/kevinbadi/jev-voice/blob/main/README.md) — melhor exemplo de arquitetura Whisper → Jev.
- [jev-on-air — PR adicionando transcrição de YouTube via faster-whisper](https://github.com/valuecodes/jev-on-air/pull/1) — vídeo → faster-whisper → Jev.
- [Slides que navegam sozinhos com Jev (post LinkedIn)](https://www.linkedin.com/posts/harshil1712_i-got-access-to-jev-a-new-model-from-typesafe-activity-7506395781399080961-4bKA) — fala → decisão; próximo do mundo "aula".

Ideias pra pesquisar depois (lacuna — ainda sem fonte): usar Jev pra classificar segmentos da aula (tópico, qualidade, "precisa revisão?") e o padrão *confidence-gated routing* pra mandar só trechos duvidosos pra correção por LLM.
