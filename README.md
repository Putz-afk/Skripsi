# Comparative Analysis of Face Recognition Adaptation in NIR Domain

## 📌 Overview
This repository archives the code and experimental data for a thesis project investigating **Face Recognition performance under domain shift conditions**. Specifically, it addresses the significant performance drop observed when models trained on visible spectrum (RGB) images are applied to **Near-Infrared (NIR)** imagery.

The primary objective was not to build a commercial product, but to conduct a **comparative study** to identify the most effective adaptation strategy for a pre-trained **InceptionResNet** model under limited data constraints.

---

## 📄 Research Abstract & Results
The study evaluated three distinct implementation scenarios to adapt the model to the NIR domain:

- **Scenario A (Baseline)**  
  Using the pre-trained model directly as a feature extractor (Frozen Backbone).

- **Scenario B (Fine-Tuning)**  
  Conventional fine-tuning of the model’s top layers.

- **Scenario C (Metric Learning)**  
  Adopting a Siamese Network architecture with **Triplet Loss** to optimize embedding distances.

### Key Findings
Experimental results demonstrated that conventional methods (Scenario A & B) were insufficient for this specific domain shift.  
**Scenario C (Siamese Network)** emerged as the superior approach.

| Scenario | Approach                     | ROC-AUC | Outcome                                   |
|---------:|------------------------------|--------:|-------------------------------------------|
| A        | Baseline (Frozen Backbone)   | 0.5903  | Failed (Near Random Guessing)              |
| B        | Conventional Fine-Tuning     | 0.8090  | Partial Improvement (High FAR)             |
| C        | Siamese (Triplet Loss)       | 0.9999  | Effective Adaptation                       |

> **Note:** The results above represent the peak performance metrics achieved during the testing phase of this research.

---

## 📂 File Structure & Guide
The codebase is organized into modular notebooks, each representing a different stage of the research pipeline.

### `main.ipynb`
**Role:** Experiment Orchestrator  
**Description:**  
Drives the comparative study by loading the dataset, initializing the InceptionResNetV2 backbone, and executing the training loops for Scenarios A, B, and C. Generates comparison metrics such as ROC curves and EER.

### `head_pose.ipynb`
**Role:** Robustness Analysis  
**Description:**  
Analyzes the distribution of head orientations (yaw / pitch) in the test set to ensure evaluation includes challenging poses rather than only frontal images.

### `main_script_9_copy.ipynb`
**Role:** Experimental Sandbox  
**Description:**  
Contains the low-level Siamese Network implementation, including MTCNN-based face detection, custom Triplet Mining (Anchor–Positive–Negative selection), and detailed visualization of triplet batches.

### `utils.ipynb`
**Role:** Data Utility  
**Description:**  
Handles dataset management tasks such as unzipping archives, sorting images into class folders based on labels, and restoring dataset integrity.

---

## ⚙️ Methodology
The best-performing scenario relies on **Metric Learning** rather than standard classification.

- **Backbone**  
  InceptionResNetV2 maps face images into a high-dimensional embedding space.

- **Triplet Loss**  
  Minimizes the distance between an Anchor and a Positive (same identity) while maximizing the distance between an Anchor and a Negative (different identity).

- **Evaluation Metrics**
  - ROC-AUC  
  - True Acceptance Rate (TAR)  
  - False Acceptance Rate (FAR)  

These metrics are used to strictly evaluate security reliability.

---

## ⚠️ Disclaimer
This repository serves as an **academic archive** for a thesis project.

- **Research Prototype**  
  The code was developed to validate a specific hypothesis regarding domain adaptation. While **Scenario C** yielded strong metrics (ROC-AUC ≈ 0.99), the results are specific to the experimental test set constructed for this study.

- **Not Production Ready**  
  The system has not been deployed in a real-time production environment. The code reflects the experimental state used to generate the data for the final report.

---

## 👤 Author
**I Putu Wahyu Kusuma**  
Affiliation: Informatics Engineering, Hasanuddin University
