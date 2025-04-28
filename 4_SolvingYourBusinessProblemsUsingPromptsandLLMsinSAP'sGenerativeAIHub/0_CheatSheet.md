# Recap

---

## Template

- **What it is**: A structure defining how the prompt is sent to the model.
- **Usage**: Automatically built by the SDK when sending a prompt.
- **Importance**: Guarantees that the input and output formats are correctly understood by the model.
- **In SAP Generative AI Hub**: Each prompt/request is wrapped inside a template before orchestration.

---

## Orchestration

- **What it is**: The process of handling the interaction between your prompt and the LLM.
- **Usage**: Manages prompt dispatching, model selection, input formatting, and output processing.
- **Importance**: Allows SAP AI Core to scale and control multiple LLMs securely and efficiently.

---

## Proxy Client

- **What it is**: A secure connection bridge between your local code and SAP AI Core.
- **Usage**: Needed to authenticate and communicate with the SAP AI Hub APIs.
- **Importance**: Every session using the SDK must start by getting a proxy client.

---

## Deployment

- **What it is**: A running environment where an orchestration (prompt flow) is executed.
- **Usage**: Can either connect to an existing deployment or trigger a new one dynamically.
- **Importance**: Without an active deployment, no prompts can be processed.

---

## Resource Group

- **What it is**: A logical isolation inside SAP AI Core for managing workloads and assets.
- **Usage**: Separates different ML projects, users, or departments.
- **Importance**: Ensures data security and organized access control.

---

## Executable

- **What it is**: Defines a program (training, inference, serving) that SAP AI Core can run.
- **Usage**: Specifies inputs, outputs, pipelines, and infrastructure requirements.
- **Importance**: The building block for running AI tasks inside SAP AI Core.

---

## Model Serving

- **What it is**: Deploying a trained ML model to respond to inference (prediction) requests.
- **Usage**: After training, the model must be served to accept new data and provide outputs.
- **Importance**: Real-time predictions, APIs, and applications need model serving.

---

## Hyperscaler Object Store

- **What it is**: Cloud storage used to store training datasets, models, and outputs.
- **Usage**: Example: Azure Blob Storage, AWS S3.
- **Importance**: Reliable, scalable, and cost-effective way to manage large AI assets.

---

## AI Launchpad

- **What it is**: Web-based interface for monitoring SAP AI Core resources and processes.
- **Usage**: Check deployments, review logs, manage models, monitor workflows.
- **Importance**: Visual tool to supervise AI activities without coding.

---

## Fine-tuning

- **What it is**: Process of adjusting an already pre-trained model with new domain-specific data.
- **Usage**: Used when you want the model to better perform on your business tasks.
- **Importance**: Increases model relevance but requires data, compute power, and expertise.

---

## RAG (Retrieval-Augmented Generation)

- **What it is**: Technique that enriches prompts with real-time retrieved knowledge.
- **Usage**: Fetches documents and passes them as additional context to the LLM.
- **Importance**: Ensures responses are accurate, up-to-date, and grounded in real business data.

---
