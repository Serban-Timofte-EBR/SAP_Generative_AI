# Training an ML Model with SAP AI Core

---

Training a machine learning model in SAP AI Core follows a **structured and modular pipeline**, combining data, executable logic, and infrastructure to produce deployable AI services.

---

## Step 1 – Dataset Preparation and Object Store Integration

To start model training:

- A **training dataset must be made accessible** to SAP AI Core.
- This is typically done by **storing the dataset in a hyperscaler object store** (e.g., Azure Blob Storage, AWS S3, GCP Buckets).

### Why use an Object Store?

- A **Hyperscale Object Store** provides:
  - High scalability
  - Cost efficiency
  - Redundancy and durability
- It is the **preferred method** to store datasets, trained models, and other AI artifacts.

### SAP AI Core Access

- You must configure **access rights and credentials** to allow SAP AI Core to read/write to the object store.
- The connection is declared in the pipeline configuration YAML files.

---

## Segregation of AI Artifacts Using Resource Groups

To ensure **data isolation and controlled access**, assets can be organized via **Resource Groups**:

- **AI Artifacts** include:
  - Input dataset
  - Executable training scripts
  - Output models
  - Logs and metrics

- Resource Group governance:
  - Input datasets are **only visible** to users assigned to that group.
  - But they are **accessible across all components** in that group (e.g., training pipeline, evaluation scripts).

📌 You can run the same training pipeline multiple times with **different input datasets**, resulting in **different trained models**, all within the same resource group.

---

## Creating a Training Configuration

To train a model in SAP AI Core, you must define a **training configuration**, composed of:

- An **executable**: a Docker-based script defining the training process.
- A **dataset reference**: path to training data in the object store.
- A **ML definition that links data, code, and infrastructure.
- An optional **parameter set**: hyperparameters or runtime options.

🛠️ These configurations are **registered via API or YAML manifespipeline template**: YAt** in SAP AI Core.

---

## Triggering the Training Pipeline Execution

Once configured, the training is executed as a **workflow job**. Key concepts:

### Executable

- Includes:
  - The **input/output logic**
  - The **container image** to use
  - Metadata and labels

### Resource Plans

- SAP AI Core provides **predefined infrastructure bundles** called **Resource Plans**.
- Each plan defines:
  - Number of **vCPUs**
  - Amount of **memory**
  - GPU availability (if required)
- Choose the appropriate plan based on model complexity.

---

## Model Evaluation and Metrics Logging

During or after training, you should evaluate model quality.

- SAP AI Core allows you to **register and track metrics** using the API.
  - Accuracy
  - Precision/Recall
  - Loss
- These metrics can be:
  - Written to logs
  - Displayed in **SAP AI Launchpad**
  - Retrieved programmatically for dashboards

📊 Metric logging is **customizable** based on your evaluation logic.

---

## Monitoring and Logging with AI Launchpad

Once a training job is triggered:

- You can use **SAP AI Launchpad** to:
  - View job status (Running, Completed, Failed)
  - Inspect logs and errors
  - Monitor resource usage
  - Access registered metrics

This helps you understand **training performance**, debug failures, or validate the quality of your model.

---

## Model Registration and Storage

After successful training:

- The trained model is:
  - Stored in the same **hyperscaler object store**.
  - **Automatically registered** as a **model artifact** in SAP AI Core.
- The model is now:
  - Versioned
  - Traceable
  - Ready for deployment and serving

🚀 This concludes the end-to-end training lifecycle:  
from dataset → configuration → training → evaluation → registration.

---

## ✅ Summary Table

| Step                       | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Dataset Setup              | Upload to object store, configure access                                   |
| Resource Group Assignment  | Logical separation of assets for isolation and reuse                       |
| Training Configuration     | Define executable, dataset, pipeline template, resource plan               |
| Pipeline Execution         | Launch job in SAP AI Core using selected infrastructure plan               |
| Metric Evaluation          | Register and retrieve model performance metrics                            |
| Monitoring with Launchpad  | Track execution, logs, metrics in the web UI                               |
| Model Storage & Registration | Save model artifacts, automatically register in SAP AI Core registry     |

---
