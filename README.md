# Voice Guide 2.0 — Material da aula

Open source, criado por **Eric Luciano** na **Mentoria Automações Inteligentes** (Expert Integrado).

> **Entenda a arquitetura:** https://voice-guide.ericluciano.com.br

Como criar um Voice Guide próprio (ou da sua empresa) pra fazer IA falar como você (ou como a sua marca) em qualquer canal: Claude, ChatGPT, Gemini, automações no n8n/Zapier, e-mail, WhatsApp, LinkedIn.

---

## Instalação automática (recomendado)

Você não precisa clonar este repositório. Cole o texto abaixo no **Claude Code** — ele guia tudo:

```
Leia e execute as instruções em:
https://raw.githubusercontent.com/expertintegrado/voice-guide/main/ONBOARDING.md

Conduza em português brasileiro. Não pule etapas. Aguarde minha resposta
a cada pergunta antes de avançar.
```

O instalador detecta automaticamente se você já tem um Voice Guide ou ainda precisa criar um, e configura tudo globalmente no seu sistema.

> **Tem o WhatsApp Agent?** Se a sua sessão do Claude tiver as tools do WhatsApp Agent, o instalador puxa o corpus direto das suas conversas (só leitura, com sua permissão) em vez de você exportar conversa na mão — mais rápido e completo. E, depois de pronto, o Agent passa a **aplicar o seu Voice Guide automaticamente** em toda mensagem que a IA enviar no seu nome, com checagem de fingerprints. Não tem? O caminho manual funciona igual.

> **Voice Guide 2.0** (validado num ciclo real de otimização): o pipeline agora tem uma etapa explícita de **higiene de corpus** (a mais importante — tira do material o que não é a sua voz), captura o seu **motor retórico** (como você fricciona em vez de concordar, que é o que engana o teste às cegas), usa **exemplos reais** em vez de só regras, e valida em **2 camadas** (juiz LLM cego + teste humano com correção do viés de memória). Detalhes em `pipeline/`.

---

## Instalação manual da skill (macOS, Linux e Windows)

A instalação automática acima funciona igual nos três sistemas — o Claude Code cria os arquivos no lugar certo pra você. Esta seção é pra quem prefere instalar **na mão** ou entender exatamente onde cada arquivo vai parar.

### Pré-requisitos (todos os sistemas)

- **Claude Code CLI** instalado e autenticado (`claude`). Versão **1.0 ou superior** (skills são suportadas desde a 1.0).
  - Verifique com `claude --version`. Para instalar/atualizar, siga a [documentação oficial do Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview).
- Um arquivo **`voice-guide.md`** já pronto (gerado pelo pipeline em `pipeline/`). Se ainda não tem, use a instalação automática — ela cria o guide do zero.
- **`git`** (opcional) apenas se você for clonar este repositório em vez de copiar os arquivos da skill à mão.

### Onde ficam os arquivos (path da pasta de config por OS)

O Claude Code guarda a configuração do usuário na pasta `~/.claude`. O que muda entre sistemas é como o `~` (home) é resolvido:

| Sistema | Pasta de config do Claude Code | Skill instalada em |
|---|---|---|
| **macOS** | `~/.claude` → `/Users/SEU_USUARIO/.claude` | `~/.claude/skills/voice-apply/` |
| **Linux** | `~/.claude` → `/home/SEU_USUARIO/.claude` | `~/.claude/skills/voice-apply/` |
| **Windows** | `%USERPROFILE%\.claude` → `C:\Users\SEU_USUARIO\.claude` | `%USERPROFILE%\.claude\skills\voice-apply\` |

No macOS e no Linux o caminho é idêntico (`~/.claude/...`). No Windows, o equivalente de `~` é `%USERPROFILE%` (normalmente `C:\Users\SEU_USUARIO`), e o separador de pasta é `\` em vez de `/`.

> **Dica (Windows):** se você usa o Claude Code dentro do **WSL** (Windows Subsystem for Linux), siga as instruções de **Linux** — dentro do WSL o `~` é o home do Linux (`/home/SEU_USUARIO`), não o `C:\Users`.

### Passo a passo

A skill é composta por dois arquivos que ficam em `skills/voice-apply/` dentro da sua pasta `.claude`:

- `SKILL.md` — a definição da skill (copie de [`skill/voice-apply/SKILL.md`](skill/voice-apply/SKILL.md)).
- `voice-guide-path.txt` — uma linha com o **caminho absoluto** do seu `voice-guide.md`.

Além disso, coloque o seu `voice-guide.md` num lugar fixo (o padrão é a raiz da pasta `.claude`).

#### macOS / Linux

```bash
# 1. Crie a pasta da skill
mkdir -p ~/.claude/skills/voice-apply

