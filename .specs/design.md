# Design Tecnico (baseline minimo)

Usar como base entre as Etapas 2 e 3: validar tasks em .specs/tasks.md e implementar com /speckit.implement.

## Arquitetura

Aplicacao FastAPI monolitica simples com armazenamento em memoria.

## Estrutura de Arquivos

- app/main.py (criado na Etapa 3)
- .specs/spec.yaml
- .specs/requirements.md
- .specs/design.md
- .specs/tasks.md

## Endpoints

- GET /
- POST /tasks
- GET /tasks
- PATCH /tasks/{id}
- DELETE /tasks/{id}

## Modelos

- TaskCreate(title, description?)
- TaskUpdate(status)
- Task(id, title, description, status, created_at)

## Estrategia de Persistencia

- Lista em memoria (tasks_db)

## Tratamento de Erros

- 404 para recurso nao encontrado
- 422 para payload invalido (validacao FastAPI/Pydantic)

## Decisoes de Design

- Sem banco para manter foco no fluxo SDD
- UUID para identificacao
