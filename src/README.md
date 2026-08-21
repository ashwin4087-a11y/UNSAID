# Source layout

The source tree is intentionally separated by responsibility:

```text
src/
├── data/        # dataset ingestion, validation, splitting
├── vision/      # webcam and MediaPipe processing
├── features/    # landmark normalization and feature generation
├── models/      # model definitions and checkpoints interface
├── training/    # training/evaluation entry points
└── inference/   # real-time prediction pipeline
```

Keep data processing, model code, and application/inference code separate so experiments remain reproducible.
