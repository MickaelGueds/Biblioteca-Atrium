# Wiki LLM: A Ideia Central

## Ideia Principal

A maioria das pessoas experimenta LLMs e documentos através de RAG: você faz upload de uma coleção de arquivos, o LLM recupera chunks relevantes no momento da consulta e gera uma resposta. Isso funciona, mas o LLM está **redescobrindo conhecimento do zero a cada pergunta**. Não há acúmulo. Faça uma pergunta sutil que exija sintetizar cinco documentos, e o LLM terá que encontrar e juntar os fragmentos relevantes todas as vezes. Nada é construído. NotebookLM, uploads de arquivos do ChatGPT e a maioria dos sistemas RAG funcionam assim.

## A Diferença

A ideia aqui é diferente. Em vez de apenas recuperar de documentos brutos no momento da consulta, o LLM **constrói incrementalmente e mantém um wiki persistente** — uma coleção estruturada e interligada de arquivos markdown que fica entre você e as fontes brutas.

Quando você adiciona uma nova fonte, o LLM não apenas a indexa para recuperação posterior. Ele lê a fonte, extrai as informações-chave e as integra ao wiki existente — atualizando páginas de entidades, revisando resumos de tópicos, notando onde novos dados contradizem afirmações antigas, fortalecendo ou desafiando a síntese em evolução.

O conhecimento é compilado uma vez e então *mantido atualizado*, não rederivado a cada consulta.

## A Chave

**O wiki é um artefato persistente e composto.** As referências cruzadas já estão lá. As contradições já foram sinalizadas. A síntese já reflete tudo o que você leu. O wiki fica cada vez mais rico com cada fonte que você adiciona e cada pergunta que faz.

## Divisão de Papéis

Você nunca (ou raramente) escreve o wiki você mesmo — o LLM escreve e mantém tudo. Você é responsável por:
- Curadoria de fontes
- Exploração
- Fazer as perguntas certas

O LLM faz todo o trabalho pesado — o resumo, referências cruzadas, arquivamento e gerenciamento que torna uma base de conhecimento útil ao longo do tempo.

## Fluxo Prático

Na prática, tenho o agente LLM aberto de um lado e o Obsidian aberto do outro. O LLM faz edições baseadas na nossa conversa, e eu navego os resultados em tempo real — seguindo links, verificando a visualização de grafo, lendo as páginas atualizadas.

- **Obsidian** = IDE
- **LLM** = Programador
- **Wiki** = Codebase

## Contextos de Aplicação

Isso pode se aplicar a muitos contextos diferentes:

### 📖 Pessoal
Acompanhamento de suas próprias metas, saúde, psicologia, autoaperfeiçoamento — arquivando entradas de diário, artigos, notas de podcasts e construindo uma imagem estruturada de você mesmo ao longo do tempo.

### 🔬 Pesquisa
Ir fundo em um tópico por semanas ou meses — lendo papers, artigos, relatórios e construindo incrementalmente um wiki abrangente com uma tese em evolução.

### 📚 Leitura de Livro
Arquivando cada capítulo conforme você avança, construindo páginas para personagens, temas, linhas de trama e como eles se conectam. No final, você tem um wiki companheiro rico. Pense em wikis de fãs como o [Tolkien Gateway](https://tolkiengateway.net/wiki/Main_Page) — milhares de páginas interligadas cobrindo personagens, lugares, eventos, idiomas, construídos por uma comunidade de voluntários ao longo de anos. Você poderia construir algo assim pessoalmente enquanto lê, com o LLM fazendo todo o cruzamento de referências e manutenção.

### 💼 Negócios/Equipe
Um wiki interno mantido por LLMs, alimentado por threads do Slack, transcrições de reuniões, documentos de projeto, chamadas de clientes. Possivelmente com humanos no loop revisando atualizações. O wiki permanece atualizado porque o LLM faz a manutenção que ninguém na equipe quer fazer.

### 🎯 Outros
Análise competitiva, due diligence, planejamento de viagem, notas de curso, deep dives em hobbies — qualquer coisa onde você está acumulando conhecimento ao longo do tempo e quer organizado em vez de espalhado.

---

**Tradução de**: [karpathy/llm-wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)  
**Autor Original**: Andrej Karpathy  
**Data**: 4 de abril de 2026