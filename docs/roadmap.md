# UNSAID Roadmap

## Milestone 0 — Foundation

- [x] Repository created
- [x] Project documentation
- [x] Python environment configuration
- [x] ML architecture defined
- [x] Dataset policy defined

## Milestone 1 — Data pipeline

- [ ] Select and verify public ISL dataset source(s)
- [ ] Freeze initial 20–30 class vocabulary
- [ ] Build ingestion script
- [ ] Build landmark extraction script
- [ ] Create signer-aware train/validation/test split
- [ ] Run data quality checks

## Milestone 2 — Baseline model

- [ ] Train static landmark classifier
- [ ] Measure accuracy and macro F1
- [ ] Produce confusion matrix
- [ ] Test on unseen signers
- [ ] Save reproducible model artifact outside Git

## Milestone 3 — Real-time recognition

- [ ] Webcam capture
- [ ] Real-time landmark extraction
- [ ] Inference loop
- [ ] Confidence threshold
- [ ] Prediction smoothing
- [ ] Live word output

## Milestone 4 — Dynamic signs

- [ ] Collect/prepare sequence data
- [ ] Define sequence windowing
- [ ] Train GRU/LSTM baseline
- [ ] Compare temporal model against simpler baseline
- [ ] Evaluate unseen signers

## Milestone 5 — Language and speech

- [ ] Word buffer
- [ ] Sign-boundary handling
- [ ] Sentence normalization
- [ ] Text-to-speech

## Milestone 6 — Product

- [ ] Frontend
- [ ] Backend API
- [ ] Model serving
- [ ] Error/loading states
- [ ] Accessibility checks
- [ ] Deployment

## Definition of done for MVP

The MVP is complete when a user can open the app, enable their camera, perform supported ISL signs, receive stable text predictions with confidence handling, and hear the resulting text spoken aloud.
