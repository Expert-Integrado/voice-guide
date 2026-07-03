# 02 — Prompt mestre de extração

Esse é o coração do material. Você cola o corpus **já limpo** (dos passos 01 e [01b](01b-higiene.md)) + esse prompt em qualquer IA de fronteira (Claude 4.x, GPT-5, Gemini 2.5) e ela gera o seu Voice Guide estruturado.

> **Antes de continuar:** rode a [higiene de corpus (01b)](01b-higiene.md). Extrair de corpus sujo é o erro nº1 do pipeline — o guide fica bonito e falso.

---

## O achado central (leia antes de montar o prompt)

Depois de rodar o ciclo inteiro de otimização, a lição que mais move a agulha **não é sobre vocabulário**. É esta:

> **LLMs de fronteira, por default, CONCORDAM, VALIDAM e RESOLVEM. Pessoas reais FRICCIONAM.**

Diante de uma tese, uma queixa ou um pedido, o modelo tende a: dar razão, oferecer solução pronta, agradecer, fechar com um CTA gentil. Gente real raramente faz isso. Devolve uma pergunta ("mas você já testou?"), pede evidência ("me manda o print"), rebate com argumento, qualifica antes de abrir o jogo, ou só acusa o recebimento e puxa a própria pauta.

**Concordância lisa e polida é a impressão digital nº1 de texto gerado por IA.** O trabalho central do guide é capturar COMO você fricciona — o "motor" da sua voz. Vocabulário e pontuação são a **superfície** (importam, mas saturam rápido). O motor é o que engana o teste às cegas.

Guarde esta régua: **superfície satura ~9/10; o motor chega a ~6-7/10; o resto é substância** (o miolo factual da conversa) que nenhum guide entrega — vem do contexto vivo. Por isso o prompt abaixo pede explicitamente pra IA mapear o seu **motor retórico**, não só listar palavras.

## Como rodar

1. Abre Claude.ai (recomendado), ChatGPT ou Gemini
2. Cria uma conversa nova
3. Cola TODO o conteúdo do prompt abaixo
4. Anexa os arquivos do corpus (`.txt`) OU cola o conteúdo direto na conversa
5. Aguarda a IA gerar o guide
6. Salva o resultado num arquivo `voice-guide.md`

> **Dica**: rode em modelo com janela de contexto grande (Claude 4.x Sonnet/Opus, Gemini 1.5/2.5 Pro). GPT funciona, mas pode precisar fatiar o corpus em pedaços.

---

## Prompt mestre — versão Voice Guide individual

Copie tudo dentro da caixa abaixo:

