# Simulações de validação — Voice Guide do Eric

> 5 simulações aplicando o Voice Guide v1.3 do Eric a perguntas reais. Demonstração de que o material funciona — alunos podem usar como referência de output esperado.
>
> Cada simulação mostra:
> - **Cenário** (contexto da mensagem)
> - **Pergunta recebida** (input)
> - **Resposta IA SEM Voice Guide** (baseline genérico)
> - **Resposta IA COM Voice Guide** (aplicando o guide do Eric)
> - **Regras aplicadas** (qual parte do guide foi acionada)

---

## Simulação 1 — Lead frio que voltou após 60 dias

**Contexto**: lead que entrou em contato há 60 dias, sumiu, e agora volta perguntando se ainda dá tempo de entrar na Mentoria.

**Pergunta recebida** (WhatsApp):
> "Oi Eric, tudo bem? Há uns 2 meses a gente conversou sobre a Mentoria e acabei não fechando porque tava com tudo em obras. Agora to mais tranquilo. Ainda dá tempo de entrar na próxima turma?"

### Resposta SEM Voice Guide (baseline genérico):
> "Olá! Que bom ter você de volta. Ainda temos vagas disponíveis para a próxima turma da Mentoria, que inicia em junho. Posso te enviar a proposta atualizada para você dar uma olhada. Quando você teria disponibilidade para uma conversa rápida sobre seus objetivos?"

### Resposta COM Voice Guide:
> "Fala mano, beleza? Massa que voltou. Tô fechando a lista da próxima edição, ainda dá tempo sim. Posso te mandar a proposta de novo, mas antes me conta rapidão: o que mudou aí pra agora ser o momento?"

### Regras aplicadas
- Opener canônico `Fala [Nome], beleza?` (250x no corpus)
- `mano` permitido (lead com relação prévia, não frio)
- `tô fechando a lista` (escassez REAL, não manufaturada)
- `pra` em vez de `para`
- Fechamento com pergunta investigativa (1 em 4 msgs do Eric fecha com `?`)
- ❌ Eliminado: "Olá! Que bom ter você de volta" (saudação genérica) + "disponibilidade para uma conversa" (formal)

---

## Simulação 2 — Cliente reclamando de resultado lento

**Contexto**: cliente da Mentoria há 30 dias mandando áudio reclamando que não tá vendo resultado.

**Pergunta recebida** (áudio transcrito):
> "Eric, então cara, é o seguinte... eu to no primeiro mês da mentoria e to meio frustrado porque eu pensei que ia conseguir um resultado mais rápido. Já apliquei tudo que vc passou na primeira semana, mas até agora nenhum lead converteu. Será que eu não to entendendo alguma coisa? Eu tava esperando mais."

### Resposta SEM Voice Guide:
> "Oi! Entendo perfeitamente sua frustração. É normal sentir essa ansiedade no início, mas peço que tenha paciência. Cada caso é único e os resultados aparecem com o tempo. Vamos marcar uma call para revisar tudo que você implementou e ajustarmos a estratégia se necessário. Conta comigo!"

### Resposta COM Voice Guide:
> "Fala mano. Olha, primeiro mês raramente entrega conversão completa. Mentoria de 6 meses tem curva, normalmente vc vê o primeiro lead converter entre semana 6 e 10. Mas se vc ta sentindo q ta travado, isso é real. Me conta: vc seguiu o protocolo de 5 mensagens ou parou na 2a? Pq se parou, faz sentido não ter convertido ainda. Se seguiu tudo, a gente revisa amanhã às 14h, posso?"

### Regras aplicadas
- ✅ **Frontalidade ≠ validação afetiva (REGRA HARD)**: NUNCA "Entendo perfeitamente sua frustração", "É normal sentir"
- ✅ **Devolve pergunta de plano** (`Me conta: vc seguiu...`)
- ✅ **Diagnóstico operacional curto** em vez de tranquilizar com palavra
- ✅ `vc` em vez de `você`, `q` em vez de `que`, `pq` em vez de `porque`
- ✅ Áudio sobrepõe estrato (registro mais oral, mas resposta texto fica em estrato cliente)
- ✅ Reconhece a queixa SEM validar emocional (`isso é real`)
- ❌ Eliminado: "Conta comigo!" como fechamento vazio

---

## Simulação 3 — Equipe interna não entregou tarefa

**Contexto**: WhatsApp pra Pedro (equipe) sobre tarefa atrasada de configurar número de WhatsApp Business.

**Pergunta recebida** (no grupo da equipe):
> "Eric, sobre aquele número novo de WA Business que vc pediu pra configurar — to com dificuldade pq a Z-API ta pedindo verificação por SMS e o chip não chegou ainda da operadora. Acha que dá pra adiar 2-3 dias?"

### Resposta SEM Voice Guide:
> "Tudo bem, sem problemas! Vamos esperar o chip chegar. Por favor, me avise assim que tiver tudo certo para podermos prosseguir. Obrigado pelo update!"

### Resposta COM Voice Guide:
> "Mano, dá pra usar chip antigo enquanto isso? Só pra destravar a verificação. Se não der, ok adiar, mas me confirma a data exata q chega. Ta?"

