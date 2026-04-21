# Quick Start - Cognexus Knowledge Base

⚡ Comece a usar em 3 minutos

## Passo 1: Construir o grafo inicial

```bash
cd ~/Atrium_Knowledge
/graphify ./raw --wiki --obsidian
```

## Passo 2: Entenda o conhecimento

```bash
# Leia o resumo executivo (IMPORTANTE!)
cat ~/Atrium_Knowledge/graphify-out/GRAPH_REPORT.md
```

Este arquivo mostra:
- **God Nodes**: conceitos centrais
- **Surprising Connections**: relações não óbvias
- **Suggested Questions**: o que o grafo pode responder

## Passo 3: Navegue

```bash
# Opção 1: Wiki gerada
cat graphify-out/wiki/index.md

# Opção 2: Grafo visual
firefox graphify-out/graph.html

# Opção 3: Queries
/graphify query "como graphify conecta conceitos?"
/graphify path "Graphify" "Repository"
/graphify explain "Knowledge Graph"
```

## Passo 4: Adicione conteúdo

```bash
# Use templates
cp ~/Atrium_Knowledge/templates/pattern.md ~/Atrium_Knowledge/raw/patterns/meu-padrao.md
vim ~/Atrium_Knowledge/raw/patterns/meu-padrao.md

# Atualize o grafo
cd ~/Atrium_Knowledge
/graphify ./raw --update
```

## 📚 Documentação completa

- [README completo](README.md)
- [Tutorial de onboarding](~/Atrium_Knowledge/raw/tutorials/onboarding.md)
- [AGENTS.md - Instruções para IAs](AGENTS.md)

## 🎯 Comandos úteis

| Comando | O que faz |
|---------|-----------|
| `/graphify ./raw` | Constrói grafo completo |
| `/graphify ./raw --update` | Atualiza incremental |
| `/graphify query "...?"` | Faz pergunta ao grafo |
| `/graphify path "A" "B"` | Mostra caminho entre A e B |
| `/graphify explain "X"` | Explica conceito X |
| `graphify hook install` | Atualização automática no git |

---

**💡 Lembre-se:** O poder está nas **conexões**, não apenas no conteúdo. Comece sempre pelo `GRAPH_REPORT.md`!
