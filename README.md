# MusicGen Audio Restoration

## Project Overview
This project evaluates and compares different audio restoration methods applied to MusicGen-generated audio. MusicGen outputs often contain noise, limited bandwidth, compression artifacts, etc. 

The main goal of this project is not only to improve audio quality, but to systematically compare the effectiveness of different restoration approaches and determine which method or combination of methods produces the best overall results.

The project compares classical DSP methods and multiple pretrained audio restoration models, and evaluates their performance using spectral analysis, CLAP score, spectrograms, and listening tests.

## Methods
I compare the following methods:

- **Raw MusicGen** – Original generated audio without processing
- **DSP (Baseline)** – DC offset removal, normalization, and gentle high-pass filtering
- **FlashSR** – Audio super-resolution model
- **AudioSR** – Audio super-resolution model (via online demo, see note below)
- **Apollo** – Audio restoration model
- **AudioSR + Apollo** – Combined restoration pipeline

---

## AudioSR Implementation Note
During the project, I encountered dependency and version compatibility issues when trying to run the AudioSR model on Google Colab (PyTorch, torchaudio, and CUDA version conflicts).

I used the online demo version of AudioSR to generate outputs:

AudioSR Demo:  
https://huggingface.co/spaces/Nick088/Audio-SR

## Repository Structure
```
musicgen-audio-restoration/
│
├── data/                      # All audio files
│   ├── musicgen_raw/
│   ├── dsp_output/
│   ├── flashsr_output/
│   ├── audiosr_output/
│   ├── apollo_output/
│   ├── audiosr_apollo_output/
│   └── prompts.csv
│
├── preprocessing/             # Preprocessing scripts
│   ├── dsp_preprocessing.ipynb
│   └── audiosr_input.ipynb
│
├── models/                    # Model inference scripts
│   ├── generate_musicgen_interface.ipynb
│   ├── flashsr_interface.ipynb
│   └── audiosr_plus_apollo_interface.ipynb
│
├── evaluation/                # Evaluation scripts
│   ├── clap.ipynb
│   ├── mos.ipynb
│   ├── spectral_analysis.ipynb
│   └── spectrogram.ipynb
│
├── results/                   # Tables, figures
│   ├── clap_results/
│   ├── spectral_results/
│   └── figures
│
└── README.md
```

## Evaluation Methods
I evaluate audio quality using multiple objective and subjective metrics:

Spectral Analysis:
- Spectral centroid
- Spectral bandwidth
- Spectral roll-off
- Spectral flatness
- High-frequency energy

CLAP Score:
I use a pretrained CLAP model to compute similarity between the raw generated audio, the improved versions, and the original text prompt.

Spectrogram Analysis:
I visually compare spectrograms to check frequency reconstruction and high-frequency content across different methods.

MOS (Mean Opinion Score):
I perform a listening test where different audio samples are rated by listeners to evaluate perceptual audio quality.

## How to Run
Step 1 – Generate MusicGen Audio:
models/generate_musicgen_interface.ipynb

Step 2 – DSP Baseline:
preprocessing/dsp_preprocessing.ipynb

Step 3 – FlashSR:
models/flashsr_interface.ipynb

Step 4 – AudioSR (Preprocessing + Demo):
Run preprocessing:
preprocessing/audiosr_input.ipynb
Then upload the processed audio to the AudioSR demo and download the outputs.

Step 5 – AudioSR + Apollo:
models/audiosr_plus_apollo_interface.ipynb

Step 6 – Evaluation:
evaluation/spectral_analysis.ipynb
evaluation/clap.ipynb
evaluation/spectrogram.ipynb
evaluation/mos.ipynb

## Results
Results are stored in:
results/clap_results/
results/spectral_results/
results/figures/

These include numerical evaluation tables and spectrogram comparisons.

## Final Goal of the Project
The main objective of this project is to identify which restoration method provides the best improvement over raw MusicGen audio and to determine whether combining models (e.g., AudioSR + Apollo) produces better results than individual models. The outcome of the project is a restoration pipeline based on experimental evaluation.

## Author
Seyedamin Hosseini
hosseini.2047991@studenti.uniroma1.it
Sapienza University of Rome
Master’s Degree in Computer Science
Course: Deep Learning and Applied AI
