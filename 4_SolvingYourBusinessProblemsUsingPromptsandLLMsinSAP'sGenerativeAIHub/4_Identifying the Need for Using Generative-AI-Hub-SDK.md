# Identifying the Need for Using Generative-AI-Hub-SDK

## Software Development Kits (SDKs) for LLMs

- SDK = a collection of tools, libraries, and documentation that developers use to create software applications for specific platforms or frameworks

## Business Scenario

We saw that the Facility solutions company faces high volumes of customer communications, requiring efficient processing and prioritization within their internal applications to ensure timely and accurate responses.

We used generative AI hub in SAP AI Launchpad to create basic prompts.

We used a basic prompt to generate a structured response for the prompt. However, the business need is to streamline this process to handle large scale queries and enhance the performance of LLMs for the problem. Going forward, you want to create a customized solution and integrate this output in applications.

You can achieve this using SDKs for LLMs.

### Why to use SDK in this context?

1. Streamlined Processes:
    - SDKs provide developers with prebuilt tools, libraries, and APIs that simplify the development workflow. This eliminates the need to implement complex infrastructure or low-level details when accessing LLMs.

2. Enhanced Efficiency:
    - SDKs facilitate easier integration of LLMs into applications, improving development efficiency. Developers can concentrate on creating solutions instead of managing model deployment and maintenance.

3. Customization Opportunities:
    - SDKs often offer customization features, such as generative-ai-hub-sdk, to leverage the power of large language models available in generative AI hub. Customization enables developers to tailor foundation LLMs for specific use cases.

4. Improved Performance:
    - SDKs optimize LLMs for particular hardware (for example, GPUs) and cloud platforms. Google's API, for instance, delivers state-of-the-art on-device latency for LLMs on Android and iOS devices.

## Generative-AI-Hub-SDK

1. Installation

```bash
pip install "generative-ai-hub-sdk[all]"
```

- Here [all] implies installing all extra packages including langchain, which is not available by default.

2. Configuration

- Ensure that you have access to generative AI hub and deployed models.

- The SDK reuses configuration settings from the AI-core-SDK. These include client ID, client secret, authentication URL, base URL, and resource group. You can set these values as environment variables or via a config file.

- To utilize LLMs, you must configure the proxy modules.

- We suggest setting these values as environment variables for AI core credentials via a configuration file. The default path for this file is ~/.aicore/config.json for Mac.

3. For Mac users

- Open Notepad and replace the values in below json with your AI core Service keys that you downloaded from BTP and press Ctrl + S (Command + O for mac) to save file. A pop up will appear on the screen where navigate to ~/.aicore/ and location and save the file as config.json

- In case you are using mac, you might not be able to create .aicore folder directly. In that case, create the folder using the command

```bash
mkdir ~/.aicore/
```

- Now use the following command to open config.json file in nano.

```bash
nano ~/.aicore/config.json
```

- Now paste the following json script on config.json file.

```json
"AICORE_AUTH_URL": "https://* * * .authentication.sap.hana.ondemand.com",
  "AICORE_CLIENT_ID": "* * * ",
  "AICORE_CLIENT_SECRET": "* * * ",
  "AICORE_RESOURCE_GROUP": "* * * ",
  "AICORE_BASE_URL": "https://api.ai.* * *.cfapps.sap.hana.ondemand.com/v2"
}
```

4. For windows, use the following steps:

- Create .aicore folder in C:\Users\<current user>

- Create a config.json file with the below contents

```json
{
"AICORE_AUTH_URL": 
"AICORE_CLIENT_ID": ,
"AICORE_CLIENT_SECRET": ,
"AICORE_RESOURCE_GROUP": 
"AICORE_BASE_URL":
}
```

---

## Understanding Embeddings in SAP Generative AI

---

### 🔍 What Are Embeddings?

**Embeddings** are **vector representations of text (or other data)** that capture the **semantic meaning** of words, sentences, or entire documents.

Instead of treating text as raw strings, embeddings **convert language into numerical vectors** in a high-dimensional space, allowing AI models to:

- Measure **similarity** between concepts
- Perform **semantic search**
- Support **context-aware generation**

---

### 📐 Example

- "invoice" and "bill" → close vectors (similar meaning)
- "invoice" and "airplane" → distant vectors (different meaning)

This transformation enables SAP AI systems to understand that different terms may have similar intent.

---

### 🧠 How Are Embeddings Used in SAP Generative AI?

Embeddings power several intelligent capabilities inside the SAP ecosystem, especially in **Retrieval-Augmented Generation (RAG)** and **semantic search**.

#### Key Use Cases

1. **RAG (Retrieval-Augmented Generation)**:
   - Embeddings are used to **match user queries with internal business documents**.
   - The top-matching documents (based on embedding similarity) are retrieved and passed to the LLM to generate accurate, context-based responses.

2. **Semantic Search in SAP Analytics or SuccessFactors**:
   - Enables **natural language queries** over structured/unstructured enterprise data.
   - Embeddings help in finding **related results**, even if exact keywords are not used.

3. **Classification and Clustering**:
   - Grouping customer feedback, contracts, or HR data by **semantic meaning** using embeddings.

---

### 🧰 Technical View

- Each text is encoded into a **dense vector** (e.g., 384 or 768 dimensions).
- Similar vectors = semantically similar content.
- Vector similarity is calculated via **cosine similarity** or **Euclidean distance**.

---

### ✅ Summary

| Concept         | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Embedding        | Numeric vector capturing semantic meaning of a text                        |
| Purpose          | Compare meanings, retrieve relevant data, enrich LLM prompts              |
| SAP Use Cases    | RAG systems, semantic enterprise search, AI-driven classification         |
| Benefit          | Improved context, smarter document matching, human-like understanding     |

---

Embeddings are a **core enabler** for contextual intelligence in SAP’s Generative AI approach.  
They allow the system to reason about meaning — not just words — making AI results significantly more relevant and business-aware.

---
