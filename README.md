# Hybrid Anomaly Detection in Satellites

Two-layer architecture for cyber-attack detection via data injection
in satellite telemetry, using the NASA SMAP P-1 channel.

- **Tier-1**: DPCM with leaky accumulator, executable on-board.
- **Tier-2**: LSTM-Autoencoder on the ground segment, with event
  consolidation and reconstruction-error filtering.

## Main results

| Metric | Tier-1 | Hybrid Pipeline |
|---|---|---|
| Precision | 0.039 | 0.456 |
| Recall | 0.557 | 0.523 |
| F1 | 0.073 | 0.487 |
| Bandwidth saving | 41.5% | 41.5% |

## Optimal configuration

- Tier-1: threshold = 0.025, forgetting factor = 0.9
- Tier-2: window = 30, LSTM layers 2×80, MAX_GAP = 2, threshold τ₂ = p99.5

## Requirements

Install dependencies with:

    pip install numpy pandas scikit-learn matplotlib seaborn tensorflow

## Expected structure

The notebook expects the `datasets/` folder containing the NASA SMAP files
to exist one level above the notebook directory:

    parent_folder/
    ├── datasets/
    │   └── data/
    │       ├── train/P-1.npy
    │       └── test/P-1.npy
    └── FinalProject/          (this repository)
        └── HybridAnomalyDetection_Definitivo.ipynb

To reproduce the results:

1. Download the telemanom dataset from
   https://www.kaggle.com/datasets/patrickfleith/nasa-anomaly-detection-dataset-smap-msl?resource=download
2. Extract the archive in the parent directory following the structure above.

## Execution

Open `HybridAnomalyDetection_Definitivo.ipynb` in Jupyter or VS Code and
run the cells in order.

## Author

María Begara Girón — Universidad Pontificia Comillas (ICAI)

## References

- Hundman, K. et al. (2018). *Detecting Spacecraft Anomalies Using LSTMs
  and Nonparametric Dynamic Thresholding.* KDD 2018.
- Holzmann, G.J. (2006). *The Power of 10: Rules for Developing
  Safety-Critical Code.* IEEE Computer.
