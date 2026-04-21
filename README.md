# Atrium Knowledge Base

🧠 Uma rede de conhecimento interconectada powered by graphify

> Esta é uma **central de conhecimento interligada** que usa graphify para criar conexões automáticas entre padrões, práticas, documentação e recursos de aprendizado. Não é apenas uma wiki - é um grafo de conhecimento vivo que se reorganiza automaticamente conforme você adiciona conteúdo.

## 🚀 Como começar

### 1. Primeiro passo: Construir o grafo inicial

Use o comando apropriado para sua plataforma:

**Claude Code / OpenCode / Cursor / VS Code Copilot:**
```bash
cd ~/Atrium_Knowledge
/graphify ./raw --wiki --obsidian
```

**Codex:**
```bash
cd ~/Atrium_Knowledge
$graphify ./raw --wiki --obsidian
```

**Aider / Gemini CLI / Outras plataformas:**
Consulte [PLATFORM_COMPATIBILITY.md](PLATFORM_COMPATIBILITY.md) para detalhes.

Isso vai:
- Ler todo o conteúdo em `raw/`

```bash
cd ~/Atrium_Knowledge
/graphify ./raw --wiki --obsidian
```

Isso vai:
- Ler todo o conteúdo em `raw/`
- Extrair conceitos e relacionamentos
- Construir um grafo de conhecimento
- Gerar wiki navegável em `graphify-out/wiki/`
- Criar vault do Obsidian em `graphify-out/obsidian/`

### 2. Navegue pelo conhecimento

O arquivo `graphify-out/GRAPH_REPORT.md` contém:
- **Nós de Deus**: conceitos centrais que conectam tudo
- **Conexões Surpreendentes**: relações não óbvias entre conteúdo
- **Perguntas Sugeridas**: perguntas que o grafo pode responder

### 3. Use queries para descobrir

```bash
/graphify query "como pattern X afeta prática Y?"
/graphify query "o que conecta conceito A ao conceito B?"
/graphify path "Authentication" "Database"
```

## 📁 Estrutura do projeto

```
Atrium_Knowledge/
├── raw/                           # Conteúdo cru (seu repositório de conhecimento)
│   ├── patterns/                  # Padrões de design, arquiteturais, etc.
│   ├── practices/                 # Práticas recomendadas, boas práticas
│   ├── docs/                      # Documentação técnica
│   ├── guidelines/                # Diretrizes, regras, padrões de equipe
│   ├── tutorials/                 # Tutoriais, guias passo a passo
│   └── media/                     # Imagens, diagramas, vídeos, PDFs
├── graphify-out/                  # Grafo gerado automaticamente
│   ├── graph.html                # Visualização interativa do grafo
│   ├── GRAPH_REPORT.md           # Resumo executivo (SEMPRE comece aqui!)
│   ├── graph.json                # Grafo consultável (JSON)
│   ├── wiki/                     # Wiki gerada automaticamente
│   │   └── index.md              # Índice principal
│   ├── obsidian/                 # Vault do Obsidian (opcional)
│   ├── cache/                    # Cache de processamento (ignorar no git)
│   └── transcripts/              # Transcrições de vídeo/áudio
├── examples/                      # Exemplos de uso
│   └── {case}/
│       ├── raw/
│       ├── graphify-out/
│       └── review.md
├── templates/                     # Templates para novos conteúdos
│   ├── pattern.md
│   ├── practice.md
│   └── tutorial.md
├── .graphifyignore               # Arquivos/pastas a ignorar
├── README.md                     # Este arquivo
└── AGENTS.md                     # Instruções para IAs
```

## 🎯 Como usar como central de navegação

### Fluxo de estudo sugerido

1. **Comece pelo resumo executivo**
   ```bash
   cat graphify-out/GRAPH_REPORT.md
   ```
   - Identifique os "Nós de Deus" (conceitos centrais)
   - Veja as "Conexões Surpreendentes"
   - Anote as "Perguntas Sugeridas"

2. **Explore comunidades**
   - Cada comunidade é um cluster de conceitos relacionados
   - Use `graphify-out/wiki/index.md` para navegar

3. **Faça queries específicas**
   ```bash
   /graphify query "como implementar autenticação JWT?"
   /graphify path "JWT" "Database"
   /graphify explain "OAuth 2.0"
   ```

4. **Visualize o grafo**
   ```bash
   # Abra no navegador
   firefox graphify-out/graph.html
   ```
   - Clique em nós para ver conexões
   - Filtre por comunidade
   - Use a busca para encontrar conceitos

### Integração com ferramentas

**Obsidian:**
```bash
/graphify ./raw --obsidian
# Aponte o Obsidian para graphify-out/obsidian/
```

**MCP Server (para queries automatizadas):**
```bash
~/.graphify-env/bin/python -m graphify.serve graphify-out/graph.json
```

## 📖 Como expandir o conhecimento

### Adicionando conteúdo

1. Crie arquivo em `raw/content/` com seu editor favorido:

