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

## Dataset strategy

UNSAID uses multiple publicly available ISL datasets as a **raw data pool**. The datasets will not be blindly merged. Before training, they will be audited for class overlap, duplicate images, inconsistent labels, annotation quality, image quality, and signer leakage.

### Current dataset pool

| Dataset | Approx. scope | Role | Status |
|---|---|---|---|
| **Indian Sign Language** | 6,770 images / 32 classes | Primary ISL dataset | 🟢 Downloaded |
| **Indian Sign Language_40** | ~3,381 images / 44 classes | Additional vocabulary and signer diversity | 🟢 Downloaded |
| **Sign language** | ~590 images / 87 classes | Optional supplementary data | 🟡 Downloaded |
| **Indian sign language — multiclass** | ~9,900 images | Additional ISL data for later comparison | 🟢 Downloaded |

### Dataset workflow

```text
Raw Roboflow datasets
        ↓
Dataset inventory
        ↓
Class-name normalization
        ↓
Class overlap analysis
        ↓
Duplicate / near-duplicate detection
        ↓
Image and annotation quality checks
        ↓
Final UNSAID vocabulary
        ↓
Signer-aware train / validation / test split
        ↓
MediaPipe landmark extraction
        ↓
Processed ML dataset
```

### Initial vocabulary target

The first UNSAID model will target approximately **20–30 useful ISL signs** rather than attempting to learn every available class immediately. Candidate classes will be selected based on conversational usefulness, sample availability, label consistency, and visual separability.

Examples from the current data pool include signs such as:

`Hello` · `Help` · `Water` · `Food` · `Please` · `Sorry` · `Thank-you` · `Yes` · `No` · `Today` · `Time` · `What` · `Where` · `I` · `You`

The final vocabulary will be frozen only after the dataset audit.

### Dataset formats

The Roboflow datasets were downloaded in formats appropriate to their original annotation types, including **YOLOv11**, **YOLOv8**, and multiclass annotation formats. These formats are treated as raw dataset representations; they do **not** determine the final UNSAID model architecture.

For the initial pipeline, the images will be processed into hand landmarks using MediaPipe before training the classifier.

### Dataset provenance

Dataset sources, licenses, preprocessing steps, class mappings, and any self-collected data protocol will be documented in `docs/dataset.md` before training. Raw datasets are intentionally excluded from Git and should remain outside version control.

## Design system

UNSAID follows a classic, professional visual language designed to feel calm, credible, accessible, and human rather than overly futuristic.

### Color palette

| Role | Hex | RGB | Usage |
|---|---|---|---|
| Primary | `#F9F7F7` | `249, 247, 247` | Main backgrounds |
| Secondary | `#DBE2EF` | `219, 226, 239` | Cards and secondary surfaces |
| Tertiary | `#3F72AF` | `63, 114, 175` | Primary actions, links, active states |
| Neutral | `#112D4E` | `17, 45, 78` | Headings, body text, navigation |

### Typography

UNSAID uses a serif/sans-serif pairing to balance editorial character with interface readability:

- **Source Serif 4** — logo, headings, and major display text
- **Inter** — body copy, navigation, buttons, labels, controls, and technical/data UI

Typography should remain restrained and professional. Avoid overly rounded, playful, futuristic, or decorative typefaces.

### Visual principles

- Minimal and accessible
- Calm rather than flashy
- High readability and clear hierarchy
- Restrained use of color
- No unnecessary gradients or excessive glassmorphism
- Interfaces should feel like a serious accessibility product, not a generic AI dashboard

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
- Dataset audit and consolidation plan

### Phase 1 — Dataset engineering
- Inspect all downloaded ISL datasets
- Normalize class names
- Identify overlapping and duplicate samples
- Select the initial 20–30-sign vocabulary
- Create a reproducible signer-aware split

### Phase 2 — Static sign recognition
- Extract MediaPipe hand landmarks
- Normalize landmark coordinates
- Build the processed feature dataset
- Train a baseline classifier
- Evaluate on unseen samples and, where possible, unseen signers

### Phase 3 — Real-time inference
- Webcam pipeline
- Live landmark extraction
- Prediction smoothing
- Confidence thresholding
- Live text output

### Phase 4 — Dynamic signs
- Sequence data
- Temporal model
- Sign-boundary detection
- Evaluation across unseen signers

### Phase 5 — Language layer
- Word buffering
- Basic sentence normalization
- Text-to-speech

### Phase 6 — Product polish
- Web UI
- Model/API integration
- Performance optimization
- Deployment

## ML evaluation principles

UNSAID will not rely only on training accuracy. Evaluation should include validation/test splits and, where possible, **unseen signers** so that performance reflects generalization rather than memorization of individual people.

Important evaluation metrics will include:

- Accuracy
- Macro F1-score
- Per-class precision and recall
- Confusion matrix
- Inference latency / FPS
- Performance on unseen signers

## Data policy

Raw datasets should not be committed to Git. Large files, generated features, model checkpoints, and local environments are excluded through `.gitignore`.

Each dataset used by UNSAID should have its source, license, version, class mapping, preprocessing decisions, and transformation history documented before it becomes part of a training run.

## Status

**Early development — repository bootstrap and dataset acquisition complete.**

### Current milestone

> **Next: audit and consolidate the four downloaded ISL datasets before training.**

No model has been trained yet. UNSAID will first establish a clean, reproducible dataset and baseline before moving to real-time inference.

## License

MIT License — see `LICENSE`.
