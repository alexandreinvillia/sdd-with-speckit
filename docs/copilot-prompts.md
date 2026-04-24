# Copilot Prompts — Spec-Driven Development

> Prompts organizados para o fluxo reduzido do hands-on.
> Use no Copilot Chat (Ctrl+Alt+I) referenciando os artefatos de spec com #.

---

## Passo 0 — Setup do Spec Kit

```bash
specify init . --script sh
specify integration install copilot
```

---

## Etapa 1 — Refinar Requisitos (requirements.md)

```
/speckit.clarify Identifique critérios de aceite faltando em #.specs/requirements.md
e casos de borda para endpoints de tarefas.
```

```
Com base em #.specs/spec.yaml e #.specs/requirements.md, refine critérios de aceite,
respostas de erro e regras de validação sem alterar o escopo principal.
```

```
Revise #.specs/requirements.md e liste ambiguidades que possam causar implementação inconsistente.
```

---

## Etapa 2 — Refinar Tasks (tasks.md)

```
/speckit.tasks Com base em #.specs/design.md, quebre em tasks pequenas,
com critério de pronto e ordem de implementação.
```

```
Com base em #.specs/design.md e #.specs/tasks.md, refine a ordem e granularidade das tasks.
```

```
Estou trabalhando na TASK-04 em #.specs/tasks.md.
Descreva exatamente o que implementar, critérios de aceite e como validar rapidamente.
```

---

## Etapa 3 — Implementação Guiada (app/main.py)

```
/speckit.implement Implemente a próxima task pendente em #.specs/tasks.md
usando #.specs/design.md como fonte de verdade.
```

### TASK-01 — Health Check
```
Crie app/main.py com uma aplicação FastAPI e um endpoint GET / de health check
que retorne {"status": "ok"}.
```

### TASK-02 — Modelos
```
Com base em #.specs/design.md, crie os modelos Pydantic Task, TaskCreate e TaskUpdate em app/main.py.
```

### TASK-03 — Storage
```
Adicione uma lista em memória chamada tasks_db para armazenar tarefas em app/main.py.
```

### TASK-04 — POST /tasks
```
Implemente o endpoint POST /tasks em app/main.py com body TaskCreate, id UUID,
status inicial pending, created_at atual e retorno HTTP 201.
```

### TASK-05 — GET /tasks
```
Implemente GET /tasks em app/main.py retornando todas as tarefas de tasks_db.
```

### TASK-06 — PATCH /tasks/{id}
```
Implemente PATCH /tasks/{id} em app/main.py para atualizar status via TaskUpdate.
Retorne 200 com tarefa atualizada ou 404 se não encontrar.
```

### TASK-07 — DELETE /tasks/{id}
```
Implemente DELETE /tasks/{id} em app/main.py.
Retorne 204 sem body em sucesso e 404 se a tarefa não existir.
```

---

## Etapa 4 — Validação e Revisão

```
Gere comandos curl para validar todos os endpoints da API em localhost:8000:
GET /, POST /tasks, GET /tasks, PATCH /tasks/{id}, DELETE /tasks/{id}.
```

```
Revise #app/main.py com base em #.specs/requirements.md e aponte requisitos faltantes,
incorretos ou parcialmente implementados.
```

```
@workspace Compare #.specs/tasks.md com #app/main.py e liste quais tasks ainda estão pendentes.
```

```
@workspace A implementação em #app/main.py corresponde ao design em #.specs/design.md?
Liste divergências objetivas.
```
