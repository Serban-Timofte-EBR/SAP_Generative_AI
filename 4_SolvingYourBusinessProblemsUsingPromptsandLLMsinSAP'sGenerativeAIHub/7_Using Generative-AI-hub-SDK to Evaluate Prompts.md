# Using Generative-AI-hub-SDK to Evaluate Prompts

- You need automated and consistent evaluation of prompts across various scenarios, ensuring reliability and efficiency.

- For this you need to create custom evaluation functions using generative-ai-hub-sdk.

- Using an SDK for evaluating prompts offers the following benefits:
  - Reliable Testing: SDKs automate testing of prompts across various scenarios, ensuring consistent and efficient results.
  - Measuring Performance: They provide objective metrics such as relevance, coherence, and fluency to quantitatively assess response quality.
  - Tailored Evaluations: SDKs allow you to create custom evaluators that meet specific needs, enabling more precise and relevant assessments.
  - Scalable Results: They support large-scale evaluations, making it easier to test prompts on extensive datasets.

## Implementating Evaluation Functions

1. We start the evaluation with the import of packages.

```python
from tqdm.auto import tqdm
import time


class RateLimitedIterator:
    def __init__(self, iterable, max_iterations_per_minute):
        self._iterable = iter(iterable)
        self._max_iterations_per_minute = max_iterations_per_minute
        self._min_interval = 1.0 / (max_iterations_per_minute / 60.)
        self._last_yield_time = None

    def __iter__(self):
        return self

    def __next__(self):
        current_time = time.time()

        if self._last_yield_time is not None:
            elapsed_time = current_time - self._last_yield_time
            if elapsed_time < self._min_interval:
                time.sleep(self._min_interval - elapsed_time)

        self._last_yield_time = time.time()
        return next(self._iterable)
```

- The code defines a "RateLimitedIterator" class to control the rate at which you can iterate over an iterable. By specifying a maximum number of iterations per minute, it ensures that the iteration process adheres to a defined speed, preventing hitting rate limits. It uses the "tqdm" library for progress visualization and the "time" module for timing control.

2. Next we define an evaluation function

```python
def evaluation(mail: Dict[str, str], extract_func: Callable, _print=True, **kwargs):
    response = extract_func(input=mail["message"], _print=_print, **kwargs)
    result = {
        "is_valid_json": False,
        "correct_categories": False,
        "correct_sentiment": False,
        "correct_urgency": False,
    }
    try:
        pred = json.loads(response)
    except json.JSONDecodeError:
        result["is_valid_json"] = False
    else:
        result["is_valid_json"] = True
        result["correct_categories"] = 1 - (len(set(mail["ground_truth"]["categories"]) ^ set(pred["categories"])) / len(categories))
        result["correct_sentiment"] = pred["sentiment"] == mail["ground_truth"]["sentiment"]
        result["correct_urgency"] = pred["urgency"] == mail["ground_truth"]["urgency"]
    return result
evaluation(mail, f_8)
```

3. We'll implement an evaluation function for a large number of mails to support large-scale evaluations, making it easier to test prompts on extensive datasets.

```python
from tqdm.auto import tqdm

def transpose_list_of_dicts(list_of_dicts):
    keys = list_of_dicts[0].keys()
    transposed_dict = {key: [] for key in keys}
    for d in list_of_dicts:
        for key, value in d.items():
            transposed_dict[key].append(value)
    return transposed_dict

def evalulation_full_dataset(dataset, func, rate_limit=100, _print=False, **kwargs):
    results = [evaluation(mail, func, _print=_print, **kwargs) for mail in tqdm(RateLimitedIterator(dataset, rate_limit), total=len(dataset))]
    results = transpose_list_of_dicts(results)
    n = len(dataset)
    for k, v in results.items():
        results[k] = sum(v) / len(dataset)
    return results


def pretty_print_table(data):
    # Get all row names (outer dict keys)
    row_names = list(data.keys())

    # Get all column names (inner dict keys)
    if row_names:
        column_names = list(data[row_names[0]].keys())
    else:
        column_names = []

    # Calculate column widths
    column_widths = [max(len(str(column_name)), max(len(f"{data[row][column_name]:.2f}") for row in row_names)) for column_name in column_names]
    row_name_width = max(len(str(row_name)) for row_name in row_names)

    # Print header
    header = f"{'':>{row_name_width}} " + " ".join([f"{column_name:>{width}}" for column_name, width in zip(column_names, column_widths)])
    print(header)
    print("=" * len(header))

    # Print rows
    for row_name in row_names:
        row = f"{row_name:>{row_name_width}} " + " ".join([f"{data[row_name][column_name]:>{width}.1%}" for column_name, width in zip(column_names, column_widths)])
        print(row)

overall_result = {}
```

This code now performs evaluation on the entire dataset, evaluates each entry through a function with rate limiting, transposes the results for better aggregation, and then pretty-prints the final evaluation metrics in a tabular format. It uses the "tqdm" library to show a progress bar, making it easier to track processing status. The entire flow ensures streamlined, efficient processing and clear presentation of results.

4. Implement the final function to the final combined function.

```python
overall_result["basic--llama3-70b"] = evalulation_full_dataset(test_set_small, f_8)
pretty_print_table(overall_result)
```
