# Reference Papers

This directory contains the source papers used to extract writing patterns, terminology, and style conventions for the `paper-methodology` skill.

## Naming Convention

```
NN-{own|other}-ShortName.txt
```

- `NN`: Two-digit sequence number (01-99)
- `own`: Papers authored by the user (primary style source)
- `other`: External reference papers (secondary style + terminology source)
- `ShortName`: Abbreviated model/method name

## Current Papers

### Own Papers (Primary Style Reference)

| File | Model | Domain |
|------|-------|--------|
| `01-own-PitGAN.txt` | PitGAN | Excavation deformation prediction via cGAN surrogate |
| `02-own-PI-ETGCN.txt` | PI-ETGCN | Physics-informed spatiotemporal GCN for tunnelling |
| `03-own-THGAN.txt` | THGAN | Digital-twin GAN for tunnel health monitoring |

### Other Papers (Terminology + Pattern Reference)

| File | Model | Domain |
|------|-------|--------|
| `04-other-LLM-GNN.txt` | LLM-enhanced GNN | LLM + GNN for geological risk quantile prediction |
| `05-other-AC-GGN.txt` | AC-GGN | GCN+GRU+Attention for shield tunnelling |
| `06-other-LLM-KG.txt` | LLM-KG | LLM-empowered knowledge graph for metro construction |
| `07-other-TSFRA.txt` | TSFRA | Fuzzy AHP + DAG-GNN risk assessment |
| `08-other-TwoStageSVM.txt` | Two-stage SVM | LSSVM + copula prediction intervals |
| `09-other-MS-STGCN.txt` | MS-STGCN | Spectral-temporal GCN with multi-source fusion |

## Adding New Papers

1. Use the next available sequence number
2. Follow the naming convention above
3. Place the full-text `.txt` file here
4. Update this README table
5. If the paper introduces new domain-specific terms, update `../term_glossary.yml`
