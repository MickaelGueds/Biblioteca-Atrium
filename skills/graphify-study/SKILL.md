---
name: graphify-study
description: Cria notas de estudo em markdown a partir de links ou texto colado, usando o método Feynman para retenção, decompondo conceitos complexos em notas filhas linkadas, e integrando tudo ao grafo de conhecimento via graphify. Use sempre que o usuário enviar uma URL pedindo pra "resumir pra estudo", "criar nota", "aprender isso", "estudar esse artigo/vídeo", colar um bloco de texto pedindo aprendizado, ou pedir pra transformar conteúdo em conhecimento retido. Triggere também quando o usuário quer organizar leituras, construir uma base de estudo pessoal, ou quando mencionar Feynman, active recall, notas Zettelkasten-style, base de conhecimento pessoal. Não use pra responder perguntas diretas sobre código do projeto nem pra gerar documentação técnica de API.
---

# graphify-study

Transformar conteúdo bruto (link ou texto colado) em notas de estudo estruturadas que **ensinam o conceito de volta pra você** (método Feynman), separam conceitos densos em notas filhas linkadas, e entram automaticamente no grafo de conhecimento do projeto via graphify.

A filosofia: notas não servem pra arquivar, servem pra **ensinar o futuro você**. Se o resumo fosse lido daqui a 3 meses, ele precisa ativar o entendimento — não só descrever o que o artigo disse.

---

## Quando usar

- Usuário manda URL (artigo, YouTube, paper arXiv, tweet, blog) e pede pra estudar/resumir/aprender.
- Usuário cola um bloco de texto pedindo pra virar nota.
- Usuário quer construir/expandir a base de estudos em `conhecimentos_tecnicos/`.

---

## Fluxo

### Passo 1 — Ingerir o conteúdo

**Se o usuário deu uma URL:**
- YouTube, arXiv, Twitter, webpage genérica → preferir `graphify add <url>` (já salva em `./raw/` com metadata), depois ler o `.md` gerado.
- Se `graphify add` não estiver disponível ou falhar, use `WebFetch` direto.

**Se o usuário colou texto:**
- Tratar o texto da mensagem como o conteúdo-fonte.
- Perguntar ao usuário a origem (se não informada) pra preencher `source` no frontmatter — não inventar URL.

### Passo 2 — Decidir o tema e o destino

Pergunte-se: **qual pasta em `conhecimentos_tecnicos/` abriga melhor essa nota?**

- Se já existe pasta temática adequada (ex: `otimizacao_de_contexto/`, `rag/`, `transformers/`), use ela.
- Se não existe, **proponha** uma ao usuário antes de criar — uma pergunta curta: "Essa nota fala sobre X. Salvar em `conhecimentos_tecnicos/<pasta-sugerida>/` ou você prefere outra pasta?"
- Nome do arquivo: slug curto, kebab-case, baseado no conceito central. Ex: `attention-is-all-you-need.md`, não `paper_2017_12_06_final.md`.

### Passo 3 — Checar o grafo existente (coerência)

Antes de escrever, se `graphify-out/graph.json` existir, leia os labels dos nós pra identificar conceitos já presentes na base. Isso evita criar ilhas: se a nota menciona "attention" e já existe uma nota sobre atenção, linke via `[[nome-da-nota-existente]]` em vez de criar duplicata.

Comando rápido pra listar labels existentes:

```bash
python3 -c "
import json
from pathlib import Path
if Path('graphify-out/graph.json').exists():
    data = json.loads(Path('graphify-out/graph.json').read_text())
    for n in data.get('nodes', []):
        print(n.get('label', n.get('id')))
" 2>/dev/null | sort -u
```

Se o arquivo não existir, siga em frente — a primeira nota do grafo tem que nascer em algum lugar.

### Passo 4 — Escrever a nota principal (Feynman)

O princípio Feynman: **se você não consegue explicar com palavras simples, você não entendeu.** A nota principal tem que passar nesse teste — qualquer pessoa que leia deve sair com o conceito na cabeça, não com jargão decorado.

Use este template exato:

```markdown
---
source: <url ou "texto colado por usuário">
captured_at: <YYYY-MM-DD>
tags: [tema-principal, tema-secundario]
type: study-note
---

# <Título claro, não o título original — reescreva pra capturar a essência>

## TL;DR
<2-3 frases. A ideia central em linguagem simples. Sem jargão. Se um amigo leigo perguntasse "o que é isso?", essa é a resposta.>

## Explicação Feynman
<Explique como se estivesse ensinando pra alguém inteligente mas fora da área. Use analogias concretas. Se precisar de um termo técnico, defina ele na mesma frase. Este é o coração da nota — 1 a 3 parágrafos.>

## Pontos-chave
- <Afirmação objetiva 1>
- <Afirmação objetiva 2>
- <...>

## Conceitos envolvidos
- [[conceito-x]] — <uma linha explicando o que é e como se relaciona>
- [[conceito-y]] — <idem>

## Por que importa
<1 parágrafo curto: em que situação real esse conhecimento é aplicável? Quando você vai querer lembrar disso?>

## Perguntas de revisão (active recall)
<3 a 5 perguntas que testam entendimento, não memorização. Evite "qual o nome de X?" — prefira "por que X funciona?" ou "o que aconteceria se X não existisse?">
- ?
- ?
- ?

## Fonte
<link ou descrição da origem>
```

