# Caderno Temático: Arquitetura de Software com NotebookLM (Gemini Notebook)

## 1. Contexto e Objetivos
* **Tema Escolhido:** Princípios de Design de Software, Governança Arquitetural (ADR) e Padrões Distribuídos (Saga).
* **Objetivo de Estudo:** Criar um guia prático e curadoria técnica de conceitos fundamentais de arquitetura e design de software, utilizando o Google NotebookLM para sintetizar e cruzar informações de referências conceituadas do setor.

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

* **Teste 1 (Prompt Amplo):**
  * *Prompt:* "O que é DRY e Saga?"
  * *Resultado:* Respostas superficiais e sem aprofundamento na relação entre abstração de código e arquitetura distribuída.
* **Teste 2 (Refinamento com Persona e Foco nas Fontes):**
  * *Prompt:* "Atue como um Arquiteto de Software Sênior. Com base exclusivamente nas fontes fornecidas, compare o princípio DRY com AHA Programming e explique quando aplicar o padrão Saga em microsserviços."
  * *Resultado:* A IA detalhou o perigo da duplicação versus abstração prematura e explicou claramente a orquestração e coreografia no padrão Saga.
* **Ajustes e Lições (Troubleshooting):** Fornecer links de fontes autoritativas (como Martin Fowler e Microsoft Learn) e estruturar prompts pedindo comparações conceituais garantiu respostas fundamentadas e livres de alucinações.

---

## 4. Miniguia de Estudo (Entrega Final)

### Resumo Estruturado
* **DRY vs. AHA Programming:** O princípio DRY (*Don't Repeat Yourself*) visa evitar a duplicação de conhecimento. No entanto, o princípio AHA (*Avoid Hasty Abstractions*) alerta que a duplicação precoce é frequentemente muito mais barata de manter do que a abstração errada criada antes da hora.
* **Architecture Decision Records (ADRs):** Documentos curtos e versionados com o código que registram decisões arquiteturais importantes, o contexto em que foram tomadas e suas consequências.
* **Padrão Saga:** Padrão para manter a consistência de dados em arquiteturas de microsserviços por meio de uma sequência de transações locais, onde falhas disparam ações de compensação (rollback compensatório).

### Glossário de Conceitos
* **ADR (Architecture Decision Record):** Registro formal e estruturado de uma decisão arquitetural.
* **AHA (Avoid Hasty Abstractions):** Princípio que preconiza preferir código duplicado a uma abstração apressada.
* **Saga Pattern:** Mecanismo para gerenciar transações distribuídas sem depender de bloqueios de transação distribuída de duas fases (2PC).
* **Compensating Transaction (Transação de Compensação):** Transação que desfaz logicamente o efeito de uma transação anterior caso uma etapa da Saga falhe.

### Prompts Reutilizáveis
```text
Atue como um Arquiteto de Software Sênior. Com base nas fontes cadastradas, explique como documentar uma mudança estrutural de monólito para microsserviços usando ADRs e quais os critérios para decidir entre coreografia ou orquestração ao adotar o padrão Saga.
