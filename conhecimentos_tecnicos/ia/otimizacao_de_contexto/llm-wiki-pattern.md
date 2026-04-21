---
source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
captured_at: 2026-04-21
tags: [ia, otimizacao-de-contexto, knowledge-base, llm, obsidian]
type: study-note
---

# LLM como mantenedor de wiki pessoal: conhecimento que acumula em vez de ser redescoberto

## TL;DR
Em vez de usar LLM pra ler seus arquivos e responder perguntas do zero toda vez (RAG), você deixa ele **construir e manter incrementalmente um wiki de markdown** entre você e as fontes. A cada fonte nova, o LLM atualiza páginas existentes, cria cross-references e marca contradições. O conhecimento é compilado uma vez e mantido atualizado — não re-derivado a cada pergunta.

## Explicação Feynman
Pensa numa biblioteca normal versus num bibliotecário que, toda vez que chega um livro novo, reescreve o índice geral, atualiza as fichas dos autores relacionados, anota nos cartões antigos "isso contradiz o que o livro X dizia" e mantém um mapa dos temas sempre vivo. No final, quando alguém pergunta algo, o bibliotecário consulta o **índice já sintetizado** em vez de reler a estante inteira.

O [[rag-vs-wiki]] tradicional (NotebookLM, ChatGPT com uploads) é a estante — cada pergunta é uma nova busca que precisa achar e costurar fragmentos do zero. O padrão do Karpathy é o bibliotecário: o LLM lê cada fonte nova, destila ela em páginas de wiki interligadas, e as próximas perguntas consultam esse wiki já sintetizado.

A divisão de trabalho é clara: **o humano escolhe as fontes, explora e pergunta; o LLM escreve e mantém tudo.** Você raramente digita no wiki — você browsa. A analogia do Karpathy: Obsidian é o IDE, o LLM é o programador, o wiki é o codebase. Tudo versionado num repo git.

O motivo disso funcionar agora e não antes: a parte tediosa de manter uma base de conhecimento nunca foi ler ou pensar — foi a bookkeeping. Atualizar referência cruzada, manter resumos em dia, notar contradições, consistência entre dezenas de páginas. Humanos abandonam wikis porque a manutenção cresce mais rápido que o valor. LLM não cansa, não esquece, toca 15 arquivos num único passe. O custo de manutenção vai pra perto de zero — e aí o wiki finalmente fica vivo.

## Pontos-chave
- Três camadas: **raw sources** (imutável, só leitura) + **wiki** (LLM escreve) + **[[schema-de-wiki]]** (CLAUDE.md/AGENTS.md: regras de como o LLM opera).
- Fluxo de três verbos: **Ingest** (fonte entra, LLM propaga pro wiki) → **Query** (pergunta consulta o wiki já sintetizado; respostas boas voltam pra dentro dele) → **Maintain** (refactor, lint, consolidação).
- Toda boa resposta de query pode virar página nova — exploração compounds igual ingestão.
- `log.md` append-only (prefixo `## [data] ingest|query|lint | ...`) dá timeline parseável com `grep`.
- Obsidian graph view mostra hubs, órfãos e a forma real da base; é diagnóstico de saúde do wiki.
- Casa com Vannevar Bush / Memex (1945): a parte que ele não resolveu — quem faz a manutenção — agora tem resposta.

## Conceitos envolvidos
- [[rag-vs-wiki]] — por que retrieval-só não basta quando você quer conhecimento que acumula.
- [[schema-de-wiki]] — o arquivo de convenções que transforma o LLM de chatbot genérico em mantenedor disciplinado.

## Por que importa
Esse é o padrão subjacente ao que você já está montando neste repo (`conhecimentos_tecnicos/` + graphify + a skill `graphify-study`). Entender o raciocínio do Karpathy te dá o **porquê** das escolhas: por que as notas são markdown simples e não um banco vetorial, por que `[[links]]` são o formato de aresta, por que faz sentido ter um arquivo de schema (`CLAUDE.md`, a própria SKILL.md), por que rodar graphify como índice estrutural não substitui o wiki mas o complementa.

Também reenquadra o uso diário de LLM: em vez de conversas soltas que viram logs perdidos, cada conversa **deixa rastro permanente** no wiki. Isso é otimização de contexto no sentido profundo — você não precisa recarregar o entendimento toda sessão porque ele já está destilado em disco.

## Perguntas de revisão (active recall)
- Se RAG também "usa LLM sobre seus documentos", o que exatamente o padrão wiki faz que RAG não faz — e por que isso muda o resultado quando você pergunta algo que depende de 5 fontes?
- Por que esse padrão era inviável antes dos LLMs atuais, mesmo que a ideia (Memex) seja de 1945?
- Quando uma resposta de query deveria virar uma página do wiki e quando deveria ficar só no chat? Qual o critério?
- Se você tivesse que explicar em uma frase a diferença de papel entre humano e LLM nesse sistema, qual seria?
- Como `log.md` e `index.md` se diferenciam na função — e por que os dois existem em vez de um só?

## Fonte
Andrej Karpathy, "LLM Wiki" (gist público, abril 2026). https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
