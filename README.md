# SLM Confidence Signals

Code and artifacts for the paper:

**When Should a Language Model Trust Itself?**\
*Same-Model Self-Verification as a Conditional Confidence Signal*

This repository contains the evaluation pipeline used to reproduce the
paper's experiments, tables, and figures.

## Paper

**Aditya Phalod**\
Independent Researcher\
University of British Columbia (Alumnus)

This work studies confidence estimation in small language models,
Comparing likelihood-based confidence signals with the same model
self-verification under selective prediction settings.

**Paper PDF:** [`arXiv`](https://arxiv.org/abs/2605.02915)

## Repository Contents

-   `self_verification_eval.ipynb` --- end-to-end evaluation notebook
-   `requirements.txt` --- Python dependencies
-   `paper.pdf` --- paper draft/preprint

## What This Repository Reproduces

The notebook implements the full experimental pipeline:

-   evaluation on reasoning and truthfulness multiple-choice benchmarks
-   computation of **LL-AVG**, **LL-SUM**, and **self-verification**
    confidence signals
-   aggregation of run-level outputs and summary metrics
-   export of paper-ready tables and figures

Reported metrics include:

-   **AUROC**
-   **AURC**
-   **Brier score**
-   **ECE-10**
-   selective prediction operating points

## Running the Notebook

1.  Open `self_verification_eval.ipynb` in Google Colab.
2.  Install dependencies.
3.  Set `OUTPUT_DIR`.
4.  Run the notebook from top to bottom.

Example output directory:

    /content/self_verify_runs

For persistent Colab storage:

    /content/drive/MyDrive/self_verify_runs

## Outputs

The notebook writes outputs under `OUTPUT_DIR`, including:

    summary_metrics.csv
    <dataset>/<model>/prompt_variant=<variant>/results.csv
    <dataset>/<model>/prompt_variant=<variant>/metrics.json
    paper_artifacts/

`paper_artifacts/` contains exported tables, figures, and CSV summaries
used in the paper.

## Reproducibility Notes

For reproducible runs:

-   use a fixed random seed
-   keep dataset splits unchanged
-   preserve model identifiers and prompt variants
-   store outputs separately for each dataset / model / prompt condition

Typical output structure:

    OUTPUT_DIR/
    ├── summary_metrics.csv
    ├── ai2_arc_challenge/
    ├── truthfulqa_mc/
    └── paper_artifacts/
        ├── tables/
        ├── figures/
        └── csv/

## Hardware

The notebook is designed for a CUDA-backed Google Colab runtime.\
Larger models may require the included 4-bit quantization path.

## Citation

If you use this repository, please cite:

``` bibtex
@article{phalod2026selfverification,
  title={When Should a Language Model Trust Itself? Same-Model Self-Verification as a Conditional Confidence Signal},
  author={Phalod, Aditya},
  year={2026}
}
```

## License

MIT License
