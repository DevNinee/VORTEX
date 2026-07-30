# 🚀 Super Aula: Projeto 1 (Mini ETL) — Construindo o Pensamento Analítico

Bem-vindo(a) a esta super aula focada em **Engenharia de Dados** e na construção de um **Mini ETL** (Extract, Transform, Load). O objetivo aqui não é apenas escrever código, mas desenvolver o **modelo mental** por trás da engenharia de dados robusta.

> [!NOTE]
> **Objetivo Principal:** Desenvolver a capacidade de pensar em arquitetura, idempotência e observabilidade antes mesmo de escrever a primeira linha de código.

---

## 🏗️ Etapa 0 — Definição (Antes do Código)

Antes de abrir a IDE, todo engenheiro(a) de dados precisa definir o escopo do que será construído.

- **Problema:** Quero transformar dados públicos em um dataset utilizável no meu banco de dados estruturado.
- **Entrada:** Uma API pública que retorna dados no formato JSON.
- **Saída:** Uma tabela tratada, normalizada e limpa no PostgreSQL.
- **Validação e Qualidade:** Contagem de linhas, checagem de integridade das colunas e logs detalhados de execução.

> [!IMPORTANT]
> Nunca comece a codar sem definir a Entrada, a Saída e, o mais importante, como você vai **validar** se deu certo.

---

## 🧠 Etapa 1 — Modelo Mental do ETL

Pense no pipeline como **3 funções puras e independentes**:

1. **Extract (E):** A função de "pegar" os dados da origem.
2. **Transform (T):** A função de "arrumar", limpar e padronizar os dados.
3. **Load (L):** A função de "gravar" os dados no destino (banco).

**❓ Pergunta-chave para testar sua arquitetura:**
> *"Se eu precisar trocar a API fornecedora amanhã, quais partes do meu código mudam?"*

**✅ Resposta Ideal:** Apenas a etapa de **Extract** (e talvez pequenos ajustes no **Transform**). O **Load** deve permanecer intocável. O desacoplamento é a chave da manutenção fácil.

---

## 🎯 Etapa 2 — Escolha da Fonte (Simples e Eficaz)

Para focar no processo e não em burocracias, usaremos:
🔗 **[JSONPlaceholder - Posts](https://jsonplaceholder.typicode.com/posts)**

**Por que essa fonte?**
- O JSON é limpo e bem estruturado.
- Não exige autenticação (tokens, OAuth, etc.), evitando complexidades desnecessárias no início.
- É o cenário ideal para treinar o **ciclo de vida completo** de um pipeline de dados.

---

## 📜 Etapa 3 — Contrato de Dados (Raciocínio de Schema)

Antes de criar qualquer tabela no banco, defina o **Contrato de Dados**. Quais são as regras inegociáveis para esse dataset?

### Campos Esperados:
- `source_id`: O ID original vindo da API.
- `user_id`: O ID do autor do post.
- `title`: O título do post.
- `body`: O conteúdo do post.
- `ingested_at`: A data/hora exata em que o dado entrou no nosso banco.

### Validação Mental (O teste de fogo):
- **O `source_id` deve ser único?** **Sim.** Isso será a nossa Chave Primária (ou Unique Key) para evitar duplicação de dados nas próximas execuções.
- **O `title` ou `body` podem ser vazios (Null)?** **Não é o ideal.** Devemos tratar isso.
- **O `ingested_at` vem de onde?** Da API? Não. Ele é **gerado pelo próprio pipeline** no momento da carga.

---

## 🛠️ Etapa 4 — Transformação (Onde a Engenharia Acontece)

Aqui é onde você agrega valor ao dado cru.

### Regras Mínimas de Transformação:
1. **Remover duplicados** com base no `source_id`.
2. **Aplicar `trim` em textos** (remover espaços em branco sobrando no início e fim das strings).
3. **Normalizar tipos de dados** (garantir que Inteiro é Inteiro, String é String).
4. **Remover ou tratar nulos críticos** (Ex: descartar linhas sem `source_id`).

> [!CAUTION]
> **A Pergunta de Engenharia:** *"Se esse pipeline rodar todo dia, ele vai sujar ou duplicar os dados no banco?"*
> 
> Se a resposta for sim, faltou a regra de ouro: **Idempotência**. Um script de carga deve poder rodar 1.000 vezes e o estado final do banco deve ser o mesmo que se ele tivesse rodado apenas 1 vez. (Dica: Use `INSERT ... ON CONFLICT DO UPDATE` ou `MERGE`).

---

## 🔒 Etapa 5 — Carga com Segurança (Load)

A inserção de dados no banco não pode ser feita de qualquer jeito.

- **Use Transações:** Se der erro na metade, o banco faz *Rollback*. Nada de dados pela metade.
- **Insira em Lote (Batch):** Inserir linha a linha é lento. Insira blocos de 1.000, 10.000 linhas.
- **Garanta a Unicidade:** O banco deve ter uma `Constraint Unique` no `source_id`.

**Validação Prática:** Rode o ETL 2 vezes seguidas. Se a tabela dobrou de tamanho, o seu script falhou na lógica de idempotência.

---

## 📊 Etapa 6 — Observabilidade Mínima

Você nunca deve rodar um script no escuro. Se ele quebrar em produção às 3 da manhã, os logs salvarão seu emprego.

Sempre registre (em console, arquivo ou tabela de logs):
- 🟢 Horário de Início / Fim da execução.
- 📥 Quantidade de registros extraídos.
- ⚙️ Quantidade de registros transformados / descartados.
- 📤 Quantidade de registros inseridos / atualizados no banco.
- ❌ Erros e exceções (stack trace completo).

> [!WARNING]
> Sem observabilidade, você fica cego em produção. Você precisa saber o que o pipeline está fazendo em tempo real.

---

## 🚀 Etapa 7 — Critério de "Entrega Real" no GitHub

O projeto não está finalizado só porque "rodou na sua máquina". O seu Pull Request (PR) só está pronto se tiver:

1. **Código executável e modular.**
2. **Script SQL** (DDL) de criação da tabela de destino.
3. Um **README.md** claro com o passo a passo de "Como Rodar o Projeto".
4. **Evidência de execução** (um print do log ou da tabela populada no banco).
5. **Próximos passos** (o que poderia ser melhorado na v2).

---

## 📝 Template de Raciocínio (Checklist VORTEX)

Para acelerar sua maturidade técnica, preencha este template a cada entrega ou projeto concluído. Ele força a reflexão técnica sobre o que você construiu:

- **O que aprendi no curso/estudo:** _(Ex: Aprendi sobre idempotência e transações no Postgres)_
- **Como apliquei no projeto:** _(Ex: Implementei um `ON CONFLICT DO UPDATE` no script de Load)_
- **Decisão técnica que tomei:** _(Ex: Decidi usar `pandas` para transformação e `psycopg2` com `execute_batch` para carga)_
- **Trade-off aceito:** _(Ex: O script roda em memória, então se a API retornar 10 milhões de linhas, o servidor vai travar. Aceitei isso porque sei que essa API retorna poucos dados)_
- **Como testei:** _(Ex: Rodei o script duas vezes e contei as linhas no banco)_
- **O que melhoraria na v2:** _(Ex: Adicionar testes unitários no módulo de transformação)_

---
*Mão na massa! A verdadeira aprendizagem começa quando o código quebra e você precisa investigar o porquê.*
