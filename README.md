# VORTEX

Este repositório é meu compromisso público: estudar e construir ao mesmo tempo.

Minha regra é simples:
1. estudar;
2. aplicar no código no mesmo dia;
3. registrar o progresso.

Sem perfeccionismo. Sem esperar “o momento ideal”.

## Plano de estudo aplicado (DataCamp + prática)

A sequência abaixo é a que vou seguir.  
Cada bloco de curso precisa gerar uma entrega real no repositório.

## 1) Python e SQL (base)

Cursos DataCamp:
- Introduction to Python
- Intermediate Python
- Object-Oriented Programming in Python
- Introduction to SQL
- Joining Data in SQL
- Intermediate SQL

Por que:
- preciso base sólida para construir com velocidade e consistência.

Aplicação imediata:
- organizar estrutura de código;
- consultas SQL reais no PostgreSQL;
- primeira camada de dados do projeto.

## 2) Coleta de dados e Web Scraping

Cursos DataCamp:
- Introduction to APIs in Python
- Web Scraping in Python
- Importing Data in Python (quando necessário para formatos diversos)

Por que:
- preciso coletar dados de fontes públicas de forma confiável.

Aplicação imediata:
- coletor com requests + beautifulsoup4;
- coletor dinâmico com playwright para páginas com JavaScript.

## 3) Processamento e análise de dados

Cursos DataCamp:
- Data Manipulation with pandas
- Joining Data with pandas
- Cleaning Data in Python
- Working with Dates and Times in Python (para séries temporais e logs)

Por que:
- dado bruto não resolve problema; precisa limpeza e estrutura.

Aplicação imediata:
- pipeline de transformação;
- deduplicação e normalização;
- preparação para análise investigativa.

## 4) API e backend em Python

Cursos DataCamp:
- API development path (conteúdos equivalentes no DataCamp)
- cursos de boas práticas de backend Python disponíveis na trilha

Por que:
- preciso expor dados de forma reutilizável e estável.

Aplicação imediata:
- endpoints com FastAPI;
- validação, paginação e filtros;
- documentação automática.

## 5) Banco, modelagem e persistência

Cursos DataCamp:
- Database Design (fundamentos)
- SQL for data workflows (conteúdos equivalentes)

Por que:
- sem modelagem boa, investigação vira caos.

Aplicação imediata:
- modelagem de tabelas;
- SQLAlchemy para persistência;
- evolução controlada de schema.

## 6) Qualidade e confiabilidade

Cursos DataCamp:
- Software Engineering Principles in Python (ou equivalente disponível)
- Test concepts aplicados em Python

Por que:
- quero manter ritmo sem quebrar qualidade.

Aplicação imediata:
- testes com pytest;
- padrão com ruff e black;
- pipeline mínima de qualidade no repositório.

## 7) Node.js para integração

Cursos recomendados (fora DataCamp, se necessário):
- Node.js + Express (fundamentos)
- consumo de APIs com fetch/axios

Por que:
- preciso integrar serviços e preparar uma camada de gateway.

Aplicação imediata:
- serviço Node.js consumindo API Python;
- rotas agregadas para clientes.

## 8) Docker e Kubernetes

Cursos DataCamp:
- Introduction to Docker (se disponível na sua trilha atual)
- fundamentos de deploy/cloud (conteúdos equivalentes)

Cursos externos recomendados para Kubernetes:
- Kubernetes fundamentals (curso prático focado em deploy real)

Por que:
- ambiente reproduzível e caminho para escala.

Aplicação imediata:
- docker-compose com serviços do projeto;
- evolução para manifests Kubernetes.

## Projetos paralelos além do VORTEX

Vou criar projetos menores para acelerar aprendizado e depois reaproveitar no VORTEX.

## Projeto 1: Mini ETL de dados públicos
Objetivo:
- consumir uma API pública;
- transformar dados com pandas;
- salvar no PostgreSQL.

Stack:
- Python, pandas, SQLAlchemy, PostgreSQL.

## Projeto 2: Scraper de notícias com armazenamento
Objetivo:
- coletar de 2-3 fontes;
- limpar conteúdo;
- armazenar histórico com timestamp.

Stack:
- requests, beautifulsoup4, playwright, PostgreSQL.

## Projeto 3: API de consulta de dados
Objetivo:
- expor busca, filtro e paginação;
- retornar dados processados pelo ETL.

Stack:
- FastAPI, SQLAlchemy, PostgreSQL.

## Projeto 4: Gateway Node.js para API Python
Objetivo:
- construir uma camada Node.js que consome e agrega endpoints Python.

Stack:
- Express, axios/fetch.

## Projeto 5: Pipeline agendado
Objetivo:
- executar coleta e processamento em rotina automática;
- registrar logs e falhas.

Stack:
- Python + agendamento (cron/worker), Docker.

## Como vou executar

- ciclos curtos de estudo + prática;
- tarefas pequenas e claras;
- uma entrega por vez;
- checklist simples no README e nas issues;
- foco em progresso semanal, não em perfeição.

## Regras deste repositório

- estudar sem aplicar não conta;
- toda semana precisa de entrega real;
- cada módulo estudado gera código;
- decisões importantes ficam documentadas.

## Roadmap de execução

- [ ] Base do projeto organizada
- [ ] API inicial funcional
- [ ] Primeira coleta funcional
- [ ] Primeiro pipeline com pandas
- [ ] Persistência estável no PostgreSQL
- [ ] Testes + ruff + black no fluxo padrão
- [ ] Gateway Node.js integrado
- [ ] Ambiente completo com Docker
- [ ] Evolução para Kubernetes
