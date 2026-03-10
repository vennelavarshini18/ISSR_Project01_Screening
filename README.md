# Team Communication Processing — GSoC 2026 Screening
**HumanAI / TRIP Lab, University of Alabama**  
**Name:** Vennela Varshini Anasoori

---

## Overview

This submission covers the two main parts of the screening task:

1. Selecting and analyzing a suitable public dataset for team communication audio
2. Implementing and evaluating audio enhancement techniques on a sample recording

---

## Notebook 1 — Dataset Selection
**File:** `Dataset_selection_N1.ipynb`

### Goal
Choose the most suitable dataset for team communication analysis and explore a sample.

### Dataset Used
**AMI Meeting Corpus** — https://groups.inf.ed.ac.uk/ami/corpus/

Before selecting AMI, I evaluated four candidate datasets (AMI, LibriSpeech, NOIZEUS, CHiME-6) against criteria directly relevant to this project: multi-speaker setting, real team communication, overlapping speech, diarization annotations, and benchmark prevalence. AMI was the only dataset that satisfied all of them.

**Why AMI is the best option:**
- Real groups of 3–5 people working together on tasks — not scripted, not read speech
- Natural conversation dynamics: interruptions, overlapping speech, coordination
- Word-level speaker-aligned transcripts for per-speaker transcription evaluation
- Annotated overlapping speech segments — critical for diarization
- Standard benchmark for speaker diarization (DER) and meeting transcription research
- 100+ hours, openly available for academic use

### What I analyzed
- Waveform and spectrogram → `sample_waveform_spectrogram.png`
- MFCC features (13 coefficients) → `sample_mfcc.png`
- Basic audio stats: RMS energy, zero crossing rate, spectral centroid, estimated SNR

---

## Notebook 2 — Audio Enhancement
**File:** `Audio_enhancement_N2.ipynb`

### Goal
Apply audio enhancement methods to improve speech clarity and evaluate how much the audio improves — including whether it becomes more suitable for transcription.

### Methods Used

| Method | Output |
|------|------|
| High-pass filter + normalization | `enhanced_highpass.wav` |
| Spectral subtraction | `enhanced_spectral_subtraction.wav` |
| Wiener filter | `enhanced_wiener.wav` |
| Full pipeline (all three combined) | `sample_output.wav` |

### Evaluation

Metrics were computed for each method against the original clean audio:

| Metric | What it measures |
|------|------|
| SNR (dB) | How much noise was removed |
| RMS | Signal energy level |
| Spectral Flatness | Noise vs tonal balance |
| STOI | Speech intelligibility — how suitable the audio is for transcription (0–1, higher is better) |

STOI (Short-Time Objective Intelligibility) was included specifically because the task requires enhancement to improve clarity for transcription. Unlike SNR, STOI directly reflects how understandable the speech is to a listener or transcription model.

**Key finding:** The Wiener filter achieved the highest STOI score, meaning it preserved speech content better than spectral subtraction or the combined pipeline. This suggests that for transcription purposes, Wiener filtering alone may outperform the full pipeline.

- Waveform comparison → `waveform_comparison.png`
- Spectrogram comparison → `spectrogram_comparison.png`

---

## Files

| File | Purpose |
|-----|-----|
| `Dataset_selection_N1.ipynb` | Dataset selection, evaluation, and sample analysis |
| `Audio_enhancement_N2.ipynb` | Enhancement methods and evaluation |
| `sample_input.wav` | Input meeting audio (3 min AMI sample) |
| `sample_noisy.wav` | Noisy version (simulated environment) |
| `sample_output.wav` | Final enhanced output (full pipeline) |
| `enhanced_spectral_subtraction.wav` | Spectral subtraction result |
| `enhanced_wiener.wav` | Wiener filter result |
| `enhanced_highpass.wav` | High-pass filter result |
| `sample_waveform_spectrogram.png` | Input waveform and spectrogram |
| `sample_mfcc.png` | MFCC visualization |
| `waveform_comparison.png` | Waveform comparison across methods |
| `spectrogram_comparison.png` | Spectrogram comparison across methods |

---

## Setup

Install the required dependencies:
```bash
pip install -r requirements.txt
```

---

## Run Order

1. `Dataset_selection_N1.ipynb` — dataset selection and exploratory analysis
2. `Audio_enhancement_N2.ipynb` — enhancement and evaluation