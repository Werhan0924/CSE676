# Building and Stress-Testing a Sparse Epigenetic Clock

This project asks whether a sparse linear epigenetic clock can predict chronological age from DNA methylation data in the `ComputAgeBench` study `GSE100264`, and what the model's errors reveal about the limits of that approach. The repository is organized as a small, reproducible research artifact: a curated final notebook, the checkpoint notebooks showing project progression, and lightweight instructions for rerunning the analysis in Google Colab.

Start here: [main_notebook.ipynb](./main_notebook.ipynb)

Project video: https://youtu.be/cZHimz5gjpo

## Research Questions

- Can an ElasticNet model predict chronological age from DNA methylation features in `GSE100264` better than a naive baseline?
- How stable is performance across different feature budgets and train/test splits?
- Do error patterns suggest systematic weaknesses, such as shrinkage at the youngest and oldest ages?
- Do unsupervised methylation archetypes help explain where the clock performs better or worse?

## Main Deliverable

The main graded notebook is [main_notebook.ipynb](./main_notebook.ipynb). It walks through:

- motivation and project framing
- dataset loading and alignment
- exploratory data analysis
- the main ElasticNet modeling pipeline
- robustness checks
- error analysis
- unsupervised archetype analysis
- age-gap profiling
- final interpretation and conclusion

## Data

This project uses the [`computage/computage_bench`](https://huggingface.co/datasets/computage/computage_bench) dataset and focuses on study `GSE100264`.

- Primary data used by the notebook:
  - `computage_bench_meta.tsv`
  - `data/benchmark/computage_bench_data_GSE100264.parquet`
- Access pattern:
  - the notebook looks for a local `computage_bench_local/` folder first
  - if the files are not present, it can download the needed study slice from Hugging Face
- Preprocessing performed in the notebook:
  - align methylation samples to metadata by `SampleID`
  - orient the methylation matrix so samples are rows
  - coerce `Age` to numeric and drop rows with missing age
  - cast methylation values to `float32`

See [data/README.md](./data/README.md) for the expected data layout.

## Results Summary

On the main held-out split, the ElasticNet clock achieved approximately `MAE = 3.14`, `RMSE = 4.06`, and `R^2 = 0.60`, compared with a mean-age baseline MAE of `5.24`. A more informative follow-up result is that the best performance came from a moderate feature budget of roughly `500-1000` CpGs rather than the largest feature set, suggesting that controlled sparsity improved generalization.

## Reproducibility

This project was developed for Google Colab.

1. Clone or download this repository.
2. Open [main_notebook.ipynb](./main_notebook.ipynb) in Colab.
3. Install dependencies from [requirements.txt](./requirements.txt) if needed.
4. Make sure the `ComputAgeBench` data is accessible:
   - either let the notebook download the required files
   - or place them in `computage_bench_local/` as described in [data/README.md](./data/README.md)
5. Run the notebook top to bottom.
6. Review the earlier project trajectory in:
   - [checkpoints/checkpoint_1.ipynb](./checkpoints/checkpoint_1.ipynb)
   - [checkpoints/checkpoint_2.ipynb](./checkpoints/checkpoint_2.ipynb)

## Key Dependencies

- Python `3.12.13`
- `numpy 1.26.4`
- `pandas 2.2.2`
- `scikit-learn 1.5.1`
- `matplotlib 3.9.2`
- `seaborn 0.13.2`
- `pyarrow 16.1.0`
- `huggingface-hub` for dataset download

The `requirements.txt` in this repo was exported from Colab. If you rerun the notebook in a different Colab runtime later, regenerate that file so the environment stays accurate.

## Repo Structure

```text
main/
├── README.md
├── requirements.txt
├── .gitignore
├── main_notebook.ipynb
├── checkpoints/
│   ├── checkpoint_1.ipynb
│   └── checkpoint_2.ipynb
└── data/
    └── README.md
```


