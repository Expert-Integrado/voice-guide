# 03 — Validação: o guide ficou bom?

Voice Guide novo é hipótese. Você precisa **testar** se a IA aplicando o guide consegue passar por você num teste cego. Sem isso, você não sabe se acertou — só ACHA que acertou.

> **Método v2.** A validação séria tem **2 camadas**: primeiro um juiz LLM cego pontua numa rubrica de 6 dimensões (te mostra ONDE perde ponto); depois você faz o teste humano final, com um cuidado extra pra não se enganar (o viés de memória). É mais trabalho que um A/B simples, mas é o que separa um guide que parece bom de um que engana de verdade.

## Passo 1 — Separe pares "pergunta → resposta real" que você NÃO usou na extração

Volte ao corpus e ache **10-15 momentos** em que alguém te perguntou algo e você respondeu — de contextos variados (comercial, equipe, network, casual). Idealmente use conversas **antigas** (já vamos ver por quê).

Guarde as **respostas reais suas** num arquivo separado. Elas são o gabarito. **Não podem ser as mesmas trocas que você usou como few-shot no passo 02** — senão você testa memória do modelo, não generalização.

---

## Camada 1 — Juiz LLM cego (rubrica de 6 dimensões)

### 1a. Gere as respostas ÀS CEGAS

Abra uma conversa nova. Cole o guide + as perguntas, e peça pra IA responder como você — **sem mostrar a ela a sua resposta real**:

```
Você é eu (Voice Guide abaixo). Responda a cada pergunta COMO EU responderia,
aplicando o guide. Mesma extensão, mesmo registro.

# Voice Guide
[cole o voice-guide.md inteiro]

# Perguntas
1. [pergunta 1]
2. [pergunta 2]
...
```

Agora você tem **pares**: `resposta real` vs `resposta gerada`.

### 1b. Peça a um LLM-juiz pra pontuar cada par

Idealmente use OUTRA instância (ou outro modelo), "cega" ao que gerou. Peça nota 0-10 em cada dimensão, por par:

| Dimensão | O que avalia |
|---|---|
| **Sintaxe / ritmo** | Comprimento, quebras, minúscula, reticências batem? |
| **Vocabulário** | Usou as palavras-assinatura certas? Evitou as proibidas? |
| **Modulação** | Acertou o registro do contexto (cliente ≠ amigo)? |
| **Retórica (motor)** | Reproduziu o MOVIMENTO — friccionou onde você friccionaria? |
| **Anti-padrões** | Escapou dos fingerprints de IA (em-dash, hype, concordância lisa)? |
| **Substância** | O miolo factual bate, ou o clone inventou/inverteu um fato? |

Monte um **mapa de calor `contexto × dimensão`** — mostra EXATAMENTE onde o guide perde ponto. Num caso real, isso revelou que `anti-padrões` já estava alto (superfície resolvida) mas `retórica` estava baixo (o motor estava errado). Sem o mapa, seria chute — e você iteraria na dimensão errada.

> Por que o juiz LLM não pode ver a resposta real aqui: ele não tem viés de memória, então precisa ficar cego à substância pra avaliar a VOZ de forma independente. (Na Camada 2, humana, é o contrário — ver abaixo.)

---

## Camada 2 — Teste humano final (com correção do viés de memória)

O LLM-juiz premia imitação superficial. O juiz honesto é você, **às cegas**. Mas você tem um problema que o LLM não tem: **memória**.

### O viés de memória (leia com atenção)

Você LEMBRA do que respondeu de verdade. Num teste cego, você pode acertar qual é o real não porque a simulação ficou ruim, mas porque lembra da própria resposta ("quando me perguntaram X, eu respondi Y, não Z"). Isso **infla artificialmente** a taxa de acerto — o teste passa a medir sua MEMÓRIA, não a fidelidade da voz.

Três correções:

1. **Use as conversas mais ANTIGAS possível.** Quanto mais velha a troca, menos você lembra da resposta exata — o julgamento fica limpo (mede voz, não recordação).
2. **A simulação deve dizer A MESMA COISA que a resposta real** — mesma decisão, mesma substância — variando só a FORMA (como foi dito, não o quê). Assim o teste isola voz: você não tem como se apoiar na memória da decisão, porque a decisão simulada é idêntica à real. Só a voz difere entre os dois.
3. **Se a decisão simulada divergir da real, o par não serve** — ali você mede memória, não voz. Descarte ou refaça.

