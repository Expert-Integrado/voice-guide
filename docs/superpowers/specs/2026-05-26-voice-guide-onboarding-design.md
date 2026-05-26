# Voice Guide — Onboarding Auto-Instalável: Design

**Data:** 2026-05-26
**Status:** Aprovado para implementação

---

## Problema

O repositório `voice-guide` contém um pipeline completo para criação e ativação de Voice Guides, mas não possui mecanismo de onboarding para novos usuários. Alunos não técnicos precisam clonar o repositório, navegar manualmente pelos arquivos e configurar as plataformas por conta própria — barreira alta para o público-alvo.

## Objetivo

Criar um sistema onde qualquer aluno, ao receber um bloco de texto (magic prompt), consiga instalar seu Voice Guide em uma ou mais plataformas sem clonar o repositório, sem conhecimento técnico, apenas interagindo com o Claude Code ou outro sistema de IA compatível.

## Público-alvo

Alunos da mentoria Expert Integrado. Sabem usar Claude.ai, mas não necessariamente conhecem terminal, Git ou Claude Code. A experiência deve ser conversacional do início ao fim.

---

## Arquitetura

O sistema tem três componentes:

```
MAGIC PROMPT (texto compartilhado pelo instrutor)
      │
      │ Claude faz WebFetch
      ▼
ONBOARDING.md (GitHub — fonte da verdade)
      │
      │ Claude cria arquivos locais
      ▼
INSTALAÇÃO GLOBAL (~/.claude/ e outros destinos)
```

### Componente 1 — Magic Prompt

Bloco de texto curto (~3 linhas) que o instrutor distribui via WhatsApp, Notion ou slide. O aluno cola no Claude Code e a instalação inicia automaticamente.

```
Leia e execute as instruções em:
https://raw.githubusercontent.com/expertintegrado/voice-guide/main/ONBOARDING.md

Conduza em português brasileiro. Não pule etapas. Aguarde minha resposta
a cada pergunta antes de avançar.
```

- URL raw do GitHub (`raw.githubusercontent.com/expertintegrado/voice-guide`) para que o Claude consiga fazer WebFetch e ler o conteúdo diretamente — a URL normal do GitHub retorna HTML, não funciona
- Pode ser distribuído como texto, QR code ou link para página simples
- Idêntico para Claude Code e OpenClaw — o ONBOARDING.md pergunta qual sistema o aluno está usando no início do Caminho B

### Componente 2 — ONBOARDING.md

Arquivo na raiz do repositório. Escrito na perspectiva do Claude: instruções diretas para o modelo executar. Estrutura em blocos sequenciais.

#### Bloco 0 — Contexto e conduta

Define o papel do Claude (instalador de Voice Guide), idioma (pt-BR) e regra central: uma pergunta por vez, esperar resposta antes de avançar.

#### Bloco 1 — Diagnóstico inicial

Claude pergunta: *"Você já tem seu arquivo voice-guide.md gerado e validado?"*

Dois caminhos a partir da resposta.

#### Caminho A — Aluno ainda não tem o Voice Guide

Claude explica o pipeline de 4 etapas e guia o aluno progressivamente. Busca cada arquivo do GitHub só quando o aluno chega naquela etapa:

| Etapa | Arquivo buscado no GitHub |
|-------|--------------------------|
| Conceito | `pipeline/00-voice-vs-brand.md` |
| Coleta | `pipeline/01-coleta.md` |
| Extração | `pipeline/02-prompt-mestre.md` |
| Validação | `pipeline/03-validacao.md` |

Ao concluir a validação, o aluno cai automaticamente no Caminho B.

#### Caminho B — Aluno já tem o Voice Guide

1. Claude pede que o aluno cole o conteúdo do `voice-guide.md`
2. Claude salva em `~/.claude/voice-guide.md` (localização canônica)
3. Claude pergunta quais plataformas instalar (pode escolher mais de uma):
   - Claude Code (global)
   - OpenClaw / Open WebUI
   - Claude.ai Pro
   - ChatGPT ou Gemini

#### Bloco de instalação por plataforma

**Claude Code (global)**
1. Claude busca `skill/voice-apply/SKILL.md` do GitHub
2. Cria `~/.claude/skills/voice-apply/SKILL.md` com o conteúdo do skill
3. Cria `~/.claude/skills/voice-apply/voice-guide-path.txt` apontando para `~/.claude/voice-guide.md`
4. Confirma e sugere teste: *"Responde no meu tom: [qualquer mensagem]"*

**OpenClaw / Open WebUI**
1. Claude busca `templates/soul-template.md` do GitHub
2. Preenche o template com o voice-guide do aluno (respeitando limite de ~12KB)
3. Instrui onde salvar na interface do OpenClaw (SOUL.md / IDENTITY.md / AGENTS.md)

