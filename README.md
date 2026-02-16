# CSE676
# Epigenetic Aging Clock Analysis using ComputAgeBench

## Project Overview
This project explores the intersection of **Bioinformatics** and **Deep Learning** by analyzing DNA methylation data to predict biological age. Using the **ComputAgeBench** dataset (Kriukov et al., KDD 2025), the goal is to build an "Epigenetic Clock"—a machine learning model that estimates the biological age of an individual based on methylation levels at specific CpG sites on their DNA.

The project specifically aims to address the challenge of **Batch Effects** (technical noise between different studies) and **Class Imbalance** (rare disease samples vs. healthy controls) using advanced data mining techniques.

## Dataset
* **Name:** ComputAgeBench: Epigenetic Aging Clocks Benchmark
* **Source:** [Hugging Face](https://huggingface.co/datasets/computage/computage_bench) | [Paper](https://doi.org/10.1145/3711896.3737382)
* **Size:** ~10,410 samples (Benchmarking set)
* **Features:** >900,000 continuous features (DNA Methylation Beta Values)
* **Target:** Chronological Age (Regression) and Health Condition (Classification)

## Project Roadmap
### Checkpoint 1: Exploratory Data Analysis (Current)
* **Objective:** Select a candidate dataset and perform initial cleaning and visualization.
* **Key Findings:**
    * **Bimodal Distribution:** Feature values are strictly bounded [0, 1] with peaks at unmethylated (0) and methylated (1) states, motivating the use of non-linear models over standard scaling.
    * **Class Imbalance:** Significant skew towards infectious diseases (e.g., HIV) over healthy controls, requiring balanced sampling strategies.
    * **Batch Effects:** Data aggregation from 65 distinct studies suggests the need for Domain Adaptation.

### Checkpoint 2: Methodology (Upcoming)
* Implementation of **Principal Component Analysis (PCA)** for dimensionality reduction.
* Development of a **Deep Autoencoder** for non-linear feature extraction.

## Installation & Usage
To run the analysis notebook:

1.  Clone this repository:
    ```bash
    git clone [https://github.com/yourusername/epigenetic-aging-clock.git](https://github.com/yourusername/epigenetic-aging-clock.git)
    ```
2.  Install dependencies:
    ```bash
    pip install pandas seaborn matplotlib huggingface_hub pyarrow fastparquet
    ```
3.  Open `Checkpoint1_EDA.ipynb` in Jupyter or Google Colab.

## References
* Kriukov, D., et al. (2025). *ComputAgeBench: Epigenetic Aging Clocks Benchmark*. Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining.
