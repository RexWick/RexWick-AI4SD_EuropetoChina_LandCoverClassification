#  Original Repository
Original Paper Link: https://www.researchgate.net/publication/319463676_EuroSAT_A_Novel_Dataset_and_Deep_Learning_Benchmark_for_Land_Use_and_Land_Cover_Classification

Original Paper Github Link: 
https://github.com/phelber/eurosat?tab=readme-ov-file

Code Implementation Paper Link: https://arxiv.org/abs/2401.09607

Code Implementation Github Link: https://github.com/jrterven/eurosat_classification

# File Structure

All the Technical Implementation are in eurosat_classification/AISD_ResNet_Classifier.ipynb

Answers to Assignment Requirements are in it as well.


## 📖 Overview

This project addresses the challenge of **Land Use and Land Cover (LULC)** classification in the context of rapid urbanization in China. Standard models trained on European satellite data (EuroSAT) often fail when applied to Chinese environments due to significant **Domain Shifts** (e.g., high-density "Urban Villages," complex viaducts, and resolution differences).

We implement a **Transfer Learning** strategy using a ResNet-50 architecture. By freezing the backbone pre-trained on EuroSAT and fine-tuning a new classification head on a curated subset of the AID (Aerial Image Dataset), we successfully bridge the satellite-to-aerial gap for local SDG monitoring.

## 📂 Dataset Curation

We curated a specific **7-class subset** from the AID dataset to match the EuroSAT classes while reflecting Chinese urban features.

| Target ID | EuroSAT Class (Source) | AID Class (Target - China) |
| :--- | :--- | :--- |
| **0** | AnnualCrop | **Farmland** | 
| **1** | Forest | **Forest** |
| **2** | Industrial | **Industrial** |
| **3** | Residential | **DenseResidential** |
| **4** | River | **River** |
| **5** | Pasture | **Meadow** |
| **6** | Highway | **Viaduct** |

*Note: AID images (~0.5m resolution) were downsampled to 64x64 to match the EuroSAT input tensor size.*

---

## 🏗️ Methodology: Adapted ResNet-50

To address the data scarcity in the target domain and reduce computational costs (**Green AI**), we utilized a **Frozen Backbone** strategy:

1.  **Backbone:** ResNet-50 pre-trained on EuroSAT (Feature Extractor layers **Frozen** ❄️).
2.  **Head:** A new Fully Connected (FC) layer initialized for **7 output classes** (Fine-tuned ⚙️).
3.  **Training:** Trained for 15 epochs using CrossEntropyLoss and SGD optimizer.

---

## 📊 Results & Performance

We evaluated the model on a held-out China Test Set ($N=380$).

### 1. Performance Comparison
Our adapted model significantly outperforms training from scratch, proving the effectiveness of transfer learning.

| Model Variant | Dataset | Accuracy | Status |
| :--- | :--- | :--- | :--- |
| ResNet-50 (Scratch) | EuroSAT | 82.94% | Baseline 1 |
| ResNet-50 (Pre-trained)| EuroSAT | **97.33%** | Benchmark (SOTA) |
| **Adapted ResNet-50** | **AID (China)**| **92.08%** | **Ours (Result)** |

### 2. Statistical Analysis
* **95% Confidence Interval:** `[91.1% - 95.9%]` (Wilson Score Interval).
* **Inference:** The result is statistically significant and robust.



