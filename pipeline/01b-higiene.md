# 01b — Higiene de corpus (a etapa MAIS importante)

> **Método v2.** Se você só tem tempo pra fazer UMA coisa direito neste pipeline, faça esta. Um corpus sujo produz um clone sujo — e ninguém percebe, porque as estatísticas parecem certas.

Coletar material (passo 01) é o começo. Antes de mandar pra IA extrair (passo 02), você precisa **limpar o corpus**: tirar de dentro dele tudo que NÃO é a sua voz digitada espontânea.

## Por que essa etapa existe

Num caso real de otimização, a limpeza revelou que ~4% do material bruto (quase 1.000 mensagens num corpus grande) era **contaminação** que teria distorcido gravemente o guide. Uma "regra" inteira que o guide sujo produzia — um comprimento médio inflado de mensagem — era **artefato de lixo institucional**, não a voz real: a mediana verdadeira era muito menor. Sem a higiene, o guide teria ensinado a IA a escrever de um jeito que a pessoa NUNCA escreveu.

O problema é traiçoeiro: o export "parece" seu (está no seu número, no seu histórico), mas boa parte dele foi escrita por outra coisa — um bot, um funcionário, uma transcrição de áudio, uma IA que você usou pra redigir. Colar isso na extração é clonar o clone.

## As 5 fontes de contaminação (filtre TODAS)

### 1. Transcrições de áudio
Voz **falada** ≠ voz **digitada**. Se você manda áudio e o app/bot transcreve, esse texto entra no export como se fosse digitado — mas tem outra sintaxe (mais longo, mais disfluente, cheio de "né?" e "sabe?"). Isso infla o comprimento médio e enche o guide de marcadores orais que você não digita.

- **Marcadores comuns:** mensagens começando com `*Resumo:*`, `*📊 Resumo:*`, ou blocos longos anormalmente articulados.
- **Nuance importante:** áudio transcrito é ÓTIMA matéria pra entender seu registro ORAL (útil no passo 02, no motor retórico) — mas NÃO pode se misturar com a voz digitada nas estatísticas de comprimento/pontuação. Guarde separado, num arquivo à parte. Isso é a **separação por modalidade** (ver abaixo).

### 2. Mensagens escritas por IA / assistente
Se você já usa IA pra redigir propostas, copy, análises — e cola no chat — esse texto está no seu histórico real, mas NÃO é sua voz de conversa. É documento colado.

- **Impressão digital nº1: em-dash (`—`).** Quase ninguém digita em-dash no celular. Se aparece, quase sempre é texto gerado/colado de IA. Num caso real, o em-dash era literalmente ZERO no histórico antigo e só começou a "vazar" depois que a pessoa passou a usar IA pra redigir textos longos estruturados.
- **Outros sinais:** parágrafos polidos, headers markdown (`#`, `##`), listas com bullets formatados, polidez excessiva ("Fico à disposição", "Agradeço o retorno"), estrutura de documento.
- **Marcadores explícitos:** "Mensagem enviada pelo ChatGPT", templates de outbound colados idênticos.

### 3. Mensagens de OUTROS atendentes no mesmo número
Se o número é um canal de atendimento multi-pessoa (ChatGuru, CRM, SAC), o export atribui TODAS as mensagens ao dono da conta — mas quem digitou foi um funcionário. Num caso real, vários chats inteiros (centenas de mensagens) pareciam ser do dono e eram 100% de outros funcionários assinando `*Nome:*` no corpo. Se o texto tem prefixo de assinatura de terceiro, ou é template institucional, corte o chat inteiro.

### 4. Bots e mensagens automáticas
Resumos automáticos diários, confirmações de agendamento, "Horário de funcionamento", "Atendimento encerrado", disparos de grupo gerados por bot. Num caso real, um bot de "resumo" diário representava quase METADE do volume bruto de um grupo — tudo atribuído ao dono da conta. Filtre por marcadores tipo "Gerado por [nome] IA", horários fixos repetidos, texto idêntico recorrente.