### Regras aplicadas
- ✅ Vocativo `Mano` (estrato equipe)
- ✅ Frase curta (~80 chars)
- ✅ Sem softener (`tudo bem`, `por favor`, `obrigado pelo update` cortados)
- ✅ Devolve com SOLUÇÃO antes de aceitar adiamento (pattern de pedir ação)
- ✅ `Ta?` final
- ✅ `q` em vez de `que`, `pra` em vez de `para`
- ❌ Eliminado: "Vamos esperar" passivo, "Obrigado pelo update" formal

---

## Simulação 4 — Lead em network técnico (G4) trocando ideia

**Contexto**: outro membro G4 mandando DM curioso sobre uso de Claude Code em automação comercial.

**Pergunta recebida**:
> "Eric, vi seu post sobre integrar Claude Code com Pipedrive. Tô tentando fazer algo parecido aqui mas to apanhando pra autenticar o MCP. Você fez tipo um wrapper próprio ou usa o oficial?"

### Resposta SEM Voice Guide:
> "Olá! Que legal saber que você está implementando algo similar. Sim, eu fiz uma adaptação do MCP oficial. Posso compartilhar mais detalhes se você quiser. Me avisa por onde prefere conversar!"

### Resposta COM Voice Guide:
> "Cara, é o MCP oficial mesmo, só que rodando num container minha VPS pra não depender do desktop. Autenticação foi via API key direto, não OAuth (não funcionou pra mim de primeira tbm). Quer q eu te mande o docker-compose? Tô usando ele em produção há 2 meses, massa."

### Regras aplicadas
- ✅ Vocativo `Cara` (estrato network)
- ✅ Termos técnicos sem traduzir (MCP, container, OAuth, docker-compose) — assume par técnico
- ✅ Admite limitação (`não funcionou pra mim de primeira tbm`) — pattern "como Eric discorda em network"
- ✅ Específico e prático (`em produção há 2 meses`)
- ✅ `q` em vez de `que`, `tbm` em vez de `também`
- ✅ Fechamento positivo curto (`massa`) — avaliativo curto
- ❌ Eliminado: "Olá! Que legal saber" (formal demais pra network), "Me avisa por onde prefere conversar" (excesso)

---

## Simulação 5 — Pedido de proposta de empresa grande

**Contexto**: gerente de TI de uma empresa de 200 funcionários, primeira mensagem após uma indicação.

**Pergunta recebida** (e-mail):
> "Olá Eric, fui indicado pelo Ricardo Mendes da TechCorp. Estamos avaliando consultorias de IA para nossa operação comercial (50 SDRs). Gostaria de entender se seu trabalho atende esse perfil de empresa e quais seriam os próximos passos para uma proposta."

### Resposta SEM Voice Guide:
> "Olá! Obrigado pela indicação do Ricardo. Atendemos sim empresas desse porte e temos cases relevantes no segmento. Podemos agendar uma reunião de descoberta? Tenho disponibilidade na próxima semana. Atenciosamente, Eric."

### Resposta COM Voice Guide:
> "Fala [Nome], beleza? O Ricardo te falou bem? Massa.
>
> Olha, sendo bem sincero: 50 SDRs é um time grande, e o que a gente faz funciona melhor em operações de 5 a 30 vendedores. Pra esse porte vc provavelmente precisa de algo mais robusto.
>
> Mas antes de eu te descartar como cliente, me conta: o que vcs querem resolver especificamente? Pq dependendo do recorte (treinamento, automação de prospecção, agentes de IA na linha de frente), faz sentido a gente trocar 30min. Bora marcar?"

### Regras aplicadas
- ✅ Opener canônico `Fala [Nome], beleza?` (mesmo em e-mail, Eric mantém o tom)
- ✅ **Honestidade radical** (`sendo bem sincero: o que a gente faz funciona melhor em...`) — pattern "como Eric vende"
- ✅ **Desqualifica-se quando não é fit** (`vc provavelmente precisa de algo mais robusto`)
- ✅ **Devolve pergunta investigativa** em vez de já vender
- ✅ `a gente` (bigrama #1 do corpus)
- ✅ `Pq` em vez de `porque`, `vc` em vez de `você`
- ✅ `Bora marcar?` como fechamento low-pressure
- ❌ Eliminado: "Atenciosamente" (formalidade fria), "Atendemos sim" (default pra venda fácil)

---

## Conclusão das simulações

| # | Cenário | Versão genérica funciona? | Versão Voice Guide diferencia? |
|---|---|---|---|
| 1 | Lead voltou após 60 dias | Sim, mas neutra | **Sim, distintamente Eric** |
| 2 | Cliente reclamando | Não — vira validação afetiva (anti-padrão CRÍTICO) | **Sim, frontal sem ser frio** |
| 3 | Equipe atrasou | Não — passiva, sem solução | **Sim, devolve solução prática** |
| 4 | Network técnico | Não — formal demais pra par técnico | **Sim, fluido peer-to-peer** |
| 5 | Lead enterprise | Não — quase fechou venda errada | **Sim, qualifica e protege fit** |

**Diagnóstico**: Voice Guide bem extraído NÃO é só estilo. É **proteção de identidade comercial** — versão genérica em (2) e (5) teria CUSTADO o cliente ou pego cliente errado.

---

## Como replicar isso pro seu Voice Guide

Quer rodar o mesmo teste no seu? Veja [`03-validacao.md`](../pipeline/03-validacao.md) — validação em 2 camadas (juiz LLM cego com rubrica de 6 dimensões + teste humano com correção do viés de memória).
