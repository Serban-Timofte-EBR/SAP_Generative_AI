# Describing SAP's Approach to Large Language Models (LLMs)

## 1. Describing LLMs

### 1.1 Introducing Large Language Models (LLMs)

- **LLM (Large Language Model)** is a type of AI model that specializes in **processing, understanding, and generating human language**.

- LLMs are a subset of machine learning models known as **deep learning models** because they can handle **large-scale data** and **complex pattern recognition**.

- LLMs deliver **high performance in natural language processing (NLP) tasks**.

- **Generative AI (GenAI)** focuses on **creating new data and analyzing existing data**, enabling the model to **learn from patterns** and **generate novel outputs**.  
  - Example: Shifting from **classifying** a painting to **creating** a new painting.

- LLMs are **beneficial in data-limited contexts**, as they are pretrained on massive datasets, **reducing the need for extensive new data collection**.

- **Cost-effectiveness**: Since LLMs are pretrained, they **lower the costs** and **accelerate business integration** compared to training models from scratch.

---

### 1.2 In-Depth Definition of Large Language Models (LLMs)

---

### Definition

- **LLMs (Large Language Models)** are a specialized category of AI models that focus on:
  - **Processing** human language
  - **Understanding** language context and meaning
  - **Generating** human-like text

- LLMs belong to **deep learning models**, a subset of machine learning (ML) models, capable of managing **large datasets** and **complex pattern recognition**.

---

#### Architecture

- LLMs primarily use a **neural network architecture** called the **Transformer**.

- **Transformer Architecture** leverages a **self-attention mechanism** to:
  - Capture the relationships between words
  - Understand the context across long sequences of text
  - Enable models to focus dynamically on relevant parts of the input

---

#### Training Data

- LLMs are trained on **extensive and diverse text datasets**, including:
  - Books
  - Articles
  - Websites
  - Research papers

- **Diversity** of training sources is critical to building robust and generalized models.

---

#### Training Process

- LLMs typically use **unsupervised learning**:
  - The model is exposed to massive amounts of text without labeled outputs.
  - It learns **patterns, structures, and associations** in natural language.

- Example:  
  - **Next-word prediction** — the model learns to guess the next word based on the previous sequence.

---

#### Capabilities

LLMs can perform a wide range of natural language tasks, such as:
- **Text Translation**
- **Question and Answering (Q&A)**
- **Summarization**
- **Content Generation**
- **Sentiment Analysis**

---

#### Scale

- **Scale** refers to:
  - The **amount of training data** used
  - The **number of parameters** (weights) in the model

- **Higher scale** (more parameters and data) generally leads to **better performance**, enabling the model to understand complex language nuances.

---

#### Applications

- **Virtual Assistants** (e.g., SAP Digital Assistant)
- **Automation of Customer Support**
- **AI-powered Chatbots**
- **Content Creation and Drafting**
- **Knowledge Extraction and Search Enhancement**

---

#### Limitations

- **Bias in Training Data**:  
  - LLMs can inherit and even amplify biases present in the datasets they were trained on.
  - It is critical to curate and audit training data carefully to minimize ethical risks.

---

### 1.3 Benefits and Risks of LLMs

In the context of **SAP Business AI**, Large Language Models (LLMs) bring significant benefits, but they also introduce risks that must be carefully managed.

---

| Benefits                                          | Risks                                                    |
|---------------------------------------------------|----------------------------------------------------------|
| **Efficiency**: Improves process efficiency through the ability to understand and process natural language. | **Data Privacy Concerns**: LLMs process textual data, potentially causing data privacy or data leakage risks. |
| **Cost Reduction**: Automates customer support, data analysis, and other tasks, reducing operational costs. | **Bias and Fairness**: LLMs can reflect and reproduce biases inherent in their training datasets. |
| **Data Analysis**: Enables faster and more effective analysis and interpretation of large datasets. | **Misinterpretation of Data**: LLMs can misinterpret language and generate incorrect or misleading outputs. |
| **Scalability**: Can handle increasing volumes of interactions and workloads due to deep learning capabilities. | **Technical Complexity**: Fine-tuning, deploying, and maintaining LLMs require technical expertise and significant resources. |

---

#### Summary:

- **LLMs enhance productivity and innovation** but require **strict governance, data privacy controls, and ethical considerations** to ensure responsible usage within SAP solutions.

---

### 1.4 Further Reading

1. AI Ethics:

- Ethical AI Practices:
  - **Transparent**
  - **Accountable**
  - **Robust and reliable**
  - **Respectful of human rights**

- SAP has a dedicated framework for ethical AI, detailed in the official learning journey:  
  [🔗 AI Ethics: Putting AI Ethics into Practice at SAP](https://learning.sap.com/learning-journeys/putting-ai-ethics-into-practice-at-sap)

---

2. Generative AI Cybersecurity Strategy:

- Comprehensive cybersecurity approach for Generative AI, focusing on:
  - **Data protection**
  - **Model robustness**
  - **Secure development lifecycles**
  - **Continuous monitoring for threats**

- Key aspects of SAP’s GenAI cybersecurity strategy include:
  - Risk-based assessment of AI models
  - Secure handling of customer and training data
  - Protection against adversarial attacks
  - Compliance with international regulations

- Detailed documentation is available here:  
  [🔗 SAP Generative AI Cybersecurity Strategy (2024)](https://www.sap.com/documents/2024/01/5e4f6acf-a37e-0010-bca6-c68f7e60039b.html)

---

## 2. Describing SAP's Generative AI Strategy

### LLMs in SAP AI Core

- With these models, the SAP AI Core can perform tasks such as drafting e-mails, writing code, creating written content, translating languages, and much more. They enable users to generate coherent, contextually appropriate sentences and paragraphs in response to a given prompt.

- The SAP AI Core models can be trained, enabling them ot learn and improve over time on custom data

- In the context of Generative AI Hub, these models are typically used in SaaS setup. The models can be trained and hosted into the cloud and integrated directly into the applications, products or services

### SAP Business AI Approach

- SAP Business AI Approach provide business proess specific AI services

- Most use scenarios: Business Document Processing, Data Attribute Recommendation or Robotic Process Automation

- Embedded AI Capacilities with access directly to business data