# Hands-on: Spec-Driven Development com GitHub Copilot + Spec Kit

## Cenário

Você irá construir uma **API de gestão de tarefas (To-Do)** usando:

- **Python + FastAPI** (mínimo necessário)
- **GitHub Copilot** (Chat + sugestões inline)
- **Spec Kit** (fluxo SDD estruturado)

A ideia **não é codar muito** — é aprender o fluxo:

```
Proposta → Spec → Design → Plano → Tasks → Código (via Copilot)
```

## Nota Importante Sobre a Abordagem

Este treinamento usa **SDD em modo hibrido**:

- O repositorio traz um baseline minimo em `.specs/` (ponto de partida comum)
- A turma refina esse baseline com Spec Kit + Copilot durante o hands-on
- O codigo nasce apenas na Etapa 5, guiado pelos artefatos refinados

> Em times reais, esse fluxo reduz ambiguidade, alinha expectativas antes de escrever
> uma linha de código e torna o Copilot muito mais preciso — porque ele recebe contexto,
> não só um pedido vago.

---

## Setup (1 minuto)

**GitHub Codespaces:**
1. Clique em **Code → Codespaces → Create Codespace**
2. Aguarde o ambiente subir
3. Abra o terminal integrado

**Validar ferramentas no Codespace:**
```bash
python --version
specify --help
```

**Se precisar inicializar o Spec Kit manualmente:**
```bash
uvx --from git+https://github.com/github/spec-kit.git specify init . --script sh
```

**Observação:** neste momento você ainda não executa a API, porque o `app/main.py`
será criado na Etapa 5.

**Neste hands-on, vamos conduzir todas as etapas (spec, requisitos, design, tasks, testes e código)
dentro do próprio Codespace para manter o fluxo unificado para toda a turma.**

## Comandos do Spec Kit no Fluxo

Use estes comandos no Copilot Chat durante o hands-on (dentro do Codespace):

1. Definir regras do projeto: `/speckit.constitution`
2. Criar proposta: `/speckit.specify`
3. Refinar ambiguidade: `/speckit.clarify`
4. Validar checklist da spec: `/speckit.checklist`
5. Gerar plano tecnico: `/speckit.plan`
6. Gerar tarefas: `/speckit.tasks`
7. Analisar plano/risco: `/speckit.analyze`
8. Implementar tarefas: `/speckit.implement`

---

## Estrutura do Repositório

```
.specs/
  spec.yaml          ← Proposta do sistema (Etapa 1)
  requirements.md    ← Requisitos funcionais (Etapa 2)
  design.md          ← Design técnico (Etapa 3)
  tasks.md           ← Plano de implementação (Etapa 4)
app/
  main.py            ← Criado somente na Etapa 5
docs/
  copilot-prompts.md ← Prompts prontos para usar com Copilot
```

> Os artefatos em `.specs/` são a "fonte da verdade" do sistema.
> O Copilot usa esses arquivos como contexto para gerar código mais preciso.

## Dinamica do Hands-on (baseline + refinamento)

Neste treinamento, os artefatos em `.specs/` ja trazem requisitos minimos para reduzir
variacao entre alunos. O trabalho da turma e **refinar e detalhar** cada arquivo em sequencia.

Variacoes entre alunos sao esperadas, mas com convergencia nos pontos abaixo:
- mesmo escopo funcional (CRUD simples de tarefas)
- criterios de aceite equivalentes
- endpoints e status HTTP compatveis
- tarefas pequenas e em ordem de implementacao

O que pode variar sem problema:
- escrita dos textos
- nomes internos de secoes/tarefas
- detalhes de mensagens e exemplos

---

## Etapa 1 — Criar a Proposta (`spec.yaml`)

**Objetivo:** Definir o sistema antes de escrever qualquer código.

**O que fazer:**
1. Abra `.specs/spec.yaml`
2. Revise o baseline minimo ja definido
3. Refine descricao, contexto e limites com Copilot Chat
4. Ajuste `author` e `updated_at`

**Copilot Chat — Spec Kit:**
```
/speckit.specify Build a simple Task Manager API for personal tasks.
Users can create, list, update status and delete tasks.
No authentication and no database for this training.
```

**Resultado esperado:** `spec.yaml` refinado, mantendo o baseline comum e alinhando escopo com o grupo.

> **Conexão com o mundo real:** Times de produto e engenharia usam propostas como essa
> para alinhar expectativas antes do sprint. O `spec.yaml` é o contrato inicial.

---

## Etapa 2 — Refinar Requisitos (`requirements.md`)

**Objetivo:** Transformar a proposta em requisitos concretos com critérios de aceite.

**O que fazer:**
1. Abra `.specs/requirements.md`
2. Revise os requisitos minimos ja definidos
3. Detalhe criterios de aceite e edge cases
4. Salve a versao refinada

**Copilot Chat — Spec Kit:**
```
/speckit.clarify Focus on acceptance criteria, error responses and edge cases.
```
```
/speckit.checklist
```

**Resultado esperado:** `requirements.md` refinado ao vivo, com RF e criterios de aceite claros.

> **Conexão com o mundo real:** Requisitos mal definidos são a principal causa de retrabalho.
> O Copilot consegue identificar lacunas que passariam despercebidas em uma revisão humana rápida.

---

## Etapa 3 — Criar o Design Técnico (`design.md`)

**Objetivo:** Decidir como o sistema será construído (endpoints, modelos, estratégia de dados).

