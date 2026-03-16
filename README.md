# SEA-AD MTG snATAC-seq — Chromatin Module Analysis

Analysis of single-nucleus ATAC-seq (snATAC-seq) data from the **Seattle Alzheimer's Disease Brain Cell Atlas (SEA-AD)** cohort, focusing on the **Middle Temporal Gyrus (MTG)**. The goal is to identify chromatin modules (CMs) correlated with Alzheimer's disease (AD) pathology using the **Clomics** framework.

---

## Project Overview

**Dataset:** SEA-AD — 82 donors (spanning the full spectrum of AD neuropathological change), Middle Temporal Gyrus  
**Modalities:** snATAC-seq (chromatin accessibility) + snRNA-seq (gene expression)  
**Method:** Chromatin module (CM) inference via Clomics → pseudobulk aCM scores → correlation with AD pathology scores (PPS)

### Key questions
- Which chromatin modules have their activity significantly correlated with AD pathology?
- Do CM-associated peaks map to genes also dysregulated at the transcriptomic level?
- How does chromatin accessibility of neuronal populations relate to disease progression?



---

## Notebooks


### 1. `MTG.ipynb` — snATAC-seq Exploration
Full exploration of the snATAC-seq AnnData object.  
- QC metrics (total counts, number of peaks, TSS enrichment)
- Dimensionality reduction and UMAP visualization
- Cell type annotation inspection

### 3. `mtg_celltype_selection.ipynb` — Cell Type Filtering
- Subsetting to neuronal populations
- Pseudobulk aggregation per donor
- Quality control of pseudobulk profiles


### 5. `mtg_corr_aCM_AD.ipynb` — aCM × AD Pathology Correlation
Core analysis notebook.  
- Spearman correlation of aCM scores with the **pseudoprogression score (PPS)**
- Multiple testing correction (Benjamini-Hochberg)
- Sensitivity analysis across background thresholds (1.5, 2, 3, 4)
- Identification of **78 significant CMs** (padj < 0.1, |ρ| > 0.3)
- Peak-to-gene mapping using a gene body BED file

### 6. `mtg_corr_RNA_AD.ipynb` — RNA × AD Pathology Correlation
- QC metrics
- Subsetting to neuronal populations
- Pseudobulk snRNA-seq aggregation by donor
- Spearman correlation of gene expression with PPS
- Cross-modal comparison with aCM results

---

## Data

Raw `.h5ad` files are **not included** in this repository. See [data/README.md](data/README.md) for download instructions.

---

## Dependencies

```bash
pip install scanpy anndata muon scipy statsmodels pandas numpy matplotlib seaborn h5py
```
---

## Citation

If you use this code or the SEA-AD dataset, please cite:

> **SEA-AD Consortium** (2024). Seattle Alzheimer's Disease Brain Cell Atlas. *Allen Brain Cell Atlas.*  
> https://portal.brain-map.org/atlases-and-data/rnaseq/human-mtg-10x_sea-ad

> **Clomics** — chromatin module inference:   
> https://github.com/DeplanckeLab/Chromatin_modules

---