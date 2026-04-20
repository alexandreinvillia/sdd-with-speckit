# Copilot Prompts — Task Manager API

> Prompts organizados por etapa do fluxo SDD.
> Use no **Copilot Chat** (`Ctrl+Alt+I`) referenciando os arquivos de spec com `#`.

---

## Passo 0 — Inicialização do Spec Kit

```bash
specify init . --script sh
specify integration install copilot
```

---

## Etapa 1 — Constituição do Projeto

```
@workspace Compare #.specs/tasks.md com #app/main.py e diga quais tasks ainda não foram implementadas
```

```
@workspace A implementação atual em #app/main.py corresponde ao design definido em #.specs/design.md?
Liste quaisquer divergências.
```

```
@workspace Com base em todos os arquivos de spec em .specs/, qual seria a próxima funcionalidade a adicionar nesta API?
```
status HTTP corretos e código acessível para iniciantes.
```

---

## Etapa 2 — Proposta (spec.yaml)

```
@workspace Revise o baseline em #.specs/spec.yaml e proponha melhorias sem mudar o escopo principal
```

```
Com base em #.specs/spec.yaml, refine o texto da proposta mantendo as mesmas funcionalidades centrais (health + CRUD de tarefas)
```

---

## Etapa 3 — Requisitos (requirements.md)

```
Com base em #.specs/spec.yaml e #.specs/requirements.md, refine critérios de aceite e casos de borda
sem alterar o escopo principal.
```

```
Revise #.specs/requirements.md e identifique casos de borda ou critérios de aceite que estejam faltando
```

---

## Etapa 4 — Design Técnico (design.md)

```
Com base em #.specs/requirements.md e #.specs/design.md, refine o design técnico.
Mantenha estáveis os endpoints e o contrato de status HTTP.
```

```
Com base no design em #.specs/design.md, quais modelos Pydantic preciso criar?
```

---

## Etapa 5 — Tasks (tasks.md)

```
Com base em #.specs/design.md e #.specs/tasks.md, refine a ordem e a granularidade das tasks.
Cada task deve permanecer com duração estimada abaixo de 5 minutos.
```

```
Estou trabalhando na TASK-04 em #.specs/tasks.md. O que exatamente eu preciso implementar?
```

---

## Etapa 6 — Implementação (app/main.py)

### Criar arquivo inicial
```
Crie app/main.py com uma aplicação FastAPI e um endpoint GET / de health check que retorne {"status": "ok"}
```

### Modelos Pydantic
```
Com base em #.specs/design.md, crie os modelos Pydantic Task, TaskCreate e TaskUpdate em Python
```

### POST /tasks
```
Implemente o endpoint POST /tasks usando FastAPI. Ele deve:
- receber um body TaskCreate (title, description opcional)
- gerar um id UUID
- definir status como "pending"
- definir created_at com datetime.now()
- salvar na lista tasks_db
- retornar a tarefa com HTTP 201
```

### GET /tasks
```
Implemente o endpoint GET /tasks retornando todas as tarefas de tasks_db em formato de lista
```

### PATCH /tasks/{id}
```
Implemente PATCH /tasks/{id} usando FastAPI. Encontre a tarefa por id em tasks_db,
atualize o campo status usando o modelo TaskUpdate.
Retorne HTTP 200 com a tarefa atualizada ou HTTP 404 se não encontrar.
```

### DELETE /tasks/{id}
```
Implemente DELETE /tasks/{id} usando FastAPI. Encontre e remova a tarefa por id de tasks_db.
Retorne HTTP 204 sem body em caso de sucesso, e HTTP 404 se não encontrar.
```

---

## Etapa 7 — Testes e Validação

```
Gere comandos curl para testar todos os endpoints de uma API FastAPI de Task Manager rodando em localhost:8000:
- POST /tasks
- GET /tasks
- PATCH /tasks/{id}
- DELETE /tasks/{id}
```

```
Revise #app/main.py com base nos critérios de aceite em #.specs/requirements.md
e me diga se algum requisito está faltando ou foi implementado incorretamente
```

---

## Prompts de Revisão Cross-Artefato

```
@workspace Compare #.specs/tasks.md com #app/main.py e diga quais tasks ainda não foram implementadas
```

```
@workspace A implementação atual em #app/main.py corresponde ao design definido em #.specs/design.md?
Liste quaisquer divergências.
```

```
@workspace Com base em todos os arquivos de spec em .specs/, qual seria a próxima funcionalidade a adicionar nesta API?
```
