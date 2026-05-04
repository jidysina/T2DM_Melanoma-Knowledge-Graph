# T2DM–Melanoma Knowledge Graph

A computational knowledge graph analysis of the molecular interface between 
type 2 diabetes mellitus (T2DM) and melanoma, constructed as part of a 
dissertation project at Teesside University (2025–2026).

## Overview

This repository contains the supporting materials for a heterogeneous 
biomedical knowledge graph (KG) that integrates disease-gene associations, 
drug-target annotations, and protein-protein interactions to systematically 
map the shared molecular biology between T2DM and melanoma, and to rank 
antidiabetic drug classes by their structural proximity to melanoma-associated 
biology.

## Repository Contents

```
T2DM_Melanoma_KG_Dataset_auto6.xlsx   # Final cleaned dataset (STRING ≥0.9)
T2DM_Melanoma_KG_Results.xlsx         # All analysis results (6 sheets)
T2DM_Melanoma_KG_extraction.ipynb     # Original data extraction pipeline
T2DM_MELANOMA_2.ipynb                 # Graph construction and analysis
README.md
```

## Data Sources

| Database | Version | Access Date | Usage |
|----------|---------|-------------|-------|
| KEGG | Continuously updated | March 2026 | Disease entries, pathway diagrams, drug targets |
| ChEMBL | v33 | March 2026 | Drug-target annotations (fallback) |
| STRING | v12.0 | March 2026 | Protein-protein interactions (confidence ≥ 0.9) |

## Knowledge Graph

**Final dataset (auto6):**
- 290 nodes: 157 genes, 102 drugs, 20 pathways, 7 metabolites, 4 disease nodes
- 1,027 directed edges across 8 relationship types
- Single connected component (verified)

**Node types:** Disease · Pathway · Gene · Drug · Metabolite

**Edge types:** HAS_GENE · HAS_DRUG · TARGETS · INTERACTS_WITH · 
RELATED_PATHWAY · HAS_KEGG_PATHWAY · HAS_METABOLITE · SAME_AS

## Methods

The pipeline was implemented in Python 3.13.5 using NetworkX 3.4.2 for 
graph operations and PyVis for interactive visualisation.

**Two analyses were performed on the undirected graph projection:**

1. **Betweenness centrality** — Brandes (2001) algorithm, normalised, 
   unweighted, across all 290 nodes
2. **Drug proximity scoring** — mean shortest path length between drug 
   target genes and the melanoma gene set (78 genes), following the 
   framework of Cheng *et al*. (2018)

## Key Findings

- Nine shared PI3K/MAPK pathway genes identified between the T2DM pathway 
  (hsa04930) and the melanoma pathway (hsa05218)
- AKT2 identified as the sole cross-disease gene (T2DM disease entry H00409 
  and melanoma pathway hsa05218) and highest-scoring gene node by betweenness 
  centrality (BC = 0.078, rank 5/290)
- Insulin formulations ranked as the T2DM drug class closest to melanoma 
  biology (mean proximity 3.397)
- Metformin ranked last among T2DM drug classes (mean proximity 5.756)
- GLP-1 receptor agonists showed intermediate proximity (mean proximity 4.147)

> **Note:** All proximity scores represent structural graph distances only 
> and do not indicate therapeutic efficacy or clinical benefit. This study 
> is exploratory and intended for hypothesis generation, not causal inference.

## Interactive Visualisations

The HTML files can be opened directly in any web browser via 
the hosted links below:

- Full graph: https://t2dm-melanoma-kg-full.netlify.app/
- Subgraph: https://t2dm-melanoma-kg-subgraph.netlify.app/

## Requirements

```bash
pip install networkx pandas openpyxl pyvis matplotlib requests
```

## Usage

Run the notebooks in the following order:

1. `T2DM_Melanoma_KG_extraction.ipynb` — data extraction from KEGG, 
   ChEMBL, and STRING APIs (requires internet connection)
2. `T2DM_MELANOMA_2.ipynb` — graph construction, analysis, and 
   visualisation (can be run from the saved dataset without re-extraction)

> The dataset files allow the analysis notebook to be run independently 
> without re-fetching from the APIs.

## Citation

If you use this dataset or code, please cite:

> Chukwuedo, Jacinta O. (2026). *A knowledge graph analysis of the molecular interface 
> between type 2 diabetes mellitus and melanoma*. Dissertation, Teesside 
> University.

## References

- Brandes, U. (2001). A faster algorithm for betweenness centrality. 
  *Journal of Mathematical Sociology*, 25(2), 163–177.
- Cheng, F. *et al*. (2018). Network-based approach to prediction and 
  population-based validation of in silico drug repurposing. 
  *Nature Communications*, 9, 2691.
- Kanehisa, M. *et al*. (2023). KEGG for taxonomy-based analysis of pathways 
  and genomes. *Nucleic Acids Research*, 51(D1), D587–D592.
- Szklarczyk, D. *et al*. (2023). The STRING database in 2023. 
  *Nucleic Acids Research*, 51(D1), D638–D646.
- Zdrazil, B. *et al*. (2024). The ChEMBL Database in 2023. 
  *Nucleic Acids Research*, 52(D1), D1180–D1192.

## Licence

This project is released under the MIT Licence.
