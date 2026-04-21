# 📁 Content - Seu Conteúdo Vai Aqui

Esta pasta é para **seus documentos e conhecimento**. Coloque o que quiser aqui!

## 📝 Estrutura sugerida

Você pode organizar como preferir:

```
content/
├── patterns/       # Padrões de design e arquitetura
├── practices/      # Práticas recomendadas e boas práticas
├── tutorials/       # Tutoriais e guias passo a passo
├── docs/           # Documentação técnica
├── guidelines/      # Diretrizes e padrões de equipe
└── media/          # Imagens, diagramas, vídeos, PDFs
```

## ✅ Como criar arquivos

### Opção 1: Seu editor favorido

```bash
# VS Code
code ~/Atrium_Knowledge/raw/content/meu-arquivo.md

# Vim
vim ~/Atrium_Knowledge/raw/content/meu-arquivo.md

# Nano
nano ~/Atrium_Knowledge/raw/content/meu-arquivo.md
```

### Opção 2: Templates como referência

Se quiser um ponto de partida, pode copiar de `~/Atrium_Knowledge/templates/`:

```bash
# Listar templates disponíveis
ls ~/Atrium_Knowledge/templates/

# Copiar um template (opcional)
cp ~/Atrium_Knowledge/templates/pattern.md ~/Atrium_Knowledge/raw/content/meu-padrao.md
```

Depois de copiar, **edite o arquivo** com seu conteúdo real.

## 🎯 Formato recomendado para arquivos

Use **Markdown (.md)** - é o formato que o graphify lê melhor.

Estrutura básica:

```markdown
# Título do Conteúdo

## 📋 Visão geral

Breve descrição em 1-2 parágrafos. O que é este conteúdo?

## 🎯 Problema

Qual problema este conteúdo resolve?
- Situação: quando surge o problema?
- Sintomas: quais os sintomas?

## ✅ Solução

Descreva a solução:
- Conceito chave: ideia central
- Abordagem: como funciona

## 📝 Exemplo de implementação

\`\`\`python
# ou a linguagem apropriada
# Exemplo de código ou configuração
\`\`\`

## 💡 Notas e insights

Observações, lições aprendidas, dicas práticas

## 🔗 Conteúdo relacionado

Links para outros arquivos ou recursos:

- [[outro-conceito]]
- [[outra-pratica]]
```

## 🏷️ Tags

\`#tipo #[categoria] #[subcategoria]\`
```

**Dicas:**
- Use títulos claros (`#`, `##`, `###`)
- Adicione exemplos práticos
- Inclua referências quando aplicável
- Use tags para facilitar busca

---

**Depois de criar:** Atualize o grafo para incluir o novo conteúdo:

```bash
cd ~/Atrium_Knowledge
/graphify ./raw --update
```

O graphify vai automaticamente extrair conceitos e conexões do seu novo arquivo!

**Dúvidas?** Consulte o [guia principal](../README.md) ou [AGENTS.md](../AGENTS.md).