### 5. Ruído estrutural
URLs isoladas, separadores (`____`, `----`), placeholders de mídia (`<Mídia oculta>`, `imagem ocultada`), mensagens de sistema ("Você adicionou...", "As mensagens são criptografadas de ponta a ponta").

## Preferir a janela PRÉ-IA

Se você começou a usar IA pesado em algum momento (ex: fim de 2025), o corpus DEPOIS desse ponto está progressivamente contaminado por texto assistido — mesmo em conversa casual, porque um pedaço já saiu de uma IA.

**Prefira uma janela de tempo ANTERIOR ao uso pesado de IA** pra ter a voz espontânea limpa. Num caso real, a janela pré-IA-pesada foi a referência canônica; o corpus "atual" já estava contaminado por texto assistido e teria retroalimentado o clone.

> Regra prática: se você não lembra a partir de quando passou a redigir com IA, procure o primeiro em-dash do seu histórico. Ele costuma marcar a fronteira.

## Separação por modalidade (voz digitada ≠ voz falada)

São **idiomas diferentes**. Voz digitada é curta, fragmentada, abreviada. Voz falada (áudio transcrito, transcrição de Zoom/live) é longa, disfluente, com muletas orais.

- Se o seu guide vai ser usado pra **texto** (WhatsApp, e-mail, post) — treine **só com texto digitado**. Deixe o áudio transcrito de fora das estatísticas.
- O áudio transcrito continua útil, mas pra outra coisa: entender COMO você raciocina em voz alta (o motor retórico do passo 02). Ele informa o movimento, não a superfície.
- **Nunca** misture os dois no mesmo balde de contagem de caracteres/pontuação. Misturar é o erro nº2 mais comum do pipeline inteiro.

## Como executar a higiene sem código

Você não precisa programar. Depois de colar os `.txt` (ou trechos) na IA, peça:

```
Analise este export de WhatsApp. Liste TODAS as mensagens que provavelmente
NÃO foram digitadas espontaneamente por [meu nome]:
- transcrições de áudio (blocos longos, "né?/sabe?", marcadores de resumo)
- texto que parece redigido por IA (em-dash, headers markdown, polidez de documento)
- mensagens de outros atendentes no mesmo número (assinaturas *Nome:*)
- bots e automações (resumos diários, confirmações, horários fixos)
- ruído estrutural (URLs soltas, <Mídia oculta>, mensagens de sistema)

Para cada uma, diga o marcador que a denuncia. NÃO remova ainda — só liste
pra eu revisar.
```

Revise a lista (a IA erra pros dois lados), confirme, e só então peça o corpus limpo. **A inspeção manual dos casos-limite é obrigatória** — num caso real, TODOS os achados de contaminação mais importantes surgiram na revisão manual, nenhum estava na lista de filtros original.

## Checklist da higiene

- [ ] Removi transcrições de áudio do balde de "voz digitada" (guardei à parte se quero cobrir registro oral)
- [ ] Removi texto redigido por IA (varri em-dash, headers, polidez de documento)
- [ ] Removi mensagens de outros atendentes do mesmo número
- [ ] Removi bots, resumos automáticos e confirmações
- [ ] Removi ruído estrutural (URLs, mídia oculta, mensagens de sistema)
- [ ] Prefiri a janela PRÉ-IA (antes de eu redigir com assistente)
- [ ] Anotei quantas mensagens sobraram por contexto (vai importar no passo 02)

## Saída desta etapa

Um corpus **limpo** — só a sua voz digitada espontânea — separado por contexto, com o áudio transcrito num arquivo à parte. Agora sim está pronto pra extração.

---

Anterior: [`01-coleta.md`](01-coleta.md) · Próximo: [`02-prompt-mestre.md`](02-prompt-mestre.md) — colar o corpus limpo na IA e gerar o guide.