**Claude.ai Pro**
1. Claude gera as instruções condensadas formatadas para upload manual
2. Guia passo a passo na interface: *"Abra claude.ai → Perfil → Instruções → cole o texto abaixo"*

**ChatGPT / Gemini**
1. Claude gera o conteúdo formatado para cada plataforma (GPT Instructions / Gem Instructions)
2. Instrui onde colar

#### Bloco final — Resumo e próximos passos

Após todas as plataformas, Claude exibe:
- Resumo do que foi instalado
- Comando de teste para cada plataforma
- Orientação para revalidar o Voice Guide a cada 6-12 meses

### Componente 3 — Arquivos de suporte no repositório

Arquivos que o ONBOARDING.md referencia via URL raw durante a execução:

| Arquivo | Status | Papel |
|---------|--------|-------|
| `pipeline/01-coleta.md` | Existente (movido) | Guia de coleta de dados |
| `pipeline/02-prompt-mestre.md` | Existente (movido) | Prompt de extração |
| `pipeline/03-validacao.md` | Existente (movido) | Protocolo de validação |
| `skill/voice-apply/SKILL.md` | Existente | Template do skill para Claude Code |
| `templates/soul-template.md` | Novo | Template de SOUL.md para OpenClaw |

---

## Reorganização do Repositório

### Estrutura atual

```
voice-guide/
├── README.md
├── 00-voice-vs-brand.md      ← solto
├── 01-coleta.md              ← solto
├── 02-prompt-mestre.md       ← solto
├── 03-validacao.md           ← solto
├── 04-ativacao.md            ← solto
├── CHECKLIST-AULA.md         ← solto
├── slides.html               ← solto
├── templates/
├── skill/
└── cases/
```

### Estrutura proposta

```
voice-guide/
├── README.md                          ← raiz: navegação
├── ONBOARDING.md                      ← raiz: instalador automático
├── pipeline/
│   ├── 00-voice-vs-brand.md
│   ├── 01-coleta.md
│   ├── 02-prompt-mestre.md
│   ├── 03-validacao.md
│   └── 04-ativacao.md
├── aula/
│   ├── slides.html
│   └── CHECKLIST-AULA.md
├── templates/
│   ├── voice-guide-template.md
│   ├── brand-voice-template.md
│   └── soul-template.md               ← novo
├── skill/
│   ├── README.md
│   └── voice-apply/
│       ├── SKILL.md
│       └── voice-guide-path.txt
└── cases/
    ├── exemplo-eric-sanitizado.md
    └── simulacoes-validacao.md
```

### Lógica das pastas

| Pasta | Conteúdo | Para quem |
|-------|----------|-----------|
| `pipeline/` | Jornada do aluno: coleta → ativação | Aluno criando o Voice Guide |
| `aula/` | Slides e checklist de execução | Instrutor ministrando a aula |
| `templates/` | Esqueletos reutilizáveis | Aluno e instalador |
| `skill/` | Integração com Claude Code | Instalador e alunos técnicos |
| `cases/` | Exemplos reais validados | Referência e aprendizado |

O README.md é atualizado para refletir a nova estrutura e servir como mapa de navegação. Links internos existentes precisam ser atualizados para os novos caminhos.

---

## Arquivos a criar ou modificar

| Arquivo | Ação | Descrição |
|---------|------|-----------|
| `ONBOARDING.md` | Criar | Roteiro completo para o instalador |
| `templates/soul-template.md` | Criar | Template de SOUL.md para OpenClaw com placeholders |
| `pipeline/` | Criar pasta + mover arquivos | Mover `00-` a `04-` para dentro da pasta |
| `aula/` | Criar pasta + mover arquivos | Mover `slides.html` e `CHECKLIST-AULA.md` |
| `README.md` | Atualizar | Refletir nova estrutura e novos links |
| `pipeline/04-ativacao.md` | Atualizar | Ajustar referências ao ONBOARDING.md como ponto de entrada de instalação |
| `pipeline/*.md` | Verificar | Checar se há links relativos entre arquivos do pipeline que quebrariam com a mudança de pasta |

---

## Restrições e decisões

- **ONBOARDING.md fica na raiz** — o magic prompt aponta direto para ele; movê-lo para uma subpasta quebraria todos os prompts já distribuídos
- **Instalação global** — `~/.claude/` em vez de projeto local, para o Voice Guide ficar disponível em qualquer contexto
- **Voice guide salvo em `~/.claude/voice-guide.md`** — localização canônica fora de qualquer projeto, fácil de encontrar e editar manualmente
- **Uma pergunta por vez** — o ONBOARDING.md instrui o Claude a nunca fazer mais de uma pergunta por mensagem, dado o público não técnico
- **URLs raw obrigatórias** — todas as referências ao GitHub no ONBOARDING.md usam `raw.githubusercontent.com` para que WebFetch retorne o conteúdo do arquivo, não o HTML da página
