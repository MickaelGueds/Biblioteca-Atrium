---
source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
captured_at: 2026-04-21
tags: [ia, llm-ops, claude-md, convencoes]
type: study-note
---

# O schema: o arquivo que faz o LLM virar mantenedor disciplinado e não chatbot genérico

## TL;DR
O schema é um arquivo de convenções (ex: `CLAUDE.md`, `AGENTS.md`, ou uma SKILL) que descreve **como o wiki é estruturado e qual o fluxo pra ingerir, consultar e manter**. Sem ele, o LLM improvisa toda sessão. Com ele, cada sessão opera sob as mesmas regras — é o que torna a base consistente ao longo do tempo.

## Explicação Feynman
Pensa num estagiário novo chegando toda segunda-feira sem lembrar de nada da semana anterior. Se ele só entender "organize meus arquivos", você vai ter uma pasta diferente por semana. Se ele ler um manual do time que diz "fontes vão em `raw/`, resumos em `wiki/`, append no `log.md` com o prefixo tal, contradições são marcadas assim" — aí ele opera igual a qualquer outro estagiário que leu o mesmo manual.

O schema é exatamente esse manual, mas escrito pro LLM. Ele resolve o problema de que cada conversa começa do zero: em vez de redescobrir convenções, o LLM carrega o schema no contexto e age a partir dele.

O importante é que o schema **co-evolui com você**. Na primeira semana ele tem três linhas. Depois de usar um mês você percebe "toda vez eu tenho que lembrar o LLM de linkar pra página índice" — aí vira regra no schema. Depois de seis meses você tem um documento denso que codificou todas as suas preferências de organização. Esse documento é quase mais valioso que o próprio wiki: ele é o **DNA operacional** da sua base de conhecimento.

Em Claude Code específicamente, o equivalente é o `CLAUDE.md` do projeto + skills (como esta). Em Codex é `AGENTS.md`. Em OpenCode é config do projeto. O formato muda, o papel é idêntico.

## Pontos-chave
- Schema não é documentação pra humanos — é instrução operacional pra LLM.
- Bons schemas explicam o **porquê** das convenções, não só o quê (LLM atual interpreta intenção; regras mudas geram rigidez).
- Deve listar: onde ficam raw sources, estrutura do wiki, como fazer ingest, como responder query, o que atualizar em cada caso, formato do log.
- Evolui por observação: toda vez que você corrige o LLM duas vezes pela mesma coisa, vira linha no schema.
- Versionado junto com o wiki no mesmo repo git — o histórico do schema conta como sua metodologia de estudo amadureceu.

## Por que importa
Essa é a peça que separa "usei LLM pra organizar arquivos uma vez" de "tenho uma base que cresce sozinha há um ano". Sem schema, você é obrigado a re-explicar regras em cada sessão e a base fica com estilo inconsistente entre períodos. Com schema, a base mantém identidade mesmo que você troque de modelo, de agente, ou fique meses sem mexer.

No contexto do seu repo: o `graphify.md` na raiz + `SKILL.md` da graphify-study já são embriões de schema. Faz sentido, à medida que a base cresce, consolidar isso num `CLAUDE.md` do projeto com as convenções explícitas (onde fica o quê, como nomear, quando criar nota filha).

## Perguntas de revisão (active recall)
- Por que o schema precisa explicar o *porquê* das regras e não só listar as regras?
- Qual o sinal, na prática, de que uma regra deveria ser promovida pra dentro do schema?
- Se você trocasse de LLM (de Claude pra outro modelo) amanhã, o que no schema precisaria mudar — e o que não?
- Por que o schema fica no mesmo repo git que o wiki, e não separado?

## Fonte
Inferido de Andrej Karpathy, "LLM Wiki" (gist), abril 2026 — seção "The schema". Ver [[llm-wiki-pattern]] pro contexto completo.