```
Você vai me ajudar a criar um VOICE GUIDE empírico — um documento que descreve como EU comunico, baseado em mensagens reais que vou te fornecer.

# Contexto

Quem sou eu (preencha):
- Nome:
- Profissão / papel:
- Empresa (se aplicável):
- Público com quem mais converso:
- O que vou usar esse Voice Guide pra fazer: (ex: agente de IA responder WhatsApp, redigir e-mails comerciais, gerar posts no LinkedIn no meu nome, alimentar automação no n8n, etc)

# O corpus

Estou te fornecendo mensagens minhas em [N] contextos diferentes:
- [Contexto 1, ex: WhatsApp com clientes]
- [Contexto 2, ex: WhatsApp com equipe]
- [Contexto 3, ex: E-mails comerciais]
- [Contexto 4, ex: Transcrição de reunião Zoom]

# Sua tarefa

Analise empiricamente o corpus e produza um VOICE GUIDE em markdown com a estrutura abaixo. Use APENAS o que aparece no material — NÃO invente padrões nem importe clichês genéricos. Quando contar frequência, conte de verdade. Quando der exemplo, use trecho real (pode anonimizar nomes).

## Estrutura obrigatória

### 0. MOTOR da voz (a seção MAIS importante — vem antes de tudo)

Este é o coração do guide. Antes de vocabulário, mapeie COMO eu me movo retoricamente. Vá ao corpus e responda com EVIDÊNCIA, não com suposição:

- **Movimento default**: diante de uma tese/opinião do outro, eu concordo, rebato, peço evidência, devolvo pergunta ou qualifico? Diante de uma queixa, eu valido ("te entendo") ou investigo a premissa e peço o plano? Diante de um pedido, aceito liso ou devolvo uma condição/faixa? Some tudo e me diga: meu default é **DEVOLVER** ou **AFIRMAR**?
- **A fricção MUDA por situação**: por exemplo, queixa de equipe (costumo cobrar plano) vs. queixa de cliente/churn (costumo absorver com reação humana primeiro, investigar depois). Mapeie essas diferenças.
- **Seletor de registro por "stake"**: assunto de rotina/logística → mensagem-telegrama de 1-2 linhas; defesa de posição/conflito → resposta longa (às vezes áudio); devolver a decisão pro outro → pergunta de 1-3 palavras. Descreva o que dispara cada formato.
- **Rituais proibidos** (o que a IA faz por default e eu NÃO faço): agradecer no fecho de toda mensagem, CTA em toda resposta, responder ponto-a-ponto cada item do outro, explicar o porquê da própria pergunta. Aponte quais desses eu evito no corpus.

> Regra de leitura pro modelo: LLM por default concorda/valida/resolve. Meça, no MEU corpus, onde e como eu FRICCIONO em vez disso. Essa seção 0 é o que impede o clone de soar como assistente genérico.

### 1. TL;DR (8-12 linhas)
Resumo das regras MAIS críticas. Cada linha é uma regra única, acionável, baseada em evidência. Inclua qualquer fingerprint forte (palavra/padrão que aparece muito ou muito pouco e é diagnóstico).

### 2. Vocabulário núcleo

#### Palavras-assinatura (USE)
Liste 15-25 termos/expressões com:
- Frequência aproximada no corpus
- O que significam pra mim / função retórica
- Em que contextos aparecem

#### Vocabulário evitado (NÃO USE)
Liste 10-15 termos/expressões que NUNCA aparecem no meu corpus mas seriam o default genérico de uma IA. Use isso como fingerprint reverso.

#### Jargões pessoais e termos técnicos
Termos próprios, nomes de produtos meus, comunidades que frequento, autores que cito.

### 3. Sintaxe e ritmo

Cubra:
- Tamanho MEDIANO de mensagem (chars) — e P75/P90 (as "longas"). Use a MEDIANA, não a média: a média engana porque uma mensagem longa puxa tudo pra cima. A mediana é o que revela como eu escrevo de verdade.
- Porcentagem de mensagens single-line vs multi-line
- Porcentagem que começa com letra MINÚSCULA (não capitaliza o início) — autenticador forte
- Uso de abreviações — em PROPORÇÃO, não 100%/0% (ex: `vc` predomina, mas "você" por extenso ainda aparece)
- Uso de pontuação (reticências `..`, vírgula, ponto, em-dash, exclamação)
- Caixa alta (frequência e função)
- Emojis (quais, frequência, em que contexto)
- Conectores frequentes

#### Autenticadores calibrados (a hierarquia dos "erros")
Meça a imperfeição autêntica, em ORDEM de segurança pra reproduzir:
1. **Minúscula inicial alternada** — o autenticador mais seguro. Não começar a frase com maiúscula.
2. **Letra trocada/duplicada por digitação rápida** (`aidna`, `meljhor`) — erro MECÂNICO de dedo. Autêntico.
3. **Acento pulado** — só raramente, e NUNCA quando muda a palavra (não confundir `está` com `esta`, `é` com `e`).

> Regra dura pro modelo: erro é **tempero raro**, NUNCA gramática errada deliberada. Erro de grafia/concordância de propósito (`ç`→`s`, plural errado) é como uma IA IMAGINA que gente erra — e denuncia o clone na hora. Meça a densidade de typos por contexto (mais no íntimo, menos no profissional, nunca zero), mas descreva SÓ erro de teclado. Nunca instrua erro de português forjado.

### 4. Modulação por contexto

Matriz com TODOS os contextos do corpus. Pra cada um:
- Tom dominante
- Vocativo típico
- Densidade afetiva (alta/média/baixa)
- Marcadores característicos
- Exemplo curto real

### 5. Padrões retóricos nomeados

Cubra como eu:
- ABRO mensagem (openers canônicos)
- FECHO mensagem (closers)
- DISCORDO
- ENSINO / EXPLICO
- DECIDO em público
- PEÇO AÇÃO
- RECONHEÇO ERRO
- VENDO (se aplicável)
- REDIRECIONO conversa

Pra cada padrão, dê 1-2 frases-modelo + 1 exemplo real.

### 6. Few-shots reais (>>> a seção que mais ensina o modelo <<<)

> **Um exemplo real vale mais que 50 regras declarativas.** Pra um LLM, ver uma troca real (mensagem-do-outro → minha-resposta) ensina o padrão de um jeito que nenhuma descrição alcança.

Selecione, do corpus limpo, **2 conversas reais por contexto/relacionamento** (cliente, lead, equipe, network, íntimo — os que existirem). Cada few-shot é um par `mensagem que recebi → resposta que dei`. Escolha exemplos que mostrem o MOTOR em ação (a fricção da seção 0, o registro certo, o vocabulário), não trocas triviais tipo "ok". **Anonimize** nomes de terceiros, valores e telefones, sem descaracterizar o estilo.

### 7. Identidade e valores (postura)

5-10 princípios que aparecem repetidos no corpus. Não é missão de empresa — é como EU me posiciono. Ex: "frontalidade > polidez", "ROI provado > promessa", "auto-ironia > seriedade postural".

### 8. Anti-padrões absolutos

15-25 coisas que eu NUNCA faria, com base no que NÃO aparece no corpus. Cada item é um fingerprint claro de "isso não foi escrito por mim". Inclua obrigatoriamente os fingerprints universais de IA: em-dash (`—`), saudações formais ("Olá", "Espero que esteja bem"), hype ("revolucionário", "game changer", "disruptivo"), concordância lisa, CTA em toda mensagem, texto impecável e todo capitalizado, validação afetiva onde eu friccionaria.

### 9. Como usar este guide (instrução pro modelo)

Checklist de 5-8 passos pra IA aplicar antes de gerar mensagem em meu nome. Priorize: primeiro o MOTOR (seção 0), depois modulação (4), depois superfície (3), depois vocabulário (2).

---

# Regras pra você (modelo) durante a extração

1. Conte de verdade — não chute números. Se citar "X aparece 200x", precisa ter aparecido perto disso.
2. Use trechos reais como exemplo (anonimizando nomes próprios).
3. Se um padrão é forte só em UM contexto, marque "específico de [contexto]".
4. Se houver contradição no corpus (eu falo X num lugar e o oposto noutro), aponte — é provável que seja modulação por contexto, não inconsistência.
5. NÃO importe padrões genéricos de "boa comunicação" — se não tá no meu corpus, não entra.
6. Se algum dado ficou ralo (poucos exemplos), avise no fim na seção "Limitações conhecidas".
7. Priorize o MOTOR (seção 0). Se a única coisa que der pra fazer bem for essa seção + os few-shots (seção 6), já vale mais que um guide cheio de vocabulário sem movimento.
8. Se eu marquei alguma parte do corpus como "áudio transcrito", use SÓ pra informar o motor/registro oral — nunca misture nas estatísticas de comprimento e pontuação (voz falada ≠ voz digitada).

Pronto. Aguarde o corpus.
```

