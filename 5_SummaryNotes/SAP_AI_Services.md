# 🔧 Overview of SAP Generative AI Services

This section summarizes the key services presented in the SAP Generative AI Developer Certification, including their purpose and typical use cases.

---

## 1. SAP AI Core

- **What it is**: The runtime environment for executing and orchestrating machine learning pipelines and serving models.
- **Use case**: Run training workflows, deploy models for inference, and manage AI lifecycle in a secure, scalable way.
- **Key features**:
  - Kubernetes-based container orchestration
  - Resource groups for tenant/data isolation
  - API-driven interaction with CI/CD pipelines

---

## 2. SAP AI Launchpad

- **What it is**: The web-based UI that allows users to monitor and manage AI artifacts, workflows, and deployments from SAP AI Core.
- **Use case**: View model status, check logs, trigger executions, manage deployments — all without code.
- **Key features**:
  - Visual management of AI pipelines and artifacts
  - Integration with AI Core for orchestration
  - Role-based access and project isolation

---

## 3. SAP AI Foundation

- **What it is**: A suite of tools and capabilities on SAP BTP that provide infrastructure and services for developing, training, deploying, and monitoring AI solutions.
- **Use case**: Create enterprise-ready AI apps using foundational services (AI API, Event Mesh, Data Management).
- **Key features**:
  - Includes SAP AI Core, AI Launchpad, and other foundational building blocks
  - Supports open-source frameworks and CI/CD
  - Cloud-native design for scalability

---

## 4. SAP Generative AI Hub

- **What it is**: A managed service that allows you to consume and orchestrate prompts to various LLM providers like OpenAI, Meta, etc.
- **Use case**: Prompt orchestration, prompt templating, LLM provider integration — no need to build infrastructure.
- **Key features**:
  - Unified access to LLMs (SAP, OpenAI, Meta)
  - Template and orchestration engine
  - SDK available for Python (`generative-ai-hub-sdk`)
  - RAG and Agent support via LangChain/LlamaIndex

---

## 5. SAP AI API (Business AI Services)

- **What it is**: Predefined APIs for applying AI in business scenarios (e.g., Document Extraction, Product Categorization).
- **Use case**: Use pretrained models for typical SAP business functions without training your own.
- **Key features**:
  - Plug-and-play APIs embedded in SAP modules
  - High-quality results without ML expertise
  - Pay-per-use model

---

## 6. SAP Joule (AI Copilot)

- **What it is**: Natural-language AI assistant integrated into SAP apps.
- **Use case**: Navigate apps, summarize data, generate content (e.g., job descriptions, reports) using LLMs.
- **Key features**:
  - Embedded in SAP S/4HANA, SuccessFactors, Ariba, etc.
  - Leverages Generative AI Hub for LLMs
  - Personalized, context-aware interaction

---

## 7. SAP Build Code (with AI Generation)

- **What it is**: Low-code development environment with AI-assisted code generation (CAP projects, CDS, services).
- **Use case**: Auto-generate backend logic, unit tests, data models using natural language.
- **Key features**:
  - Integration with Joule copilot
  - Supports CAP and BAS environments
  - Accelerates developer productivity

---

## 8. Document Information Extraction

- **What it is**: AI service for extracting structured data from semi-structured documents like invoices and purchase orders.
- **Use case**: Accounts Payable automation, legal document processing.
- **Key features**:
  - OCR + NLP + ML-based field extraction
  - Available as API or embedded in modules
  - Premium Edition uses LLMs for more context-aware results

---
