# AI Intent Classifier

This project trains an intent classification model using **KLUE RoBERTa-large** for intent classification.

---

## Project Structure

```text
AI_Intent_Classifier/
 ├── main.ipynb
 ├── requirements.txt
 ├── README.md
 └── data/
      └── dataset.xlsx
```

---

## Setup

Install required packages:

```bash
pip install -r requirements.txt
```

---

## Dataset

The dataset is included in this repository.

File location:

```text
data/dataset.xlsx
```

The dataset must contain the following columns:

* text: input sentence
* label: integer label (0 ~ 44)

---

## Run

Open the Jupyter Notebook:

```text
main.ipynb
```

Run all cells in order.

---

## CPU / GPU Setting

The current code is configured for CPU environments:

```python
bf16=False
```

Training on CPU is very slow.

If you are using a CUDA-enabled GPU that supports bfloat16, you can modify:

```python
bf16=True
```

You can also enable bfloat16 when loading the model:

```python
torch_dtype=torch.bfloat16
```

Example:

```python
model = AutoModelForSequenceClassification.from_pretrained(
    MODEL_ID,
    num_labels=NUM_LABELS,
    torch_dtype=torch.bfloat16,
    device_map="auto",
)
```

If your GPU does not support bfloat16, keep:

```python
bf16=False
```

---

## Output

After execution:

* classification_report.txt
* confusion_matrix.png

---

## Model

* Base model: klue/roberta-large
* Fine-tuning: LoRA (PEFT)
* Number of labels: 45

---

## Results

| Model            | Top-1 Accuracy | Top-3 Accuracy |
|------------------|----------------|----------------|
| RoBERTa-large    | 0.9467         | 0.9970         |

- Top-1 Accuracy improved by approximately 10% after dataset refinement
- Top-3 Accuracy reached near 100%

---

## Notes

* CPU training is extremely slow
* GPU is recommended
* Dataset path should remain:

```text
data/dataset.xlsx
```
