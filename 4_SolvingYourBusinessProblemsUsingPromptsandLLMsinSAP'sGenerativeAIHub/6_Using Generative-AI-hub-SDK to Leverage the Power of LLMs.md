# Using Generative-AI-hub-SDK to Leverage the Power of LLMs

---

## Loading Packages & Data

To start working with SAP's Generative AI Hub SDK, you must first **install the required Python packages** and **load your data**.

### Installation

```bash
!pip install -U "generative-ai-hub-sdk>=3.1" tqdm
```

- *generative-ai-hub-sdk*: Main SAP package to interact with AI Orchestration services.

- *tqdm*: Utility library to show progress bars during loops and time-consuming operations.

### Imports

```python
from typing import Literal, Type, Union, Dict, Any, List, Callable
import re, pathlib, json, time
from functools import partial
EXAMPLE_MESSAGE_IDX = 10
```

- These imports bring standard libraries for:
  - Type hinting
  - Regular expressions
  - Path operations
  - JSON processing
  - Timing and delays
  - Function customization (partial functions)

### Data Preparation

- Load and preprocess datasets (e.g., emails) stored in .json files.

- Typical preprocessing includes:
  - Splitting into development and testing sets.
  - Extracting metadata like:
    - Categories (e.g., support, finance, hr)
    - Urgency levels (e.g., high, medium, low)
    - Sentiment (e.g., positive, negative, neutral)

- Well-structured datasets allow more accurate prompt testing and model evaluation.

- **Important**: Data should be split to ensure:
  - Development data → for training prompts and tuning.
  - Test data → for unbiased evaluation.

## Helper Functions

- Before developing and running prompts via the SDK, you must establish a connection with SAP AI Core through helper functions.

### Key Concepts

- Proxy Client: Securely connects your local environment to SAP AI Orchestration APIs.

- Deployment Retrieval or Trigger: Find existing orchestration deployment or trigger a new one.

- Orchestration Service: Object that wraps all communications with SAP AI Hub Orchestration Service.

### Example Helper Code

```python
import pathlib
import yaml

from gen_ai_hub.proxy import get_proxy_client
from ai_api_client_sdk.models.status import Status

from gen_ai_hub.orchestration.models.config import OrchestrationConfig
from gen_ai_hub.orchestration.models.llm import LLM
from gen_ai_hub.orchestration.models.message import SystemMessage, UserMessage
from gen_ai_hub.orchestration.models.template import Template, TemplateValue
from gen_ai_hub.orchestration.models.content_filter import AzureContentFilter
from gen_ai_hub.orchestration.service import OrchestrationService

client = get_proxy_client()
deployment = retrieve_or_deploy_orchestration(client.ai_core_client)
orchestration_service = OrchestrationService(api_url=deployment.deployment_url, proxy_client=client)

def send_request(prompt, _print=True, _model='meta--llama3-70b-instruct', **kwargs):
    config = OrchestrationConfig(
        llm=LLM(name=_model),
        template=Template(messages=[UserMessage(prompt)])
    )
    template_values = [TemplateValue(name=key, value=value) for key, value in kwargs.items()]
    answer = orchestration_service.run(config=config, template_values=template_values)
    result = answer.module_results.llm.choices[0].message.content
    if _print:
        formatted_prompt = answer.module_results.templating[0].content
        print(f"<-- PROMPT --->\n{formatted_prompt if _print else prompt}\n<--- RESPONSE --->\n{result}")   
    return result
```

**What This Code Does:**

- get_proxy_client(): Establishes the connection to SAP AI Hub securely.

- retrieve_or_deploy_orchestration(): Either connects to an existing orchestration or deploys a new one.

- send_request():
  - Prepares a prompt.
  - Selects the LLM (default: Meta Llama 3 70B instruct).
  - Sends prompt to the orchestration endpoint.
  - Returns and prints the model's response.

- **Important**
  - Helper functions are mandatory for:
    - Triggering prompts.
    - Managing deployments automatically.
    - Monitoring LLM responses with templated outputs.

## Develop a Prompt Using generative-AI-hub-SDK

- Once connectivity is ready, you can develop, test, and optimize prompts using the SAP Generative AI Hub SDK.

Steps:

1. Prepare a prompt:
    - The input text/question/task you want the LLM to process.

2. Send it using send_request():
    - The SDK will automatically package your prompt into the appropriate format.
    - It will send it through the AI Orchestration Service endpoint.

3. Receive and process the output:
    - The model's response is extracted and can be printed or stored.

### Example

```python
prompt = "Summarize the key points from the attached customer support email regarding delivery delays."
response = send_request(prompt)
print(response)
```

### Behind the scenes

- Templates are dynamically generated in the SDK to match the prompt to the model input structure.

- Models are referenced by names like:
  - meta--llama3-70b-instruct
  - openai--gpt-4

- Optional parameters (temperature, max tokens, etc.) can be passed through **kwargs in send_request().

**Important:**

- SAP Generative AI Hub SDK uses orchestration templates internally.

- Best practices include prompt templating, temperature control, and result handling for business applications.

- The orchestration workflow ensures secure, scalable, and enterprise-grade LLM consumption.
