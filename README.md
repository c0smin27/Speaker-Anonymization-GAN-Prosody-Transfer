# Speaker Anonymization via GAN-driven Artificial Embeddings and Prosody Transfer

## Description

This repository summarizes the research presented at the **2025 IEEE International Conference on Intelligent Computer Communication and Processing (ICCP)**, held in **Cluj-Napoca, Romania, October 16–18, 2025**.  
The paper proposes a **speaker anonymization pipeline** combining **Generative Adversarial Networks (GANs)**, **prosody transfer**, and a **speech-to-text-to-speech (S2T2S)** architecture.

The complete publication can be found in `Speaker_Anonymization_GAN_Artificial_Embeddings_Prosody_Transfer.pdf`.

## Abstract

The system anonymizes a speaker’s voice by cascading speech recognition and synthesis models.  
A **multi-speaker TTS model** is driven by:
- a **GAN-based artificial embedding generator** that produces synthetic, non-identifiable voice embeddings, and  
- a **prosody transfer module** that preserves natural rhythm and intonation.  

The GAN learns the statistical distribution of real speaker embeddings but generates vectors unrelated to any real identity.  
Experimental results show:
- **Low cosine similarity** between original and anonymized embeddings (≈0.12–0.14)  
- **Consistent diversity** among anonymized voices (≈0.14–0.16)  
- **Good prosody retention**, with intelligibility rated at MOS ≈ 3.6  

The proposed approach represents a balance between **speaker privacy** and **linguistic fidelity**.

## System Architecture

**Pipeline overview:**

1. **Automatic Speech Recognition (ASR)**  
   - Implemented with **OpenAI Whisper** (Romanian model).  
   - Extracts linguistic content, removing voice-specific cues.

2. **Prosody Extraction**  
   - Retrieves pitch (F0), energy, and duration using **Librosa** and **Parselmouth**.  
   - Enables natural prosody cloning in the anonymized voice.

3. **Speaker Embedding Extraction**  
   - Performed with **ECAPA-TDNN** via **SpeechBrain**.  
   - Provides real embeddings for GAN training.

4. **GAN-based Embedding Generation**  
   - Custom **Wasserstein GAN with Gradient Penalty (WGAN-GP)**.  
   - Generates 192-dimensional synthetic embeddings from a 64-dimensional latent space.  
   - Includes **diversity loss** to avoid mode collapse.  
   - Trained on **Mozilla Common Voice 21.0** (Romanian subset).

5. **Speech Synthesis with Prosody Transfer**  
   - Uses **IMS-Toucan TTS** with **HiFi-GAN vocoder**.  
   - Synthesizes anonymous voices while preserving timing, rhythm, and pitch.

6. **Visualization Tool**  
   - Displays pitch contours, energy, duration, and cosine similarity before and after anonymization.  
   - Includes parallel playback for original vs. anonymized speech.

## Key Results

| Metric | Description | Result |
|--------|--------------|--------|
| **Cosine Similarity (orig–anon)** | Mean distance between embeddings | 0.12–0.14 |
| **Cosine Similarity (anon–anon)** | Diversity among synthetic voices | 0.14–0.16 |
| **WER (Original)** | Word Error Rate for original ASR | 5.45% |
| **WER (Anonymized)** | Word Error Rate for anonymized ASR | 37.74% |
| **MOS** | Intelligibility (1–5 scale) | 3.59 ± 0.14 |
| **PESQ** | Perceptual quality (1–5) | ~2.7 |
| **STOI** | Intelligibility (0–1) | 0.55–0.95 |

## Technologies and Frameworks

- **Python 3**, **PyTorch**
- **Whisper (ASR)**, **IMS-Toucan (TTS)**, **HiFi-GAN (vocoder)**
- **SpeechBrain (ECAPA-TDNN embeddings)**
- **Librosa**, **Parselmouth**, **Matplotlib**
- **WGAN-GP**, **Diversity Loss**
- **t-SNE visualization**, **PESQ/STOI evaluation**

## Novel Contributions

- GAN-based **artificial speaker embeddings** independent of real identities  
- Integration of **prosody transfer** onto fully synthetic voices  
- Implementation tailored for **Romanian language**, filling a gap in multilingual anonymization research  
- **Visualization dashboard** for pitch and embedding comparison  
- Achieved anonymization–naturalness trade-off suitable for privacy-preserving communication

## Experimental Evaluation

- GAN trained on **443 Romanian voices** (22 hours of speech).  
- Synthetic embeddings display strong anonymization and stable diversity.  
- Speech remains intelligible for human listeners while unrecognizable to ASR-based identification.  
- Processing speed: **~7.5 seconds per 5-second segment** on RTX 3060 GPU.

## Future Work

- Integration of more advanced ASR and TTS models  
- Development of automated quality and privacy assessment tools  
- Real-time anonymization optimization and adaptive GAN tuning  
- Expanded perceptual evaluation with larger multilingual datasets  

## Citation

If you reference this work, please cite:

**Dumitru-Cosmin Melinte and Mircea Giurgiu**,  
“*Speaker Anonymization via GAN-driven Artificial Embeddings and Prosody Transfer*,”  
*Proc. 2025 IEEE International Conference on Intelligent Computer Communication and Processing (ICCP)*, Cluj-Napoca, Romania, October 16–18, 2025.  
IEEE, 2025.

## File

- `Speaker_Anonymization_GAN_Artificial_Embeddings_Prosody_Transfer.pdf` – Full paper (IEEE format)

---

*© 2025 Dumitru-Cosmin Melinte. Presented at IEEE ICCP 2025, Cluj-Napoca, Romania.*
