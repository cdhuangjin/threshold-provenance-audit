# Threshold provenance audit: reproducibility code and outputs

This repository contains analysis code, frozen run protocols, environment/configuration manifests, machine-readable run outputs, and tests for BAF and ACS experiments. Input datasets are not included.

## Environment recorded in run manifests
- Intel(R) Core(TM) Ultra 7 270K Plus (24 physical cores / 24 logical processors; 40 MiB L2 and 36 MiB L3 cache), 16 GiB installed RAM (15.38 GiB visible to Windows); no GPU used
- 64-bit Windows 11 Pro build 26200; Python 3.12.10
- pandas 3.0.2, NumPy 2.4.4, LightGBM 4.7.0, scikit-learn 1.8.0
- folktables 0.0.12 for ACS

The author confirmed that the queried PC was the run machine. The hardware inventory was queried on 2026-09-28 after the runs; the manifests preserve this provenance distinction.

## Install
Use Python 3.12 and install the pinned core packages and plotting/runtime dependencies from `pyproject.toml`:

```powershell
python -m pip install -e .
python -m pip install -e ".[test]"  # only when running the included tests
```

## Run
Set the local dataset directories, then run the frozen commands:

```powershell
$env:PYTHONPATH = ".\src"
$bafDataDir = "C:\path\to\BAF"
$acsDataDir = "C:\path\to\WhyShift\acs\2018\1-Year"
python run_full_experiment.py --data-root $bafDataDir --output-dir results/full_threshold_policy_20260915 --resume
python run_external_transfer.py --data-root $acsDataDir --output-dir results/external_transfer_20260916_full
python survey_weight_sensitivity/run_sensitivity.py --data-root $acsDataDir --output-dir results/weighted_external_20260916 --resume
```

Set each directory to the local copy of the corresponding public source data. Exact input hashes, seeds, model settings, fit counts, and software versions for recorded runs are in JSON manifests under `results/`. Protocol files describe splits, filters, and thresholds. Raw input datasets are not included.

The code is licensed under the MIT License; see `LICENSE`. Input datasets retain their own source terms.
