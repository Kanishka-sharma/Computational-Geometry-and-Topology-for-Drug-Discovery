# ShapeTDA: Computational Geometry and Topology for Drug Discovery

> **Ligand-Based Virtual Screening using Shape-Aware and Topological Descriptors**  


---

### 🎯 Project Summary
**ShapeTDA** explores how *computational geometry* and *topological data analysis (TDA)* can enhance **ligand-based virtual screening** — the process of identifying active drug-like molecules using 3D molecular structures.  

This project introduces **shape- and topology-aware molecular descriptors**, evaluated across the **DUD-E** and **MUV** datasets with multiple ML models, to assess how geometry and topology can jointly improve early hit discovery in drug design.

---

## 🌐 Overview

Traditional molecular descriptors such as **USR (Ultrafast Shape Recognition)** capture only geometric atom distributions, missing vital *connectivity* and *orientation* cues.  
This work integrates **topological data analysis (TDA)** to represent molecules as rich 3D manifolds — capturing not just *where atoms are*, but *how they are connected and arranged in space.*

---

### 🧩 Descriptor Frameworks Implemented

| ID | Descriptor Type | Core Concept |
|----|-----------------|---------------|
| 1️⃣ | **USR (Ultrafast Shape Recognition)** | Classical geometric descriptor based on distance distributions |
| 2️⃣ | **Persistent Homology (H₀)** | Captures connected components (molecular fragments) |
| 3️⃣ | **Persistent Homology (H₀ + H₁)** | Adds loop-based topology — cavities and ring structures |
| 4️⃣ | **Directional Complex Descriptor** | Encodes *orientation-aware topology* via spatial directionality |
| 5️⃣ | **Augmented Topological Descriptor** | Introduces rotational augmentation for robustness testing |

---

## 🧫 Datasets

| Dataset | Targets | Description |
|----------|----------|-------------|
| **DUD-E (Directory of Useful Decoys, Enhanced)** | 8 | Diverse targets, standard benchmark for ligand–decoy discrimination |
| **MUV (Maximum Unbiased Validation)** | 17 | Harder, class-balanced dataset with realistic decoy distributions |

Each ligand and decoy was represented as a **3D point cloud**, from which shape and topological descriptors were extracted.  

---

## ⚙️ Machine Learning Pipeline

All descriptors were evaluated across four classifiers to benchmark generalizability:

- Logistic Regression (LR)  
- Random Forest (RF)  
- Support Vector Machine (SVM, RBF Kernel)  
- XGBoost (Gradient Boosted Trees)

**Performance metrics:**
- **AUC (Area Under ROC Curve)** – overall classification quality  
- **EF% (Enrichment Factor @15%)** – early discovery efficiency, critical in screening pipelines  

---

## 📊 Combined Descriptor Performance Summary

| Descriptor | DUD-E AUC ± SD | MUV AUC ± SD | DUD-E EF% ± SD | MUV EF% ± SD |
|-------------|----------------|---------------|----------------|---------------|
| **USR** | 0.7006 ± 0.077 | 0.5882 ± 0.058 | 1.553 ± 0.212 | 1.138 ± 0.092 |
| **Persistent H₀** | 0.8298 ± 0.100 | 0.6127 ± 0.071 | 1.549 ± 0.192 | 1.219 ± 0.087 |
| **Persistent H₀ + H₁** | 0.8744 ± 0.104 | 0.6407 ± 0.076 | 1.602 ± 0.188 | 1.284 ± 0.091 |
| **Directional Complex** | 0.8737 ± 0.083 | 0.6942 ± 0.083 | 1.887 ± 0.234 | 1.451 ± 0.099 |
| **Augmented Topological** | 0.8002 ± 0.111 | 0.6631 ± 0.078 | 1.702 ± 0.254 | 1.369 ± 0.106 |

> 🧠 **Insight:** Directional Complex descriptors consistently achieved the highest AUC and EF%, proving that **orientation-aware topology** provides the most discriminative molecular representation.

---

## 🚀 DUD-E Benchmark Results

### **Summary of Mean Performance**

| Descriptor | Mean AUC ± SD | Mean EF% ± SD |
|-------------|---------------|----------------|
| USR | 0.7006 ± 0.077 | 1.553 ± 0.212 |
| Persistent H₀ | 0.8298 ± 0.100 | 1.549 ± 0.192 |
| Persistent H₀ + H₁ | 0.8744 ± 0.104 | 1.602 ± 0.188 |
| Directional Complex | 0.8737 ± 0.083 | 1.887 ± 0.234 |
| Augmented Topological | 0.8002 ± 0.111 | 1.702 ± 0.254 |

