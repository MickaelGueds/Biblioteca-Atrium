# Casos de Uso: Pesquisa Acadêmica

## Visão Geral

Construir conhecimento profundo sobre um tópico de pesquisa através de papers, artigos e fontes relacionadas.

## Fluxo de Trabalho

### Fase 1: Levantamento (Semanas 1-2)

```
1. Buscar papers chave em ArXiv, Google Scholar, PubMed
2. Ler introduções e conclusões de ~20 papers
3. Identificar 5-10 papers principais
4. Ingestão no wiki: raw/papers/
```

### Fase 2: Fundação (Semanas 3-4)

```
1. Leitura profunda dos 5-10 papers principais
2. Extração de conceitos-chave
3. Criação de páginas de conceitos e entidades
4. Identificação de lacunas de conhecimento
```

### Fase 3: Expansão (Semanas 5-8)

```
1. Buscar papers que preencham lacunas
2. Ingestão incremental
3. Atualização de páginas existentes
4. Criação de sínteses comparativas
```

### Fase 4: Síntese (Semanas 9-12)

```
1. Identificar tendências e evolução temporal
2. Criar linha do tempo do tópico
3. Síntese de estado da arte
4. Identificar direções futuras
```

## Estrutura do Wiki

```
wiki/pesquisa/[topico]/
├── conceitos/
│   ├── conceito-1.md
│   ├── conceito-2.md
│   └── ...
├── entidades/
│   ├── autores-chave.md
│   ├── laboratorios.md
│   └── datasets.md
├── papers/
│   ├── paper-1.md
│   ├── paper-2.md
│   └── ...
├── sintese/
│   ├── estado-da-arte.md
│   ├── evolucao-temporal.md
│   ├── comparacoes.md
│   ├── lacunas.md
│   └── direcoes-futuras.md
└── questoes-abertas.md
```

## Exemplo de Consulta

```
Você: "Quais são as principais abordagens para X?"

LLM:
1. Busca "X" em index.md
2. Lê wiki/pesquisa/X/conceitos/
3. Lê wiki/pesquisa/X/sintese/estado-da-arte.md
4. Sintetiza resposta com abordagens, trade-offs e referências
```

## Padrões de Uso

- Comece com papers seminais (altamente citados)
- Construa cronologicamente (papers mais antigos → mais novos)
- Foque em papers que introduzem novos conceitos, não variações
- Use comparações para entender trade-offs
- Busque revisões de literatura para panoramas rápidos