# Roman-to-Devanagari-Back-Transliteration-System
A parameter-efficient fine-tuned model optimized for real-world "Hinglish" noise, complex Devanagari clusters (half-characters), and named entity recognition. Features phonetic-aware data augmentation and word-level evaluation for high-accuracy phonetic mapping.

##  Key Features

- **Base Model**: Fine-tuned on `Gemma-2B-IT` using the Unsloth framework for 2x faster training and reduced memory usage.
- **Optimization**: Utilizes **LoRA (Low-Rank Adaptation)**, training only ~5.89% of total parameters (156M adapters) to preserve base model knowledge while specializing in script conversion.
- **Phonetic Data Augmentation**: Implements custom noise injection logic to simulate real-world typing behavior:
    - **Phonetic Swaps**: Accounts for common character replacements like 'v' ↔ 'w' or 'ee' ↔ 'i'.
    - **Schwa Deletion Simulation**: Random middle-vowel dropping to match fast typing patterns.
    - **Entity Capitalization Noise**: Improves robustness for Named Entity Recognition (NER) by training on varied case patterns.
- **Cluster Awareness**: Uses **NFC Unicode Normalization** to ensure complex Devanagari clusters (half-characters/viramas) are treated as atomic units.

##  Performance Metrics

The model is evaluated using word-level metrics to provide an accurate representation of linguistic "recall" compared to strict sentence-level matching.

| Metric | Internal Dataset (Augmented) | External Dataset (codebyam) |
| :--- | :--- | :--- |
| **CER** (Char Error Rate) | ~0.1708 | ~0.2108 |
| **WER** (Word Error Rate) | ~0.2617 | ~0.3370 |
| **chrF Score** | 73.4686 | 62.8604 |
| **Model Word Recall** | 0.8500+ | 0.6500+ |

##  Installation

```bash
pip install unsloth evaluate jiwer rouge-score sacrebleu
