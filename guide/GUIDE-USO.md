# 📖 Guia de Uso do Atrium Knowledge

## 🚀 Começando Rápido

Este é sua base de conhecimento pessoal. Adicione conteúdo, construa o grafo e explore!

## 📁 Estrutura

```
Atrium_Knowledge/
├── raw/                    # Conteúdo cru
│   └── content/           # TODO o seu conteúdo vai aqui
│       ├── graphify-as-knowledge-center.md
│       ├── continuous-graph-maintenance.md
│       ├── onboarding.md
│       └── ...             # Seus documentos
├── graphify-out/           # Grafo gerado
├── guide/                  # ← Você está aqui!
├── add.sh                  # Script para adicionar conteúdo
├── templates/               # Templates (para referência)
├── AGENTS.md               # Instruções para IAs
└── README.md               # Documentação principal
```

## 🎯 Como usar

### 1️⃣ Adicionar conteúdo

Use o script interativo:

```bash
cd ~/Atrium_Knowledge
./add.sh
```

O script pergunta:
- Qual tipo (Pattern, Practice, Tutorial, Doc, Guideline)
- Nome do arquivo
- Abre automaticamente no editor

**Por que usar o script?**
- ✅ Não precisa copiar/colar templates
- ✅ Cria arquivo no lugar certo automaticamente
- ✅ Usa seu editor preferido (VS Code, Vim, etc.)
- ✅ Mais rápido e menos propenso a erros

### 2️⃣ Atualizar o grafo

Depois de adicionar/alterar conteúdo:

```bash
cd ~/Atrium_Knowledge
/graphify ./raw --update
```

**O que o `--update` faz?**
- Re-processa apenas arquivos alterados
- Usa cache SHA256 (muito mais rápido)
- Mescla no grafo existente

### 3️⃣ Navegar pelo conhecimento

**Opção 1 - Grafo visual:**
```bash
firefox ~/Atrium_Knowledge/graphify-out/graph.html
# ou
xdg-open ~/Atrium_Knowledge/graphify-out/graph.html
```
- Clique em nós para ver conexões
- Use a busca para encontrar conceitos
- Filtre por comunidade

**Opção 2 - Resumo executivo:**
```bash
cat ~/Atrium_Knowledge/graphify-out/GRAPH_REPORT.md
```
Este arquivo mostra:
- 🔥 **Nós de Deus** - Conceitos centrais
- 🔗 **Conexões Surpreendentes** - Relações não óbvias
- ❓ **Perguntas Sugeridas** - O que o grafo pode responder

**Opção 3 - Queries ao grafo:**
```bash
# Pergunta geral
/graphify query "como X se conecta a Y?"

# Caminho entre dois conceitos
/graphify path "Conceito A" "Conceito B"

# Explicação de um conceito
/graphify explain "Conceito X"
```

### 4️⃣ Templates (apenas referência)

Em `templates/` você encontra templates para:
- `pattern.md` - Padrão de design
- `practice.md` - Prática recomendada
- `tutorial.md` - Tutorial passo a passo
- `doc.md` - Documentação técnica
- `guideline.md` - Diretriz de equipe

Você **não precisa usar templates**! Use o `add.sh` que é muito mais fácil.

### 5️⃣ Integração com IAs

Este projeto funciona com **todas as plataformas** que suportam graphify:

- ✅ Claude Code, OpenCode, Cursor → `/graphify`
- ✅ Codex → `$graphify`
- ✅ Aider, Gemini, Kiro, Trae, Hermes → `/graphify`
- ✅ VS Code Copilot Chat → `/graphify`
- ✅ GitHub Copilot CLI → `/graphify`

O arquivo `AGENTS.md` contém instruções genéricas que funcionam em qualquer plataforma.

## 💡 Dicas

- **Comece simples**: Adicione conteúdo conforme precisa, não precisa organizar tudo antes
- **Use `--update` sempre**: É muito mais rápido que reconstruir do zero
- **GRAPH_REPORT.md é seu melhor amigo**: Comece por aí antes de qualquer pergunta
- **Grafo não se importa com pastas**: Tudo em `raw/` é lido como se fosse uma pasta só

## 🎓 Próximos passos

1. ✅ Adicione seu primeiro documento com `./add.sh`
2. ✅ Atualize o grafo com `/graphify ./raw --update`
3. ✅ Explore o GRAPH_REPORT.md para entender o que foi criado
4. ✅ Use queries para descobrir relações no seu conhecimento

---

**Você está pronto para começar a construir sua base de conhecimento! 🎉**

Dúvidas? Consulte `README.md` ou `AGENTS.md`
