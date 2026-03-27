# Self-Verification Evaluation Notebook

Code used to reproduce the evaluation pipeline, tables, and figures for the paper:

**When Should a Language Model Trust Itself?  
Same-Model Self-Verification as a Conditional Confidence Signal**

This repository contains a single Colab notebook implementing the evaluation pipeline used in the paper.

---

## Paper

**Aditya Phalod**  
Independent Researcher  
University of British Columbia (Alumnus)

The paper studies confidence signals for language models, comparing likelihood-based confidence estimators with same-model self-verification across reasoning and truthfulness benchmarks.

Preprint submitted onto arXiv.

---

## Repository contents

- `self_verification_eval.ipynb` — main Colab notebook containing the full evaluation pipeline.
- `requirements.txt` — Python dependencies used by the notebook.

---

## What the notebook does

The notebook is organized into three stages.

### 1. Evaluation setup and execution

- loads the evaluation datasets;
- loads each language model;
- scores multiple-choice answers with **LL-AVG** and **LL-SUM** likelihood signals;
- computes **same-model self-verification** confidence scores;
- saves per-example outputs and per-run metrics.

### 2. Merge and summarize results

- merges per-run outputs into `summary_metrics.csv`;
- computes evaluation metrics including:

  - AUROC  
  - AURC  
  - Brier score  
  - ECE-10  
  - selective-prediction operating points.

### 3. Generate paper artifacts

- exports LaTeX and CSV tables;
- saves figures used in the paper as PNG files.

---

## Running in Google Colab

1. Open `self_verification_eval.ipynb` in **Google Colab**.
2. Run the dependency-install cell.
3. (Optional) Mount Google Drive if you want outputs to persist across runtime restarts.
4. Edit `OUTPUT_DIR` in the configuration cell.

Default output location:

```
/content/self_verify_runs
```

For persistent storage:

```
/content/drive/MyDrive/self_verify_runs
```

5. Run the notebook from top to bottom.

---

## Expected outputs

The notebook writes outputs under `OUTPUT_DIR`.

```
summary_metrics.csv
<dataset>/<model>/prompt_variant=<variant>/results.csv
<dataset>/<model>/prompt_variant=<variant>/metrics.json
paper_artifacts/
```

`paper_artifacts/` contains:

- tables exported for the paper
- figures exported as PNG files.

---

## Hardware notes

- The notebook is designed for a **CUDA-backed Colab runtime**.
- Larger models may require the **4-bit quantization path** included in the notebook.
- The artifact-generation stage assumes that evaluation has already been run and that `summary_metrics.csv` exists.

---

## Reproducibility

This repository is organized to make the paper results easy to reproduce from a single notebook.

### Reproducibility workflow

1. Run the evaluation cells for each dataset / model / prompt condition.
2. Save all per-run outputs under a single `OUTPUT_DIR`.
3. Run the merge and summarization section to produce `summary_metrics.csv`.
4. Run the artifact-generation section to export the paper tables and figures.

### Directory structure

Typical output layout:

```
OUTPUT_DIR/
├── summary_metrics.csv
├── ai2_arc_challenge/
│   └── <model_name>/
│       └── prompt_variant=<variant>/
│           ├── results.csv
│           └── metrics.json
├── truthfulqa_mc/
│   └── <model_name>/
│       └── prompt_variant=<variant>/
│           ├── results.csv
│           └── metrics.json
└── paper_artifacts/
    ├── tables/
    ├── figures/
    └── csv/
```

### Determinism notes

For reproducible runs:

- use a fixed random seed;
- keep dataset splits constant;
- preserve the exact model identifiers used in the paper;
- avoid changing prompt templates unless testing prompt ablations;
- store outputs separately for each dataset / model / prompt condition.

---

## Citation

If you use this code or results in your work, please cite:

```
@article{phalod2026selfverification,
  title={When Should a Language Model Trust Itself? Same-Model Self-Verification as a Conditional Confidence Signal},
  author={Phalod, Aditya},
  year={2026}
}
```

---

## License

This repository is released under the **MIT License**.

---

## Author

**Aditya Phalod**  
Independent Researcher  
University of British Columbia (Alumnus)
