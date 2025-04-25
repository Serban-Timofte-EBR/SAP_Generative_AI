# Serving an ML Model with SAP AI Core

---

Once a machine learning model is trained and validated, the next step is to make it **available for consumption** through **model serving**, also called **inference**.

---

## What Is Model Serving?

- **Model Serving (or Inferencing)** refers to:
  - **Deploying a trained model** as an API service.
  - Accepting **new data (input)** via HTTP request.
  - Returning a **predicted output** based on the model.

📌 Inference = "using" the trained model to generate real-time or batch predictions.

---

## Model Deployment in SAP AI Core

After training, SAP AI Core allows you to **deploy the model** by:

1. Defining a **serving application** (executable).
2. Referencing the **trained model artifact** (stored in object store).
3. Launching a **deployment job** via configuration templates.

Once deployed, SAP AI Core exposes an **HTTP(S) endpoint** to:

- Send new data (in JSON format).
- Receive prediction output.
- Integrate this into other SAP or custom applications.

---

## Kubernetes Scaling for Inference

SAP AI Core uses **Kubernetes** behind the scenes to deploy and scale model serving jobs:

### 🔄 On-Demand Scaling

1. **Auto-Scaling**:
   - When inference requests increase, Kubernetes **clones the container automatically**.
   - Supports **horizontal scaling** for large-volume, low-latency applications.

2. **Scale to Zero**:
   - When no requests are received, containers are automatically shut down.
   - Great for **cost efficiency** and **pay-per-use** pricing.
   - When needed again, the containers are restarted automatically.

📌 This is especially important in enterprise settings where **resource optimization** is critical.

---

## 10.4 Serving Application (Model Server)

To serve a model, you need to build a **serving application**, usually a **Docker container** that performs:

- **Step 1**: Accepts inference requests via HTTP.
- **Step 2**: Extracts request data from the payload.
- **Step 3**: Loads the model from the hyperscaler object store.
- **Step 4**: Applies the model to the input data.
- **Step 5**: Returns a formatted prediction result.

This serving logic is defined as an **Executable Template** in SAP AI Core, specifying:

- The Docker image to use
- Required compute resources (via resource plan)
- Access to the trained model location
- Environment variables and startup commands

---

## 10.5 Deployment & Integration Flow

1. The customer pushes a **deployment configuration** (YAML) that links:
   - Model serving executable
   - Trained model path
   - Resource plan

2. SAP AI Core spins up a **model server** (in containerized form).

3. Once active, an **endpoint URL** is exposed for inference requests.

4. The model can now be consumed using:
   - **Postman** (manual testing)
   - **Jupyter Notebook** (interactive testing)
   - **CAP applications** (business application integration)
   - **Any HTTP client**

---

## 10.6 Summary Table

| Component              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| Model Serving          | Deploying trained model to produce predictions on new input                 |
| Kubernetes             | Auto-scales model servers; supports cost-efficiency with "scale to zero"    |
| Serving App (Executable)| Web service that loads model and handles prediction requests               |
| Deployment Template    | YAML file defining serving logic, model reference, and resource needs       |
| Inference Endpoint     | Exposed HTTP URL used by clients to send data and receive predictions       |
| Integration Clients    | Tools like Postman, Jupyter, CAP-based applications                         |

---

## ✅ Example Integration Flow

```plaintext
[User Input or Business App] 
        ↓
[HTTP Request] —→ [Serving Endpoint @ SAP AI Core]
                        ↓
            [Model Server (Container)]
                        ↓
       [Prediction Computation + Response]
                        ↓
[Business App receives output]
