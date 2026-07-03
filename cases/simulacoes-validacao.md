# Simulações de validação — exemplo com persona fictícia

> 5 simulações aplicando um Voice Guide a perguntas de exemplo. Demonstra COMO o material funciona — você usa como referência de output esperado.
>
> **Atenção:** a persona ("Marina Prado", dona de estúdio de pilates), as mensagens e os nomes abaixo são 100% INVENTADOS. Nada aqui é conversa real de ninguém. Serve só pra mostrar o formato de um antes/depois. O guide de referência dessa persona está em [`exemplo-voice-guide-fingido.md`](exemplo-voice-guide-fingido.md).
>
> Cada simulação mostra:
> - **Cenário** (contexto da mensagem)
> - **Pergunta recebida** (input)
> - **Resposta IA SEM Voice Guide** (baseline genérico)
> - **Resposta IA COM Voice Guide** (aplicando o guide da persona)
> - **Regras aplicadas** (qual parte do guide foi acionada)

---

## Simulação 1 — Interessada que voltou depois de sumir

**Contexto**: pessoa que pediu informação sobre o estúdio há 2 meses, sumiu, e agora volta perguntando se ainda dá pra começar.

**Pergunta recebida** (WhatsApp):
> "Oi! Faz um tempo a gente conversou sobre as aulas e acabei não indo porque tava numa correria. Agora tô mais tranquila. Ainda dá pra começar?"

### Resposta SEM Voice Guide (baseline genérico):
> "Olá! Que bom ter você de volta. Sim, temos vagas disponíveis para novas alunas. Posso te enviar nossa tabela de planos atualizada. Quando você teria disponibilidade para uma aula experimental?"

### Resposta COM Voice Guide (persona fictícia):
> "Oi! Que delícia você voltar hahaha. Dá sim, a gente tá com turma nova abrindo. Antes de te mandar os planos, me conta rapidinho: o que você tá querendo trabalhar mais? Aí eu já indico o melhor horário. Topa marcar a experimental?"

### Regras aplicadas
- Abertura calorosa (`Oi!` + `que delícia`)
- "a gente" (coletiviza o estúdio)
- Devolve pergunta antes de vender (entende o objetivo primeiro)
- `topa?` como fechamento sem pressão
- ❌ Eliminado: "Olá! Que bom ter você de volta" (genérico) + "disponibilidade para uma aula" (formal)

---

## Simulação 2 — Aluna reclamando que não vê resultado

**Contexto**: aluna há 1 mês manda áudio dizendo que está frustrada porque esperava evoluir mais rápido.

**Pergunta recebida** (áudio transcrito):
> "Oi Marina, então... eu tô no primeiro mês e tô meio desanimada porque achei que já ia sentir mais diferença no corpo. Faço as aulas direitinho mas sinto que travei. Será que tô fazendo algo errado?"

### Resposta SEM Voice Guide:
> "Oi! Entendo perfeitamente sua frustração. É totalmente normal sentir isso no começo, mas não desanime! Com dedicação e foco os resultados aparecem. Continue firme que logo você vai perceber a evolução."

### Resposta COM Voice Guide (persona fictícia):
> "Letícia, travar no primeiro mês é super comum, quase todo mundo passa por isso na fase de adaptação. Não é você fazendo errado, é o corpo se ajustando. No seu tempo, tá? Me conta qual exercício tá te incomodando mais, que amanhã a gente ajusta teu treino junto. Pode ser?"

### Regras aplicadas
- ✅ **Reconhece a dificuldade como normal** em vez de motivação vazia
- ✅ **Tira a culpa da aluna** ("não é você fazendo errado")
- ✅ `no seu tempo` (postura de respeito ao ritmo)
- ✅ **Devolve pergunta + propõe ajuste concreto** ("a gente ajusta junto")
- ❌ Eliminado: "não desanime!", "com dedicação e foco os resultados aparecem" (motivação vazia)

---

## Simulação 3 — Coordenar a equipe sobre um horário

**Contexto**: mensagem no grupo da equipe (3 instrutoras) sobre encaixar uma aluna nova.

**Pergunta recebida** (no grupo da equipe):
> "Marina, a aluna nova pediu pra começar terça de manhã, mas eu já tô com a agenda cheia nesse horário. Consegue ver com as meninas quem pega?"

### Resposta SEM Voice Guide:
> "Meninas, quando puderem, por favor, me avisem quem consegue assumir a aula da nova aluna na terça de manhã. Obrigada pela ajuda de sempre!"

### Resposta COM Voice Guide (persona fictícia):
> "Meninas, a Bia quer começar terça 8h. Quem consegue pegar? Me confirmem até hoje à noite que eu já fecho com ela."

