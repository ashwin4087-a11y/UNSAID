# Configs

Keep versioned experiment settings here rather than hard-coding them in training scripts.

Suggested future files:

```text
configs/
├── vocabulary.yaml
├── static_baseline.yaml
└── temporal_baseline.yaml
```

Each experiment should record the dataset version, class mapping, preprocessing choices, model hyperparameters, and evaluation split.