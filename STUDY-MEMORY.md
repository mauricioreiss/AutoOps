# STUDY-MEMORY - AutoOps

<!-- Maintained by the mentor-buddy skill. Read the header every session; open sections only when needed. -->

## Header
- Conversation language: pt
- English corrections: n/a
- Tone: banter
- Notebook: paper
- Level: mid (engenharia geral) / junior (sintaxe Python) (set 2026-10-22; last recalibration: none)
- Stack: Python 3.12.10 (via pyenv-win), FastAPI, IDE VS Code, OS Windows 11
- Project: Background worker with a queue (+ porta REST) - AutoOps: ingestao de telemetria, deteccao de anomalia e diagnostico via agente de IA
- Now: Phase 2 Environment / Step 2.4 Git / Misses 0
- Next action: decidir se o projeto usa git; se sim, git init + .gitignore + primeiro commit (Mauri digita). Confirmar autocomplete no scratch.py e apagar o arquivo
- Last session: 2026-10-22 - Upgrade Python 3.7.4 -> 3.12.10 via pyenv-win; extensoes Python + Pylance instaladas (interpretador ainda nao confirmado)
- Review on resume: (sem revisao tecnica ainda - sessao 1 foi so setup de ambiente, nenhum conceito de codigo ensinado)

## Index
1. Brief
2. Phase plan
3. Decisions
4. Error map
5. Session log
6. Open questions
7. Verified facts
8. Skill drift
9. Review drills
<!-- END HEADER -->

## 1. Brief
Problem: times de SRE recebem telemetria (metricas/logs) e precisam detectar anomalias automaticamente e receber diagnostico + sugestao de acao, em vez de vasculhar dashboard na mao.
Users: engenheiro de SRE/DevOps monitorando um servico.
Acceptance criteria:
1. API REST assincrona (FastAPI) recebe eventos de telemetria (metrica: nome, valor, timestamp, servico), validados via Pydantic v2, responde rapido sem bloquear.
2. Evento validado e publicado numa fila RabbitMQ simples (sem DLQ/retry ainda); a API so garante que foi enfileirado.
3. Worker assincrono consome a fila, agrega eventos numa janela de tempo por servico e detecta anomalia simples (valor fora de um limite configuravel / desvio padrao).
4. Anomalia detectada aciona um agente simples (LangChain) que busca historico salvo no Postgres e devolve diagnostico + sugestao de acao em JSON estruturado.
5. Tudo sobe com `docker compose up` (API, worker, RabbitMQ, Postgres).
6. Testes automatizados (pytest) cobrindo validacao de payload e logica de deteccao de anomalia.
Out of scope / Later: gRPC; DLQ + exponential backoff no RabbitMQ; LangGraph com maquina de estados completa + pgvector real; mypy estrito, Ruff, uv/Poetry, structlog com correlation ID, testcontainers, diagramas C4 (entram na Fase 7); Redis; deploy em producao real (free tier pode nao comportar o stack - decidir na Fase 10).

## 2. Phase plan
- [x] 0 Interview
- [x] 1 Project
- [ ] 2 Environment
  - [x] 2.1 Detectar toolchain (Python, pip, Docker, VS Code) - done when os outputs de versao forem colados (Python 3.7.4 estava EOL, upgrade para 3.12.10 via pyenv-win; Docker 29.3.0 ja ok)
  - [x] 2.2 Configurar suporte Python no VS Code (extensao oficial + Pylance) - barra mostra pyenv (3.12.10) (VS Code tinha auto-selecionado 3.14.3; Mauri trocou manualmente). Autocomplete a confirmar
  - [x] 2.3 Escolher terminal vs IDE para rodar comandos - terminal integrado, python --version = 3.12.10
  - [ ] 2.4 Decidir sobre git (usar ou nao; se sim, init + .gitignore + primeiro commit) - done when decisao registrada (e `git log` mostrando commit, se optou por git)
  - [ ] 2.5 (opcional) Criar repositorio remoto e push - done when remoto criado e push feito, se desejado
- [ ] 3 Folder structure
- [ ] 4 Walking skeleton
- [ ] 5 Feature slices
- [ ] 6 Persistence
- [ ] 7 Quality
- [ ] 8 Docker
- [ ] 9 CI
- [ ] 10 Deploy
- [ ] 11 Retro

## 3. Decisions
| Date | Decision | Why | Doc |
|---|---|---|---|
| 2026-10-22 | IDE: VS Code | Leve, extensao oficial de Python + Pylance, boa integracao com Docker | - |
| 2026-10-22 | Escopo cortado para MVP (ver Brief) | 3h/semana disponiveis; spec original era projeto de um ano | - |
| 2026-10-23 | Terminal: integrado do VS Code | Mesma janela do codigo; ativa o venv sozinho com o interpretador selecionado | code.visualstudio.com/docs/terminal/basics |
| 2026-10-22 | Python alvo: 3.12.x (via pyenv-win, ja instalado) | 3.7.4 esta EOL e abaixo do minimo do Pydantic v2 (>=3.9) e do langchain-core (>=3.10); 3.12 tem suporte de seguranca ate 2028 e e o ponto doce de compatibilidade de libs (menos atrito que a 3.14, recem lancada) | python.org/downloads, pydantic.dev/docs, langchain-core PyPI |

## 4. Error map
| Topic | Misses | Last seen | Doc (exact section) |
|---|---|---|---|

## 5. Session log
- 2026-10-22: Interview completa (perfil, nivel, tom, brief aprovado), STUDY-MEMORY.md criado. Python atualizado de 3.7.4 (EOL) para 3.12.10 via pyenv-win. Extensoes Python + Pylance instaladas no VS Code. Pasta do projeto ainda com nome fora do padrao (espaco/parenteses) - Mauri vai renomear depois que a memoria estiver salva.
Earlier:

## 6. Open questions
- (resolvida 2026-10-23) Pasta renomeada para `c:\dev\estudos\AutoOps`, sem espaco nem parenteses.

## 7. Verified facts
| Fact | Value | Source | Verified |
|---|---|---|---|
| Pydantic v2 (2.11+) minimo Python | >=3.9 | pydantic.dev/docs/validation/2.11/get-started/install | 2026-10-22 |
| langchain-core (1.4.0) minimo Python | >=3.10,<4.0 | langchain-core PyPI metadata | 2026-10-22 |
| Python 3.12 status | bugfix/security ate 2028 | python.org/downloads | 2026-10-22 |

## 8. Skill drift
- (nenhum ainda)

## 9. Review drills
| # | File | Answer key (line: defect) | Found | Missed |
|---|---|---|---|---|
