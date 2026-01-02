# AI Singing Voice Conversion (Voice Replacement System)

## Overview

This project implements an **AI-based Singing Voice Conversion system** that replaces the original singer’s voice in a song with a target singer’s voice, while preserving:

* 🎵 Melody & pitch
* 📝 Lyrics & pronunciation
* 🎶 Original instrumental music

The system accepts:

1. A full song audio file (vocals + music)
2. Voice samples of a target singer

And produces:

* A new version of the song where the **original singer is replaced** by the target voice.

This project is designed as a **local, research-grade AI system**, developed on **Windows using VS Code**, and optimized for learning, experimentation, and future productization.

---

## Core Concept

In AI terminology, this problem is called:

> **Singing Voice Conversion (SVC)**

The system does **not** generate a new song. Instead, it:

* Extracts the *content* (lyrics + phonetics)
* Extracts the *pitch* (melody)
* Replaces only the *timbre* (voice identity)

This allows the target voice to sing the *same song* naturally.

---

## High-Level Workflow

1. **Input Song** → Vocal & Instrumental Separation
2. **Target Voice Samples** → Model Training
3. **Voice Conversion** → Replace singer
4. **Audio Mixing** → Final song output

```
Song.wav
  │
  ├──► Vocal Separation
  │      ├── vocals.wav
  │      └── instrumental.wav
  │
  ├──► Voice Conversion Model (RVC)
  │      └── converted_vocals.wav
  │
  └──► Audio Mixing
         └── final_song.wav
```

---

## System Architecture

### 1. Audio Separation Layer

* Separates vocals from background music
* Ensures music quality is preserved

**Tool:** Demucs

---

### 2. Feature Extraction Layer

Extracts key vocal features:

* **Pitch (F0):** Melody of the song
* **Content embeddings:** Phonetic structure
* **Timing:** Alignment with original audio

**Models used:**

* HuBERT (content encoder)
* RMVPE (high-accuracy pitch extraction)

---

### 3. Voice Conversion Model

This is the core AI model.

**Model:** RVC (Retrieval-based Voice Conversion)

Learns:

* Vocal tract characteristics
* Timbre and tone of the target singer

Does NOT learn:

* Song melody
* Lyrics
* Music

---

### 4. Vocoder

Converts model outputs into realistic waveform audio.

Preserves:

* Emotion
* Expression
* Singing dynamics

---

### 5. Mixing & Post-processing

* Combines converted vocals with original instrumental
* Ensures volume balance and clarity

**Tool:** FFmpeg

---

## Technology Stack

### Programming & Environment

* **Python 3.10**
* **VS Code** (development)
* **Git** (version control)

### AI & ML

* **PyTorch** (deep learning framework)
* **RVC (Retrieval-based Voice Conversion)**
* **HuBERT** (speech content modeling)
* **RMVPE** (pitch extraction)

### Audio Processing

* **Demucs** – vocal/instrument separation
* **Librosa** – audio analysis
* **Soundfile** – WAV handling
* **FFmpeg** – audio mixing

### Optional UI (Future Scope)

* Gradio
* Streamlit

---

## Project Directory Structure

```
ai-voice-conversion/
├── data/
│   ├── songs/
│   └── raw_samples/
│
├── datasets/
│   └── target_singer/
│       ├── 001.wav
│       ├── 002.wav
│       └── ...
│
├── separated/
│   └── song_name/
│       ├── vocals.wav
│       └── instrumental.wav
│
├── Retrieval-based-Voice-Conversion-WebUI/
│   ├── infer-web.py
│   ├── assets/
│   ├── logs/
│   └── weights/
│
├── inference/
│   └── converted_vocals.wav
│
├── final/
│   └── final_song.wav
│
└── README.md
```

---

## Training Pipeline

### Input Requirements

* Clean voice samples (single singer)
* WAV format
* 5–30 minutes total duration
* Minimal background noise

### Training Process

1. Audio normalization
2. Feature extraction
3. Pitch alignment
4. Timbre learning
5. Checkpoint saving

### Output

* `.pth` model file
* Index files for retrieval

---

## Inference Pipeline

### Inputs

* `vocals.wav`
* Trained voice model

### Controls

* Pitch transpose (gender adjustment)
* Index rate (voice similarity)
* Noise reduction

### Output

* `converted_vocals.wav`

---

## Performance & Hardware

### Minimum Recommended

* NVIDIA GPU (6GB VRAM)
* 16GB RAM
* SSD storage

### Training Time

* RTX 3060: ~45 minutes
* RTX 4070: ~25 minutes

---

## Common Challenges

### Robotic Voice

* Increase training data
* Reduce overfitting
* Adjust index rate

### Pitch Errors

* Use RMVPE
* Apply pitch transpose

### Artifacts

* Improve sample quality
* Use noise-free recordings

---

## Ethical & Legal Considerations

⚠️ This project is intended for:

* Personal research
* Education
* Non-commercial experimentation

Do NOT:

* Impersonate real artists commercially
* Redistribute copyrighted content

---

## Future Enhancements

* So-VITS-SVC integration
* Diffusion-based singing models
* Indian classical & film music optimization
* Local web UI
* Multi-language singing support

---

## Learning Goals of This Project

This project is also a **learning-first AI system**, designed to help understand:

* Audio ML pipelines
* Voice representation learning
* Pitch & timbre separation
* End-to-end ML system design

---

## Author & Vision

This project bridges:

* **Software Architecture**
* **AI/ML**
* **Music & Sound Healing**

With the long-term vision of building **ethical, human-centric voice AI systems**.

---

## License

This project is for research and educational purposes only.

---

If you are reading this README, you are at the intersection of **technology, sound, and intelligence**.
