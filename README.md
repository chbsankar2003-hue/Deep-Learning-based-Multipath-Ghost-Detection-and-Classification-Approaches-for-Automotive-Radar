# Deep Learning-based Multipath Ghost Detection and Classification for Automotive Radar

TU Dortmund Master Project

## Objective

Implement and evaluate a Physics-Aware Graph Neural Network (PAGNN) for detecting multipath ghost targets in automotive radar point clouds.

The project follows the assigned workflow:
1. Study radar multipath and the PAGNN publication.
2. Build data loaders, scenario/sequence-disjoint splits, and evaluation tools for the Radar Ghost Dataset and View-of-Delft (VoD).
3. Reproduce and validate PAGNN on the Radar Ghost Dataset.
4. Adapt the method to VoD 3+1D radar data and moving-ego-vehicle measurements, including ego-motion-compensated Doppler and urban reflector extraction.
5. Train with three random seeds; select hyperparameters using validation data only; report precision, recall, F1 for the multipath class by range, model size, and inference time.
6. Document results in an IEEE-format report and final presentation.

## Planned repository structure

```text
.
├── configs/             # Experiment and dataset configurations
├── docs/                # Notes, literature review, setup and experiment records
├── scripts/             # Data inspection, preprocessing and experiment scripts
├── src/
│   ├── data/            # Dataset readers and preprocessing
│   ├── geometry/        # Reflector extraction and multipath geometry
│   ├── models/          # PAGNN modules
│   ├── training/        # Training and validation
│   └── evaluation/      # Metrics and analysis
├── tests/               # Unit and integration tests
├── outputs/             # Local-only experiment outputs (not committed)
├── README.md
└── .gitignore
```

## Important data policy

Do not commit datasets, raw/processed point clouds, labels supplied with the dataset, credentials, or large model checkpoints to this repository. The dataset is stored separately on the university lab PC. Follow the supervisor's instructions and obtain/confirm the required dataset permission before using or redistributing it.

## Environment

Record the exact Python, PyTorch, CUDA runtime, NVIDIA driver, spconv, OpenPCDet commit, and package versions used for every experiment. Do not assume that the home and lab machines have identical GPU environments.

## Current status

- [ ] Confirm dataset permission and document the supplied dataset layout.
- [ ] Verify the lab OpenPCDet/PyTorch/CUDA installation.
- [ ] Run an existing OpenPCDet PointPillars training smoke test on VoD.
- [ ] Implement dataset inspection and loaders.
- [ ] Reproduce PAGNN on Radar Ghost Dataset.
- [ ] Adapt and evaluate on VoD.
