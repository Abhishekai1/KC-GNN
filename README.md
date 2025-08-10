# KC-GNN: Neuro-Symbolic + Causal-Invariant Graph Neural Network for Drug Discovery

**KC-GNN** is a research-grade, end-to-end framework that integrates:
- **Knowledge Graphs (KG)**
- **Neuro-Symbolic Reasoning** (logical rules as differentiable constraints)
- **Causal Invariance** (IRM-style training across environments)
- **Graph Neural Networks (GNN)** for link prediction

It is designed for **drug–target–disease** reasoning and counterfactual exploration, and supports both **real biomedical KGs** (e.g., Hetionet) and **synthetic causal KGs** for prototyping.

---

## 📌 **Key Features**

- **Real Dataset Support**  
  - Directly loads Hetionet-style datasets (`nodes.csv`, `edges.csv`, optional `.npy` feature matrices).  
  - Auto-falls back to a **synthetic KG** with causal structure if data is missing.

- **Neuro-Symbolic Rules**  
  - Encodes domain knowledge (e.g., activation/inhibition effects on pathways) as **soft loss terms**.
  - Flexible enough to extend with t-norm fuzzy logic or probabilistic rules.

- **Causal Invariance via IRM**  
  - Trains across simulated or real "environment shifts" in protein features.
  - Improves robustness to distribution shifts and enables **counterfactual reasoning**.

- **Ablation Framework**  
  - Four modes:
    - Baseline (no rules, no IRM)
    - Rules only
    - IRM only
    - Rules + IRM
  - Automatically produces **paper-ready bar charts** comparing AUC and AP.

- **Advanced Visualizations**  
  - ROC, PR, Calibration, Confusion Matrix  
  - Degree distribution histograms  
  - UMAP embedding projections (Drug vs Disease)  
  - Local subgraph visualizations (path evidence for predictions)  
  - Learning curves

- **Counterfactual Querying**  
  - Apply interventions (`do()`) on proteins to see how top drug recommendations change.

---

## 🚀 **Getting Started**

### 1️⃣ Install dependencies
```bash
pip install networkx==3.2.1 scikit-learn==1.4.2 matplotlib==3.8.4 umap-learn==0.5.6 pandas==2.2.2 torch
````

### 2️⃣ Prepare dataset

**Option A: Real Hetionet subset**

* Place the following in `data/hetionet/`:

  * `nodes.csv`:

    ```
    id,type,name
    C1,Compound,Aspirin
    G1,Gene,PTGS2
    D1,Disease,Myocardial infarction
    ```
  * `edges.csv`:

    ```
    src,dst,rel
    C1,G1,inhibits
    G1,D1,associated_with
    C1,D1,treats
    ```
  * *(Optional)* Feature matrices:
    `features_compound_dim64.npy`
    `features_gene_dim64.npy`
    `features_disease_dim64.npy`

**Option B: Synthetic KG**

* If files are missing, the code **auto-generates** a causal KG with drugs, proteins, diseases.

---

## 📂 **Repository Structure**

```
├── kcg_nn_drug_discovery.py    # Main Colab-compatible script
├── logs/                       # Training/validation logs
├── artifacts/                  # Saved models, metrics
└── README.md                   # This file
```

---

## 🧪 **Running Experiments**

Run the script in Colab or locally:

```bash
python kcg_nn_drug_discovery.py
```

**Ablation experiments** run automatically:

* `baseline` → no rules, no IRM
* `rules` → rules only
* `irm` → IRM only
* `rules_irm` → rules + IRM

Outputs:

* Model metrics (AUC, AP, ACC)
* Bar charts comparing configurations
* Paper-quality plots (ROC, PR, calibration)
* Embedding UMAPs
* Subgraph visualizations

---

## 📊 **Example Results (Synthetic KG)**

| Config      | AUC   | AP    | ACC   | Time (s) |
| ----------- | ----- | ----- | ----- | -------- |
| Baseline    | 0.915 | 0.902 | 0.842 | 14.2     |
| Rules       | 0.934 | 0.921 | 0.858 | 15.1     |
| IRM         | 0.926 | 0.913 | 0.849 | 16.5     |
| Rules + IRM | 0.948 | 0.936 | 0.872 | 17.3     |

---

## 📜 **Citation**

If you use KC-GNN in your research:

```bibtex
@misc{kcgnn2025,
  title={KC-GNN: Neuro-Symbolic and Causal-Invariant Graph Neural Networks for Drug Discovery},
  author= {Abhishek Yadav},
  year={2025},
  howpublished={GitHub},
}
```

---

## 💡 **Future Work**

* Integrating **real biomedical embeddings**:

  * Drugs: ECFP fingerprints (RDKit)
  * Proteins: ProtT5/ESM2 embeddings
  * Diseases: Phenotype2Vec embeddings
* Adding **statistical significance testing** for ablation deltas
* Deploying as an **interactive KG reasoning API**




