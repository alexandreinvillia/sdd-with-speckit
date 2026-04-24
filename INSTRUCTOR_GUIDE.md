# Guia do Instrutor: Spec-Driven Development com GitHub Copilot

Este documento fornece orientações práticas para facilitar o hands-on de SDD com GitHub Copilot.

## Objetivo do Hands-on

Mostrar como **especificação clara melhora a qualidade, consistência e rastreabilidade** do código gerado por IA, e como o desenvolvedor permanece no controle — refinando requisitos, validando implementação, e mantendo alinhamento com a visão do projeto.

---

## Checklist de Preparação

### Uma Semana Antes

- [ ] Validar que o repositório está em estado inicial (checklist abaixo).
- [ ] Testar os comandos Spec Kit localmente:
  ```bash
  specify init . --script sh
  specify integration install copilot
  ```
- [ ] Confirmar que GitHub Copilot funciona em sua máquina/Codespace.

### Estado Inicial Esperado

Antes de iniciar o hands-on com os participantes:

```
✓ .specs/ com spec.yaml, requirements.md, design.md, tasks.md
✓ app/.gitkeep (SEM app/main.py ainda)
✓ workshop/README.md
✗ .github/ (será criada durante hands-on)
✗ .specify/ (será criada durante hands-on)
✗ app/main.py (será criado durante etapa 3)
```

Confirme:
```bash
cd sdd-with-speckit
Test-Path .github  # deve retornar False
Test-Path app/main.py  # deve retornar False
git status  # deve estar clean
```

Se precisar resetar, execute:
```bash
# Remover alterações locais
git restore .
git clean -fd

# Ou fazer checkout de uma branch limpa
git checkout refactor/sdd
```

### No Dia do Hands-on

- [ ] Codespace ou ambiente local pronto e testado.
- [ ] GitHub Copilot funcionando (testar num arquivo qualquer).
- [ ] Projetor/câmera configurada para compartilhar tela.
- [ ] Abrir [workshop/README.md](workshop/README.md) em aba separada para referência.

---

## Fluxo Recomendado (Timing: ~40-50 minutos)

| Etapa | Tempo | Atividade |
|-------|-------|----------|
| **Abertura** | 5 min | Contexto breve: por que SDD? |
| **Etapa 1** | 10 min | Refinar requisitos com `/speckit.clarify` |
| **Etapa 2** | 5 min | Quebrar tasks com `/speckit.tasks` |
| **Etapa 3** | 20-25 min | Implementar com `/speckit.implement` (TASK-01 a TASK-05 apenas) |
| **Etapa 4** | 5 min | Validar conformidade com `@workspace` |
| **Reflexão** | 3-5 min | Aprendizados e próximos passos |

---

## Narrativa de Abertura (Use Assim) — 5 min

Rápido e direto:

> *"Bem-vindo. Vocês vão ver como especificação clara melhora o trabalho com Copilot.*
>
> *Contexto: ontem teve reunião, saiu o escopo de uma API simples de tarefas. Spec está em baseline minimo em `.specs/`. Seu trabalho agora é refinar, implementar e validar, sempre guiado por spec, não por achismo.*
>
> *Isso é SDD: especificação como bússola, não como decoração.*
>
> *Vamos começar. 40 minutos. Bora."*

---

## Dicas de Facilitação por Etapa

### Etapa 1: Refinar Requisitos

**Objetivo**: Que os participantes vivenciem um diálogo com Copilot para melhorar a especificação.

