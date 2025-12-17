<h1 align="center">🍄 Mushroom Edibility Classification (Neural Network + PCA)</h1>

<p align="center">
  <b>Binary classifier</b> to predict whether a mushroom is <span title="Safe to eat">✅ edible</span> or <span title="Dangerous">☠️ poisonous</span> using the classic <b>Agaricus–Lepiota</b> dataset.
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.x-informational">
  <img alt="TensorFlow" src="https://img.shields.io/badge/TensorFlow-Keras-informational">
  <img alt="scikit-learn" src="https://img.shields.io/badge/scikit--learn-ML-informational">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-lightgrey">
</p>

---

## 🎯 Project Objective

Misclassifying a poisonous mushroom as edible is high-risk.  
Goal: predict the label:

- **Target:** `class`
  - `e` = edible ✅
  - `p` = poisonous ☠️

---

## 📦 Dataset

📚 **Source:** The Audubon Society Field Guide to North American Mushrooms (1981)  
📄 Files:
- `data/agaricus-lepiota.csv`
- `data/agaricus-lepiota.names` (feature reference)

📊 **Rows:** 8,124  
🧩 **Features:** 22 categorical attributes (nominal)

> The `.names` file is used for understanding the dataset, not training.

---

## ⚡ Quick Highlights

✅ Fully categorical data → **One-hot encoding**  
🧠 Neural network baseline (Dense → Dense)  
🧪 Evaluation via **Confusion Matrix**  
🧊 PCA retains **95% variance** while shrinking features  
📉 Feature count reduced **94 → 38** with near-identical performance

---

## 🔬 Workflow

### 1) Data Validation ✅
- Loaded dataset + confirmed no nulls using `isnull().sum()`

### 2) Train/Test Split ✂️
- 80/20 split with stratification to preserve class balance

### 3) Encoding 🔁
- One-hot encode categorical features (`pd.get_dummies(drop_first=True)`)
- Label encode target (`LabelEncoder`): `0=edible`, `1=poisonous`
- Align train/test columns via `reindex(..., fill_value=0)`

### 4) Baseline Neural Network 🧠
Architecture:
- Dense(32, ReLU) → Dense(1, Sigmoid)

Training:
- Adam + Binary Cross Entropy
- 20 epochs + validation split
- Tracked training time with `%%time`

Evaluation:
- Threshold at 0.5
- Confusion matrix

<p align="center">
  <img src="assets/confusion_matrix_baseline.png" alt="Confusion Matrix - Baseline" width="520">
</p>

### 5) PCA Dimensionality Reduction 🧊
- PCA retaining **95% variance**
- Features reduced from **94 → 38**

<p align="center">
  <img src="assets/pca_variance.png" alt="PCA Variance Explained" width="520">
</p>

### 6) PCA Neural Network ⚙️
Architecture:
- Dense(16, ReLU) → Dense(1, Sigmoid)

Evaluation:
- Confusion matrix

<p align="center">
  <img src="assets/confusion_matrix_pca.png" alt="Confusion Matrix - PCA Model" width="520">
</p>

---

## 🏁 Results

| Model | Features | Train Time (20 epochs) | Test Accuracy | Notes |
|------:|---------:|------------------------:|--------------:|------|
| Baseline NN | 94 | ~1.82s | ~1.0000 | No FP/FN observed |
| PCA NN (95% var) | 38 | ~1.65s | ~0.9996 | No FP/FN observed |

✅ PCA delivered a major dimensionality reduction with negligible performance loss.

---

👤 Author

Imanuel Annoh
GitHub: https://github.com/annohimanuel
