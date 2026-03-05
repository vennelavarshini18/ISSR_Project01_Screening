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
Choose a suitable dataset and analyze a small sample.

### Dataset Used
**AMI Meeting Corpus**

**Why this dataset**
- Contains 100+ hours of real meeting recordings (multiple speakers)
- Represents natural team communication
- Open for academic research
- Includes speaker transcripts
- Commonly used in speech/NLP research

### What I analyzed
- Waveform and spectrogram → `sample_waveform_spectrogram.png`
- MFCC features (13 coefficients) → `sample_mfcc.png`
- Basic audio stats:
  - RMS energy
  - Zero crossing rate
  - Spectral centroid
  - Estimated SNR

---

## Notebook 2 — Audio Enhancement
**File:** `Audio_enhancement_N2.ipynb`

### Goal
Apply a few audio enhancement methods to improve speech clarity.

### Methods Used

| Method | Output |
|------|------|
| High-pass filter + normalization | `enhanced_highpass.wav` |
| Spectral subtraction | `enhanced_spectral_subtraction.wav` |
| Wiener filter | `enhanced_wiener.wav` |
| Full pipeline (combined) | `sample_output.wav` |

### Evaluation
- Waveform comparison → `waveform_comparison.png`
- Spectrogram comparison → `spectrogram_comparison.png`
- Metrics used:
  - SNR
  - RMS energy
  - Spectral flatness

---

## Files

| File | Purpose |
|-----|-----|
| `Dataset_selection_N1.ipynb` | Dataset choice + sample analysis |
| `Audio_enhancement_N2.ipynb` | Enhancement methods + evaluation |
| `sample_input.wav` | Input meeting audio |
| `sample_noisy.wav` | Noisy version |
| `sample_output.wav` | Final enhanced output |
| `enhanced_spectral_subtraction.wav` | Method 1 result |
| `enhanced_wiener.wav` | Method 2 result |
| `enhanced_highpass.wav` | Method 3 result |
| `sample_waveform_spectrogram.png` | Input waveform + spectrogram |
| `sample_mfcc.png` | MFCC visualization |
| `waveform_comparison.png` | Enhancement comparison |
| `spectrogram_comparison.png` | Spectrogram comparison |

---
## Setup

Install the required dependencies:

```bash
pip install -r requirements.txt
```
---

## Run the notebooks in the following order:

1. Dataset_selection_N1.ipynb
2. Audio_enhancement_N2.ipynb
