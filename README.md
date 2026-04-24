# Spec-Driven Development com GitHub Copilot

Use especificação como contexto de engenharia para orientar o GitHub Copilot do refinamento de requisitos até a implementação.

## Bem-vindo

- Para quem é: desenvolvedores, arquitetos, tech leads, educadores e equipes que querem usar GitHub Copilot com mais previsibilidade e consistência.
- O que você vai aprender: como aplicar Spec-Driven Development para reduzir ambiguidade, organizar decisões técnicas e melhorar a qualidade das entregas geradas com IA.
- O que você vai construir: uma API simples de gestão de tarefas em FastAPI, implementada a partir de artefatos de especificação já preparados no repositório.
- Pré-requisitos: conta no GitHub, acesso ao GitHub Copilot e noções básicas de leitura de código Python e APIs HTTP.

Neste material, a preparação do ambiente fica na raiz do repositório e a execução do hands-on fica em [workshop/README.md](workshop/README.md).

## O que este repositório contém

Este repositório foi organizado para separar claramente preparação e execução:

- [README.md](README.md): visão geral do projeto, contexto do workshop, pré-requisitos e setup do ambiente.
- [workshop/README.md](workshop/README.md): guia prático do hands-on com o fluxo de SDD.
- [.specs](.specs/): baseline dos artefatos de especificação usados como fonte de verdade.
- [app](app/): código da aplicação criado durante o hands-on.
- [docs/copilot-prompts.md](docs/copilot-prompts.md): prompts de apoio para instrutor e participantes.

## Por que usar SDD com GitHub Copilot?

Spec-Driven Development coloca clareza antes de velocidade. Em vez de pedir código diretamente para a IA com contexto incompleto, o fluxo começa com artefatos que deixam explícitos escopo, regras, critérios de aceite, decisões técnicas e sequência de implementação.

Com isso, o GitHub Copilot deixa de operar por inferência ampla e passa a trabalhar sobre um contexto mais restrito e verificável. O resultado prático é:

- Menos ambiguidade na interpretação do problema.
- Mais consistência entre diferentes pessoas gerando código a partir da mesma base.
- Melhor alinhamento entre requisitos, design, tasks e implementação.
- Menos retrabalho durante revisão e validação.
- Maior capacidade de ensinar, demonstrar e repetir o fluxo em equipe.

## Como preparar o ambiente

### 1. Criar uma cópia do repositório

Use este repositório como template ou faça um fork para sua conta, conforme o fluxo adotado na sua turma.

Se estiver usando o template do GitHub, você pode iniciar por aqui:

[![](https://img.shields.io/badge/Copiar%20Exerc%C3%ADcio-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/new?template_owner=alexandreinvillia&template_name=sdd-with-speckit&owner=%40me&name=spec-driven-development&description=Exerc%C3%ADcio:+Spec-Driven+Development+com+GitHub+Copilot&visibility=public)

### 2. Abrir no GitHub Codespaces

Depois de criar sua cópia do repositório:

1. Acesse o repositório na sua conta.
2. Clique em `Code`.
3. Abra a aba `Codespaces`.
4. Crie um novo Codespace.

## Próximo passo

Com o Codespace aberto, siga para [workshop/README.md](workshop/README.md) para validar o ambiente e executar o hands-on.

## Estrutura do repositório

```text
.specs/
  spec.yaml
  requirements.md
  design.md
  tasks.md
app/
  .gitkeep
docs/
  copilot-prompts.md
workshop/
  README.md
```

## Recursos

- [Spec Kit Quickstart](https://github.github.com/spec-kit/quickstart.html)
- [FastAPI Documentation](https://fastapi.tiangolo.com)
- [GitHub Copilot Chat Documentation](https://docs.github.com/en/copilot/github-copilot-chat)
- [Prompts do workshop](docs/copilot-prompts.md)

## Notas para instrutores

- Mantenha o foco em SDD, não em FastAPI.
- Use o código como demonstração do valor da especificação, não como objetivo principal.
- Evite expandir o escopo além do CRUD básico de tarefas.
- Preserve o baseline comum do repositório para reduzir variabilidade entre participantes.

&copy; 2025 GitHub &bull; [Código de Conduta](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)