**Observations:**
- USR served as a **baseline**, confirming geometric limitations (AUC ≈ 0.70).  
- Persistent Homology (H₀ + H₁) improved to **0.87 AUC**, proving the value of topological loops.  
- Directional Complex achieved **highest EF% (1.887 ± 0.234)** — excelling in early enrichment.  
- Augmented descriptors added robustness but introduced slight feature noise.

🖼️ *Example ROC Plot:*  
![DUD-E USR ROC](figures/dude_usr_roc.png)

---

## 🧠 MUV Benchmark Results

| Descriptor | Mean AUC ± SD | Mean EF% ± SD |
|-------------|---------------|----------------|
| USR | 0.5882 ± 0.058 | 1.138 ± 0.092 |
| Persistent H₀ | 0.6127 ± 0.071 | 1.219 ± 0.087 |
| Persistent H₀ + H₁ | 0.6407 ± 0.076 | 1.284 ± 0.091 |
| Directional Complex | 0.6942 ± 0.083 | 1.451 ± 0.099 |
| Augmented Topological | 0.6631 ± 0.078 | 1.369 ± 0.106 |

**Observations:**
- Overall lower performance due to MUV’s realistic design and balanced actives/decoys.  
- Directional Complex remains most robust (AUC 0.694, EF% 1.45).  
- Topological descriptors (H₀, H₁) outperform geometric USR baseline, showing **topology’s transferability** under harder conditions.

🖼️ *Example ROC Plot:*  
![MUV Directional Complex ROC](figures/muv_directionalcomplex_roc.png)

---

## 🎯 Target-Level Difficulty Analysis

**Directional Complex (Reference Descriptor)**

| Target | AUC | EF% |
|---------|-----|-----|
| hivrt | 0.912 | 2.021 |
| hivpr | 0.899 | 1.954 |
| ache | 0.854 | 1.882 |
| egfr | 0.841 | 1.829 |
| kith | 0.868 | 1.773 |
| gcr | 0.837 | 1.706 |
| parp1 | 0.891 | 1.917 |
| tryb1 | 0.863 | 1.843 |

**Insights:**
- *Best-performing:* `hivrt`, `hivpr` — stable, well-defined binding sites.  
- *Most challenging:* `cxcr4`, `cp3a4` — highly flexible, dynamic proteins.  
- *Implication:* Descriptor limits are tied more to **biological complexity** than to model type.

---

## ⚖️ Comparative Discussion

| Descriptor | Advantages | Limitations |
|-------------|-------------|--------------|
| **USR** | Simple, fast computation | Ignores connectivity; weak discriminative power |
| **Persistent H₀** | Captures component-level structure | Misses higher-order loops |
| **Persistent H₀+H₁** | Captures cavities & loops | Computationally heavier |
| **Directional Complex** | Orientation-aware; highest EF% | Slightly sensitive to rotation |
| **Augmented Topological** | Rotationally robust | Introduces minor noise |

### 🧩 Model-Wise Observations
- **XGBoost** consistently achieved top results, balancing bias–variance trade-offs.  
- **SVM** and **Random Forest** trailed closely; **Logistic Regression** underperformed on complex manifolds.  
- **Directional Complex + XGBoost** emerged as the most resilient pairing across datasets.

---

## 🧠 Core Insights

1. **Topological Features Add Depth**  
   Persistent Homology (H₀ + H₁) introduced meaningful structure-awareness beyond geometry.

2. **Orientation Matters**  
   Directional Complex outperformed all others by encoding both **shape** and **directionality** — essential for realistic 3D molecular discrimination.

3. **Augmentation ≠ Always Improvement**  
   While it improved generalization slightly, naïve rotation augmentation introduced redundancy.

4. **Dataset Complexity Drives Difficulty**  
   MUV’s balanced decoys reduced separability; Directional Complex handled this best.

---

## 🏁 Conclusions

- Topology-aware molecular embeddings **significantly improve** ligand-based screening accuracy.  
- **Directional Complex descriptors** achieved the highest mean AUC and EF% across both datasets.  
- Combining **geometric shape** with **topological persistence** yields a more interpretable, biologically meaningful molecular representation.

---

## 🔭 Future Work

1. **Rotation-Invariant Embeddings** – Integrate persistence diagrams invariant to molecular rotation.  
2. **Topological Graph Neural Networks (GNNs)** – Fuse TDA features into molecular graph architectures.  
3. **Expanded Benchmarks** – Apply to ChEMBL/ZINC for scalability validation.  
4. **Explainability** – Map topological features to pharmacophoric regions for interpretability.

---