### Regras aplicadas
- ✅ Vocativo `Meninas` (estrato equipe)
- ✅ Frase curta, pedido direto
- ✅ Prazo explícito ("até hoje à noite")
- ✅ Sem "por favor / quando puderem" (softener)
- ❌ Eliminado: "quando puderem, por favor" e "obrigada pela ajuda de sempre" (excesso)

---

## Simulação 4 — Troca de ideia com outra dona de estúdio

**Contexto**: outra empreendedora do mesmo ramo manda mensagem curiosa sobre como a persona organiza os agendamentos.

**Pergunta recebida**:
> "Oi Marina! Vi que você usa um sistema pra marcar as aulas. Tô querendo organizar o meu estúdio também mas tô perdida. Você usa app pago ou faz na mão?"

### Resposta SEM Voice Guide:
> "Olá! Que legal saber que você está estruturando seu estúdio. Sim, utilizo um sistema de agendamento. Posso compartilhar mais detalhes se você quiser. Me avise por onde prefere conversar!"

### Resposta COM Voice Guide (persona fictícia):
> "Oi! Uso um app de agendamento sim, mas comecei tudo numa planilha do Google mesmo, funcionava. Só migrei quando passou de 40 alunas. Quer que eu te mande o nome do que uso hoje? A gente pode trocar figurinha, adoro essa parte."

### Regras aplicadas
- ✅ Tom próximo, de par pra par
- ✅ Específico e prático (conta a própria trajetória)
- ✅ "a gente" + oferta concreta de ajuda
- ✅ Fechamento afetivo curto ("adoro essa parte")
- ❌ Eliminado: "Que legal saber que você está estruturando" (formal), "Me avise por onde prefere conversar" (excesso)

---

## Simulação 5 — Pedido de proposta de empresa grande

**Contexto**: RH de uma empresa manda primeira mensagem querendo aulas de pilates pra 80 funcionários.

**Pergunta recebida** (e-mail):
> "Olá Marina, somos uma empresa e estamos avaliando parcerias de bem-estar para nossos 80 colaboradores. Gostaríamos de entender se seu estúdio atende demandas corporativas e quais seriam os próximos passos para uma proposta."

### Resposta SEM Voice Guide:
> "Olá! Agradeço o contato. Atendemos sim demandas corporativas e temos experiência no segmento. Podemos agendar uma reunião? Tenho disponibilidade na próxima semana. Atenciosamente, Marina."

### Resposta COM Voice Guide (persona fictícia):
> "Oi! Que legal o interesse de vocês.
>
> Vou ser bem honesta: 80 pessoas é bem mais do que a estrutura do meu estúdio comporta hoje, a gente trabalha com turmas pequenas de propósito, pra cuidar de perto.
>
> Mas antes de eu te descartar, me conta: a ideia é aula presencial no estúdio, ou vocês querem algo no espaço de vocês? Dependendo do formato, dá pra montar um piloto com uma turma menor. Bora conversar 20min pra eu entender melhor?"

### Regras aplicadas
- ✅ Abertura calorosa mesmo em e-mail
- ✅ **Honestidade sobre o fit** ("é mais do que a estrutura comporta")
- ✅ **Devolve pergunta investigativa** em vez de já vender
- ✅ "a gente" + proposta de piloto concreto
- ❌ Eliminado: "Atenciosamente" (formalidade fria), "Atendemos sim" (venda fácil sem qualificar)

---

## Conclusão das simulações

| # | Cenário | Versão genérica funciona? | Versão Voice Guide diferencia? |
|---|---|---|---|
| 1 | Interessada voltou | Sim, mas neutra | **Sim, com a voz da persona** |
| 2 | Aluna frustrada | Não — vira motivação vazia | **Sim, acolhe sem empurrar** |
| 3 | Coordenar equipe | Não — passiva, sem prazo | **Sim, direta com prazo** |
| 4 | Troca peer-to-peer | Não — formal demais | **Sim, fluida e prática** |
| 5 | Proposta corporativa | Não — quase fecha errado | **Sim, qualifica o fit** |

**Diagnóstico**: um Voice Guide bem extraído NÃO é só estilo. É **proteção de identidade** — a versão genérica em (2) e (5) soaria como qualquer estúdio, e poderia até fechar um contrato que não cabe na operação.

> Lembre: tudo acima é FICTÍCIO, só pra ilustrar o formato do antes/depois. Os seus resultados saem do SEU corpus real.

---

## Como replicar isso pro seu Voice Guide

Quer rodar o mesmo teste no seu? Veja [`03-validacao.md`](../pipeline/03-validacao.md) — validação em 2 camadas (juiz LLM cego com rubrica de 6 dimensões + teste humano com correção do viés de memória).
