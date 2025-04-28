# Implementing Advanced Prompt Engineering Techniques

## Few-Shot Prompting

```python

prompt_10 = """Your task is to extract and categorize messages. Here are some example:
---
{{?few_shot_examples}}
---
Use the examples when extract and categorize the following message:
---
{{?input}}
---
Extract and return a json with the follwoing keys and values:
- "urgency" as one of {{?urgency}}
- "sentiment" as one of {{?sentiment}}
- "categories" list of the best matching support category tags from: {{?categories}}
Your complete message should be a valid json string that can be read directly and only contain the keys mentioned in the list above. Never enclose it in ```json...```, no newlines, no unnessacary whitespaces.
"""

import random
random.seed(42)

k = 3
examples = random.sample(dev_set, k)

example_template = """<example>
{example_input}

## Output

{example_output}
</example>"""

examples = '\n---\n'.join([example_template.format(example_input=example["message"], example_output=json.dumps(example["ground_truth"])) for example in examples])


f_10 = partial(send_request, prompt=prompt_10, few_shot_examples=examples, **option_lists)

response = f_10(input=mail["message"])
```

- The code aims to create a prompt template to extract and categorize messages according to their urgency, sentiment, and support category tags. By using randomly selected examples from a development set, it generates a formatted few-shot learning prompt. The prompt is sent to a language model to process and categorize a given input message, and the overall performance of the model is then evaluated and displayed in a table format.

## Metaprompting

```python

example_template_metaprompt = """<example>
{example_input}

## Output
{key}={example_output}
</example>"""

prompt_get_guide = """Here are some example:
---
{{?examples}}
---
Use the examples above to come up with a guide on how to distinguish between {{?options}} {{?key}}.
Use the following format:
```

### **<category 1>**

- <instruction 1>
- <instruction 2>
- <instruction 3>

### **<category 2>**

- <instruction 1>
- <instruction 2>
- <instruction 3>
...

```
When creating the guide:
- make it step-by-step instructions
- Consider than some labels in the examples might be in correct
- Avoid including explicit information from the examples in the guide
The guide has to cover: {{?options}}
"""

guides = {}

for i, key in enumerate(["categories", "urgency", "sentiment"]):
    options = option_lists[key]
    selected_examples_txt_metaprompt = '\n---\n'.join([example_template_metaprompt.format(example_input=example["message"], key=key, example_output=example["ground_truth"][key]) for example in dev_set])
    guides[f"guide_{key}"] = send_request(prompt=prompt_get_guide, examples=selected_examples_txt_metaprompt, key=key, options=options, _print=False, _model='gpt-4o')
print(guides['guide_urgency'])
```

example_template_metaprompt = """<example>
{example_input}

## Output

{key}={example_output}
</example>"""

prompt_get_guide = """Here are some example
---

{{?examples}}
---

Use the examples above to come up with a guide on how to distinguish between {{?options}} {{?key}}.
Use the following format:

```
### **<category 1>**
- <instruction 1>
- <instruction 2>
- <instruction 3>
### **<category 2>**
- <instruction 1>
- <instruction 2>
- <instruction 3>
...
```

When creating the guide:

- make it step-by-step instructions
- Consider than some labels in the examples might be in correct
- Avoid including explicit information from the examples in the guide
The guide has to cover: {{?options}}
"""

guides = {}

for i, key in enumerate(["categories", "urgency", "sentiment"]):
    options = option_lists[key]
    selected_examples_txt_metaprompt = '\n---\n'.join([example_template_metaprompt.format(example_input=example["message"], key=key, example_output=example["ground_truth"][key]) for example in dev_set])
    guides[f"guide_{key}"] = send_request(prompt=prompt_get_guide, examples=selected_examples_txt_metaprompt, key=key, options=options,_print=False, _model='gpt-4o')
print(guides['guide_urgency'])

- This code generates step-by-step guides for different categories—like "categories," "urgency," and "sentiment"—from labeled examples in a dataset.

- It creates tailored guides for distinguishing between categories, urgency, and sentiment in text data. It formats examples using a specific template, then sends these examples to a model for generating step-by-step instructions. The guides help users distinguish between these categories based on patterns in the provided examples.

1. Template Definitions:
    - "example_template_metaprompt": Defines a template to format examples, specifying how to structure input and output within an example.
    - "prompt_get_guide": Outlines a prompt format to request the generation of a guide based on formatted examples. It also specifies the format and requirements for the guide, including making it a step-by-step instruction, accounting for possible incorrect labels, and avoiding explicit replication of the examples.

2. Guide Preparation:
    - The script iterates over three keys: "categories", "urgency", and "sentiment".
    - For each key, it retrieves relevant options from "option_lists".

3. Example Selection and Formatting: It formats examples from "dev_set" using the predefined template for each key, embedding the input message and corresponding ground truth.

4. Guide Generation:
    - It sends a formatted prompt along with the examples to a model (gpt-4o), requesting the generation of a guide for distinguishing between the specified options for each key.
    - It stores the generated guides in a dictionary (guides), with each guide associated with its respective key (for example, "guide_categories", "guide_urgency", "guide_sentiment").

## Combining Metaprompting and Few-shot Prompting

```python

prompt_13 = """Your task is to classify messages.
Here are some examples:
---
{{?few_shot_examples}}
---
This is an explanation of `urgency` labels:
---
{{?guide_urgency}}
---
This is an explanation of `sentiment` labels:
---
{{?guide_sentiment}}
---
This is an explanation of `support` categories:
---
{{?guide_categories}}
---
Giving the following message:
---
{{?input}}
---
extract and return a json with the following keys and values:
- "urgency" as one of {{?urgency}}
- "sentiment" as one of {{?sentiment}}
- "categories" list of the best matching support category tags from: {{?categories}}
Your complete message should be a valid json string that can be read directly and only contain the keys mentioned in the list above. Never enclose it in ```json...```, no newlines, no unnecessary whitespaces.
"""

f_13 = partial(send_request, prompt=prompt_13, **option_lists, few_shot_examples=examples, **guides)

response = f_13(input=mail["message"])
```
