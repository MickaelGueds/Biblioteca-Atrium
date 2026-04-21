---
source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
captured_at: 2026-04-21
tags: [ia, rag, knowledge-base, retrieval]
type: study-note
---

# RAG vs Wiki persistente: a diferença entre redescobrir e acumular

## TL;DR
RAG lê fragmentos brutos a cada pergunta — conhecimento é **redescoberto do zero** toda vez. O padrão wiki destila as fontes uma vez em páginas interligadas e responde a partir do destilado — conhecimento **acumula**. A diferença aparece fortemente quando a pergunta exige síntese entre várias fontes.

## Explicação Feynman
Imagina duas formas de responder "quais os principais argumentos contra X nos últimos 10 artigos que li?".

Forma 1 (RAG): o sistema quebra todos os artigos em pedacinhos, busca os pedaços com mais palavras parecidas com a pergunta, joga isso num LLM e pede pra costurar. Funciona pra perguntas diretas ("onde o artigo Y fala de Z?"). Mas quando a resposta depende de comparar cinco fontes, o LLM tem que re-ler cinco fontes e re-sintetizar — toda vez, do zero. Nada do trabalho anterior é reaproveitado.

Forma 2 (wiki): quando cada artigo entrou na base, o LLM já escreveu uma página de síntese sobre "argumentos contra X", já linkou cada aparição, já marcou onde um artigo contradizia outro. Quando você pergunta, ele abre essa página pronta. O trabalho pesado foi feito na ingestão, não na query.

A questão central: **onde mora o custo do pensamento?** RAG paga no tempo da pergunta; o wiki paga uma vez, no tempo da ingestão, e depois capitaliza. Isso muda drasticamente o custo marginal de fazer uma pergunta nova, e libera você pra explorar de verdade em vez de economizar perguntas.

RAG também sofre em perguntas cuja resposta não está em nenhum chunk específico, mas na **relação** entre chunks — tipo "o que mudou no meu pensamento sobre X ao longo desses artigos?". Chunking não captura relação; wiki captura.

## Pontos-chave
- RAG: custo na query, reretrabalha a cada pergunta, bom pra lookup direto.
- Wiki: custo na ingestão, reaproveita trabalho, bom pra síntese e perguntas sobre relações.
- RAG é stateless entre queries; wiki é stateful — o estado é o próprio markdown versionado.
- Não são mutuamente exclusivos: você pode rodar RAG *sobre* o wiki pra lookup rápido dentro das páginas já destiladas.
- Wiki tem cross-references explícitas; RAG só tem similaridade implícita via embeddings.

## Por que importa
Quando você entende essa distinção, fica claro por que ferramentas como NotebookLM são ótimas pra "me lembre onde foi dito Y" e frustrantes pra "me ajude a entender minha posição sobre Y". Também explica por que este repo prefere markdown + graphify + `[[links]]` manuais em vez de um banco vetorial: você está otimizando pra síntese acumulada, não pra retrieval rápido.

Na prática, isso define quando cada abordagem faz sentido:
- Base de estudos pessoal / pesquisa de longo prazo → wiki.
- Base de docs de API que muda toda semana → RAG (não vale manter síntese de algo efêmero).
- Notas de livro, journal, projeto de pesquisa → wiki.
- Helpdesk sobre 10 mil tickets → RAG.

## Perguntas de revisão (active recall)
- Se o custo total fosse o mesmo, ainda faria diferença escolher wiki em vez de RAG? Por quê?
- Em que tipo de pergunta RAG tende a dar resposta pior que wiki, mesmo com o mesmo conjunto de fontes?
- O que a frase "RAG é stateless entre queries" implica na prática quando você faz 20 perguntas parecidas sobre o mesmo corpus?
- Dá pra ter wiki sem usar LLM na manutenção? O que muda?

## Fonte
Inferido de Andrej Karpathy, "LLM Wiki" (gist), abril 2026. Conceito estendido com base no padrão descrito em [[llm-wiki-pattern]].
