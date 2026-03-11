# HumanAI, ISSR Project 01, University of Alabama
## Team communication processing and analysis in human-factors simulated environment, GSoC 2026 Screening Test
**Name:** Vennela Varshini Anasoori


## Overview

This submission has two parts:

1. Picking and analyzing a public dataset suitable for team communication audio
2. Building and comparing audio enhancement methods on a sample from that dataset


## Notebook 1: Dataset Selection
**File:** `Dataset_selection_N1.ipynb`

### Goal
Find the most suitable dataset for this project and do a quick exploratory analysis on a sample.

### Dataset Used
**AMI Meeting Corpus**: https://groups.inf.ed.ac.uk/ami/corpus/

Before settling on AMI, I compared four options (AMI, LibriSpeech, NOIZEUS, CHiME-6) on criteria that matter for this project: multi-speaker setup, real team communication, overlapping speech, diarization annotations, and research benchmark usage. AMI was the only one that checked every box.

I used the **IHM (Individual Headset Microphone)** channel specifically, where each speaker is captured through their own close-talking headset. This matches the recording setup TRIP Lab uses in their simulated studies, so results here should transfer well to real lab data.

**Why AMI:**
- Real groups of 3–5 people doing tasks together, not actors or read speech
- Has natural interruptions, overlapping speech, and coordination patterns
- Word-level transcripts aligned per speaker
- Overlap annotations useful for studying turn-taking
- Widely used benchmark for diarization and meeting transcription
- 100+ hours, free for academic use

### What I analyzed
- Waveform and spectrogram -> `sample_waveform_spectrogram.png`
- MFCC features (13 coefficients) -> `sample_mfcc.png`
- Basic stats: RMS energy, zero crossing rate, spectral centroid, estimated SNR


## Notebook 2: Audio Enhancement
**File:** `Audio_enhancement_N2.ipynb`

### Goal
Test different enhancement methods on a noisy version of the AMI sample and see which one actually improves the audio for transcription.

### Methods

| Method | Output |
|---|---|
| High-pass filter + normalization | `enhanced_highpass.wav` |
| Spectral subtraction | `enhanced_spectral_subtraction.wav` |
| Wiener filter | `enhanced_wiener.wav` |
| Non-stationary noise reduction (noisereduce) | `enhanced_noisereduce.wav` |
| Combined classical pipeline | `sample_output.wav` |

### Evaluation

| Metric | What it measures |
|---|---|
| SNR (dB) | Noise removed relative to signal |
| RMS | Signal energy level |
| Spectral Flatness | Noise vs tonal balance |
| STOI | Speech intelligibility for transcription (0–1) |
| DNSMOS | Perceptual quality, no clean reference needed (1–5) |

I added STOI because the task is specifically about improving audio for transcription, and STOI measures that directly. DNSMOS was useful here because it does not need a clean reference file to work, which is exactly the situation TRIP Lab will face with their real recordings.

**What I found:**
- NoiseReduce (NS) scored highest on DNSMOS (1.725) and was the most consistent method across all five metrics
- The Wiener filter had the best STOI (0.638), so it preserved speech the best for transcription
- The combined pipeline actually scored worst on STOI and DNSMOS, which shows that chaining more methods together does not always give better results


## Files

| File | Purpose |
|---|---|
| `Dataset_selection_N1.ipynb` | Dataset selection and sample analysis |
| `Audio_enhancement_N2.ipynb` | Enhancement methods and evaluation |
| `sample_input.wav` | 3 min AMI IHM sample |
| `sample_noisy.wav` | Noisy version used for testing |
| `enhanced_highpass.wav` | Method 1 output |
| `enhanced_spectral_subtraction.wav` | Method 2 output |
| `enhanced_wiener.wav` | Method 3 output |
| `enhanced_noisereduce.wav` | Method 4 output |
| `sample_output.wav` | Combined pipeline output |
| `sample_waveform_spectrogram.png` | Input waveform and spectrogram |
| `sample_mfcc.png` | MFCC visualization |
| `waveform_comparison.png` | Waveform comparison across methods |
| `spectrogram_comparison.png` | Spectrogram comparison across methods |


## Setup
```bash
pip install -r requirements.txt
```

## Run Order
1. `Dataset_selection_N1.ipynb`
2. `Audio_enhancement_N2.ipynb`
