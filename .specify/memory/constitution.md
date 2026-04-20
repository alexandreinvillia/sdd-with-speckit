<!--
SYNC IMPACT REPORT — Constitution v1.0.0
============================================

**Version Change**: INITIAL → 1.0.0 (MAJOR initial release)

**Principles Created** (5 new):
  ✅ I. Stack: Python 3.11 + FastAPI
  ✅ II. Armazenamento Em Memória
  ✅ III. Status HTTP Corretos (NON-NEGOTIABLE)
  ✅ IV. Código Acessível para Iniciantes
  ✅ V. Simplicidade Radical: Sem Autenticação, Sem Banco de Dados

**Sections Added**:
  ✅ Constraints Técnicas (technology, storage, API, HTTP compliance, dependencies, no external services)
  ✅ Workflow de Desenvolvimento (5 steps: Spec First, Type Annotations, Test Coverage, HTTP Semantics Review, Beginner Review)

**Templates Updated** (compliance verification):
  ✅ spec-template.md — already includes user scenarios + acceptance scenarios (aligns with principle IV & III)
  ✅ plan-template.md — includes "Constitution Check" gate (✓ ready to use for compliance)
  ✅ tasks-template.md — already structured for independent user stories (aligns with workflow step 6)

**Runtime Guidance Files** (verified):
  ✅ README.md — already references `/speckit.constitution` command and example rules (fully aligned)
  ✅ .specify/integration.json — integration with Copilot confirmed (v0.7.4.dev0)

**Ratification Date**: 2026-04-20 (project inception)
**Last Amendment Date**: 2026-04-20 (initial ratification)

**No Follow-Up TODOs**: All placeholders filled with concrete values.
-->

# API de Gestão de Tarefas (To-Do) — Constitution

## Core Principles

### I. Stack: Python 3.11 + FastAPI
Todas as funcionalidades DEVE utilizar Python 3.11 e FastAPI como framework web.
FastAPI garante type-safety nativo e geração automática de documentação OpenAPI.
Nenhuma dependência alternativa de framework é permitida; o escolhido é mandatório por sua pedagogia.

### II. Armazenamento Em Memória
Todos os dados DEVEM ser armazenados exclusivamente em memória (estruturas Python nativas: dict, list, set).
Persistência em banco de dados é PROIBIDA — simplifica o espaço problema e foca aprendizado em API design.
Reinicialização da aplicação limpa todos os dados; isso é aceitável para o escopo.

### III. Status HTTP Corretos (NON-NEGOTIABLE)
Cada response HTTP DEVE usar o código de status correto:
— `200 OK` para sucesso com corpo de resposta
— `201 Created` para criação bem-sucedida
— `204 No Content` para sucesso sem resposta
— `400 Bad Request` para erro de validação do cliente
— `404 Not Found` para recurso não encontrado
— `500 Internal Server Error` para erros não esperados

Violações desta regra DEVEM ser detectadas em PR review e rejeitadas.

### IV. Código Acessível para Iniciantes
Código DEVE priorizar legibilidade sobre performance. Nomes descritivos de variáveis e funções são obrigatórios.
Comentários explicativos DEVEM ser inclusos em lógica não-óbvia. Funções DEVEM ser pequenas e com responsabilidade única.
Este princípio garante que alguém novo ao Python entenda o que está acontecendo sem precisar ser especialista.

### V. Simplicidade Radical: Sem Autenticação, Sem Banco de Dados
Nenhuma camada de autenticação/autorização é necessária — a API é pública.
Nenhum banco de dados externo (SQL, NoSQL) será usado — memória é suficiente.
YAGNI (You Ain't Gonna Need It): features de segurança complexas NÃO devem ser adicionadas.
Esta simplicidade reduz complexidade e permite foco 100% em HTTP status correctness e boas práticas FastAPI.

## Constraints Técnicas

- **Python Version**: 3.11 obrigatório (nada menor)
- **Framework**: FastAPI (nenhuma alternativa)
- **Storage**: Estruturas nativas Python (dict, list); sem ORM, sem migrations
- **API Format**: JSON é o único formato suportado
- **HTTP Compliance**: Cada endpoint DEVE respeitar semântica HTTP correcta
- **Dependencies**: Apenas FastAPI + uvicorn; sem extensões desnecessárias
- **No External Services**: Nenhuma integração com bases de dados, APIs externas ou serviços de auth

## Workflow de Desenvolvimento

1. **Spec First**: Cada feature inicia com especificação clara em `spec.md` (contracts, responses, status codes)
2. **Type Annotations**: FastAPI models DEVEM usar Pydantic com type hints explícitos
3. **Test Coverage**: Testes unitários DEVEM cobrir todos os endpoints e casos de erro
4. **HTTP Semantics Review**: PR review DEVE verificar status codes e semântica HTTP
5. **Beginner Review**: Código DEVE passar por revisão de "legibilidade para iniciantes"
6. **No Breaking Changes Without Spec Amendment**: Mudanças em API contracts DEVEM ser documentadas em spec antes de PR

## Governance

- **Constitution Authority**: Esta constituição supersede todas as outras práticas e documentação de runtime.
- **Amendment Process**: Mudanças na constituição DEVEM ser votadas e documentadas com histórico de versão.
- **PR Compliance Checks**: Todos os PRs DEVEM verificar conformidade com os 5 princípios; PRs não-conformes são rejeitadas.
- **Rationale on Complexity**: Qualquer desvio da "Simplicidade Radical" (ex: adicionar auth, DB) DEVE incluir justificativa explícita no PR.
- **Runtime Guidance**: Vejo [.specify/](../../.specify/) para templates de especificação, planejamento e tarefas que incorporam estes princípios.

**Version**: 1.0.0 | **Ratified**: 2026-04-20 | **Last Amended**: 2026-04-20
