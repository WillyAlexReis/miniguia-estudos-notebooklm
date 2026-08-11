# Caderno Temático: Arquitetura de Software com NotebookLM

## 1. Contexto e Objetivos
* **Tema Escolhido:** Arquitetura de Software (Padrões Arquiteturais, Monolitos vs. Microsserviços e Boas Práticas).
* **Objetivo de Estudo:** Criar um guia de consulta rápida e curadoria técnica sobre princípios de arquitetura de software, utilizando o Google NotebookLM para sintetizar e organizar conteúdos de referência sem alucinações.

---

## 2. Curadoria de Fontes
Relação de artigos e documentos inseridos no NotebookLM para fundamentação das respostas:
1. `monoliths-vs-microservices.pdf` - Comparativo sobre monolitos e microsserviços.
2. `clean-architecture-principles.md` - Princípios e separação de camadas em Clean Architecture.
3. `design-patterns-summary.pdf` - Resumo de padrões de projeto estruturais e criacionais.

---

## 3. Engenharia de Prompts & Troubleshooting ("Cicatrizes")

* **Teste 1 (Prompt Genérico):**
  * *Prompt:* "O que é arquitetura de software?"
  * *Resultado:* Resposta muito ampla e vaga, sem focar nas fontes.
* **Teste 2 (Ajuste de Contexto):**
  * *Prompt:* "Com base exclusivamente nas fontes enviadas, liste as 3 principais diferenças entre monolitos e microsserviços em formato de tabela."
  * *Resultado:* Excelente síntese em tabela com pontos de acoplamento, escalabilidade e complexidade operacional.
* **Ajustes e Lições (Troubleshooting):** Foi necessário especificar o papel da IA ("Atue como um Arquiteto de Software Sênior") e solicitar dados em tabelas/tópicos para obter saídas estruturadas e sem prolixidade.

---

## 4. Miniguia de Estudo (Entrega Final)

### Resumo Estruturado
* **Arquitetura Monolítica:** Aplicação unificada onde todas as camadas (UI, regra de negócio, acesso a dados) residem no mesmo codebase. Alta simplicidade inicial, mas escalabilidade complexa.
* **Microsserviços:** Divisão do sistema em serviços independentes por domínio de negócio. Alta flexibilidade e escalabilidade, porém traz complexidade de rede e governança.
* **Clean Architecture:** Foco na independência de frameworks e separação de responsabilidades (camadas internas protegem as regras de negócio de mudanças externas).

### Glossário de Conceitos
* **Coupling (Acoplamento):** O nível de dependência entre dois módulos de software.
* **Cohesion (Coesão):** O grau em que as responsabilidades de um único módulo estão relacionadas entre si.
* **RAG (Retrieval-Augmented Generation):** Técnica usada pelo NotebookLM para responder perguntas ancoradas em documentos específicos fornecidos pelo usuário.

### Prompts Reutilizáveis
```text
Atue como um Arquiteto de Software Sênior. Com base nos documentos fornecidos, explique o impacto do acoplamento em um sistema monolítico e sugira 3 estratégias de refatoração para desacoplá-lo.
