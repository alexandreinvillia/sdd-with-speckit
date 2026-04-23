# SDD with Speckit Constitution

## Core Principles

### I. Stack e Escopo Obrigatorios
O projeto MUST ser implementado em Python 3.11 usando FastAPI. O escopo MUST ser
uma API HTTP para gestao de tarefas pessoais. Mudancas de stack, adicao de
frontend dedicado ou troca de framework backend nao sao permitidas sem emenda
formal desta constituicao.

### II. Dados Somente em Memoria
Os dados MUST ser mantidos exclusivamente em memoria de processo (ex.: listas e
dicionarios Python). Reiniciar a aplicacao MUST limpar o estado. Persistencia em
arquivo, cache externo ou qualquer camada de armazenamento permanente nao e
permitida nesta fase.

### III. Sem Autenticacao e Sem Banco de Dados
O projeto MUST permanecer sem autenticacao, autorizacao, gestao de sessoes e sem
dependencia de banco de dados. Bibliotecas de ORM, migracoes e infraestrutura de
credenciais MUST NOT ser introduzidas.

### IV. Contrato HTTP Correto e Consistente
Cada endpoint MUST retornar status HTTP coerente com o resultado da operacao,
incluindo respostas de erro previsiveis e payloads claros. Como regra geral:
sucesso de leitura/atualizacao com 200, criacao com 201, exclusao sem corpo com
204, entrada invalida com 400/422 e recurso inexistente com 404.

### V. Codigo Didatico para Iniciantes
O codigo MUST priorizar legibilidade: nomes explicitos, funcoes curtas,
responsabilidades simples e organizacao direta. Abstracoes desnecessarias,
metaprogramacao e padroes avancados sem ganho claro MUST ser evitados. Tipagem e
comentarios curtos sao incentivados quando melhorarem entendimento.

## Restricoes Tecnicas e de Qualidade

- Dependencias MUST ser minimas e justificadas.
- Modelos de entrada e saida MUST usar validacao explicita do FastAPI/Pydantic.
- Erros de regra de negocio MUST ser tratados de forma uniforme e previsivel.
- O projeto SHOULD manter cobertura de testes para fluxos principais e casos de
  erro esperados.

## Fluxo de Desenvolvimento e Revisao

- Toda alteracao de comportamento MUST manter alinhamento com
  .specs/spec.yaml, .specs/requirements.md e .specs/design.md.
- Implementacao MUST seguir ordem de tarefas em .specs/tasks.md, com entregas
  incrementais e verificaveis.
- Revisoes de codigo MUST checar conformidade com esta constituicao,
  especialmente escopo tecnico, simplicidade e contrato HTTP.

## Governance

Esta constituicao prevalece sobre preferencias locais e exemplos temporarios.
Emendas MUST registrar motivacao, impacto e versao semantica resultante.

Politica de versao:
- MAJOR para mudancas incompativeis de principios ou remocao de garantias.
- MINOR para novos principios, secoes ou expansao normativa material.
- PATCH para clarificacoes editoriais sem alterar o significado normativo.

Conformidade MUST ser revisada em cada PR e revalidada ao final de cada etapa
do fluxo Speckit.

**Version**: 1.0.0 | **Ratified**: 2026-04-20 | **Last Amended**: 2026-04-20
