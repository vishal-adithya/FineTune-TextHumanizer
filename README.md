---
license: apache-2.0
datasets:
- vishal-adithya/texthumanizer-preprocessed-data
language:
- en
metrics:
- accuracy
base_model:
- mistralai/Ministral-8B-Instruct-2410
library_name: mlx
tags:
- mlx
- finetune
model-index:
- name: Th-4bit
  results:
  - task:
      type: text-generation
    dataset:
      name: train
      type: train
    metrics:
    - name: Training Loss
      type: loss
      value: 0.171
  - task:
      type: text-generation
    dataset:
      name: validation
      type: validation
    metrics:
    - name: Validation Loss
      type: loss
      value: 0.175
  - task:
      type: text-generation
    metrics:
    - name: Learning Rate
      type: lr
      value: 0.00001
  - task:
      type: text-generation
    metrics:
    - name: Tokens per sec
      type: t/sec
      value: 117.298
---


# TextHumanizer - Fine-tuned Ministral-8B-Instruct:

**TextHumanizer** is a fine-tuned version of the [`Ministral-8B-Instruct`](https://huggingface.co/mistralai/Ministral-8B-Instruct-2410) model. It is designed to transform robotic, overly-formal, or synthetic AI-generated text into fluent, natural, and human-like language.

This model was fine-tuned using Apple's [MLX framework](https://github.com/ml-explore/mlx) on a custom dataset of AI-generated text paired with humanized rewrites.

---

## Model Details:

- **Base model**: `mistralai/Ministral-8B-Instruct`
- **Model size**: 8B parameters
- **Fine-tuned using**: MLX (Apple Silicon-native training)
- **Fine-tuning method**: QLora
- **Precision**: float16
- **Hardware used**: Apple Silicon M1 Macbook Pro
- **Training time**: 10 mins
- **Epochs / Steps**: 200
- **Batch size**: 4

---

## Training Metrics:

| Metric               | Value      |
|----------------------|------------|
| Final Training Loss  | `0.171` |
| Final Validation Loss| `0.175` |

---

## Dataset:

- **Source**: Custom synthetic-to-human text pairs
- **Size**: 10k rows
- **Structure**: Pairs of `(synthetic_input, humanized_output)`
- **Preprocessing**: Standard MLX tokenization, formatting for instruct tuning
- **License**: Public

---

##  Capabilities:

TextHumanizer is designed to:

- Improve fluency and tone of AI outputs
- Make answers sound more relatable and natural
- Polish robotic or overly formal language

---

### MLX (Apple Silicon):

```python
from mlx_lm import load, generate

model, tokenizer = load("vishal-adithya/ministral-8B-texthumanizer")
prompt = "Instruction: Make this sound more natural.Input: The individual proceeded to consume nourishment.Response:"
generate(model, tokenizer, prompt)