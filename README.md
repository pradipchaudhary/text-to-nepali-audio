# nepali-tts

nepali audio converter

If your goal is to build **your own Nepali TTS engine** (not just an app that uses TTS), there are different levels of complexity.

| Goal                                                   | Difficulty | Time        |
| ------------------------------------------------------ | ---------- | ----------- |
| Build a TTS app using an existing open-source model    | ⭐⭐         | 1–3 days    |
| Fine-tune an existing model with your own Nepali voice | ⭐⭐⭐⭐       | 2–8 weeks   |
| Train a TTS model completely from scratch              | ⭐⭐⭐⭐⭐      | 3–12 months |

For most independent developers, **fine-tuning an existing open-source model** is the most practical path.

---

# TTS Engine Architecture

```
Text

↓

Text Normalization

↓

Tokenizer

↓

Phoneme Generator

↓

Acoustic Model

↓

Mel Spectrogram

↓

Vocoder

↓

WAV Audio
```

---

# Step 1: Learn the Basics

Understand these concepts:

* Text normalization
* Grapheme-to-Phoneme (G2P)
* Phonemes
* Spectrograms
* Vocoders
* Deep learning
* PyTorch

Recommended background:

* Python
* PyTorch
* NumPy
* Audio processing

---

# Step 2: Choose an Open-Source Model

Popular open-source TTS models include:

* **Piper** (lightweight, CPU-friendly)
* **VITS**
* **XTTS**
* **Coqui TTS**
* **StyleTTS2**
* **MeloTTS**
* **Kokoro TTS**

For Nepali, **VITS**, **StyleTTS2**, or **XTTS** are generally better starting points than training from scratch.

---

# Step 3: Collect a Nepali Dataset

This is the most important part.

Aim for:

* 10–100 hours of speech
* One speaker (for a single voice)
* Quiet recording environment
* 16-bit PCM WAV
* 22.05 kHz or 24 kHz

Example structure:

```
dataset/

wavs/

0001.wav
0002.wav
0003.wav

metadata.csv
```

---

# metadata.csv

```
0001|नमस्ते, तपाईंलाई स्वागत छ।
0002|आजको मौसम निकै राम्रो छ।
0003|जीवन एउटा यात्रा हो।
```

---

# Step 4: Record the Voice

Use:

* USB condenser microphone
* Quiet room
* Pop filter
* Audio interface (optional)

Recommended recording settings:

* Mono
* 24 kHz
* WAV
* 16-bit

---

# Step 5: Clean the Audio

Remove:

* Background noise
* Echo
* Breathing (if excessive)
* Long silences

Normalize audio levels.

Tools:

* Audacity
* FFmpeg
* SoX

---

# Step 6: Text Normalization

Convert text into a spoken form.

Examples:

```
२०२६

↓

दुई हजार छब्बीस
```

```
१०:३०

↓

दश बजेर तीस मिनेट
```

```
Rs.500

↓

पाँच सय रुपैयाँ
```

You'll likely need custom rules for Nepali numbers, dates, abbreviations, and currency.

---

# Step 7: Build a Nepali G2P System

A Grapheme-to-Phoneme (G2P) model converts written Nepali into pronunciation units.

Example:

```
नेपाल

↓

/ne pal/
```

A custom G2P improves pronunciation significantly.

---

# Step 8: Train the Acoustic Model

Using PyTorch:

```
Text

↓

Phonemes

↓

Encoder

↓

Attention

↓

Decoder

↓

Mel Spectrogram
```

Train until the model produces accurate mel spectrograms.

---

# Step 9: Train a Vocoder

Convert mel spectrograms into waveforms.

Popular vocoders:

* HiFi-GAN
* BigVGAN
* WaveGlow

---

# Step 10: Export the Model

Possible formats:

```
model.pt

model.onnx

model.pth
```

---

# Step 11: Build an Inference API

Example flow:

```
User Text

↓

Tokenizer

↓

TTS Model

↓

Vocoder

↓

WAV

↓

Browser
```

---

# Tech Stack

Frontend:

* Next.js
* React
* TypeScript

Backend:

* Python
* FastAPI

AI:

* PyTorch

Audio:

* FFmpeg

Deployment:

* Docker
* Linux

---

# Folder Structure

```
tts-engine/

dataset/
metadata.csv

wavs/

training/

models/

vocoder/

g2p/

api/

frontend/
```

---

# Typical Training Command

```
python train.py
```

Training time depends on:

* Dataset size
* GPU
* Model architecture

---

# Hardware

Minimum:

* NVIDIA RTX 3060 (12 GB VRAM)

Recommended:

* RTX 4090
* A100
* H100

Training on CPU is possible for experiments but is generally too slow for full models.

---

# Voice Cloning

To create a model that speaks like a particular person:

1. Record 30–60 minutes of clean speech (or more for better quality).
2. Segment and transcribe the recordings accurately.
3. Fine-tune a model that supports speaker adaptation (for example, XTTS or StyleTTS2).
4. Evaluate pronunciation and naturalness, then continue training if needed.

Only clone voices when you have the person's permission.

---

# Free Tools

* Python
* PyTorch
* FFmpeg
* Audacity
* Docker
* FastAPI
* ONNX Runtime

---

# A Realistic Roadmap

### Phase 1 (1–2 weeks)

* Learn PyTorch and audio fundamentals.
* Build a simple TTS API using an existing open-source model.

### Phase 2 (2–4 weeks)

* Record 10–20 hours of Nepali speech.
* Build text normalization and begin fine-tuning.

### Phase 3 (1–2 months)

* Fine-tune a high-quality open-source model.
* Improve pronunciation, pacing, and expressiveness.

### Phase 4 (Ongoing)

* Add multiple speakers.
* Improve prosody and emotional styles.
* Optimize for faster inference.

## If your long-term goal is to build something comparable to ElevenLabs for Nepali

That is feasible as a multi-stage project, but it typically involves several specialized models working together:

* Text normalization
* Nepali G2P
* Acoustic model
* Neural vocoder
* Speaker encoder
* Voice cloning
* Emotion/prosody control
* Streaming inference API
* Web application

A practical strategy is to start with a strong open-source model, build a high-quality Nepali dataset, and iterate from there rather than attempting to create every component from scratch. This dramatically reduces development time while still allowing you to create a unique Nepali TTS engine.

end