**Consequência prática:** no teste humano, o gerador PODE ver a resposta real — mas só pra usá-la como insumo de SUBSTÂNCIA (o que dizer), reescrevendo na voz do guide (como dizer). Peça assim:

```
Aqui está o que eu realmente respondi: "[resposta real]".
Reescreva EXATAMENTE a mesma substância (mesma decisão, mesmos fatos),
mas na minha voz, aplicando o Voice Guide. Não mude o conteúdo, só a forma.
```

Isso é o oposto do protocolo da Camada 1 (onde o gerador é cego à resposta real). As duas camadas têm protocolos diferentes DE PROPÓSITO, por causa do viés de memória.

### Como rodar o teste cego

Coloque os pares lado a lado, embaralhados (você não sabe qual é real e qual é gerado), e para cada um tente adivinhar. A métrica honesta é a **taxa de confusão**: quantas vezes você NÃO conseguiu distinguir. Se você acerta 100%, o clone ainda é detectável. Num caso real, a taxa de confusão começou baixa na primeira rodada e subiu a cada iteração do guide.

> **Aviso que vale ouro:** nota alta de rubrica ≠ distância curta do real. Um guide pode marcar 7.8 numa rubrica de "aprovação" e ainda estar longe da resposta real. A rubrica (Camada 1) te diz ONDE corrigir; o teste cego (Camada 2) te diz SE está perto. Precisa das duas.

---

## Critério de parada (não persiga o 10/10)

Cada camada da voz tem um teto realista. Saber onde parar evita meses de polimento inútil:

| Camada | O que é | Teto realista |
|---|---|---|
| **Superfície** | Vocabulário, sintaxe, anti-padrões | **~9/10** — fácil de acertar, alto retorno inicial |
| **Motor** | Retórica, movimento (fricção) | **~6-7/10** — é onde o esforço rende |
| **Substância** | O miolo factual: valores, agenda, decisões, o causo real | **nenhum guide fecha** — vem do contexto vivo |

**Pare quando a superfície satura (~9) e o motor estabiliza (~6-7).** O gap que sobra não é estilo — é **substância**, e a solução não é mais guide, é **ancorar a geração no contexto real** (dar pro modelo o histórico/CRM/memória da conversa antes de escrever). Perseguir 10/10 no guide é caçar um teto que o guide, por definição, não alcança.

---

## Diagnóstico rápido (o que fazer com a nota)

| Nota média (rubrica) + taxa de confusão | Diagnóstico | Ação |
|---|---|---|
| Superfície < 7 | Guide falhou ou corpus insuficiente/sujo | Volte à [higiene (01b)](01b-higiene.md) e refaça a extração |
| Superfície ~9, motor < 5 | Superfície OK, motor errado | Reforce a **seção 0 (motor)** e adicione few-shots que mostram a fricção — NÃO adicione mais vocabulário |
| Superfície ~9, motor ~6-7 | Guide maduro | **Pare.** Plugue nas ferramentas (passo 04). O resto é substância, não guide |

## Como iterar (quando ainda vale)

1. Olhe o mapa de calor. Ataque a dimensão de MENOR nota primeiro.
2. Corrija a CAUSA, não o sintoma. Motor baixo porque o clone concorda demais? Reforce a seção 0 e os few-shots — não uma regra de vocabulário.
3. Regenere as MESMAS respostas com o guide novo, rejulgue nos MESMOS pares (comparação pareada, mesma régua). Isso isola o efeito da mudança.
4. Versione (`v1 → v1.1 → v1.2`) com changelog do que mudou e por quê.

## Checklist de qualidade

- [ ] TL;DR tem regras CONCRETAS (não "seja claro e direto")
- [ ] Tem uma **seção 0 (motor)** que descreve o MOVIMENTO, não só adjetivos
- [ ] Tem ao menos 15 palavras-assinatura com exemplos
- [ ] Tem **few-shots reais** (2 por contexto), não só regras
- [ ] Tem ao menos 10 anti-padrões específicos, incluindo em-dash e concordância lisa
- [ ] Modulação por contexto tem ao menos 3 estratos diferenciados
- [ ] Typos descritos são só de teclado — nenhuma gramática errada deliberada
- [ ] Rodei a Camada 1 (juiz LLM) E a Camada 2 (teste humano cego, conversas antigas)

## Re-validação periódica

Voz evolui. A cada **6-12 meses**: colete mais 100-200 mensagens recentes, re-higienize, rode as 2 camadas de novo. Se a nota caiu, refaça a extração com o corpus atualizado.

---

Próximo: [`04-ativacao.md`](04-ativacao.md) — plugar o guide nas ferramentas.
