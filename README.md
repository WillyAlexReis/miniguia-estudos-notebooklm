# Caderno Temático: Arquitetura de Software com NotebookLM

## 1. Contexto e Objetivos
* **Tema Escolhido:** Princípios de Design de Software (DRY vs. AHA), Governança Arquitetural (ADR) e Transações Distribuídas (Saga Pattern).
* **Objetivo de Estudo:** Criar um guia prático e curadoria técnica sobre princípios fundamentais de arquitetura e design de software, utilizando o Google NotebookLM para sintetizar e cruzar informações de referências conceituadas do setor sem alucinações.

---

## 2. Curadoria de Fontes
Relação de fontes de referência utilizadas como base de conhecimento no NotebookLM:
1. [AHA Programming (Kent C. Dodds)](https://kentcdodds.com/blog/aha-programming) - Princípio *Avoid Hasty Abstractions* (Evite Abstrações Precipitadas) e o equilíbrio com DRY/WET.
2. [Don't Repeat Yourself (Wikipedia)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) - Definição formal e implicações do princípio DRY na redução de redundância.
3. [Architecture Decision Record (GitHub Org)](https://github.com/architecture-decision-record/architecture-decision-record) - Repositório e documentação do padrão ADR para registro de decisões arquiteturais.
4. [Architecture Decision Record (Martin Fowler)](https://martinfowler.com/bliki/ArchitectureDecisionRecord.html) - Análise de Martin Fowler sobre como documentar decisões técnicas contextuais ao longo do tempo.
5. [Saga Distributed Transactions Pattern (Microsoft Learn)](https://learn.microsoft.com/en-us/azure/architecture/patterns/saga) - Padrão arquitetural Saga para gerenciamento de transações em sistemas distribuídos e microsserviços.

---

## 3. Engenharia de Prompts & Troubleshooting ("Cicatrizes")

### Teste 1: Abordagem Direta (Zero-shot Básico)
* **Prompt Executado:**
  > *"O que é DRY e Saga?"*
* **Resultado Obtido:**
  * O modelo explicou a definição do DRY (*Don't Repeat Yourself*) de Andy Hunt e Dave Thomas, focando na premissa de evitar duplicação de conhecimento e regras de negócio. Citou brevemente o risco da abstração prematura (*hasty abstraction*) e o contraponto com AHA/WET.
  * Em relação ao Saga, explicou o conceito de decompor transações em microsserviços (*database-per-service*) e introduziu a ideia de transações compensatórias, além de diferenciar brevemente os modelos de **Coreografia** e **Orquestração**.
* **Diagnóstico/Limitação:** Embora correta e didática, a resposta tratou os dois temas de forma isolada e não explorou critérios práticos de decisão arquitetural (como transação pivô e pré-requisitos operacionais).

### Teste 2: Refinamento com Persona, Escopo Restrito e Comparação Específica
* **Prompt Executado:**
  > *"Atue como um Arquiteto de Software Sênior. Com base exclusivamente nas fontes fornecidas, compare o princípio DRY com AHA Programming e explique quando aplicar o padrão Saga em microsserviços."*
* **Resultado Obtido:**
  * A IA assumiu o tom de Arquiteto Sênior e confrontou diretamente as filosofias de abstração, ressaltando a máxima de Sandi Metz (*"A duplicação é muito mais barata do que a abstração errada"*), o problema do acoplamento temporal e a regra prática do WET (tolerar duplicação até a 3ª ocorrência).
  * No padrão Saga, o modelo aprofundou a explicação técnica: detalhou os cenários de aplicação (*cross bounded contexts*, bancos heterogêneos sem suporte a 2PC e tolerância à consistência eventual) e introduziu o conceito crucial de **Transação Pivô** (o ponto de não retorno do fluxo). Além disso, elencou explicitamente quando **NÃO** utilizar o padrão (dependências cíclicas, exigência de consistência imediata rígida e baixa maturidade de observabilidade/DLQ).

### Lições Aprendidas (Troubleshooting)
1. **Atribuição de Papel (*Role Prompting*):** Instruir o modelo a atuar como "Arquiteto Sênior" elevou o nível da resposta de um resumo conceitual para uma análise crítica e pragmática de engenharia.
2. **Restrição às Fontes (*Grounding*):** Limitar a resposta estritamente aos documentos carregados evitou alucinações e aproveitou o poder das fontes de alta autoridade técnica (como Martin Fowler, Kent C. Dodds e Microsoft Learn).
3. **Comparação Direta:** Pedir para contrapor conceitos (DRY vs. AHA) gerou uma síntese muito mais rica sobre os prós e contras da abstração prematura.

---

## 4. Miniguia de Estudo (Entrega Final)

### Resumo Estruturado dos Conceitos

#### 1. DRY vs. AHA Programming: A Perspectiva da Abstração Pragmática
* **DRY (Don't Repeat Yourself):** Estabelece que cada pedaço de conhecimento lógico deve ter representação única. A armadilha do DRY é a **abstração prematura** (*hasty abstraction*): unificar códigos com similaridade apenas sintática gera acoplamento nocivo, exigindo condicionais complexas quando as regras de negócio divergem.
* **AHA (Avoid Hasty Abstractions):** Baseia-se na máxima de Sandi Metz de que *"a duplicação é muito mais barata do que a abstração errada"*. O AHA preconiza tolerar o código duplicado nas primeiras ocorrências e só criar a abstração quando o padrão de negócio estiver totalmente claro e estável.

#### 2. Padrão Saga em Microsserviços
* **O Problema:** Em arquiteturas com *database-per-service*, transações ACID distribuídas via *Two-Phase Commit (2PC)* são lentas, bloqueantes e inviáveis na maioria dos bancos modernos.
* **A Solução:** O Saga decompõe uma operação de negócio em uma sequência de transações locais atômicas. Se ocorrer falha antes da **transação pivô**, o fluxo executa **transações compensatórias** no sentido inverso para reverter o estado.
* **Cenários Ideais:**
  * Operações que cruzam múltiplos *Bounded Contexts*.
  * Bancos de dados heterogêneos ou NoSQL sem suporte nativo a 2PC.
  * Sistemas e domínios de negócio que suportam **consistência eventual**.
* **Quando NÃO Utilizar:**
  * Requisitos que demandam consistência imediata absoluta.
  * Sistemas com dependências circulares entre serviços.
  * Falta de maturidade de infraestrutura para lidar com mensageria assíncrona, *Dead Letter Queues* (DLQ), idempotência e observabilidade distribuída.

---

### Glossário de Conceitos
* **Abstração Prematura (Hasty Abstraction):** Unificação precoce de trechos de código antes de compreender plenamente a evolução das regras de negócio.
* **ADR (Architecture Decision Record):** Registro estruturado e versionado com o código que documenta uma decisão técnica, suas motivações, alternativas descartadas e consequências.
* **Consistência Eventual:** Modelo onde as atualizações de dados se propagam pelo sistema de forma assíncrona até convergirem para um estado coerente.
* **Transação de Compensação:** Operação que desfaz logicamente os efeitos de uma transação local executada com sucesso em caso de falha posterior.
* **Transação Pivô:** O ponto de não retorno em uma Saga. Uma vez concluída com sucesso, o fluxo não pode mais ser revertido por compensação e deve ser levado até o final (*forward recovery*).

---

### Prompts Reutilizáveis
```text
Atue como um Arquiteto de Software Sênior. Com base nas fontes cadastradas, explique detalhadamente como o conceito de "Transação Pivô" afeta o design de um fluxo Saga Orquestrado e descreva como lidar com falhas nas etapas retentáveis (após o pivô).