# 2. Coloque seu guide no lugar padrão
cp /caminho/para/seu/voice-guide.md ~/.claude/voice-guide.md

# 3. Copie a definição da skill (deste repositório, ou baixe direto)
cp skill/voice-apply/SKILL.md ~/.claude/skills/voice-apply/SKILL.md
#   (sem o repo clonado, baixe direto:)
#   curl -fsSL https://raw.githubusercontent.com/expertintegrado/voice-guide/main/skill/voice-apply/SKILL.md \
#     -o ~/.claude/skills/voice-apply/SKILL.md

# 4. Aponte a skill para o seu guide (caminho absoluto)
echo "$HOME/.claude/voice-guide.md" > ~/.claude/skills/voice-apply/voice-guide-path.txt
```

#### Windows (PowerShell)

```powershell
# 1. Crie a pasta da skill
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\voice-apply" | Out-Null

# 2. Coloque seu guide no lugar padrão
Copy-Item "C:\caminho\para\seu\voice-guide.md" "$env:USERPROFILE\.claude\voice-guide.md"

# 3. Baixe a definição da skill
Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/expertintegrado/voice-guide/main/skill/voice-apply/SKILL.md" `
  -OutFile "$env:USERPROFILE\.claude\skills\voice-apply\SKILL.md"

# 4. Aponte a skill para o seu guide (caminho absoluto do Windows)
Set-Content -Path "$env:USERPROFILE\.claude\skills\voice-apply\voice-guide-path.txt" `
  -Value "$env:USERPROFILE\.claude\voice-guide.md"
```

> **Conteúdo do `voice-guide-path.txt`:** é uma única linha com o caminho absoluto do seu guide.
> No macOS/Linux: `/Users/SEU_USUARIO/.claude/voice-guide.md` ou `/home/SEU_USUARIO/.claude/voice-guide.md`.
> No Windows: `C:\Users\SEU_USUARIO\.claude\voice-guide.md`.
> Se esse arquivo faltar ou estiver vazio, a skill tenta os fallbacks nesta ordem: `~/.claude/voice-guide.md`, depois `~/voice-guide.md`, depois `./voice-guide.md` (a própria pasta da skill).

### Ativar e testar

1. **Feche e reabra o Claude Code** — skills são carregadas no início de cada sessão.
2. Rode `claude` na pasta de qualquer projeto (a skill é global; vale em todos).
3. Teste com: `Responde no meu tom: [qualquer mensagem]`. A skill `voice-apply` deve disparar, ler seu Voice Guide e redigir aplicando as suas regras.

