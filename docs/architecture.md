# UNSAID Architecture

## Target pipeline

```text
Camera
  ↓
Frame capture
  ↓
Hand / pose landmark extraction
  ↓
Landmark preprocessing
  ↓
Static classifier OR temporal sequence model
  ↓
Confidence filtering + prediction smoothing
  ↓
Sign / word buffer
  ↓
Sentence normalization
  ↓
Text output + text-to-speech
```

## Why landmarks first?

The initial system uses MediaPipe hand landmarks rather than training an end-to-end image model immediately. Landmarks give the model a compact numerical representation of hand geometry and make the first experiments faster and easier to debug.

## Static recognition

For static signs, a single normalized landmark vector is passed to a baseline classifier. The first benchmark should establish accuracy, per-class precision/recall, confusion matrix, and inference latency.

## Dynamic recognition

For movement-based signs, a fixed-length or padded sequence of landmark vectors is passed to a temporal model such as a GRU, LSTM, or Transformer encoder. The temporal model should be introduced only after the static baseline is working.

## Real-time inference

The real-time loop should:

1. Capture a frame.
2. Extract landmarks.
3. Normalize landmarks.
4. Run model inference.
5. Reject low-confidence predictions.
6. Smooth repeated predictions.
7. Emit a sign only when a stable prediction is detected.
8. Append accepted signs to the word buffer.

## Evaluation

Accuracy alone is insufficient. Track:

- Accuracy
- Macro F1
- Per-class precision and recall
- Confusion matrix
- Median inference latency
- Performance on unseen signers

The unseen-signer evaluation is especially important because the goal is to generalize to people who did not contribute training examples.

## Expansion path

The architecture should leave room for two-handed signs and body/pose landmarks without forcing them into the first MVP. A later model can combine hand and pose features before temporal modeling.
