# 04 — Ativação: como plugar o Voice Guide

Voice Guide só serve se a IA realmente CONSULTAR ele toda vez. **4 ferramentas** principais. Em todas, o mesmo arquivo `voice-guide.md` é a fonte.

> Boa notícia: em dez/2025, **Agent Skills virou padrão aberto** ([agentskills.io](https://agentskills.io)). O mesmo formato roda em Claude.ai, Claude Code e (com pequenos ajustes) em ChatGPT/Codex CLI. Cria 1 vez, usa em todo lugar.

---

## 1. Claude.ai (web)

Skill nativa. Requer plano Pro ou superior.

### Pré-requisito
Antes de subir skills: **Settings → Capabilities → ativar Code Execution e File Creation**.

### Instalação
1. Empacote a skill como ZIP:
   ```
   minha-voz/
     SKILL.md           ← obrigatório (frontmatter + instruções)
     voice-guide.md     ← seu guide
   ```
   Compacte a pasta `minha-voz/` num `.zip` (a pasta tem que estar dentro do ZIP, não só os arquivos)

2. Settings → Customize → Skills → **"+ Create skill"** → Upload do ZIP

3. Skill aparece na lista, toggle pra ativar

### Como dispara
Claude.ai aciona a skill automaticamente quando você pedir algo no escopo dela ("redige uma mensagem", "responde esse cliente"). Custom skills são privadas da sua conta.

### Requisitos do SKILL.md
- Campo `name` no frontmatter deve ser **lowercase**, só letras/números/hífen
- Campo `description` é o que dispara a skill — descreva quando ativar

> Template pronto: ver [`skill/voice-apply/SKILL.md`](../skill/voice-apply/SKILL.md) deste repo.

---

## 2. Claude Code (terminal local)

Duas opções, escolha conforme o uso:

### Opção A — CLAUDE.md global (simples, sempre ativo)
1. Edita `~/.claude/CLAUDE.md` (cria se não existir)
2. Adiciona no final:
   ```markdown
   ## Voice Guide ativo
   Para qualquer texto que você redigir em meu nome (e-mail, mensagem, post),
   consulte e aplique: ~/voice-guide.md
   ```
3. Coloca o `voice-guide.md` em `~/voice-guide.md`
4. Todas as sessões Claude Code carregam o guide

**Trade-off**: guide sempre carregado, mesmo debugando código. Recomendado se você usa Claude Code majoritariamente pra redação.

### Opção B — Skill on-demand (recomendado)
Use a skill `voice-apply` deste repo. Carrega o guide só quando você dispara.

1. Copia `skill/voice-apply/` deste repo pra `~/.claude/skills/`
2. Edita `voice-apply/voice-guide-path.txt` com o path do seu voice guide
3. Sessões novas detectam a skill automaticamente

Em sessão Claude Code, basta dizer:
- "redige no meu tom: [conteúdo]"
- "responde esse cliente como eu falaria"
- "rascunha email pra X"

---

## 3. OpenClaw / Open WebUI (agente 24/7 em servidor)

Se você roda um agente próprio 24/7 num servidor (padrão OpenClaw / Open WebUI), ele geralmente **não usa `CLAUDE.md`** — tem um canone próprio de arquivos na raiz do repo, tipicamente `SOUL.md`, `IDENTITY.md`, `AGENTS.md`, `USER.md`, `TOOLS.md`, `MEMORY.md`.

### Onde plugar o voice guide
O Voice Guide entra no **`SOUL.md`** (carta de identidade do agente) ou é referenciado a partir dele.

### Setup
1. Acesse o repo do seu agente
2. Edita `SOUL.md` adicionando:
   ```markdown
   ## Voice Guide
   Toda comunicação externa (WhatsApp, e-mail, post) que sair em nome do
   [dono] deve aplicar o voice guide abaixo:

   [cole o conteúdo do voice-guide.md aqui — máx ~12KB pra não truncar]
   ```
3. Commit + push pro repo
4. Próxima sessão do agente carrega automaticamente

**Atenção:** OpenClaw trunca silenciosamente arquivos > ~12KB no bootstrap. Se seu voice guide for grande, mantém só TL;DR + anti-padrões críticos no `SOUL.md` e referencia o arquivo completo em `memory/`.

---

## 4. ChatGPT (Custom GPT)

Requer ChatGPT Plus ou superior.

### Setup
1. https://chat.openai.com/gpts/editor → "Create a GPT"
2. **Configure tab** (não Create chat):
   - **Name**: "Voz [seu nome]" / "Voz [empresa]"
   - **Description**: 1 linha curta
   - **Instructions**: cole o conteúdo COMPLETO do voice-guide.md + linha final:
     ```
     Aja como [seu nome]. Aplique este guide em toda resposta. Antes de redigir,
     identifique o contexto (lead, cliente, equipe, parceiro) e aplique a modulação
     correspondente.
     ```
   - **Knowledge**: também faça upload do `voice-guide.md` como arquivo (até 20 arquivos, 512MB cada). Knowledge serve como fonte consultável durante a conversa.
3. Save / Publish (privado pra você ou compartilhado)

### Por que usa Instructions + Knowledge
- **Instructions**: sempre carregado, define personalidade
- **Knowledge**: arquivo referenciável quando o assistente precisar dos detalhes (variações por contexto, exemplos)

Em conversa nova com esse GPT, pede direto: "redige follow-up pra lead X". Aplica voz automaticamente.

---

## 5. Gemini (Gems)

Disponível pra todas as contas Gemini (web + mobile).

### Setup
1. https://gemini.google.com/ → menu lateral → **Gems** → "+ Create new Gem"
2. **Instructions**: cole o conteúdo do `voice-guide.md` + linha:
   ```
   Aja como [seu nome]. Aplique este guide em toda resposta.
   ```
3. **Knowledge**: "Add files" → faça upload do `voice-guide.md`
4. Save

### Knowledge maior
Se seu corpus de referência cresceu (vários exemplos, casos, anti-padrões expandidos), use **NotebookLM** (até 50 sources) como knowledge source primária — conecta no Gem como fonte.

---

## Tabela-resumo

| Ferramenta | Como ativa | Pré-requisito |
|---|---|---|
| **Claude Code** | `~/.claude/CLAUDE.md` ou skill em `~/.claude/skills/` | Claude Code instalado |
| **OpenClaw** | `SOUL.md` (canone do agente, NÃO usa CLAUDE.md) | Agente OpenClaw rodando na VPS |
| **Claude.ai** | Skill (Settings → Customize → Skills) | Pro+ |
| **ChatGPT** | Custom GPT (Instructions + Knowledge) | Plus+ |
| **Gemini** | Gem (Instructions + Knowledge) | Conta Gemini |

---

## Manter sincronizado entre ferramentas

Edita o `voice-guide.md` em **1 lugar**. Replica nas outras:
- Sobe novo ZIP no Claude.ai
- Atualiza Knowledge do Custom GPT
- Re-upload no Gem
- Faz pull se mora num repo git

Voz evolui — re-extraia o guide a cada 6-12 meses (ver [`03-validacao.md`](03-validacao.md)).

---

Próximo passo: pega o [`templates/voice-guide-template.md`](../templates/voice-guide-template.md), começa o seu, e plugue.