**O que fazer:**
1. Abra `.specs/design.md`
2. Revise o design tecnico base
3. Refine endpoints, modelos e tratamento de erro com o grupo

**Copilot Chat — Spec Kit:**
```
/speckit.plan Use Python 3.11 with FastAPI. Keep implementation simple and in-memory.
Define endpoints and data models from the approved requirements.
```

**Resultado esperado:** `design.md` refinado ao vivo, descrevendo exatamente como implementar.

> **Conexão com o mundo real:** O design técnico evita que cada desenvolvedor do time
> tome decisões diferentes. O Copilot gera código mais consistente quando recebe um design claro.

---

## Etapa 4 — Gerar o Plano de Tasks (`tasks.md`)

**Objetivo:** Quebrar o design em tarefas pequenas e executáveis.

**O que fazer:**
1. Abra `.specs/tasks.md`
2. Revise a lista base de tasks
3. Refine ordem, granularidade e criterios de pronto

**Copilot Chat — Spec Kit:**
```
/speckit.tasks
```
```
/speckit.analyze
```

**Resultado esperado:** `tasks.md` refinado durante a sessao, pronto para guiar implementacao incremental.

> **Conexão com o mundo real:** Tasks bem escritas aceleram o code review e facilitam
> o pair programming com o Copilot — você sabe exatamente o que pedir.

---

## Etapa 5 — Implementar com Copilot (criar `app/main.py`)

**Objetivo:** Usar os artefatos de spec como contexto para o Copilot gerar código preciso.

Siga a ordem das tasks em `.specs/tasks.md`. Para cada task:
1. Crie `app/main.py` na TASK-01
2. Use o prompt da task no Copilot Chat
3. Aceite ou ajuste a sugestão
4. Marque a task como `[x]` no `tasks.md`

**Copilot Chat — Spec Kit:**
```
/speckit.implement
```

---

### TASK-01 — Criar `app/main.py` + Health Check

**Prompt:**
```
Create app/main.py with a FastAPI app and a GET / health check endpoint
that returns {"status": "ok"}
```

**Depois da TASK-01, rode a API:**
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Acesse o Swagger UI em: `http://localhost:8000/docs`

---

### TASK-02 — Modelos Pydantic

**Prompt:**
```
Based on .specs/design.md, create Pydantic models for Task, TaskCreate and TaskUpdate in app/main.py
```

**Resultado esperado:**
```python
from pydantic import BaseModel
from typing import Literal
from datetime import datetime

class TaskCreate(BaseModel):
    title: str
    description: str | None = None

class TaskUpdate(BaseModel):
    status: Literal["pending", "in_progress", "done"]

class Task(BaseModel):
    id: str
    title: str
    description: str | None
    status: str
    created_at: datetime
```

---

### TASK-03 — Storage em memória

**Prompt:**
```
Add an in-memory storage list called tasks_db to store task dictionaries in app/main.py
```

---

### TASK-04 — POST /tasks

**Prompt:**
```
Implement POST /tasks endpoint in app/main.py. It should:
- receive a TaskCreate body
- generate a UUID id
- set status to "pending" and created_at to now
- save to tasks_db and return the task with HTTP 201
```

**Teste rápido com curl:**
```bash
curl -X POST http://localhost:8000/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Minha primeira tarefa", "description": "Criada via SDD"}'
```

---

### TASK-05 — GET /tasks

**Prompt:**
```
Implement GET /tasks endpoint in app/main.py that returns all tasks from tasks_db
```

**Teste:**
```bash
curl http://localhost:8000/tasks
```

---

### TASK-06 — PATCH /tasks/{id}

**Prompt:**
```
Implement PATCH /tasks/{id} in app/main.py. Find task by id in tasks_db,
update its status with TaskUpdate. Return 200 or 404.
```

**Teste:**
```bash
curl -X PATCH http://localhost:8000/tasks/{ID} \
  -H "Content-Type: application/json" \
  -d '{"status": "done"}'
```

---

### TASK-07 — DELETE /tasks/{id}

**Prompt:**
```
Implement DELETE /tasks/{id} in app/main.py. Remove task by id from tasks_db.
Return 204 on success, 404 if not found.
```

---

## Etapa 6 — Validar com os Requisitos

**Objetivo:** Confirmar que o código entrega o que foi especificado.

**Prompt Copilot:**
```
@workspace Review app/main.py against the acceptance criteria in .specs/requirements.md
and tell me if any requirement is missing or incorrectly implemented
```

**Resultado esperado:** Copilot compara artefato de spec com código e aponta gaps — sem você precisar fazer isso manualmente.

---

## Resultado Final

Ao concluir, você terá:

| Artefato                   | Propósito                              |
|----------------------------|----------------------------------------|
| `.specs/spec.yaml`         | Proposta e escopo do sistema           |
| `.specs/requirements.md`   | O que o sistema deve fazer             |
| `.specs/design.md`         | Como o sistema será construído         |
| `.specs/tasks.md`          | Plano de execução incremental          |
| `app/main.py`              | API funcional gerada com Copilot       |
| `docs/copilot-prompts.md`  | Prompts reutilizáveis para o time      |

---

## Referências

- [Spec Kit Quickstart](https://github.github.com/spec-kit/quickstart.html)
- [FastAPI Docs](https://fastapi.tiangolo.com)
- [GitHub Copilot Chat](https://docs.github.com/en/copilot/github-copilot-chat)