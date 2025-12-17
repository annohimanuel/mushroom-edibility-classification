# 🍄 Mushroom Edibility Classification (Neural Network + PCA)

🧠 **Goal:** Predict whether a mushroom is **✅ edible** or **☠️ poisonous** using the Agaricus–Lepiota dataset.

📌 **Target:** `class`  
- `e` = edible ✅  
- `p` = poisonous ☠️  

---

## 📊 Findings

✅ **Data quality**
- 8,124 records, 22 categorical features
- No null values detected in the loaded CSV

🧩 **Feature engineering**
- One-hot encoding expanded features from **22 → 94**
- Label encoding applied to target (`0 = edible`, `1 = poisonous`)
- Train/test split: **80/20**, stratified for class balance

🧠 **Model 1: Baseline Neural Network**
- Architecture: Dense(32, ReLU) → Dense(1, Sigmoid)
- Optimizer: Adam | Loss: Binary Cross-Entropy
- Training: 20 epochs, validation split 0.2
- Training time: ~**1.82s**
- Performance: **~1.000 accuracy** with **no false positives/negatives** in the confusion matrix

🧊 **Dimensionality Reduction (PCA)**
- PCA retained **95% variance**
- Reduced features from **94 → 38**

⚙️ **Model 2: PCA Neural Network**
- Architecture: Dense(16, ReLU) → Dense(1, Sigmoid)
- Training: 20 epochs
- Training time: ~**1.65s**
- Performance: **~0.9996 accuracy** with **no false positives/negatives** in the confusion matrix

📌 **Conclusion**
- PCA achieved a large reduction in feature dimensionality (**94 → 38**) with **negligible loss in accuracy**, indicating the encoded feature space contains substantial redundancy.

---

## 👤 Author

Imanuel Annoh
