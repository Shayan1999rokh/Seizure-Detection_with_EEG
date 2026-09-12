# EEG Seizure Detection Using Classical Machine Learning

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-yellow.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Classification-red.svg)
![EEG](https://img.shields.io/badge/Domain-EEG%20Analysis-purple.svg)

## Overview

This project explores **EEG-based seizure detection using classical machine learning algorithms**. The workflow includes exploratory data analysis, visualization of EEG-derived features, correlation analysis, binary-label construction, class-imbalance handling, feature standardization, training of multiple classifiers, and comparative model evaluation.

The notebook compares **10 machine learning algorithms**, ranging from linear models to ensemble tree-based methods, to study how different approaches perform on the EEG classification task.

> **Project type:** Binary classification  
> **Data modality:** EEG-derived numerical features  
> **Environment:** Python / Jupyter Notebook

---

## Dataset

The dataset used in the notebook contains:

- **11,500 observations**
- **178 numerical EEG-derived features** (`X1` to `X178`)
- **1 identifier column** (`Unnamed`)
- **1 target column** (`y`)
- **5 original target classes**
- **2,300 samples per original class**
- **No missing values** in the loaded dataset

For the binary classification experiment, the target labels are transformed as follows:

```text
Class 1          -> 1
Classes 2,3,4,5 -> 0
```

After this transformation, the class distribution becomes:

```text
Class 0: 9,200 samples
Class 1: 2,300 samples
```

This produces a clear class-imbalance problem that is addressed in the modeling pipeline.

---

## Project Workflow

The notebook covers the following stages:

1. **Data loading and inspection**
2. **Descriptive statistical analysis**
3. **Missing-value inspection**
4. **Class-distribution visualization**
5. **EEG-feature visualization**
6. **Correlation analysis**
7. **Conversion from five classes to binary labels**
8. **Class balancing using SMOTEENN**
9. **Train / validation / test splitting**
10. **Feature standardization using `StandardScaler`**
11. **Training multiple machine learning classifiers**
12. **Validation-based model comparison**
13. **ROC/AUC analysis**

---

## Exploratory Data Analysis

Several exploratory analyses are performed before model training.

### Class Distribution

The original dataset is perfectly balanced across its five classes, with **2,300 observations in each class**.

After binary-label conversion, the dataset becomes imbalanced, with approximately **80% class 0** and **20% class 1**.

### EEG Feature Visualization

Selected EEG-derived features are plotted to inspect their variation and overall behavior across observations.

### Correlation Matrix

A correlation matrix is computed across the **178 numerical features** to examine linear relationships among the EEG-derived variables.

---

## Handling Class Imbalance

The project uses **SMOTEENN**, which combines:

- **SMOTE (Synthetic Minority Over-sampling Technique)** to generate synthetic minority-class observations.
- **Edited Nearest Neighbours (ENN)** to remove potentially noisy or ambiguous observations.

In the current notebook, the class counts after resampling are approximately:

```text
Class 0: 9,070
Class 1: 9,058
```

---

## Feature Scaling

The numerical features are standardized using:

```python
from sklearn.preprocessing import StandardScaler
```

The scaler is fitted on the training features and then applied to the validation and test features.

---

## Machine Learning Models

The following algorithms are explored:

| # | Model |
|---|---|
| 1 | Logistic Regression |
| 2 | K-Nearest Neighbors (KNN) |
| 3 | Support Vector Machine (SVM) |
| 4 | Stochastic Gradient Descent Classifier |
| 5 | Gaussian Naive Bayes |
| 6 | Decision Tree |
| 7 | Random Forest |
| 8 | Extra Trees Classifier |
| 9 | Gradient Boosting Classifier |
| 10 | XGBoost |

---

## Validation Results

The strongest validation accuracies reported by the current notebook are:

| Model | Validation Accuracy |
|---|---:|
| Decision Tree | 93.02% |
| Random Forest | 96.61% |
| Extra Trees | 98.10% |
| Gradient Boosting | 98.12% |
| **XGBoost** | **98.23%** |

Among the evaluated models, **XGBoost achieved the highest validation accuracy in the current notebook pipeline**.

> These values are validation results from the current implementation and should not be interpreted as final clinical performance.

---

## ROC Curve Analysis

The notebook also compares classifiers using ROC curves and AUC-based analysis.

The strongest models are the ensemble methods, particularly:

- XGBoost
- Gradient Boosting
- Extra Trees
- Random Forest

If you export the ROC figure from the notebook as `roc_curve.png`, you can display it here with:

```markdown
![ROC Curve](roc_curve.png)
```

---

## Technologies and Libraries

The project uses the following Python libraries:

- NumPy
- Pandas
- Matplotlib
- Seaborn
- SciPy
- scikit-learn
- imbalanced-learn
- XGBoost
- Jupyter Notebook

---

## Installation

Clone the repository:

```bash
git clone <YOUR-REPOSITORY-URL>
cd <YOUR-REPOSITORY-NAME>
```

Install the required packages:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn imbalanced-learn xgboost jupyter
```

Then start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
EEG-Seizure-Detection_MLProject_SHAYAN.ipynb
```

---

## Running the Notebook

The current notebook loads the dataset from a local Windows path. Before running it, update the following line to match the location of the dataset on your own system:

```python
path = r"YOUR_PATH/Epileptic Seizure Recognition.csv"
```

Then run the notebook cells sequentially.

---

## Methodological Notes and Future Improvements

This project is intended as a machine-learning exploration of EEG classification. Several improvements can make the experimental pipeline more rigorous:

- Apply **train/validation/test splitting before SMOTEENN**, and perform resampling only on the training data.
- Compute ROC curves using `predict_proba()` or `decision_function()` scores rather than hard class predictions.
- Recompute KNN and Naive Bayes evaluation metrics directly from their own predictions.
- Perform final evaluation on the untouched test set after model selection.
- Add cross-validation and systematic hyperparameter optimization.
- Add EEG-specific signal-processing steps such as band-pass filtering, notch filtering, FFT, power spectral density, or frequency-band analysis.

These extensions would make the pipeline more robust and improve its value as an EEG machine-learning study.

---

## Disclaimer

This project is intended for **research and educational purposes only**. It is not designed or validated for clinical diagnosis, medical decision-making, or real-world patient care.
