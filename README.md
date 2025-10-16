# bert-turkish-sentiment-analysis
This model is a fine-tuned version of dbmdz/bert-base-turkish-cased on the winvoker/turkish-sentiment-analysis-dataset.
model : https://huggingface.co/yusufalt46/bert-turkish-sentiment-analysis
---
library_name: transformers
license: mit
datasets:
- winvoker/turkish-sentiment-analysis-dataset
language:
- tr
base_model:
- dbmdz/bert-base-turkish-cased
tags:
- text
- turkish
- bert
---

### Model Description
This model is a fine-tuned version of **dbmdz/bert-base-turkish-cased** on the **winvoker/turkish-sentiment-analysis-dataset**.

- Shuffle function was applied during preprocessing.
- **Training dataset:** 229,483 samples
- **Test dataset:** 57,371 samples
- **Total dataset:** 286,854 samples

This model is designed for **Turkish sentiment analysis**, classifying texts as either **Positive (1)** or **Negative (0)**.

**Training Details:**

**Training dataset**

- **Dataset**: winvoker/turkish-sentiment-analysis-dataset
- **Training**: 229,483 samples
- **Testing**: 57,371 samples
- **Preprocessing**: shuffle and truncate/pad to 128 tokens

**Training Procedure**

**Fine-tuned using Hugging Face Transformers Trainer**

- **Learning rate**: 2e-5
- **Batch size**: 16
- **Epochs:** 2
- **Optimizer:** AdamW
- **Weight decay**: 0.01

**Evaluation**

- **Eval Loss**: 0.1505
- **Accuracy**: 0.9614
- **F1 Score**: 0.9767
- **Epoch**: 2

**Label Mapping**

- **LABEL_1 = Positive (1)**

- **LABEL_0 = Negative (0)**



- **Developed by:** Yusuf Altunbaş  
- **Model type:** Sequence Classification  
- **Language(s):** Turkish  
- **License:** MIT  
- **Finetuned from model:** dbmdz/bert-base-turkish-cased  

### Model Sources
- **Repository:** [GitHub Notebook](https://github.com/Yusufaltnbs/bert-turkish-sentiment-analysis/blob/main/bert-turkish-sentiment-analysis.ipynb)

## Uses

### Direct Use
- The model can be directly used for predicting the sentiment of Turkish text using the Hugging Face `transformers` library.

### Downstream Use
- Can be integrated into larger NLP pipelines, sentiment analysis dashboards, or recommendation systems.

### Out-of-Scope Use
- This model is **not trained for neutral or multi-class sentiment beyond Positive/Negative**.
- Not suitable for languages other than Turkish.

## Bias, Risks, and Limitations
- The model is trained on **winvoker/turkish-sentiment-analysis-dataset**.  
- It may reflect biases present in the dataset.  
- Misuse or misinterpretation of predictions can occur; always review results in context.

## How to Get Started with the Model
### Using Hugging Face Pipeline
```python
from transformers import pipeline

text = "Bugün çok mutluyum!"
model_id = "yusufalt46/bert-turkish-sentiment-analysis"

classifier = pipeline("text-classification", model=model_id, tokenizer=model_id)
preds = classifier(text)
print(preds)

# Example output:
# [{'label': 'LABEL_1', 'score': 0.9823}]  # 1 = Positive

from transformers import AutoTokenizer, AutoModelForSequenceClassification
import torch

tokenizer = AutoTokenizer.from_pretrained("yusufalt46/bert-turkish-sentiment-analysis")
model = AutoModelForSequenceClassification.from_pretrained("yusufalt46/bert-turkish-sentiment-analysis")

text = "Bu ürün harika!"
inputs = tokenizer(text, return_tensors="pt", padding=True, truncation=True, max_length=128)
outputs = model(**inputs)
pred = torch.argmax(outputs.logits, dim=-1)
print(pred.item())  # 1: Positive, 0: Negative

Yusuf Altunbaş, bert-turkish-sentiment-analysis, Hugging Face Model Hub, 2025
