# Requirements (baseline minimo)

Refinar na Etapa 2 com base em .specs/spec.yaml usando /speckit.clarify e /speckit.checklist.

## Visao Geral

API REST para gerenciamento de tarefas com armazenamento em memoria.

## Requisitos Funcionais

- RF01: GET / retorna {"status": "ok"} com HTTP 200.
- RF02: POST /tasks cria tarefa com id, title, description opcional, status inicial pending e created_at.
- RF03: GET /tasks lista tarefas com HTTP 200.
- RF04: PATCH /tasks/{id} atualiza status (pending, in_progress, done), retorna 200 ou 404.
- RF05: DELETE /tasks/{id} remove tarefa, retorna 204 ou 404.

## Requisitos Nao Funcionais

- RNF01: API responde em JSON.
- RNF02: Erros retornam mensagem descritiva.
- RNF03: Codigo legivel para fins didaticos.

## Modelo de Dados

- id: string (uuid)
- title: string
- description: string | null
- status: pending | in_progress | done
- created_at: datetime

## Fora do escopo

- Banco de dados
- Autenticacao e autorizacao
- Paginacao
