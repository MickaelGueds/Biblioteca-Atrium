# Otimização de Contexto com LLMs

## 🎯 O que é

Um padrão para construir bases de conhecimento pessoais usando LLMs, onde o modelo **constrói e mantém um wiki persistente** entre você e suas fontes originais.

## ⚡ Como Usar (Resumido)

### Arquitetura em 3 Camadas

```
📁 raw/              → Fontes originais (imutáveis)
📁 wiki/             → Markdown gerado pelo LLM
📄 schema.md         → Instruções para o LLM (CLAUDE.md/AGENTS.md)
```

### Operações Principais

1. **Ingestão** → Adicione fontes ao `raw/`, o LLM processa e atualiza o `wiki/`
2. **Consulta** → Pergunte ao wiki, receba respostas com citações
3. **Manutenção** → Lint periódico para consistência e novos insights

### Por que funciona

- **Custo de manutenção ≈ zero**: LLMs não ficam entediados
- **Cruzamento de referências automático**: O wiki já está interligado
- **Acúmulo de conhecimento**: Cada nova fonte enriquece o que já existe

## 📚 Estrutura para Estudos

```
otimizacao-de-contexto/
├── README.md                 ← Você está aqui (guia rápido)
├── 01-conceitos/
│   ├── ideia-central.md      ← Tradução completa do Karpathy
│   ├── arquitetura.md        ← 3 camadas explicadas
│   └── diferenciais.md       ← Por que ≠ RAG tradicional
├── 02-implementacao/
│   ├── fluxo-ingestao.md     ← Como adicionar novas fontes
│   ├── consultas.md          ← Como fazer perguntas eficientes
│   ├── manutencao.md         ← Lint e health-checks
│   └── indice-e-log.md       ← Navegação no wiki
├── 03-casos-de-uso/
│   ├── pessoal.md            ← Metas, saúde, psicologia
│   ├── pesquisa.md           → Papers, artigos, teses evolutivas
│   ├── leitura-livros.md     ← Personagens, temas, plot
│   └── equipe-negocio.md     ← Slack, reuniões, projetos
└── 04-ferramentas/
    ├── obsidian.md           ← Configuração recomendada
    ├── busca-qmd.md          ← Engine de busca local
    ├── marp.md               ← Slides em markdown
    └── dataview.md           ← Queries dinâmicas
```

## 🚀 Próximos Passos

1. Leia `01-conceitos/ideia-central.md` para entender a fundo
2. Configure seu `CLAUDE.md` ou `AGENTS.md` como schema
3. Comece pequeno: 1-2 fontes no `raw/`, deixe o LLM construir o wiki inicial
4. Expanda gradualmente conforme desenvolve seu fluxo de trabalho

---

**Fonte Original**: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f  
**Autor**: Andrej Karpathy (4 de abril de 2026)