**Como facilitar**:
1. Abra [../.specs/requirements.m — Enxuto

### Etapa 1: Refinar Requisitos (10 min)

1. Abra [requirements.md](.specs/requirements.md).
2. Prompt:
   ```
   /speckit.clarify Identifique critérios de aceite faltando em #.specs/requirements.md 
   e casos de borda para endpoints de tarefas.
   ```
3. **Discuta**: Copilot sugeriu algo fora do escopo? (ex: auth, banco). Se sim, corte. Lembre constitution.md.
4. Atualize requirements.md rapidamente com 1-2 sugestões principais.

**Tempo**: Não se perca em perfeição. A ideia é vivenciar o diálogo, não terminar tudo.

---

### Etapa 2: Quebrar Tasks (5 min)

1. Prompt:
   ```
   /speckit.tasks Com base em #.specs/design.md, quebre em tasks pequenas, 
   com critério de pronto e ordem clara.
   ```
2. **Rápido**: Copilot ordenou certo? (POST antes de GET? Sim, porque precisa criar antes de listar).
3. Atualize [tasks.md](.specs/tasks.md).

**Tempo**: Bem rápido. Foco na ordem lógica.

---

### Etapa 3: Implementar (20-25 min) — O Coração

**Importante**: Implemente **apenas TASK-01 até TASK-05** (health check, modelos, storage, POST, GET). Deixe PATCH, DELETE e testes para "próximos passos".

1. Comando:
   ```bash
   specify init . --script sh
   specify integration install copilot
   ```
   Isso cria `.github/` com prompts.

2. Primeira task:
   ```
   /speckit.implement Implemente TASK-01 em #.specs/tasks.md 
   (criar app/main.py com FastAPI e health check). 
   Use #.specs/design.md como referência.
   ```

3. **Teste rápido**:
   ```bash
   python app/main.py
   # Em outro terminal:
   curl http://localhost:8000/
   ```

4. Task por task. **Nem se preocupe se não terminar TASK-05** — o importante é vivenciar o fluxo 2-3 vezes.

5. **Se Copilot errar**: Ótimo! Mostre: "Spec define o que fazer. Copilot errou. Corrigimos contra design.md."

---

### Etapa 4: Validar (5 min)

```
@workspace A implementação em #app/main.py respeita #.specs/design.md? 
O que está correto e o que diverge?
```

**Reflexão rápida**: "Sem spec, seria muito mais difícil validar. Spec permite comparação objetiva."

---

## Dicas Práticas

- **Não pause muito entre prompts**. Timing é apertado.
- **Se ficar lento**: Pule PATCH/DELETE. Foco em POST/GET.
- **Se sobrar tempo**: "O que vocês fariam diferente? Como seria sem spec?"
- **Armadilha**: Não deixe que entrem em detalhe FastAPI. "Isso é implementação. SDD é sobre spec.
**Sintomas**: Prompts `/speckit.*` não aparecem, ou retornam erro de permissão.

**Solução**:
1. Confirmar que GitHub Copilot Chat está instalado:
   ```
   code --list-extensions | findstr copilot-chat
   ```
2. Se não estiver, instalar:
   ```
   code --install-extension GitHub.copilot-chat
   ```
3. Reabrir VS Code — Rápido / Codespace.
4. Confirmar que está autenticado no GitHub.

---

### Comandos /speckit.* não aparecem

**Causa**: A pasta `.github/` ainda não foi criada, ou `copilot-instructions.md` não foi gerado.

**Solução**:
1. Confirmar que rodou:
   ```bash
   specify init . --script sh
   specify integration install copilot
   ```
2. Confirmar que `.github/` existe agora:
   ```bash
   ls -la .github/
   ```
3. Se não existir, pode ser problema com a instalação do specify. Tentar:
   ```bash
   specify --version
   pip install --upgrade specify-cli
   ```

---

### App/main.py existe mas não roda

**Sintomas**: `python app/main.py` retorna erro de módulo não encontrado (fastapi, uvicorn).

**Solução**:
1. Confirmar que dependências estão instaladas:
   ```bash
   pip install -r requirements.txt
   ```
2. Se usar Codespace, o devcontainer.json já deve instalar tudo. Reabrir container.

---

### Copilot gerou código muito complexo ou errado

**Causa**: Prompt foi vago, ou Copilot "alucionou" (inventou coisas).

**Solução**:
1. Revisar a resposta contra `design.md`. Está diferente?
2. Se estiver, pedir refinamento:
   ```
   /speckit.implement O código gerado não segue #.specs/design.md 
   (está usando [detalhe]. Refaça respeitando estritamente o design.
   ```
3. Mostrar ao grupo: "Spec clara permite validação. Sem ela, seria difícil notar essa divergência."

---

## Dicas para Engajar Participantes

### 1. Pause Frequentemente para Discussão

Depois de cada etapa, pergunte:
- "Vocês concordam com o que Copilot sugeriu?"
- "Isso mudaria se fossemos fazer de outra forma?"
- "Como seria sem spec? Confiávamos em Copilot cegamente?"

### 2. Mostre Divergências Intencionalmente

Se Copilot gerar algo que não bate com spec, **não corrija na hora**. Mostre o problema, deixe o grupo notar, e então corrija. Isso reforça o valor da spec.

### 3. Permita Experimentação

Se alguém quer tentar um prompt diferente, **deixe**. Capture o resultado, compare com spec, discuta.

### 4. Não Foque em FastAPI

Se a conversa virar sobre "qual é a forma melhor de fazer tal coisa em FastAPI", redirecione:
"Boa pergunta, mas não é sobre FastAPI agora — é sobre SDD. Spec define o que fazer; implementação é detalhe."

---

## Tempo Morto? Perguntas para Facilitar

Se ficar tempo livre ou estiverem aguardando respostas:

- "Como SDD ajuda quando há múltiplos devs trabalhando em paralelo?"
- "O que vocês fariam se Copilot sugerisse refatorar a spec?"
- "Que tipo de projeto se beneficiaria menos com SDD?"
- "Como manter spec sincronizada durante refatoração?"
- "SDD funciona em sprints curtos (1-2 semanas)?"

---

## Reflexão Final (Últimos 10 min)

Pergunte ao grupo:
Rápidas

Se terminar antes dos 50 min:

- "Como SDD ajuda com múltiplos devs?"
- "E se Copilot sugerir refatorar a spec?"
- "Qual projeto se beneficiaria menos?"


## Material de Referência para Você

- [README.md](README.md) — contexto público
- [workshop/README— 3-5 min

Perguntas rápidas:

- "Valeu a pena ter spec antes de codificar?"
- "Copilot foi mais útil com ou sem spec?"
- "Vocês usariam SDD em um projeto de vocês?"

**Não necessário terminar tudo. Fluxo > Completude.***Adapte ao público**: Devs iniciantes? Foque em conceitos. Arquitetos? Aprofunde em governance.

Boa facilitação! 🚀