**Exemplos:**
```bash
# VS Code
code ~/Atrium_Knowledge/raw/content/meu-padrao.md

# Vim
vim ~/Atrium_Knowledge/raw/content/meu-padrao.md

# Nano
nano ~/Atrium_Knowledge/raw/content/meu-padrao.md
```

2. Adicione o conteúdo desejado (padrões, práticas, tutoriais, docs, etc.)

3. Atualize o grafo:
   /graphify ./raw --update
   ```

### Adicionando práticas

1. Crie arquivo em `raw/practices/`:
   ```bash
   cp templates/practice.md raw/practices/minha-pratica.md
   ```

2. Descreva a prática, contexto e exemplos

3. Atualize o grafo

### Adicionando documentação

1. Cole documentos em `raw/docs/`

2. Pode ser markdown, PDF, código

3. Atualize o grafo

### Adicionando mídia

1. Imagens/diagramas → `raw/media/images/`
2. PDFs → `raw/media/pdfs/`
3. Vídeos → `raw/media/videos/` (transcrição automática!)

## 🔄 Manutenção

### Atualização automática

Instale o hook do git (opcional):
```bash
graphify hook install
```

Agora o grafo se reconstrói automaticamente após cada commit.

### Atualização incremental

Para apenas arquivos alterados:
```bash
/graphify ./raw --update
```

Para apenas arquivos de código (sem custo de LLM):
```bash
/graphify ./raw --mode ast-only
```

### Limpeza

Se quiser reconstruir do zero:
```bash
rm -rf graphify-out/cache/
/graphify ./raw
```

## 🎓 Casos de uso

### Estudo dirigido
```bash
# 1. Veja os nós centrais do tópico
/graphify query "quais são os conceitos principais de [tópico]?"

# 2. Entenda as relações
/graphify query "como [conceito A] se relaciona com [conceito B]?"

# 3. Trace caminhos
/graphify path "[conceito inicial]" "[conceito final]"
```

### Revisão arquitetural
```bash
# Descubra padrões não óbvios
/graphify query "quais padrões conectam X, Y e Z?"

# Encontre decisões arquiteturais
/graphify query "por que [recurso] foi implementado assim?"
```

### Onboarding de novos membros
1. Aponte para `graphify-out/wiki/index.md`
2. Use `GRAPH_REPORT.md` como mapa de navegação
3. Siga as perguntas sugeridas

## 💻 Plataformas suportadas

Este projeto foi projetado para funcionar com múltiplos assistentes de IA:

- ✅ **Claude Code** - `/graphify`
- ✅ **OpenCode** - `/graphify`
- ✅ **Codex** - `$graphify`
- ✅ **Cursor** - `/graphify`
- ✅ **GitHub Copilot CLI** - `/graphify`
- ✅ **Aider** - `/graphify`
- ✅ **Gemini CLI** - `/graphify`
- ✅ **VS Code Copilot Chat** - `/graphify`
- ✅ **OpenClaw** - `/graphify`
- ✅ **Factory Droid** - `/graphify`
- ✅ **Trae** - `/graphify`
- ✅ **Hermes** - `/graphify`
- ✅ **Kiro IDE/CLI** - `/graphify`
- ✅ **Google Antigravity** - `/graphify`

**Nota:** Consulte [PLATFORM_COMPATIBILITY.md](PLATFORM_COMPATIBILITY.md) para detalhes completos de configuração por plataforma.

## 🤖 Integração com IAs

Este projeto já está configurado para funcionar com todas as plataformas listadas acima.

O arquivo `AGENTS.md` contém instruções genéricas que funcionam em qualquer plataforma.

### Comandos úteis com IAs

"Quais são os padrões que influenciam a autenticação?"
→ A IA consulta o grafo primeiro, depois responde com precisão

"Como X se conecta a Y neste projeto?"
→ A IA traça o caminho no grafo, não adivinha

## 📊 Métricas

Após cada execução, o graphify mostra:
- **Redução de tokens**: quanto mais eficiente que ler arquivos crus
- **Conexões descobertas**: quantos relacionamentos não óbvios
- **Confiança média**: qualidade das inferências

## 🔒 Privacidade

- Código: processado localmente via AST (não sai da máquina)
- Documentos: enviados para API do seu assistente IA
- Mídia: imagens via vision API, vídeos transcritos localmente
- Nenhuma telemetria ou analytics

## 🚀 Próximos passos

1. **Primeira execução**: `/graphify ./raw --wiki --obsidian`
2. **Navegação inicial**: leia `graphify-out/GRAPH_REPORT.md`
3. **Adicione conteúdo**: use templates em `templates/`
4. **Explore queries**: experimente o comando `/graphify query`

## 📚 Recursos adicionais

- [graphify GitHub](https://github.com/safishamsi/graphify)
- [graphify Documentação](https://github.com/safishamsi/graphify/blob/master/README.md)
- [NetworkX](https://networkx.org/) - biblioteca de grafos subjacente

---

**Lembre-se:** O poder desta base de conhecimento está nas **conexões**, não apenas no conteúdo. Cada novo arquivo pode revelar relações que você nem sabia que existiam!

🌟 Happy knowledge graphing!
