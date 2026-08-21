# UNSAID Dataset Strategy

## Goal

Build a reproducible dataset pipeline for an initial Indian Sign Language vocabulary, while keeping dataset sources and licensing explicit.

## Phase 1 data

Start with a constrained vocabulary of approximately 20–30 signs selected for practical conversational value and dataset availability. Exact labels will be frozen in a versioned configuration before model training.

## Source strategy

Use suitable public datasets as a starting point, then add self-collected samples where licensing and consent allow. Do not commit large datasets or private recordings to the repository.

For every external dataset, record:

- Dataset name and source URL
- Version/date accessed
- License
- Class labels used
- Number of samples per class
- Image/video format
- Preprocessing performed
- Any class remapping

## Recommended split

Avoid random frame-level splitting when several frames come from the same signer or recording. Prefer signer-aware splits:

```text
Train signers  → training set
Validation signers → validation set
Test signers → held-out test set
```

This provides a better estimate of generalization to people the model has not seen before.

## Landmark extraction

For the initial pipeline, convert compatible image/video samples into normalized hand landmarks. Store processed features separately from the original source data.

A feature record should retain at least:

```text
sample_id
signer_id (when available)
label
frame_index (for sequences)
landmarks
source
```

## Self-collected data

When collecting new data:

- obtain informed consent from participants;
- document the intended use and retention policy;
- vary lighting, background, camera distance, and signing speed;
- capture multiple sessions rather than repeated takes from one setup;
- keep signer identity metadata separate from model features where practical.

## Data quality checks

Before training:

- remove corrupted samples;
- verify labels;
- check class balance;
- detect duplicate or near-duplicate samples;
- inspect landmark extraction failures;
- verify that validation/test signers do not leak into training.

## Important limitation

A constrained-vocabulary recognizer is not a complete Indian Sign Language translator. The project should report its supported vocabulary and test conditions clearly.
