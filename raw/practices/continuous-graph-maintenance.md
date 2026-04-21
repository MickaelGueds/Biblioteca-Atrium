# Manutenção Contínua do Grafo de Conhecimento

## 📋 Visão geral

Prática para manter o grafo de conhecimento sempre atualizado com o mínimo de esforço manual. O objetivo é que o grafo evolua organicamente com o projeto, exigindo intervenção mínima.

## 🎯 Objetivo

- Manter o grafo sincronizado com o conteúdo
- Minimizar custo de atualização (tokens e tempo)
- Automatizar onde possível
- Manter relevância das conexões

## 📖 Contexto

- **Domínio**: Gestão de conhecimento
- **Equipe**: Qualquer tamanho, especialmente útil para equipes distribuídas
- **Projeto**: Projetos com documentação ativa e múltiplos tipos de conteúdo

## ✅ A prática

### Passo 1: Configurar hooks automáticos

Instale o hook do git para rebuild automático após commits:

```bash
cd ~/Atrium_Knowledge
graphify hook install
```

Isso garante que o grafo se reconstrói após cada commit sem intervenção manual.

### Passo 2: Use atualizações incrementais

Para mudanças frequentes em arquivos de código:

```bash
/graphify ./raw --mode ast-only
```

Processa apenas arquivos de código via AST (sem custo de LLM).

### Passo 3: Atualizações manuais de conteúdo

Ao adicionar/alterar documentação ou mídia:

```bash
/graphify ./raw --update
```

Reprocessa apenas arquivos alterados, usando cache SHA256.

### Passo 4: Full rebuild periódico

Uma vez por mês ou quando houver muitas mudanças:

```bash
rm -rf graphify-out/cache/
/graphify ./raw
```

Reconstrói tudo do zero para garantir consistência.

### Passo 5: Commit o grafo

```bash
# No .gitignore
graphify-out/cache/
graphify-out/transcripts/

# No commit
git add graphify-out/
git commit -m "update: graph knowledge base"
```

Apenas o grafo (graph.json, wiki, etc), não o cache.

## 💻 Exemplo

Fluxo de trabalho típico:

```bash
# 1. Adiciona novo padrão
vim raw/patterns/novo-pattern.md

# 2. Atualiza o grafo
/graphify ./raw --update

# 3. Verifica as novas conexões
cat graphify-out/GRAPH_REPORT.md

# 4. Commit tudo
git add raw/patterns/novo-pattern.md graphify-out/
git commit -m "add: novo pattern de autenticação"
```

## 🏆 Benefícios

- **Economia de tokens**: Cache SHA256 evita reprocessamento
- **Sincronização automática**: Git hooks mantém tudo atualizado
- **Baixo esforço**: A maioria das atualizações é `--update` rápido
- **Compartilhamento**: Teammates sempre têm o grafo atualizado

## ⚠️ Riscos e mitigações

| Risco | Mitigação |
|-------|-----------|
| Grafo dessincronizado | Configure git hooks desde o início |
| Custo alto de LLM | Use `--mode ast-only` para mudanças de código |
| Cache corrompido | Full rebuild periódico mensal |
| Conexões desatualizadas | Ajuste parâmetros de similaridade em `--mode deep` |

## 🔗 Padrões relacionados

- [[Pattern: Graphify as Knowledge Center]]: Este é o padrão subjacente
- [[Practice: Atomic Commits]]: Pequenos commits facilitam updates incrementais
- [[Pattern: Continuous Integration]]: Git hooks como forma de CI

## 🎓 Pré-requisitos

- graphify instalado e configurado
- Git configurado no projeto
- Conhecimento básico de CLI

## 📊 Métricas de sucesso

- **Latência de atualização**: < 5 minutos para `--update`
- **Custo por update**: < 1000 tokens para updates típicos
- **Cache hit rate**: > 90% de arquivos não alterados não reprocessados
- **Sincronização**: Grafo sempre ≤ 1 commit atrás do conteúdo

## 📚 Referências

- [graphify CLI docs](https://github.com/safishamsi/graphify#usage)
- [Git hooks documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)

## 💡 Dicas e truques

- **Use `--watch`** para desenvolvimento ativo: `graphify watch ./raw`
- **Separação de concerns**: Código em `raw/code/`, docs em `raw/docs/` para updates específicos
- **Full rebuild após migração**: Se reorganizar pastas, sempre reconstrua do zero
- **Monitore o GRAPH_REPORT.md**: Se aparecerem muitas "conexões surpreendentes", pode ser hora de rebuild

## 🚨 Erros comuns

- **Esquecer de fazer update**: Configure git hooks para automação
- **Full rebuild excessivo**: Usa `--update` sempre que possível
- **Commitar cache**: Adicione `graphify-out/cache/` ao `.gitignore`
- **Ignorar GRAPH_REPORT.md**: Sempre leia após updates significativos

## 🏷️ Tags

`#practice #maintenance #graphify #continuous-knowledge`
