# Checklist da aula — leia ao acordar

> Documento de handoff. Aula de 20min sobre Voice Guide + Brand Voice, mentoria.

## O que foi feito

### Repo publicado
- **URL:** https://github.com/expertintegrado/voice-guide (público)
- **Local:** `C:\repos\voice-guide-aula\`
- **Branch:** `main`
- **Commit:** `feat: material inicial da aula Voice Guide + Brand Voice` (26c4e3c)

### Conteúdo entregue

| Arquivo | Pra que serve | Status |
|---|---|---|
| `README.md` | Mapa do repo, ordem de leitura | ✅ |
| `00-voice-vs-brand.md` | Diferença didática Voice × Brand | ✅ |
| `01-coleta.md` | Como coletar material (WhatsApp/Zoom/e-mail) | ✅ |
| `01b-higiene.md` | **Método v2** — higiene de corpus (5 contaminações + janela pré-IA + separação por modalidade) | ✅ |
| `02-prompt-mestre.md` | **O coração** — prompt pronto pra colar no Claude/GPT (agora com motor retórico + few-shots) | ✅ |
| `03-validacao.md` | Validação em 2 camadas (juiz LLM + teste humano com viés de memória) + critério de parada | ✅ |
| `04-ativacao.md` | Como plugar em Claude.ai/Code/ChatGPT/Gemini/n8n | ✅ |
| `templates/voice-guide-template.md` | Esqueleto pessoal | ✅ |
| `templates/brand-voice-template.md` | Esqueleto institucional | ✅ |
| `skill/voice-apply/SKILL.md` | Skill opcional pra Claude Code | ✅ |
| `cases/exemplo-voice-guide-fingido.md` | Voice Guide completo de persona fictícia (exemplo de referência) | ✅ |
| `cases/simulacoes-validacao.md` | 5 simulações antes/depois com a persona fictícia | ✅ |
| `slides.html` | 9 slides reveal.js dark mode | ✅ |

## Como rodar a aula amanhã

### Pré-aula (5min antes)
1. Abre os slides:
   - **Opção A** (mais simples): roda local —
     ```
     cd C:\repos\voice-guide-aula
     python -m http.server 8000 --directory .
     ```
     Abre `http://127.0.0.1:8000/slides.html` no browser
   - **Opção B** (alternativa): salva `slides.html` na pasta `Eventos/` do educacional submodule e abre direto pelo arquivo
2. Abre tela cheia (`F` no reveal.js)
3. Tem o link pronto: `github.com/expertintegrado/voice-guide` (mostra no slide final)

### Durante a aula (20min)
- Slide 1 (cover) — 30s
- Slide 2 (Voice × Brand) — 2min, ponto-chave: empresa solo colapsa em 1 só
- Slide 3 (Por que importa) — 2min, "CEO não escala, mensagem sim"
- Slide 4 (Anatomia) — 3min, mostrar os 6 componentes
- Slide 5 (Pipeline — método v2: coleta → higiene → extração → validação 2 camadas) — 3min. Ênfase: a higiene é a etapa que quase todo mundo pula e é a mais importante
- Slide 6 (Onde plugar) — 2min, ênfase: voice guide é UNIVERSAL
- Slide 7 (Demo antes/depois) — 3min, leia os 2 textos em voz alta, compara
- Slide 8 (Lição de casa) — 3min, mostra o link, pede que clonem
- Slide 9 (Bora?) — 2min Q&A
- **Total: ~20min**

### Pós-aula
- Manda o link no grupo da mentoria: `github.com/expertintegrado/voice-guide`
- Pede que tragam o Voice Guide v0.1 na próxima mentoria

## Troubleshooting

### Servidor python já em uso (8765 ocupado)
Já testei e tem outro python rodando na 8765. **Use 8000 ou outra porta** que comando acima usa.

### Slides não abrem
Verifique se está na pasta correta:
```
cd C:\repos\voice-guide-aula
ls slides.html  # deve listar o arquivo
```

### Reveal.js não carrega (sem internet)
Slides puxam CDN. Se for projetar offline, baixa o reveal.js pra `lib/` local e ajusta os `<link>` e `<script>` no HTML.

### Aluno pergunta "preciso de MCP ou infra especial?"
**NÃO.** Material foi construído pra rodar 100% via Claude.ai (ou ChatGPT/Gemini). Ninguém precisa de MCP nenhum — alunos rodam o prompt mestre direto na IA.

## Pontos pra você revisar antes da aula

1. **Abre o `slides.html` agora e passa pelos 9 slides em ~2min.** Testa se tela está ok pro projetor que você vai usar.
2. **Lê o `cases/simulacoes-validacao.md`** — 5 minutos. São os exemplos que você pode citar se aluno pedir "mostra mais um caso".
3. **Revisa o `cases/exemplo-voice-guide-fingido.md`** — é a persona fictícia (Marina, estúdio de pilates). Confirma que o exemplo ilustra bem o formato de um guide completo. Nenhum dado real de ninguém entra aqui.

## O que tá pendente (você decide se faz)

1. **Identidade visual**: paleta atual é `#FFB200` accent + preto. Se quiser ajustar pra teu padrão Expert Integrado, edita o `<style>` no início do `slides.html` (variáveis CSS `--accent`).
2. **Speaker notes**: slides não têm notas pro apresentador. Se quiser, abre `?print-pdf` no URL e tem notas embaixo. Posso adicionar amanhã se pedir.
3. **PDF export**: pra mandar pros alunos como suplemento — abre `slides.html?print-pdf`, imprime como PDF.
4. **README do submodule educacional**: se quiser que esse repo apareça no submodule `educacional/`, basta linkar no README do educacional.

## Links rápidos pra abrir manhã

- Repo: https://github.com/expertintegrado/voice-guide
- Slides (local): `slides.html` na raiz do repo

---

**Validado em:** slides renderizam corretamente, conteúdo revisado, links cruzados batem, 5 simulações com a persona fictícia documentadas

Bom dia. Bora?
