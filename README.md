# Hands-on: Spec-Driven Development com GitHub Copilot + Spec Kit

## Cenário

Você irá construir uma **API de gestão de tarefas (To-Do)** usando:

- **GitHub Copilot** (Chat + sugestões inline)
- **Spec Kit** (fluxo SDD estruturado)

A ideia **não é codar muito** — é aprender o fluxo:

```
Setup Spec Kit → Constituição → Proposta/Spec (refino) → Design → Plano → Tasks → Código (via Copilot)
```

## Nota Importante Sobre a Abordagem

Este treinamento usa **SDD em modo hibrido**:

- O repositorio traz um baseline minimo em `.specs/` (ponto de partida comum)
- A turma refina esse baseline com Spec Kit + Copilot durante o hands-on
- O codigo nasce apenas na Etapa 6, guiado pelos artefatos refinados

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

**Passo 0 — inicializar o projeto para usar Spec Kit com Copilot:**
```bash
specify init . --script sh
specify integration install copilot
```

Esse passo cria a pasta `.specify/` e instala os arquivos `.prompt.md` em `.github/copilot/`, habilitando os comandos slash do Spec Kit no Copilot Chat.
Esse passo cria a pasta `.specify/` e configura o Copilot com arquivos em `.github/prompts/`, `.github/agents/` e `.github/copilot-instructions.md`, habilitando os comandos slash do Spec Kit no Copilot Chat.

**Observação:** neste momento você ainda não executa a API, porque o `app/main.py`
será criado na Etapa 6.

**Neste hands-on, vamos conduzir todas as etapas (spec, requisitos, design, tasks, testes e código)
dentro do próprio Codespace para manter o fluxo unificado para toda a turma.**

## Comandos do Spec Kit no Fluxo

Use estes comandos no Copilot Chat durante o hands-on (dentro do Codespace):

0. Preparar projeto e integração Copilot: `specify init` + `specify integration install copilot`
1. Definir regras do projeto: `/speckit.constitution`
2. Refinar proposta existente: `/speckit.specify`
3. Refinar ambiguidade: `/speckit.clarify`
4. Validar checklist da spec: `/speckit.checklist`
5. Gerar plano tecnico: `/speckit.plan`
6. Gerar tarefas: `/speckit.tasks`
7. Analisar plano/risco: `/speckit.analyze`
8. Implementar tarefas: `/speckit.implement`

---

## Estrutura do Repositório

```
.specify/            ← Criado no Passo 0 pelo specify init
.github/
  copilot-instructions.md  ← Diretrizes gerais para o Copilot
  prompts/           ← Prompts slash do Spec Kit
  agents/            ← Agentes auxiliares do fluxo Spec Kit
.specs/
  constitution.md    ← Regras do projeto (Etapa 1)
  spec.yaml          ← Proposta do sistema (Etapa 2)
  requirements.md    ← Requisitos funcionais (Etapa 3)
  design.md          ← Design técnico (Etapa 4)
  tasks.md           ← Plano de implementação (Etapa 5)
app/
  main.py            ← Criado somente na Etapa 6
docs/
  copilot-prompts.md ← Prompts prontos para usar com Copilot
```

> Os artefatos em `.specs/` são a "fonte da verdade" do sistema.
> O Copilot usa esses arquivos como contexto para gerar código mais preciso.

## Dinamica do Hands-on (baseline + refinamento)

Neste treinamento, os artefatos em `.specs/` ja trazem requisitos minimos para reduzir
variacao entre alunos. O trabalho da turma e **refinar e detalhar** cada arquivo em sequencia.

Antes disso, a turma executa o **Passo 0** para inicializar o Spec Kit no projeto e habilitar os comandos slash no Copilot Chat.

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

## Passo 0 — Inicializar Spec Kit e integração com Copilot

**Objetivo:** preparar o projeto para usar os comandos slash do Spec Kit dentro do Copilot Chat.

**O que fazer:**
1. Execute `specify init . --script sh` no terminal do Codespace
2. Execute `specify integration install copilot`
3. Confirme que `.specify/`, `.github/prompts/`, `.github/agents/` e `.github/copilot-instructions.md` foram criados

**Terminal:**
```bash
specify init . --script sh
specify integration install copilot
```

**Resultado esperado:** projeto inicializado para Spec Kit, com integração do Copilot pronta para os comandos `/speckit.*`.

> **Conexão com o mundo real:** esse é o bootstrap do projeto. Antes de discutir regras, specs ou código, o ambiente precisa estar preparado para que o fluxo SDD funcione de ponta a ponta.

---

## Etapa 1 — Definir a Constituição do Projeto (`/speckit.constitution`)

**Objetivo:** Estabelecer as regras do projeto antes de refinar qualquer artefato — stack, limites técnicos, critérios de qualidade e princípios de implementação.

