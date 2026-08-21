# UNSAID

> **Turning the unspoken into language.**

UNSAID is a real-time Indian Sign Language (ISL) recognition system that uses computer vision and machine learning to interpret hand gestures, convert them into meaningful text, and eventually speak them aloud.

## Project vision

```text
Webcam
  ↓
Hand / Pose Detection
  ↓
Landmark Extraction
  ↓
Preprocessing
  ↓
Machine Learning Model
  ↓
Sign Prediction
  ↓
Word Buffer
  ↓
Sentence Formation
  ↓
Text + Speech
```

The project is intentionally being built in stages. The first milestone is reliable recognition of a constrained ISL vocabulary; continuous signing and natural sentence generation come later.

## MVP scope

- Real-time webcam input
- Hand landmark extraction
- Recognition of an initial 20–30 ISL signs
- Confidence-aware predictions
- Text output
- Browser-based text-to-speech

## Planned architecture

### Computer vision
- OpenCV for camera/frame handling
- MediaPipe Hands (initially) for 21-point hand landmark extraction
- Optional YOLO-based detection later if it provides a measurable benefit

### Machine learning
- Python
- PyTorch
- Baseline static-sign classifier
- Temporal model (GRU/LSTM or Transformer) for dynamic signs

### Application
- FastAPI backend
- Next.js frontend
- Web Speech API for the first speech prototype

## Repository structure

```text
UNSAID/
├── README.md
├── .gitignore
├── LICENSE
├── pyproject.toml
├── requirements.txt
├── configs/
│   └── README.md
├── data/
│   ├── raw/.gitkeep
│   ├── processed/.gitkeep
│   └── README.md
├── notebooks/
│   └── README.md
├── src/
│   ├── data/
│   ├── vision/
│   ├── features/
│   ├── models/
│   ├── training/
│   └── inference/
├── app/
│   └── README.md
├── tests/
│   └── README.md
└── docs/
    ├── architecture.md
    ├── roadmap.md
    └── dataset.md
```

## Development roadmap

### Phase 0 — Foundation
- Repository structure
- Environment setup
- Dataset research
- Label/vocabulary definition

### Phase 1 — Static sign recognition
- Collect/prepare image data
- Extract landmarks
- Train baseline classifier
- Evaluate on unseen samples

### Phase 2 — Real-time inference
- Webcam pipeline
- Prediction smoothing
- Confidence thresholding
- Live text output

### Phase 3 — Dynamic signs
- Sequence data
- Temporal model
- Sign-boundary detection
- Evaluation across unseen signers

### Phase 4 — Language layer
- Word buffering
- Basic sentence normalization
- Text-to-speech

### Phase 5 — Product polish
- Web UI
- Model/API integration
- Performance optimization
- Deployment

## ML evaluation principles

UNSAID will not rely only on training accuracy. Evaluation should include validation/test splits and, where possible, **unseen signers** so that performance reflects generalization rather than memorization of individual people.

## Data policy

Dataset sources, licenses, preprocessing steps, class mappings, and any self-collected data protocol will be documented in `docs/dataset.md` before training.

## Status

**Early development — repository bootstrap complete.**

## License

MIT License — see `LICENSE`.
