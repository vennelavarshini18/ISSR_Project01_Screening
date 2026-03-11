# HumanAI, ISSR Project 01, University of Alabama
## Team communication processing and analysis in human-factors simulated environment, GSoC 2026 Screening Test 
# Team Communication Processing — GSoC 2026 Screening
**HumanAI / TRIP Lab, University of Alabama**
**Name:** Vennela Varshini Anasoori


## Overview

This submission covers the two main parts of the screening task:

1. Selecting and analyzing a suitable public dataset for team communication audio
2. Implementing and evaluating audio enhancement techniques on a sample recording


## Notebook 1: Dataset Selection
**File:** `Dataset_selection_N1.ipynb`

### Goal
Choose the most suitable dataset for team communication analysis and explore a sample.

### Dataset Used
**AMI Meeting Corpus** — https://groups.inf.ed.ac.uk/ami/corpus/

I evaluated four candidate datasets (AMI, LibriSpeech, NOIZEUS, CHiME-6) against criteria directly relevant to this project. AMI was the only one that satisfied all of them.

I specifically used the **IHM (Individual Headset Microphone)** channel, where each speaker is recorded through their own close-talking headset mic. This is the same setup TRIP Lab uses in their simulated studies, which makes AMI IHM the closest available match to real TRIP Lab recordings.

**Why AMI:**
- Real groups of 3–5 people working on tasks together, not scripted or read speech
- Natural conversation dynamics: interruptions, overlapping speech, coordination
- Word-level speaker-aligned transcripts for per-speaker evaluation
- Annotated overlapping speech segments, important for diarization
- Standard benchmark for speaker diarization and meeting transcription research
- 100+ hours, openly available for academic use

### What I analyzed
- Waveform and spectrogram → `sample_waveform_spectrogram.png`
- MFCC features (13 coefficients) → `sample_mfcc.png`
- Basic audio stats: RMS energy, zero crossing rate, spectral centroid, estimated SNR


## Notebook 2: Audio Enhancement
**File:** `Audio_enhancement_N2.ipynb`

### Goal
Apply audio enhancement methods to improve speech clarity and evaluate how much the audio improves, including whether it becomes more suitable for transcription.
Apply audio enhancement methods to improve speech clarity and evaluate how much each one helps, including whether the audio becomes more suitable for transcription.

### Methods

| Method | Output |
|---|---|
| High-pass filter + normalization | `enhanced_highpass.wav` |
| Spectral subtraction | `enhanced_spectral_subtraction.wav` |
| Wiener filter | `enhanced_wiener.wav` |
| Non-stationary noise reduction (noisereduce) | `enhanced_noisereduce.wav` |
| Combined classical pipeline | `sample_output.wav` |

### Evaluation

Each method was measured across five metrics:

| Metric | What it measures |
|---|---|
| SNR (dB) | How much noise was removed relative to the signal |
| RMS | Overall signal energy level |
| Spectral Flatness | Noise vs tonal balance of the audio |
| STOI | Speech intelligibility for transcription (0–1, higher is better) |
| DNSMOS | Perceptual quality score, no clean reference needed (1–5 MOS scale) |

STOI was included because the task requires enhancement to help transcription, and STOI directly measures how understandable the speech is. DNSMOS was included because it works without a clean reference file, which is important for real TRIP Lab recordings where no reference will be available.

**Key findings:**
- NoiseReduce (NS) scored highest on DNSMOS (1.725) and performed well across all metrics, making it the most balanced method overall
- The Wiener filter achieved the best STOI (0.638), meaning it preserved speech content better than the other methods
- The combined pipeline scored lowest on both STOI and DNSMOS despite being the most complex, showing that more processing steps do not always help


## Files

| File | Purpose |
|---|---|
| `Dataset_selection_N1.ipynb` | Dataset selection, evaluation, and sample analysis |
| `Audio_enhancement_N2.ipynb` | Enhancement methods and evaluation |
| `sample_input.wav` | Input meeting audio (3 min AMI IHM sample) |
| `sample_noisy.wav` | Noisy version (simulated environment) |
| `enhanced_highpass.wav` | Method 1 output |
| `enhanced_spectral_subtraction.wav` | Method 2 output |
| `enhanced_wiener.wav` | Method 3 output |
| `enhanced_noisereduce.wav` | Method 4 output |
| `sample_output.wav` | Combined pipeline output |
| `sample_waveform_spectrogram.png` | Input waveform and spectrogram |
| `sample_mfcc.png` | MFCC visualization |
| `waveform_comparison.png` | Waveform comparison across all methods |
| `spectrogram_comparison.png` | Spectrogram comparison across all methods |


## Setup
```bash
pip install -r requirements.txt
```


## Run Order

1. `Dataset_selection_N1.ipynb` — dataset selection and exploratory analysis
2. `Audio_enhancement_N2.ipynb` — enhancement and evaluation

1. `Dataset_selection_N1.ipynb`
2. `Audio_enhancement_N2.ipynb`