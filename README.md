# README

## Project structure

```
│   .gitignore
│   README.md
│   requirements.txt
│
├───BaselineOutput
│       combined_predictions_model1.jsonl
│       combined_predictions_model2.jsonl
│       sent_only_predictions_model1.jsonl
│       sent_only_predictions_model2.jsonl
│       table_only_predictions_model1.jsonl
│       table_only_predictions_model2.jsonl
│
├───data
│       data.jsonl
│       retrieved_data_3.jsonl
│
└───Scripts
    ├───Retriever
    │       retriever.py
    │       sent_retriever.py
    │       table_retriever.py
    │       verification.py
    │
    └───VerdictPredictor
            evaluate.py
            RoBERTa.py
            RoBERTa_NLI.py
            Roberta_NLI_NEI.py
            utils.py
```

## Files overview

* **BaselineOutput** – Contains retrieved evidence and the model’s predicted verdicts for each claim in the test set. It holds predictions when using sentence-only, table-only, or combined evidence.
* **RoBERTa.py** – Script to fine-tune a RoBERTa base classifier on the training data.
* **RoBERTa_NLI.py** – Script to fine-tune a RoBERTa base classifier that was pre-trained on NLI, using the training set.
* **Roberta_NLI_NEI.py** – Script to fine-tune an NLI-pretrained RoBERTa model with NEI-balanced training data.
* **utils.py** – Helper utilities for loading and preparing data for the models.
* **evaluate.py** – Evaluate trained models on the dev or test splits.

## How to run

1. Clone this repository:

```bash
https://github.com/KartikVij2302/Fast-Verification-Pipeline.git
```

2. Install required packages (it's recommended to use a virtual environment):

```bash
pip install -r requirements.txt
```

3. Download the FEVEROUS sqlite dataset and extract it. Note: the database is large (~53 GB).

Download link: [https://fever.ai/dataset/feverous.html](https://fever.ai/dataset/feverous.html)

4. Evidence retrieval

Run the retriever to collect evidence for claims in the FEVEROUS training set:

```bash
python3 Scripts/Retriever/retriever.py
```

5. Verdict prediction (fine-tuning and evaluation)

Navigate to `./Scripts/VerdictPredictor` to find the training and evaluation scripts.

* Fine-tune the RoBERTa base classifier:

```bash
python3 RoBERTa.py
```

* Fine-tune the NLI-pretrained RoBERTa classifier:

```bash
python3 RoBERTa_NLI.py
```

* Fine-tune the NEI-balanced NLI-pretrained RoBERTa classifier:

```bash
python3 Roberta_NLI_NEI.py
```

* Evaluate a trained model on the dev/test set:

```bash
python3 evaluate.py
```

Make sure the dataset and related files are placed in the directory structure shown above so the scripts can locate them.