> **Claude Desktop (com plugin de skills):** a pasta muda. No macOS é `~/Library/Application Support/Claude/skills/voice-apply/`; no Windows, `%APPDATA%\Claude\skills\voice-apply\` (`C:\Users\SEU_USUARIO\AppData\Roaming\Claude\skills\voice-apply\`). Depois de copiar, **reinicie o Claude Desktop**.

---

## Por que isso importa

CEO, especialista, dono de empresa, produtor de conteúdo: você não escala 1:1. A sua **voz** precisa escalar. Hoje, com IA, dá pra documentar o seu jeito de comunicar (léxico, ritmo, anti-padrões) e fazer o modelo simular isso de forma consistente — em vez de cada agente, automação ou copywriter inventar do zero e desalinhar.

Voice Guide é o documento que faz esse trabalho.

---

## Estrutura do repositório

| Pasta | Conteúdo | Para quem |
|-------|----------|-----------|
| [`pipeline/`](pipeline/) | Jornada completa: conceito → coleta → **higiene** → extração → validação → ativação | Aluno criando o guide |
| [`aula/`](aula/) | Slides e checklist de execução | Instrutor |
| [`templates/`](templates/) | Esqueletos prontos para Voice Guide e Brand Voice | Aluno e instalador |
| [`skill/`](skill/) | Skill para Claude Code (instalado automaticamente via onboarding) | Claude Code |
| [`cases/`](cases/) | Exemplo completo com persona fictícia | Referência |

---

## Navegação manual (para quem prefere ler na ordem)

| # | Arquivo | Pra que serve |
|---|---|---|
| 0 | [`pipeline/00-voice-vs-brand.md`](pipeline/00-voice-vs-brand.md) | Entender a diferença Voice Guide × Brand Voice |
| 1 | [`pipeline/01-coleta.md`](pipeline/01-coleta.md) | Como coletar o material bruto (WhatsApp, Zoom, e-mail, posts) |
| 1b | [`pipeline/01b-higiene.md`](pipeline/01b-higiene.md) | **A etapa mais importante**: limpar o corpus (5 contaminações + janela pré-IA + separação por modalidade) |
| 2 | [`pipeline/02-prompt-mestre.md`](pipeline/02-prompt-mestre.md) | **O coração**: prompt pronto que gera o guide, com motor retórico + few-shots reais |
| 3 | [`pipeline/03-validacao.md`](pipeline/03-validacao.md) | Validação em 2 camadas (juiz LLM cego + teste humano) + critério de parada |
| 4 | [`pipeline/04-ativacao.md`](pipeline/04-ativacao.md) | Como plugar o guide em Claude, ChatGPT, Gemini, automações |

## Templates prontos

- [`templates/voice-guide-template.md`](templates/voice-guide-template.md) — esqueleto pessoal
- [`templates/brand-voice-template.md`](templates/brand-voice-template.md) — esqueleto institucional

## Exemplo de referência (persona fictícia)

- [`cases/exemplo-voice-guide-fingido.md`](cases/exemplo-voice-guide-fingido.md) — Voice Guide completo de uma persona inventada, pra você ver como fica um guide maduro (nenhum dado real de ninguém)
- [`cases/simulacoes-validacao.md`](cases/simulacoes-validacao.md) — 5 simulações antes/depois aplicando esse guide de exemplo

---

## Glossário rápido

- **Voice Guide**: documento que descreve como UMA PESSOA comunica (fingerprint individual)
- **Brand Voice**: documento que descreve como UMA MARCA/EMPRESA comunica (identidade institucional)
- **Estrato**: contexto de audiência (lead frio, cliente, equipe, parceiro técnico, pessoal) — o tom muda em cada um
- **Anti-padrão**: coisa que você NUNCA fala, fingerprint claro de "isso não foi eu/minha marca"
- **Corpus**: o conjunto de mensagens/textos coletados que vai virar matéria-prima do guide
- **Higiene de corpus**: limpar o material antes de extrair — tirar transcrição de áudio, texto de IA, mensagens de outros atendentes, bots e ruído. A etapa mais decisiva do pipeline
- **Motor retórico**: COMO a pessoa reage a uma tese/queixa/pedido (fricciona, devolve, qualifica) — vale mais que vocabulário, porque LLM por default concorda e a pessoa real fricciona
- **Few-shot**: exemplo real de conversa (mensagem recebida → resposta dada) colado no guide. Ensina o modelo melhor que 50 regras declarativas
- **Viés de memória**: no teste humano, você lembra do que respondeu de verdade e acerta por memória, não por detectar o clone — corrige-se usando conversas antigas e mantendo a substância idêntica entre real e simulado
