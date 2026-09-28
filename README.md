# Threshold provenance audit: reproducibility code and outputs

This repository contains the analysis implementation, frozen run protocols, environment/configuration manifests, machine-readable run outputs, and tests for the BAF and ACS experiments. Input datasets are not included.

## Environment recorded in run manifests
- Windows 11; Python 3.12.10
- pandas 3.0.2, NumPy 2.4.4, LightGBM 4.7.0, scikit-learn 1.8.0
- folktables 0.0.12 for ACS

## Run commands
From this directory, install the dependencies listed in `pyproject.toml` and set `PYTHONPATH=src`. Then run:

```powershell
python run_full_experiment.py --data-root <BAF_DATA_DIR> --output-dir results/full_threshold_policy_20260915 --resume
python run_external_transfer.py --data-root <WHySHIFT_ACS_DATA_DIR> --output-dir results/external_transfer_20260916_full
python survey_weight_sensitivity/run_sensitivity.py --data-root <WHySHIFT_ACS_DATA_DIR> --output-dir results/weighted_external_20260916 --resume
```

Set each data directory to the local copy of the corresponding public source data. The exact input hashes, seeds, model settings, fit counts, and software versions for the recorded runs are in the JSON run manifests under `results/`. The source protocols describe the splits, filters, and thresholds. Raw input data are not included.

The code is licensed under the MIT License; see `LICENSE`. Input datasets retain their own source terms and are not included.
