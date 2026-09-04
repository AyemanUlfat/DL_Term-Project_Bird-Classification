# 🐦 Bird Song Classification

> Deep learning term project for classifying bird species from audio recordings using spectrograms, extra Xeno-canto data, and model comparison — developed at University West.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Framework](https://img.shields.io/badge/Framework-Keras%20%2F%20TensorFlow-FF6F00)
![Case study](https://img.shields.io/badge/Case%20study-Bird%20Song%20Classification-orange)
![Score](https://img.shields.io/badge/Metrics-Top--1%20%7C%20Top--3%20%7C%20Top--5-green)
![Status](https://img.shields.io/badge/Course-DL%20Term%20Project-success)

Repo: https://github.com/AyemanUlfat/DL_Term-Project_Bird-Classification

---

## 📌 Overview

This project tackles a **fine-grained bird song classification** problem: identify the species from an audio recording. Many species have few labelled clips, recordings vary in length and quality, and similar calls are easy to confuse.

The pipeline was built end-to-end across five notebooks:

- inspect the Kaggle bird-call dataset
- download extra recordings from **Xeno-canto**
- convert and preprocess audio
- build train / validation / test splits
- compare trained models with top-1, top-3 and top-5 accuracy plus a confusion matrix

---

## 🎯 Key Results

```
| Item                    | Result                                              |
| ----------------------- | --------------------------------------------------- |
| Task                    | Multi-class bird song / species classification      |
| Input                   | Waveform → spectrogram / mel spectrogram            |
| Extra data source       | Xeno-canto API (species limited to the Kaggle set)  |
| Class imbalance         | Half of species have 100 clips; 17.4% have < 50     |
| Metrics reported        | Categorical accuracy, top-3, top-5                  |
| Analysis                | Training curves, test metrics, confusion matrix     |
| Training logs           | Azure Machine Learning run history (.history, .pkl) |
```

✅ Extra public recordings were added where the original set was thin.  
✅ Models are compared on the same splits with top-k accuracy, not only top-1.

---

## 🏗️ System Architecture

```
Kaggle bird-call metadata + audio
        │
        ▼
┌─────────────────────────────────┐
│  Notebook 1 — Inspect data      │
│  • species counts               │
│  • duration / sample-rate stats │
│  • spectrogram / mel plots      │
└──────────────┬──────────────────┘
               │
               ▼
┌─────────────────────────────────┐
│  Notebook 2 — More data         │
│  • Xeno-canto API search        │
│  • download clips not in Kaggle │
└──────────────┬──────────────────┘
               │
               ▼
┌─────────────────────────────────┐
│  Notebook 3 — Preprocess audio  │
│  • SoX conversion               │
│  • full-length .npy features    │
└──────────────┬──────────────────┘
               │
               ▼
┌─────────────────────────────────┐
│  Notebook 4 — Splits & labels   │
│  • merge datasets               │
│  • train / val / test           │
│  • label encoding → JSON        │
└──────────────┬──────────────────┘
               │
               ▼
┌─────────────────────────────────┐
│  Notebook 5 — Metrics           │
│  • Azure ML run logs            │
│  • accuracy / top-3 / top-5     │
│  • confusion matrix             │
└─────────────────────────────────┘
```

---

## 🧠 Technical Approach

### Notebook 1 — Data inspection
- Load Kaggle `train.csv` (ebird code, scientific name, Xeno-canto id)
- Count recordings per species
- Plot spectrogram, log spectrogram (dB), and mel spectrogram
- Check duration outliers and sample rates

### Notebook 2 — Collect more audio
- Query the Xeno-canto API for every scientific name in the Kaggle set
- Cache results in `data/xc.json`
- Download new files that are not already in the Kaggle ids

### Notebook 3 — Preprocess
- Convert formats with SoX
- Load audio with Librosa / SoundFile
- Store full-length arrays as `.npy`

### Notebook 4 — Dataset construction
- Merge Kaggle + new Xeno-canto rows
- Stratified train / validation / test split
- Label-encode species names and save JSON metadata

### Notebook 5 — Evaluation
- Pull model run logs from Azure ML
- Compare models on categorical, top-3 and top-5 test accuracy
- Plot training vs validation curves
- Confusion matrix on the test set

---

## 📁 Repository Structure

```
DL_Term-Project_Bird-Classification/
├── Bird Classification_1.ipynb
├── Bird Classification_2.ipynb
├── Bird Classification_3.ipynb
├── Bird Classification_4.ipynb
├── Bird Classification_5.ipynb
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install numpy pandas matplotlib seaborn plotly scikit-learn
pip install librosa soundfile tqdm requests requests_random_user_agent
pip install joblib tensorflow keras
```

### Run

1. Clone the repo  
   `git clone https://github.com/AyemanUlfat/DL_Term-Project_Bird-Classification.git`
2. Put the Kaggle bird-call files under `data/`
3. Open the notebooks in order: 1 → 2 → 3 → 4 → 5

---

## 📦 Dataset

- Starting set: Kaggle bird-call metadata (`train.csv`)
- Extra audio: Xeno-canto recordings for the same scientific names
- Raw audio is not fully committed to GitHub because of size

---

## 🛠️ Tech Stack

```
| Component           | Tool                                   |
| ------------------- | -------------------------------------- |
| Language            | Python 3.10+                           |
| Deep learning       | Keras / TensorFlow                     |
| Experiment tracking | Azure Machine Learning                 |
| Audio I/O           | Librosa, SoundFile, SoX                |
| Extra data          | Xeno-canto API                         |
| Analysis            | pandas, scikit-learn, seaborn, Plotly  |
```

---

## 📊 Evaluation Details

- Metrics: categorical accuracy, top-3 accuracy, top-5 accuracy
- Plots: test accuracy by model, train vs validation curves, confusion matrix

---

## 🔭 Future Work

- Publish the final accuracy table in this README
- Stronger augmentation for rare species
- Share the best `.h5` model
- Add one-file inference: wav → species + top-5 list

---

## 👤 Author

**Ayeman Ulfat**  
MSc AI & Automation · University West, Trollhättan, Sweden  
GitHub: [AyemanUlfat](https://github.com/AyemanUlfat)  
Project: [DL_Term-Project_Bird-Classification](https://github.com/AyemanUlfat/DL_Term-Project_Bird-Classification)

---