**Sobre o título:** reescreva. O título original do artigo foi otimizado pra clique; o seu tem que ser otimizado pra futura busca mental. "Attention Is All You Need" é ok, mas "Como transformers substituíram RNNs usando atenção paralela" é melhor pra retenção.

### Passo 5 — Decidir o que vira nota filha

Critério: um conceito merece arquivo próprio se **ao menos uma** for verdade:

1. Explicar ele direito consumiria mais de 2-3 frases no resumo principal (ou seja, desviaria o foco da nota).
2. Ele aparece citado em mais de um ponto da nota (sinal de que é uma peça reutilizável).
3. É um pré-requisito que você (usuário) provavelmente não domina ainda.
4. É um termo que vai aparecer em futuras leituras sobre o tema (vale investir em explicar bem uma vez).

**Não crie nota filha pra cada termo técnico.** Isso polui a base. Se "gradient descent" é só mencionado de passagem e o usuário já entende, deixa como texto normal na nota principal.

Cada nota filha segue o mesmo template Feynman acima, com foco no conceito único. Nome do arquivo: `conceito-kebab.md` na mesma pasta temática (ou numa subpasta `conceitos/` se a pasta principal tiver muitas notas).

### Passo 6 — Linkar

Na nota principal, use `[[nome-sem-extensao]]` pra cada nota filha. Graphify detecta esses links como arestas `EXTRACTED` no grafo.

Também linke pra notas **já existentes** encontradas no passo 3 — a base de estudo só tem valor se os conceitos se conectam. Uma nota isolada é um post, uma nota conectada é conhecimento.

### Passo 7 — Atualizar o grafo

Ao terminar de escrever todas as notas:

```bash
graphify . --update
```

Isso re-extrai só os arquivos novos/modificados (barato, sem custo de LLM na maioria dos casos), atualiza `graphify-out/graph.json` e `GRAPH_REPORT.md`.

Se graphify ainda não foi rodado no repo (sem pasta `graphify-out/`), rode o pipeline completo:

```bash
graphify . --wiki
```

### Passo 8 — Reportar ao usuário

Diga de forma curta:
- Quais arquivos foram criados (caminhos relativos).
- Quantas notas filhas nasceram e por quê (1 linha por nota filha).
- A sugestão de revisão: "Volte pra testar as perguntas de revisão daqui a 3 dias, depois 7, depois 21 — é quando o conhecimento consolida."
- Se linkou a notas existentes, cite quais (mostra que a base está ganhando coerência).

---

## Princípios que guiam esta skill

**Retenção > cobertura.** Uma nota curta que você vai re-ler vale mais que uma nota completa que vai ficar parada. Se estiver em dúvida entre incluir detalhe ou cortar, corte.

**Explicar > resumir.** Resumir é reproduzir. Explicar exige entendimento. A seção Feynman é a parte mais importante — gaste esforço nela, não no TL;DR.

**Conectar > arquivar.** Uma nota sem links é um documento. A diferença entre uma base de estudos e uma pasta de PDFs é que a base tem relações explícitas.

**Perguntas > respostas.** A seção de revisão não é formalidade. É o que transforma leitura passiva em conhecimento ativo. Escreva perguntas que você mesmo teria dificuldade de responder daqui a 1 mês.

---

## Exemplo resumido

**Input do usuário:** "cria nota de estudo disso: https://arxiv.org/abs/1706.03762"

**O que a skill faz:**

1. `graphify add https://arxiv.org/abs/1706.03762` → salva abstract em `./raw/`.
2. Lê o `.md` gerado. Identifica que o tema é "transformers / atenção".
3. Lê `graphify-out/graph.json` — encontra nó "RNN" já existente.
4. Pergunta ao usuário: "Salvar em `conhecimentos_tecnicos/transformers/`?"
5. Cria `conhecimentos_tecnicos/transformers/attention-is-all-you-need.md` com o template Feynman.
6. Decide que "self-attention" e "positional encoding" precisam de notas próprias (aparecem várias vezes, são pré-requisitos densos). Cria `conceitos/self-attention.md` e `conceitos/positional-encoding.md`.
7. Linka de volta pra `[[rnn]]` (nota existente) na seção "Por que importa" — contraste.
8. Roda `graphify . --update`.
9. Reporta: 3 notas criadas, 1 link pra nota existente, próxima revisão em 3 dias.
