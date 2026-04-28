# Data Notes

This repository does not commit the methylation dataset itself.

The main notebook expects the following files from the `computage/computage_bench` dataset:

- `computage_bench_meta.tsv`
- `data/benchmark/computage_bench_data_GSE100264.parquet`

Expected local layout:

```text
computage_bench_local/
├── computage_bench_meta.tsv
└── data/
    └── benchmark/
        └── computage_bench_data_GSE100264.parquet
```

The notebook first looks for that local folder. If it cannot find the files, it attempts to download the required study slice from Hugging Face.