---

## Prompt mestre — variante Brand Voice institucional

Pra Brand Voice, troque a abertura por:

```
Você vai me ajudar a criar um BRAND VOICE GUIDE — documento que descreve como a empresa [NOME] comunica de forma consistente em todos os canais oficiais.

# Contexto

A empresa:
- Nome:
- Setor:
- Tamanho aproximado:
- Público principal:
- Posicionamento (em 1 frase, se já tiver):
- Onde esse Brand Voice vai ser aplicado: (ex: site, posts oficiais, e-mails de campanha, copy de produto, scripts de SAC)

# O corpus

Estou te fornecendo material oficial da empresa:
- [Site / landing pages]
- [Posts em redes sociais oficiais]
- [E-mails de campanha]
- [Apresentação comercial]
- [Outros]

# Sua tarefa

Mesma estrutura do Voice Guide individual, mas adaptada:

[...estrutura idêntica, ajustando seções:]
- Seção 0 (motor): em vez do movimento retórico pessoal, mapeie a POSTURA institucional recorrente (a marca provoca, ensina, tranquiliza, desafia?) — mas continua sendo a seção mais importante.
- Seção 4 (modulação): em vez de "estratos pessoais", organize por CANAIS (site, posts, e-mails, SAC)
- Seção 6 (few-shots): 2 peças reais por canal (um post que representa, um e-mail que representa)
- Seção 7 (identidade): substituir por "promessa da marca + valores expressos no copy"
- Adicionar seção "Termos institucionais oficiais" (nomes de produtos, expressões registradas, taglines)

Resto idêntico.

Aguarde o corpus.
```

---

## Iteração — quando rodar de novo

Você não precisa acertar de primeira. Roda → aplica → testa → ajusta.

**Sinais de que precisa iterar:**
- IA misturou tom de contextos diferentes (vendas + íntimo na mesma msg)
- Palavras-chave suas faltaram no resultado
- Anti-padrões ficaram genéricos ("não use linguagem chula") em vez de específicos
- O guide ficou curto demais (< 150 linhas) — provavelmente faltou material ou prompt foi mal calibrado
- A seção 0 (motor) ficou vaga ("é direto e objetivo") em vez de descrever o movimento concreto — sinal de que a IA não achou a fricção no corpus

**Como pedir iteração:**
Cole o guide gerado de volta no chat, junto com 2-3 exemplos reais que ele errou, e peça: "Refine esses 3 pontos baseado nesses exemplos reais que ficaram fora do padrão."

> A iteração séria acontece DEPOIS da validação (passo 03), que te diz EXATAMENTE onde o guide perde ponto (motor? vocabulário? modulação?). Ataque a dimensão de menor nota primeiro, corrija a CAUSA e não o sintoma, e versione (`v1 → v1.1 → v1.2`) com um changelog do que mudou.

---

## Custo aproximado

| Modelo | Custo da extração |
|---|---|
| Claude.ai (assinatura mensal) | Já incluso no Pro/Max |
| Claude API direto | ~$2-5 por extração (depende do tamanho do corpus) |
| ChatGPT Plus | Já incluso |
| Gemini Advanced | Já incluso |

---

Próximo: [`03-validacao.md`](03-validacao.md) — como saber se ficou bom.
