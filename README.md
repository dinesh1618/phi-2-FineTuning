# Fine-Tuning Microsoft Phi-2 Model

This repository provides a detailed workflow for fine-tuning the `microsoft/phi-2` model on a custom dataset, specifically for mental health counseling conversations. The process leverages parameter-efficient fine-tuning techniques, such as LoRA, to adapt the model effectively.

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Dataset Preparation](#dataset-preparation)
- [Fine-Tuning](#fine-tuning)
- [Evaluation](#evaluation)
- [Usage](#usage)
- [License](#license)

## Overview

This project demonstrates how to fine-tune the `phi-2` model for causal language modeling tasks. The primary focus is to use mental health counseling conversations to adapt the model for generating helpful and empathetic responses.

## Installation

To run the notebook, ensure the required dependencies are installed:

```bash
!pip install bitsandbytes accelerate transformers peft einops torch datasets trl -q
```

## Dataset Preparation

1. **Dataset Source**:
   - The dataset used in this project is `Amod/mental_health_counseling_conversations`.

2. **Loading the Dataset**:
   ```python
   from datasets import load_dataset
   dataset_name = "Amod/mental_health_counseling_conversations"
   dataset = load_dataset(dataset_name)
   ```

3. **Data Transformation**:
   The dataset is processed and transformed to prepare it for model training. The transformations are saved to a CSV file for reuse:
   ```python
   transformmed_data.to_csv("transformed_data.csv", index=False)
   dataset = load_dataset("csv", data_files="/content/transformed_data.csv", split="train")
   ```

## Fine-Tuning

1. **Base Model**:
   - `microsoft/phi-2` is used as the base model.
   - The tokenizer is initialized with configurations for causal language modeling.

2. **LoRA Configuration**:
   - LoRA (Low-Rank Adaptation) is applied for efficient fine-tuning:
     ```python
     peft_config = LoraConfig(...)
     ```

3. **Training**:
   - Training is performed using `SFTTrainer` from the `transformers` library:
     ```python
     trainer = SFTTrainer(...)
     trainer.train()
     ```

## Evaluation

After fine-tuning, the model is evaluated for its ability to generate empathetic and coherent responses. Example:

```python
from transformers import pipeline
prompt = "I am unable to sleep at night. do you have any suggestions?"
response = pipeline(prompt)
```

## Usage

The fine-tuned model can be integrated into applications for generating contextually appropriate responses for mental health counseling or similar use cases.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
