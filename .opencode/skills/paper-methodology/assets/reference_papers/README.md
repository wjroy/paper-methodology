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
| `02-own-PI-ETGCN.txt` | PI-ETGCN | Physics-informed spatiotemporal GCN for excavation |
| `03-own-THGAN.txt` | THGAN | Digital twin with heterogeneous graph attention for deep excavation risk prediction |
| `04-own-LLM-GNN.txt` | GTAF (LLM-GNN) | LLM-enhanced GNN for railway track settlement quantile prediction |
| `05-own-TSFRA.txt` | TSFRA | Temporal-spatial fusion risk assessment for excavation |

### Other Papers (Terminology + Pattern Reference)

| File | Model | Domain |
|------|-------|--------|
| `06-other-AC-GGN.txt` | AC-GGN | GCN+GRU+Attention for excavation deformation |
| `07-other-LLM-KG.txt` | LLM-KG | LLM-empowered knowledge graph for building health resilience |
| `08-other-TwoStageSVM.txt` | Two-stage SVM | LSSVM + copula prediction intervals for excavation |
| `09-other-MS-STGCN.txt` | MS-STGCN | Spectral-temporal GCN with multi-source fusion for excavation |
| `10-other-NLP-CMS.txt` | Domain PLM | Pre-trained language models for construction management |
| `11-other-BPL-LLM.txt` | BPL-LLM | Bayesian Program Learning + LLM for risk probability estimation |
| `12-other-CM-risk.txt` | Cloud Model | Cloud Model for excavation risk assessment |
| `13-other-F2P-Net.txt` | F2P-Net | Visual prompt tuning for industrial defect segmentation |
| `14-other-SolarFM.txt` | SolarFM | TSFM (Chronos) for solar irradiance forecasting |
| `15-other-Wind-FM.txt` | Wind-FM | TSFM (Timer) + Prompt Tuning for wind power prediction |
| `16-other-TSFMs.txt` | TSFMs | Time series foundation models (Moirai, TimesFM, Chronos) with LoRA |
| `17-other-LLIAM.txt` | LLIAM | LLaMA + LoRA for time series forecasting |
| `18-other-SOH-FM.txt` | SOH-FM | TimeGPT fine-tuning for battery state of health estimation |

## Adding New Papers

1. Use the next available sequence number
2. Follow the naming convention above
3. Place the full-text `.txt` file here
4. Update this README table
5. If the paper introduces new domain-specific terms, update `../term_glossary.yml`
