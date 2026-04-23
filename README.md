# Hands-on: Spec-Driven Development com GitHub Copilot + Spec Kit

## O que é Spec-Driven Development (SDD)?

**SDD é uma abordagem que coloca especificação clara no centro do desenvolvimento.** Em vez de começar com código ou requisitos vagos, você:

1. Define **claramente o que** o sistema deve fazer (especificação)
2. Quebra **como** será implementado (design técnico)
3. Organiza **em que ordem** (tarefas ordenadas)
4. Gera código **guiado por esses artefatos** (implementação consistente)

---

## Por que SDD + GitHub Copilot?

### Benefício 1: Redução de Ambiguidade
- **Sem spec:** Copilot adivinha — endpoints inconsistentes, status HTTP diferentes, nomes de campos variáveis
- **Com spec:** Copilot tem contexto — código consistente, alinhado com decisões técnicas já validadas

### Benefício 2: Velocidade e Qualidade
- **Requisitos claros reduzem retrabalho:** cada desenvolvedor (humano ou IA) entende exatamente o que fazer
- **Código gerado é verificável:** código não só funciona, como atende à spec de forma rastreável

### Benefício 3: Colaboração em Escala
- **Time inteiro fala a mesma linguagem:** especificação é o contrato entre produto, design e engenharia
- **IA aprende as regras do projeto:** Copilot respeita convenções, arquitetura e padrões documentados

---

## O Fluxo SDD

```
ESPECIFICAÇÃO → REQUISITOS → DESIGN → TASKS → CÓDIGO (guiado)
     ↓              ↓           ↓       ↓          ↓
   O que      Validar       Arquitetura   Ordem   IA segue
   mudar?      critérios?    técnica?     lógica?  cada step
```

**Cada etapa reduz ambiguidade:** você não avança até que a etapa anterior esteja clara.

---

## Neste Hands-on

Você vai:
1. Começar com **spec refinada** (não criar do zero)
2. **Refinar requisitos** com Copilot (descobrir gaps)
3. **Quebrar em tasks** (ordem clara de execução)
4. **Gerar código** guiado pela spec (ver Copilot ser preciso)
5. **Validar** que código atende spec (ciclo fechado)

**O resultado:** uma API pronta, código consistente entre todos, e prova viva de que especificação guia IA.

---

## Agenda do Hands-on (40 minutos)

| Etapa | Comando Spec Kit | Tempo | O que acontece |
|-------|------------------|-------|-----------|
| **Setup** | `specify init` + integração | 2 min | Ambiente pronto para Spec Kit |
| **Refinamento** | `/speckit.clarify` | 8 min | Identificar gaps nos requisitos |
| **Tarefas** | `/speckit.tasks` | 5 min | Quebra incrementada e priorizada |
| **Implementação** | `/speckit.implement` | 18 min | Copilot gera código guiado pela spec |
| **Reflexão** | — | 7 min | Validação e fechamento |

---

## Passo 0 — Setup (2 minutos)

**Terminal:**
```bash
specify init . --script sh
specify integration install copilot
```

Isso cria `.specify/`, `.github/prompts/` e ativa os comandos `/speckit.*` no Copilot Chat.

---

## Etapa 1 — Refinar Requisitos (8 minutos)

**No Copilot Chat:**
```
/speckit.clarify Identifique critérios de aceite faltando em #.specs/requirements.md
e casos de borda para endpoints de tarefas.
```

**O que observar:**
- Copilot lê `.specs/spec.yaml` e `.specs/requirements.md` automaticamente
- Aponta gaps que você e a turma talvez tivessem deixado passar
- Você refina o arquivo, Copilot lê a versão nova — **feedback loop rápido**

**Checkpoint:** `.specs/requirements.md` com critérios claros e sem ambiguidade.

---

## Etapa 2 — Validar Tarefas (5 minutos)

**No Copilot Chat:**
```
/speckit.tasks Com base em #.specs/design.md, quebre em tasks pequenas (< 5 min cada).
Cada task deve ter: descrição clara, critério de aceite e prompt sugerido.
```

**O que observar:**
- Task-01: Setup (criar `app/main.py` + health check)
- Task-02: Modelos Pydantic
- Task-03–06: Endpoints (POST, GET, PATCH, DELETE /tasks)
- Task-07: Testes

**Checkpoint:** `.specs/tasks.md` pronto, ordem clara e priorizada.

---

## Etapa 3 — Implementar com Spec Kit (18 minutos)

**No Copilot Chat, para cada task:**
```
/speckit.implement Implemente a TASK-01 em #.specs/tasks.md usando FastAPI.
```

**O que observar:**
- Copilot usa o contexto de `.specs/design.md` — não precisa você explicar tudo
- O código é consistente com a especificação
- Cada task leva ~3–4 min com ajustes
- Você roda para validar: `uvicorn app.main:app --reload`

**Checkpoint:** `app/main.py` funcional com endpoints da spec.

---

## Etapa 4 — Reflexão Final (7 minutos)

**Pergunta chave para a turma:**

> Se eu tivesse pedido ao Copilot "Crie uma API de tarefas" **sem especificação**,
> qual seria a diferença?

**Respostas esperadas:**
- "Ficaria inconsistente entre as pessoas"
- "Copilot teria que adivinhar os status HTTP, os nomes dos campos..."
- "Sem spec, cada um faz de um jeito"

**Ponto central:**
> **SDD não é criar mais documentação. É usar documentação como arma para reduzir ambiguidade — tanto para o time quanto para a IA.**

### Lições-chave
1. **Spec = Contrato:** todos falam a mesma linguagem
2. **IA mais precisa:** Copilot tem contexto, não adivinha
3. **Consistência:** código gerado é alinhado ao design
4. **Velocidade:** menos revisão, mais entrega

---

## Estrutura de Baseline

**O que já vem preenchido no repositório:**
```
.specs/
  spec.yaml          ← Proposta do sistema
  requirements.md    ← Requisitos funcionais + critérios de aceite
  design.md          ← Design técnico (endpoints, modelos)
  tasks.md           ← Plano de execução (será refinado)
app/
  .gitkeep           ← main.py será criado na Etapa 3
docs/
  copilot-prompts.md ← Prompts de referência para instrutor
```

**O que será criado durante o hands-on:**
```
.specify/            ← Criado no Passo 0 (specify init)
.github/
  copilot-instructions.md  ← Integração Copilot
  prompts/           ← Comandos `/speckit.*`
app/
  main.py            ← API criada na Etapa 3
```

---

## Resultado Esperado

Ao concluir, você terá:

✅ Entendido por que **especificação guia IA**  
✅ Vivenciado o fluxo **SDD em ciclo rápido**  
✅ Visto Copilot ser **mais preciso com contexto**  
✅ Gerado uma **API consistente** entre toda a turma  
✅ Validado que **testes passam** contra a spec  

---

## Referências Rápidas

- [Spec Kit Quickstart](https://github.github.com/spec-kit/quickstart.html)
- [FastAPI Docs](https://fastapi.tiangolo.com)
- [GitHub Copilot Chat Docs](https://docs.github.com/en/copilot/github-copilot-chat)

---

## Notas para o Instrutor

- **Tempo é crítico:** use um timer por etapa
- **Não customize muito:** mantenha o baseline comum entre alunos
- **Pausas de reflexão:** após cada etapa, peça feedback
- **Foco em SDD, não em FastAPI:** o código é meio para o fim, não o foco

Os prompts prontos estão em `docs/copilot-prompts.md` para referência rápida.