**O que fazer:**
1. Execute `/speckit.constitution` no Copilot Chat
2. Defina as regras do hands-on (Python 3.11 + FastAPI, sem autenticação, sem banco, código didático)
3. Revise com a turma — esse arquivo guiará o Copilot nas próximas etapas

**Copilot Chat — Spec Kit:**
```
/speckit.constitution Defina as regras deste projeto:
Python 3.11 + FastAPI, armazenamento em memória, sem autenticação, sem banco de dados,
status HTTP corretos e código acessível para iniciantes.
```

**Resultado esperado:** arquivo `.specs/constitution.md` criado com as diretrizes do projeto. A partir daqui, o Copilot referencia essas regras automaticamente nos próximos comandos Spec Kit.

> **Conexão com o mundo real:** em times reais, as convenções do projeto ficam documentadas para que todos os desenvolvedores — e o Copilot — tomem decisões consistentes desde o início.

---

## Etapa 2 — Refinar a Proposta (`spec.yaml`)

**Objetivo:** Refinar o baseline de proposta já existente, em vez de criar do zero.

**O que fazer:**
1. Abra `.specs/spec.yaml`
2. Revise o baseline minimo ja definido
3. Use `/speckit.specify` para refinar descricao, contexto, escopo e fora de escopo
4. Ajuste `author` e `updated_at`
5. Valide se o texto continua alinhado à constituição definida na Etapa 1

**Copilot Chat — Spec Kit:**
```
/speckit.specify Refine o baseline em .specs/spec.yaml para uma API de tarefas pessoais.
Usuários podem criar, listar, atualizar status e remover tarefas.
Sem autenticação e sem banco de dados. Mantenha compatibilidade com a constituição do projeto.
```

**Resultado esperado:** `spec.yaml` refinado, mantendo o baseline comum e alinhando escopo com o grupo.

> **Conexão com o mundo real:** Times de produto e engenharia usam propostas como essa
> para alinhar expectativas antes do sprint. O `spec.yaml` é o contrato inicial.

---

## Etapa 3 — Refinar Requisitos (`requirements.md`)

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

## Etapa 4 — Criar o Design Técnico (`design.md`)

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

## Etapa 5 — Gerar o Plano de Tasks (`tasks.md`)

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

## Etapa 6 — Implementar com Copilot (criar `app/main.py`)

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

## Etapa 7 — Criar e Executar Testes (`TASK-08`)

**Objetivo:** Garantir que a API funciona conforme o especificado, criando testes automatizados.

**O que fazer:**
1. Crie o arquivo `tests/test_api.py`
2. Use o Copilot para gerar os testes a partir dos critérios de aceite
3. Execute e valide que todos passam

**Copilot Chat:**
```
Com base nos critérios de aceite em .specs/requirements.md, crie testes automatizados
para todos os endpoints em app/main.py usando pytest e httpx (TestClient do FastAPI).
```

**Rodar os testes:**
```bash
pytest tests/ -v
```

**Resultado esperado:** todos os testes passando, cobrindo os 5 endpoints (GET /, POST/GET/PATCH/DELETE /tasks).

> **Conexão com o mundo real:** testes gerados a partir da spec fecham o ciclo SDD — o código
> foi escrito para atender a spec, e os testes provam que ele realmente atende.

---

## Etapa 8 — Validar com os Requisitos

**Objetivo:** Confirmar que o código entrega o que foi especificado.

**Prompt Copilot:**
```
@workspace Revise app/main.py contra os critérios de aceite em .specs/requirements.md
e me diga se algum requisito está faltando ou foi implementado de forma incorreta
```

**Resultado esperado:** Copilot compara artefato de spec com código e aponta gaps — sem você precisar fazer isso manualmente.

---

## Resultado Final

Ao concluir, você terá:

| Artefato                   | Propósito                              |
|----------------------------|----------------------------------------|
| `.specify/`                | Configuração local do Spec Kit         |
| `.github/prompts/`         | Prompts slash do Spec Kit no Copilot   |
| `.github/agents/`          | Agentes auxiliares do fluxo Spec Kit   |
| `.github/copilot-instructions.md` | Instruções gerais do Copilot    |
| `.specs/constitution.md`   | Regras e convenções do projeto         |
| `.specs/spec.yaml`         | Proposta e escopo do sistema           |
| `.specs/requirements.md`   | O que o sistema deve fazer             |
| `.specs/design.md`         | Como o sistema será construído         |
| `.specs/tasks.md`          | Plano de execução incremental          |
| `app/main.py`              | API funcional gerada com Copilot       |
| `tests/test_api.py`        | Testes gerados a partir da spec        |
| `docs/copilot-prompts.md`  | Prompts reutilizáveis para o time      |

---

## Referências

- [Spec Kit Quickstart](https://github.github.com/spec-kit/quickstart.html)
- [FastAPI Docs](https://fastapi.tiangolo.com)
- [GitHub Copilot Chat](https://docs.github.com/en/copilot/github-copilot-chat)