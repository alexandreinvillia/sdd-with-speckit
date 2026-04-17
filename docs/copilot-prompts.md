# Copilot Prompts — Task Manager API

> Prompts organizados por etapa do fluxo SDD.
> Use no **Copilot Chat** (`Ctrl+Alt+I`) referenciando os arquivos de spec com `#`.

---

## Etapa 1 — Proposta (spec.yaml)

```
@workspace Revise o baseline em #.specs/spec.yaml e proponha melhorias sem mudar o escopo principal
```

```
Based on #.specs/spec.yaml, refine the proposal text and keep the same core features (health + task CRUD)
```

---

## Etapa 2 — Requisitos (requirements.md)

```
Based on #.specs/spec.yaml and #.specs/requirements.md, refine acceptance criteria and edge cases
without changing the main scope.
```

```
Review #.specs/requirements.md and identify any missing edge cases or acceptance criteria
```

---

## Etapa 3 — Design Técnico (design.md)

```
Based on #.specs/requirements.md and #.specs/design.md, refine the technical design.
Keep endpoints and HTTP status contract stable.
```

```
Based on the design in #.specs/design.md, what are the Pydantic models I need to create?
```

---

## Etapa 4 — Tasks (tasks.md)

```
Based on #.specs/design.md and #.specs/tasks.md, refine task order and granularity.
Each task should remain under 5 minutes.
```

```
I'm working on TASK-04 from #.specs/tasks.md. What exactly do I need to implement?
```

---

## Etapa 5 — Implementação (app/main.py)

### Criar arquivo inicial
```
Create app/main.py with a FastAPI app and a GET / health check endpoint that returns {"status": "ok"}
```

### Modelos Pydantic
```
Based on #.specs/design.md, create Pydantic models for Task, TaskCreate and TaskUpdate in Python
```

### POST /tasks
```
Implement POST /tasks endpoint using FastAPI. It should:
- receive a TaskCreate body (title, optional description)
- generate a UUID id
- set status to "pending"
- set created_at to datetime.now()
- save to tasks_db list
- return the task with HTTP 201
```

### GET /tasks
```
Implement GET /tasks endpoint that returns all tasks from tasks_db as a list
```

### PATCH /tasks/{id}
```
Implement PATCH /tasks/{id} using FastAPI. Find task by id in tasks_db,
update its status field using TaskUpdate model.
Return HTTP 200 with updated task or HTTP 404 if not found.
```

### DELETE /tasks/{id}
```
Implement DELETE /tasks/{id} using FastAPI. Find and remove task by id from tasks_db.
Return HTTP 204 with no body on success, HTTP 404 if not found.
```

---

## Etapa 6 — Testes Manuais

```
Generate curl commands to test all endpoints of a Task Manager FastAPI API running on localhost:8000:
- POST /tasks
- GET /tasks
- PATCH /tasks/{id}
- DELETE /tasks/{id}
```

```
Review #app/main.py against the acceptance criteria in #.specs/requirements.md
and tell me if any requirement is missing or incorrectly implemented
```

---

## Prompts de Revisão Cross-Artefato

```
@workspace Compare #.specs/tasks.md with #app/main.py and tell me which tasks are still not implemented
```

```
@workspace Does the current implementation in #app/main.py match the design defined in #.specs/design.md?
List any discrepancies.
```

```
@workspace Based on all spec files in .specs/, what would be the next feature to add to this API?
```
