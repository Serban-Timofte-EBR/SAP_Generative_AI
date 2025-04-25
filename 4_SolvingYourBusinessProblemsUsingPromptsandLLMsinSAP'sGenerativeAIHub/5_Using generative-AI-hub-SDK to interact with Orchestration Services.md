# Using generative-AI-hub-SDK to interact with Orchestration Services

## Need for Orchestration

- Business scenarios usually require more than the bare consumption of Foundation Models for generative tasks. They need to scale, secure, and manage these solutions.

![orchestration](../img/orchestration.png)

- Acces to Generative AI should be combined with:
  - Prompting models using scenario-specific templates from a Prompt Repository.
  - Ensuring compliance with AI Ethics and Responsible AI through Content Filtering.
  - Maintaining data privacy by using Data Masking techniques.
    Enhancing models with business context through Retrieval-Augmented Generation (RAG).

- You need a service for coordinating and managing the deployment, integration, and interaction of various AI components. This can be an erroneous and time-consuming process leading to complex and redundant code and workflows. => We are using orchestration to help us.

## AI Orchestration

- AI orchestration is the process of coordinating and managing how various AI components are **deployed, integrated, and interact** within a system or workflow.

- We can use orchestration services for different foundational models without changing the client code.

## Introduction to Orchestration in Business AI

1. **Templating**: Templating allows you to create prompts with placeholders that the system fills during inference.

2. **Content Filtering**: Content filtering lets you control the type of content that's sent to and received from a generative AI model.

3. **Orchestration Workflow**: In a basic orchestration setup, you can combine different modules into a pipeline executed with a single API call. Each module's response serves as the input for the next module.

4. **Configuration and Execution**: Orchestration defines the execution order of the pipeline centrally. You can configure each module's details and exclude optional modules by passing a JSON-formatted orchestration configuration in the request body.

5. **Harmonized API**: The harmonized API enables the use of different foundational models without changing the client code. It uses the OpenAI API as a standard and maps other model APIs to it. This includes standardizing message formats, model parameters, and response formats. The harmonized API integrates into the templating module, model configuration, and orchestration response.

## Example

1. Defining template

```python
from gen_ai_hub.orchestration.models.message import SystemMessage, UserMessage
from gen_ai_hub.orchestration.models.template import Template, TemplateValue

template = Template(
    messages=[
        SystemMessage("You are a helpful translation assistant."),
        UserMessage(
            "Translate the following text to {{?to_lang}}: {{?text}}"
        ),
    ],
    defaults=[
        TemplateValue(name="to_lang", value="German"),
    ],
)
```

2. Defining LLM

```python
from gen_ai_hub.orchestration.models.llm import LLM

llm = LLM(name="gpt-4o", version="latest", parameters={"max_tokens": 256, "temperature": 0.2})
```

3. Create the Orchestration Configuration

```python
from gen_ai_hub.orchestration.models.config import OrchestrationConfig

config = OrchestrationConfig(
    template=template,
    llm=llm,
)
```

OrchestrationConfig using the template and LLM variables. This setup is necessary to configure the orchestration process, ensuring the system uses the specified template and language model parameters.

4. Run the Orchestration Request

```python
from gen_ai_hub.orchestration.service import OrchestrationService

orchestration_service = OrchestrationService(api_url=YOUR_API_URL, config=config)
result = orchestration_service.run(template_values=[
    TemplateValue(name="text", value="The Orchestration Service is working!")
])
print(result.orchestration_result.choices[0].message.content)
```

This code leverages the OrchestrationService to run a predefined task using specific template values. It connects to the service through the provided API URL and configuration, executes the task by supplying a text value, and then prints the resulting content. The code ensures streamlined communication with the orchestration system and retrieval of results.
