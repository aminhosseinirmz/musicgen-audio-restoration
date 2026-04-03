# MusicGen Audio Restoration

## Project Overview
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
During the project, I encountered dependency and version compatibility issues when trying to run the AudioSR model locally and on Google Colab (PyTorch, torchaudio, and CUDA version conflicts).

I used the online demo version of AudioSR to generate outputs:

AudioSR Demo:  
https://huggingface.co/spaces/Nick088/Audio-SR

musicgen-audio-restoration/
│
├── data/ # All audio files
│ ├── musicgen_raw/
│ ├── dsp_output/
│ ├── flashsr_output/
│ ├── audiosr_output/
│ ├── apollo_output/
│ ├── audiosr_apollo_output/
│ └── prompts.csv
│
├── preprocessing/ # Preprocessing scripts
│ ├── dsp_preprocessing.ipynb
│ └── audiosr_input.ipynb
│
├── models/ # Model inference scripts
│ ├── generate_musicgen_interface.ipynb
│ ├── flashsr_interface.ipynb
│ └── audiosr_plus_apollo_interface.ipynb
│
├── evaluation/ # Evaluation scripts
│ ├── clap.ipynb
│ ├── mos.ipynb
│ ├── spectral_analysis.ipynb
│ └── spectrogram.ipynb
│
├── results/ # Tables, figures, audio examples
│ ├── clap_results/
│ ├── spectral_results/
│ ├── figures/
│ └── audio_examples/
│
├── report/
│ └── report.pdf
│
├── README.md
├── requirements.txt
└── .gitignore
