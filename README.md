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
