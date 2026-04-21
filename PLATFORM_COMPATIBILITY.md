# Compatibilidade Multiplataforma

Este projeto foi projetado para funcionar com múltiplos assistentes de IA que suportam o graphify.

## 🎯 Plataformas suportadas

- ✅ **Claude Code** - `/graphify` (usando a skill)
- ✅ **OpenCode** - `/graphify` (usando a skill)
- ✅ **Codex** - `$graphify` (símbolo `$` ao invés de `/`)
- ✅ **Cursor** - `/graphify` (usando a skill)
- ✅ **GitHub Copilot CLI** - `/graphify` (usando a skill)
- ✅ **Aider** - `/graphify` (via AGENTS.md)
- ✅ **Gemini CLI** - `/graphify` (via AGENTS.md)
- ✅ **VS Code Copilot Chat** - `/graphify` (via skill)
- ✅ **OpenClaw** - `/graphify` (via AGENTS.md)
- ✅ **Factory Droid** - `/graphify` (via AGENTS.md)
- ✅ **Trae** - `/graphify` (via AGENTS.md)
- ✅ **Hermes** - `/graphify` (via skill)
- ✅ **Kiro IDE/CLI** - `/graphify` (via skill)
- ✅ **Google Antigravity** - `/graphify` (via AGENTS.md)

## 📝 Sintaxe de comandos

### Comando base
Todas as plataformas usam a mesma sintaxe base:

```bash
# Constrói o grafo completo
/graphify <caminho>

# Atualiza o grafo incrementalmente
/graphify <caminho> --update

# Faz uma pergunta ao grafo
/graphify query "pergunta?"

# Mostra o caminho entre dois conceitos
/graphify path "Conceito A" "Conceito B"

# Explica um conceito
/graphify explain "Conceito"

# Gera wiki + Obsidian
/graphify <caminho> --wiki --obsidian
```

### Diferenças por plataforma

| Plataforma | Trigger | Hooks nativos | Observação |
|-----------|---------|----------------|-------------|
| Claude Code | `/graphify` | PreToolUse | Sintaxe completa |
| OpenCode | `/graphify` | tool.execute.before | Sintaxe completa |
| Codex | `$graphify` | PreToolUse | Usa `$` ao invés de `/` |
| Cursor | `/graphify` | Regras sempre-on | Sintaxe completa |
| Aider | `/graphify` | Nenhum | Usa AGENTS.md |
| Gemini CLI | `/graphify` | BeforeTool | Sintaxe completa |

## 🚀 Como configurar para sua plataforma

### Claude Code / OpenCode / Cursor

```bash
cd ~/Atrium_Knowledge
/graphify ./raw --wiki --obsidian
```

### Codex

```bash
cd ~/Atrium_Knowledge
$graphify ./raw --wiki --obsidian
```

### Aider / Gemini CLI / Outras plataformas

Essas plataformas usam o arquivo `AGENTS.md` para instruções. O arquivo já está configurado corretamente.

## 📁 Estrutura de arquivos compatível

```
Atrium_Knowledge/
├── raw/                      # Conteúdo cru
│   ├── patterns/           # Padrões
│   ├── practices/          # Práticas
│   ├── docs/               # Documentação
│   ├── guidelines/          # Diretrizes
│   ├── tutorials/           # Tutoriais
│   └── media/              # Mídia
├── graphify-out/           # Grafo gerado
│   ├── graph.html        # Visualização
│   ├── GRAPH_REPORT.md   # Resumo executivo
│   ├── graph.json        # Grafo persistente
│   ├── wiki/             # Wiki gerada
│   └── obsidian/         # Vault do Obsidian
├── AGENTS.md              # Instruções genéricas para IAs
├── README.md              # Documentação principal
└── QUICKSTART.md          # Início rápido
```

## 💡 Dicas

1. **Comandos genéricos**: A documentação usa `/graphify` como placeholder. Adapte para o trigger da sua plataforma (`/graphify`, `$graphify`, etc.)

2. **Caminhos relativos**: Quando estiver dentro do projeto, pode usar `.` ao invés do caminho completo:
   ```bash
   /graphify .
   /graphify . --update
   ```

3. **AGENTS.md**: Arquivo genérico que funciona em todas as plataformas que o suportam

4. **Compatibilidade total**: O mesmo projeto funciona em Claude, OpenCode, Codex, Cursor, Aider, Gemini, e outros sem modificações

## 🎯 Próximo passo

Após configurar, comece pelo resumo executivo:

```bash
# Claude / OpenCode / Cursor
cat ~/Atrium_Knowledge/graphify-out/GRAPH_REPORT.md

# Codex
cat ~/Atrium_Knowledge/graphify-out/GRAPH_REPORT.md
```

---

**Lembre-se:** A documentação usa `/graphify` como sintaxe padrão. Adapte para o trigger específico da sua plataforma, mas os comandos são os mesmos em todas as plataformas!
