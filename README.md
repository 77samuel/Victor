# VICTOR: Verification with Intelligent Confidence Thresholding and Optimal Retrieval


[![Zenodo](https://img.shields.io/badge/Zenodo-DOI-green)](https://doi.org/10.5281/zenodo.20688127)

VICTOR is an uncertainty-driven adaptive verification framework for mitigating hallucinations in LLM outputs. It operates at the claim level, combining token-level entropy estimation, BM25-based retrieval, LLM verification, revision, and abstention in a single pipeline.

## Key Features

- Claim-level decomposition using sentence-level splitting
- Token-level entropy estimation via Ollama logprobs for adaptive routing
- BM25-based evidence retrieval over a controlled training corpus
- LLM-based deep verification for high-uncertainty claims
- Revision and abstention for actionable outputs
- No training required, CPU-compatible

## Experimental Setup

| Parameter | Value |
|---|---|
| Model | gemma3:1b (via Ollama) |
| Seed | 42 |
| Samples per dataset | 500 |
| Train/Test split | 50/50 stratified |
| Uncertainty threshold τ | 0.3 |
| Overlap threshold δ | 0.5 |
| Abstention threshold γ | 0.2 |
| BM25 top-k | 3 |

## Requirements

Install dependencies:

```bash
pip install -r requirements.txt
```

Install and start Ollama:

```bash
# Install Ollama from https://ollama.com
ollama pull gemma3:1b
ollama serve
```

## Datasets

Download the datasets from their official sources and place them in a `datasets/` folder:

| Dataset | Source | File |
|---|---|---|
| FEVER | https://fever.ai/dataset/fever.html | `datasets/fever.jsonl` |
| HaluEval | https://github.com/RUCAIBox/HaluEval | `datasets/halueval.json` |
| TruthfulQA | https://huggingface.co/datasets/truthful_qa | `datasets/TruthfulQA.csv` |

## Running Experiments

Open `Victor.ipynb` in Jupyter:

```bash
jupyter notebook Victor.ipynb
```

Run Cell 0 for the main experiment (baselines + VICTOR Full).
Run Cell 1 for the extended ablation (No BM25, No Revision, No Abstention).
Run Cell 2 for sensitivity analysis (τ sweep and k sweep).

## Results

Results are saved to the `results/` folder:

| File | Contents |
|---|---|
| `VICTOR_gemma3_1b_S500_T0.3_*.xlsx` | Main results (Table 6, 7) |
| `ablation_new_variants.csv` | Component ablation (Table 8) |
| `tau_sensitivity.csv` | τ sensitivity analysis |
| `topk_sensitivity.csv` | Top-k sensitivity analysis |

## Citation

Code and results: https://github.com/77samuel/Victor
Zenodo archive: https://doi.org/10.5281/zenodo.20688127
```
Samuel Stephen, R. Vignesh. Uncertainty-Guided Claim-Level Verification with 
Adaptive Retrieval for Hallucination Mitigation in LLMs. 
Computers and Electrical Engineering, 2026.
```

## Authors

- Samuel Stephen (samuels24@karunya.edu.in) — Karunya Institute of Technology and Sciences
- R. Vignesh (vignesh@karunya.edu) — Karunya Institute of Technology and Sciences

## License

This repository is made available for research reproducibility. The datasets used in this study are subject to their respective licenses.
