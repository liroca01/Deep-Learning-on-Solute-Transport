# Deep-Learning-on-Solute-Transport

This repository contains the data processing scripts and modeling workflows used in the manuscript **Multilayer perceptron model for predicting conservative solute transport in streams and rivers**. The codes are organized following the manuscript workflow.

The analyses use experiemntal data from the **TIERRAS database**, publicly available on Zenodo (https://zenodo.org/records/17051166), and synthetic breakthrough curves (BTCs) generated using the analytical solution of the Advection–Dispersion Equation (ADE).

**TIERRAS** website https://www.tierras.org/
---

## Repository Structure and Workflow

The notebooks below are described **in the order of the manuscript workflow**, rather than their alphabetical order in the repository.

---

## 1. Discharge Histogram  
**Notebook:** `Discharge_Histogram.ipynb`

This notebook generates histograms of discharge values for the **entire TIERRAS database**.  
It is used to characterize the overall range and distribution of discharge conditions represented in the dataset and to provide context for the experimental data used in the modeling analyses.

---

## 2. BTC Histograms  
**Notebook:** `BTC_Histograms.ipynb`

This notebook generates histograms of key breakthrough curve (BTC) characteristics for the **subset of TIERRAS data used in modeling**, including:
- Peak concentration  
- Time to peak concentration  
- Truncation time  

These distributions describe the properties of the BTCs used for training and testing the machine-learning models.

---

## 3. Quantity Analysis (Synthetic Data)  
**Notebook:** `MLP_QuantitySynthetic.ipynb`

This notebook performs the **quantity analysis**, investigating how MLP model performance varies with the **number of training samples**.

- Synthetic BTCs are generated using the analytical ADE solution.
- The MLP is trained using increasing numbers of synthetic samples.
- Model performance is evaluated to quantify sensitivity to training data size.

---

## 4. Quality Analysis (Synthetic Data)  
**Notebook:** `MLP_QualitySynthetic.ipynb`

This notebook performs the **quality analysis**, evaluating the impact of training the MLP model on **truncated BTCs**.

- The MLP is trained using synthetic truncated BTCs.
- The trained model is tested on:
  - A subset of truncated BTCs (similar to the training data)
  - A subset of non-truncated BTCs 
- This analysis assesses how truncation in training data affects model generalization.

---

## 5. Baseline MLP (Synthetic Data)  
**Notebook:** `MLP_baselineSynthetic.ipynb`

This notebook defines the **baseline MLP model** trained and tested entirely on synthetic data.

- **3000 synthetic BTCs** generated with the ADE are used.
- The model is trained on synthetic data and tested on synthetic data.
- The trained MLP model is **saved** at the end of this notebook.

**Important note:**  
The saved model file is **not included in the repository** due to file size constraints.  
Running this notebook will regenerate the trained model, which is required for subsequent analyses.

---

## 6. MLP Trained on Experimental Data  
**Notebook:** `MLP_Experimental.ipynb`

This notebook trains and tests the MLP model using **experimental BTC data** from the TIERRAS database.

- The model is trained directly on experimental data.
- The model is tested on experiemtnal data.
- This provides a purely data-driven experimental benchmark.

---

## 7. Synthetic → Experimental Evaluation  
**Notebook:** `MLP_synthetic_experimental.ipynb`

This notebook evaluates **model transferability from synthetic to experimental data**.

- The MLP trained on synthetic data in **Notebook 5** is used without retraining.
- The synthetic-trained model is tested directly on experimental BTCs.
- This analysis quantifies how well physics-based synthetic training generalizes to real experimental data.

---

## 8. Transfer Learning  
**Notebook:** `Transfer_Learning.ipynb`

This notebook implements **transfer learning** using the synthetic-trained MLP.

- The MLP trained in **Notebook 5** is used as a pretrained model.
- The model is fine-tuned using experimental data from **TIERRAS**.
- The fine-tuned model is tested on experimental BTCs.

This workflow evaluates whether transfer learning improves performance relative to training solely on experimental data.

---

## 9. MLP vs. Random ADE Validation  
**Notebook:** `MLPvsRandomADE.ipynb`

This notebook provides a **validation benchmark** comparing the MLP model to an uncalibrated physics-based approach.

- ADE BTCs are generated using random dispersion coefficients (D).
- No calibration is performed.
- Performance against actual BTCs is evaluated. 

This analysis evaluates whether the MLP provides improvement beyond using the ADE with random parameter selection.

---

## Data Availability

- Experimental BTCs and metadata are derived from the **TIERRAS database** (https://zenodo.org/records/17051166).
- Synthetic BTCs are generated using the analytical ADE within the notebooks.
- All preprocessing and modeling steps are fully reproducible using the provided code.

---

## Reproducibility Notes

- The notebook `MLP_baselineSynthetic.ipynb` **must be run first** before executing:
  - `MLP_synthetic_experimental.ipynb`
  - `Transfer_Learning.ipynb`
- This notebook generates the pretrained MLP model used in those analyses.
