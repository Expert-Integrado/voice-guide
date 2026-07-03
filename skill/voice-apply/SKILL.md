---
name: voice-apply
description: Aplica o Voice Guide pessoal/da marca em qualquer redacao (mensagem, e-mail, post, copy, resposta comercial). Use quando o usuario pedir pra redigir algo em nome dele, da empresa, ou disser "no meu tom", "no tom da marca", "como eu falaria", "responde isso pra mim", "manda uma mensagem", "escreve esse email", "rascunha esse post". Tambem use quando for redigir comunicacao externa sem instrucoes explicitas de tom — assumir que aplicar o Voice Guide e o default.
---

# voice-apply — Skill template

Skill que faz o assistente carregar o Voice Guide do usuario e aplicar em qualquer redacao em nome dele.

## Quando essa skill dispara

Triggers obrigatorios (PT-BR):
- "responde no meu tom"
- "redige no tom da marca"
- "como eu falaria"
- "manda uma mensagem pra X"
- "rascunha email pra X"
- "escreve post sobre X"
- "redige proposta pra X"
- "responde esse cliente"
- "faz follow-up de X"

Triggers obrigatorios (EN):
- "in my voice"
- "as I'd say"
- "draft a message"

Trigger forte: quando estiver redigindo qualquer comunicacao externa em nome do usuario sem ele especificar tom — assumir que aplica.

## O que essa skill faz

1. **Carrega o Voice Guide** do path padrao (ver secao "Configuracao" abaixo)
2. **Identifica contexto** da audiencia (lead, cliente, equipe, parceiro, etc) baseado no que o usuario pediu
3. **Aplica modulacao** da matriz de estrato do guide
4. **Verifica anti-padroes** antes de entregar
5. **Entrega texto pronto** pra copiar e colar (ou enviar via tool)

## Configuracao (1x por instalacao)

Edite o arquivo `voice-guide-path.txt` neste mesmo diretorio com o caminho absoluto pro seu voice guide:

```
C:\caminho\completo\pro\seu\voice-guide.md
```

Linux/Mac:
```
/home/seunome/voice-guide.md
```

Se o arquivo `voice-guide-path.txt` nao existir ou estiver vazio, a skill tenta os fallbacks:
1. `~/.claude/voice-guide.md`
2. `~/voice-guide.md`
3. Mesmo diretorio da skill: `./voice-guide.md`

## Comportamento esperado

Quando a skill ativa:

1. Le o Voice Guide (Read tool no path configurado)
2. Pergunta brevemente o contexto se nao for obvio: "Eh msg de WhatsApp pra cliente atual, lead frio, ou equipe interna?"
3. Redige aplicando todas as regras do guide
4. Mostra o texto final ao usuario
5. Opcionalmente: marca QUAIS regras do guide foram aplicadas (so se usuario pedir "explica o que aplicou")

## Anti-comportamentos

- NAO inventar regras que nao estao no Voice Guide
- NAO suavizar tom quando o guide diz frontalidade
- NAO adicionar saudacoes/fechamentos genericos quando guide proibe
- NAO redigir sem ter lido o guide na sessao corrente
- NAO cair no default de LLM: concordar/validar/resolver com CTA gentil. Se o guide tem uma secao 0 (MOTOR), aplique o movimento dela ANTES de tudo — a pessoa real fricciona (devolve pergunta, pede evidencia, qualifica) onde a IA concorda. Concordancia lisa e o fingerprint nº1 de texto de IA.
- NAO forjar erro de gramatica pra "parecer humano". Autenticidade e so erro de teclado (minuscula inicial, letra trocada), nunca portugues errado de proposito.

## Exemplo de fluxo

**Usuario:** "Responde esse cliente que quer cancelar mentoria: 'Eric, achei que ia ter mais resultados nesse 1o mes...'"

**Skill ativa:**
1. Le voice-guide.md
2. Identifica: estrato cliente, queixa, requer postura frontal (nao validacao afetiva)
3. Redige:
   > "Fala mano. Olha, primeiro mes raramente entrega resultado completo — mentoria de 6 meses tem curva. Mas se vc ta sentindo q nao ta avancando, isso eh real. Posso te ligar amanha pra entender onde travou e ver se vale ajustar plano?"
4. Mostra ao usuario

## Instalacao em diferentes ambientes

### Claude Code

1. Copie a pasta `skill/voice-apply/` pra `~/.claude/skills/`
2. Edite `voice-guide-path.txt` com path do seu guide
3. Em sessao nova, o Claude Code carrega skills automaticamente

### Claude Desktop (com skill plugin)

1. Copie pra `~/Library/Application Support/Claude/skills/voice-apply/` (Mac) ou equivalente Windows
2. Edite path
3. Reinicie Claude Desktop

### Outras IAs (sem suporte a skill nativo)

Use abordagem alternativa: ative o Voice Guide como Project Knowledge / Custom Instructions (ver `04-ativacao.md`).

---

**Versao:** 2.0 (metodo v2 — guide construido com higiene de corpus + motor retorico + few-shots + validacao 2 camadas)
**Compativel com:** Claude Code 1.0+, Claude Desktop com skill plugin
