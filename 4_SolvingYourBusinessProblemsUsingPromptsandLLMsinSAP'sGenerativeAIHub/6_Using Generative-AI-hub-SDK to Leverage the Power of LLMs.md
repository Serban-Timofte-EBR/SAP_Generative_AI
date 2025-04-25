# Using Generative-AI-hub-SDK to Leverage the Power of LLMs

## Loading Packages & Data

- We begin with installing packages and then loading data:

```bash
!pip install -U "generative-ai-hub-sdk>=3.1" tqdm
```

- The "tqdm" package is a progress bar library that helps display the progress of tasks in the console.

```python
from typing import Literal, Type, Union, Dict, Any, List, Callable
import re, pathlib, json, time
from functools import partial
EXAMPLE_MESSAGE_IDX = 10
```

- This code begins by importing necessary modules and types from various Python libraries

- Next, you need to **load and preprocess a dataset** of emails stored in a JSON file. You can **split dataset into development and testing** sets with a smaller test set created for more focused evaluation. You can also process email data, to extract and organize categories, urgency, and sentiment into sets for further analysis.

## Helper Functions

- Before developing prompts using generative-ai-hub-sdk, you need to **enable the use of AI models** in generative AI hub. This is **done through helper functions**.
