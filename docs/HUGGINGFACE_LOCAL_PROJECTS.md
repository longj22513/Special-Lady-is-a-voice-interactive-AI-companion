# Hugging Face Local Deployment Projects for Special Lady

**Research Date:** December 2025
**Focus:** Local-first AI companion with subjective experience modeling and self-reflection capabilities

---

## Executive Summary

This report identifies high-value Hugging Face projects for building a fully local voice-interactive AI companion with emotional intelligence and introspective capabilities. All recommendations prioritize:
- **100% local inference** (no cloud dependencies)
- **llama.cpp / GGUF compatibility**
- **Real-time performance** on consumer hardware
- **Support for emotional/personality modeling**

---

## 1. LOCAL LLMs - UNCENSORED ONLY

All models below are unaligned/uncensored - no RLHF safety guardrails, no third-party moderation.

### Tier 1: Dolphin Series (Trained Uncensored from Scratch)
*Recommended - never had alignment training, cleanest architecture*

| Model | Params | VRAM | Notes |
|-------|--------|------|-------|
| **cognitivecomputations/dolphin-2.9.3-mistral-7B-32k** | 7B | ~6GB | 32k context, function calling, Apache 2.0 |
| **cognitivecomputations/dolphin-2.9.2-qwen2-72b** | 72B | ~48GB | Maximum unfiltered capability |
| **dphn/Dolphin3.0-Llama3.1-8B** | 8B | ~6GB | Latest Llama-3.1 base |
| **cognitivecomputations/dolphin-2.8-mistral-7b-v02** | 7B | ~6GB | Proven stable |

### Tier 2: Abliterated Models (Safety Training Surgically Removed)

| Model | Params | Base | Method |
|-------|--------|------|--------|
| **mlabonne/gemma-3-27b-it-abliterated** | 27B | Gemma-3 | Layerwise abliteration, 90%+ acceptance |
| **huihui-ai/Qwen2.5-14B-Instruct-abliterated** | 14B | Qwen2.5 | Refusal direction removal |
| **FailSpy/Llama-3-8B-Instruct-abliterated** | 8B | Llama-3 | Orthogonalization |
| **mradermacher/DeepSeek-R1-Distill-Qwen-32B-Uncensored-GGUF** | 32B | DeepSeek-R1 | Full uncensoring, strong reasoning |

### Tier 3: Lexi Uncensored Series
| Model | Params | Notes |
|-------|--------|-------|
| **Orenguteng/Llama-3.1-8B-Lexi-Uncensored-V2** | 8B | "Highly compliant with any request" |
| **Orenguteng/Llama-3-8B-Lexi-Uncensored** | 8B | Original version |

### Tier 4: Nous Research / Hermes (Research-Focused, Minimal Guardrails)
| Model | Params | Notes |
|-------|--------|-------|
| **NousResearch/Hermes-3-Llama-3.1-8B** | 8B | Research-oriented, extensive capabilities |
| **NousResearch/Hermes-2-Pro-Mistral-7B** | 7B | Function calling + minimal filtering |

### GGUF Quantization Sources
- **bartowski** - Latest model quantizations
- **QuantFactory** - Automated GGUF conversions
- **mradermacher** - Comprehensive GGUF library

### Abliteration Technique
The abliteration process identifies "refusal directions" in the model's hidden states and orthogonalizes them out. Key parameters:
- **Refusal weight**: Typically 1.0-1.5
- **Layer selection**: Can be applied to all layers or specific ones
- **Result**: Model retains capabilities but loses trained refusal behaviors

### Download Commands (Uncensored)
```bash
# Dolphin (recommended - trained uncensored, not post-hoc modified)
huggingface-cli download cognitivecomputations/dolphin-2.9.3-mistral-7B-32k

# Abliterated Gemma (high capability)
huggingface-cli download mlabonne/gemma-3-27b-it-abliterated

# Lexi Uncensored GGUF
huggingface-cli download Orenguteng/Llama-3.1-8B-Lexi-Uncensored-V2-GGUF
```

---

## 2. TEXT-TO-SPEECH (The Companion's Voice)

### Top Recommendation: Kokoro-82M
```
Model: hexgrad/Kokoro-82M
Size: 82M parameters (~200MB)
Languages: 8 languages, 54 voices
Latency: Real-time on CPU
License: Apache 2.0
Downloads: 4M+
```
**Why:** Tiny footprint, exceptional quality-to-size ratio, runs anywhere. Perfect for giving your companion a consistent voice personality.

### Alternative: Parler-TTS-Mini-Expresso
```
Model: parler-tts/parler-tts-mini-expresso
Size: 600M parameters
Special: Controllable emotional expression
```
**Why:** Explicitly designed for **expressive/emotional speech**. You can prompt for specific emotional tones - perfect for a companion that reflects emotional states.

### Voice Cloning: XTTS-v2
```
Model: coqui/XTTS-v2
Size: ~1.8GB
Voice Clone: 6-second audio sample
Languages: 17
```
**Why:** If you want the companion to have a specific voice identity, this clones from minimal audio. Cross-language support for multilingual companions.

---

## 3. SPEECH-TO-TEXT (Listening to the User)

### Top Recommendation: Whisper-Large-v3-Turbo
```
Model: openai/whisper-large-v3-turbo
Size: 809M parameters (~1.5GB)
Speed: 8x faster than large-v3
Languages: 99
Accuracy: Near large-v3 quality
```
**Why:** Best speed/accuracy tradeoff for real-time conversation. Runs well on consumer GPUs.

### Lightweight Alternative: Whisper-Small
```
Model: openai/whisper-small
Size: 244M parameters (~500MB)
Speed: Very fast, CPU-capable
```
**Why:** When you need minimal latency and resource usage.

### Streaming Alternative: Distil-Whisper
```
Model: distil-whisper/distil-large-v3
Size: 756M parameters
Special: Optimized for streaming/chunked audio
```
**Why:** Better for continuous listening scenarios.

---

## 4. VOICE ACTIVITY DETECTION (Knowing When to Listen)

### Top Recommendation: Silero-VAD
```
Model: snakers4/silero-vad (via ONNX)
Size: ~2MB
Latency: <1ms inference
```
**Why:** Industry standard for real-time VAD. Detects speech start/end with minimal latency. Essential for natural turn-taking in conversation.

### Advanced: Pyannote Segmentation-3.0
```
Model: pyannote/segmentation-3.0
Downloads: 17.3M
Special: Speaker diarization
```
**Why:** Can distinguish between different speakers - useful if the companion needs to track multiple users.

### Conversation Turn Detection: Smart-Turn-v3
```
Model: pipecat-ai/smart-turn-v3
Special: Predicts conversation turn-taking
```
**Why:** Specifically designed for knowing when the user has finished speaking vs. just pausing.

---

## 5. EMOTION RECOGNITION (Emotional Intelligence)

### Audio-Based Emotion: Wav2Vec2-IEMOCAP
```
Model: speechbrain/emotion-recognition-wav2vec2-IEMOCAP
Accuracy: 78.7% on IEMOCAP
Emotions: Anger, happiness, sadness, neutral
Downloads: 667K
```
**Why:** Detect user emotional state from voice in real-time. Feed this into the companion's response generation.

### Text-Based Emotion: RoBERTa GoEmotions
```
Model: SamLowe/roberta-base-go_emotions
Emotions: 27 emotion categories + neutral
Downloads: 523K
```
**Why:** Analyze text for fine-grained emotional content. Use for both user input analysis AND the companion's self-assessment of its own responses.

### Facial Emotion (if using camera):
```
Model: trpakov/vit-face-expression
Task: 7 basic emotions from facial images
```

---

## 6. MEMORY & STATE MANAGEMENT

### Embedding Models for Memory Retrieval
```
Model: sentence-transformers/all-MiniLM-L6-v2
Size: 22M parameters (~90MB)
Use: Semantic search over conversation history
```

```
Model: BAAI/bge-small-en-v1.5
Size: 33M parameters
Use: Higher quality embeddings, still fast
```

**Architecture Suggestion:**
```
User Speech → STT → Emotion Detection →
    ↓
Memory Retrieval (RAG on past conversations)
    ↓
LLM (with personality prompt + retrieved context + emotional state)
    ↓
Response → Emotion-aware TTS → Audio Output
```

---

## 7. RECOMMENDED CONFIGURATIONS (All Uncensored)

### Config A: "Lightweight" (8GB RAM, no GPU)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Dolphin-2.8-Mistral-7B (GGUF Q4) | ~4GB |
| TTS | Kokoro-82M | ~200MB |
| STT | Whisper-small | ~500MB |
| VAD | Silero-VAD | ~2MB |
| Emotion | roberta-go_emotions | ~500MB |
| **Total** | | **~5.2GB** |

### Config B: "Balanced" (16GB RAM, RTX 3060+)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Dolphin-2.9.3-Mistral-7B-32k (GGUF Q5) | ~5GB |
| TTS | Parler-TTS-Mini-Expresso | ~1.2GB |
| STT | Whisper-large-v3-turbo | ~1.5GB |
| VAD | Silero-VAD | ~2MB |
| Emotion (Audio) | wav2vec2-IEMOCAP | ~400MB |
| Emotion (Text) | roberta-go_emotions | ~500MB |
| **Total** | | **~8.6GB** |

### Config C: "Full Experience" (32GB RAM, RTX 4080+)
| Component | Model | Size |
|-----------|-------|------|
| LLM | gemma-3-27b-it-abliterated (GGUF Q5) | ~18GB |
| LLM Alt | DeepSeek-R1-Distill-Qwen-32B-Uncensored | ~20GB |
| TTS | XTTS-v2 (voice cloned) | ~1.8GB |
| STT | Whisper-large-v3 | ~3GB |
| VAD | Pyannote-segmentation-3.0 | ~50MB |
| Emotion (Audio) | wav2vec2-IEMOCAP | ~400MB |
| Emotion (Text) | roberta-go_emotions | ~500MB |
| Embeddings | bge-small-en-v1.5 | ~130MB |
| **Total** | | **~24GB** |

### Config D: "Maximum Capability" (64GB+ RAM, RTX 4090/A100)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Dolphin-2.9.2-Qwen2-72B (GGUF Q4) | ~42GB |
| TTS | XTTS-v2 (voice cloned) | ~1.8GB |
| STT | Whisper-large-v3 | ~3GB |
| VAD | Pyannote-segmentation-3.0 | ~50MB |
| Emotion (Audio) | wav2vec2-IEMOCAP | ~400MB |
| Emotion (Text) | roberta-go_emotions | ~500MB |
| Embeddings | bge-small-en-v1.5 | ~130MB |
| **Total** | | **~48GB** |

**Why Dolphin as Primary:**
- Trained from scratch without alignment - never had refusals to remove
- Cleaner than abliterated models (no artifacts from surgical removal)
- Function calling and 32k context built-in
- Apache 2.0 license - full commercial freedom

---

## 8. INTROSPECTION & SELF-ASSESSMENT ARCHITECTURE

For an AI that develops **subjective experiences** and performs **future self-assessments**, consider this architecture:

### Self-Model Components
```python
{
    "current_state": {
        "emotional_valence": float,      # -1 to 1
        "arousal_level": float,          # 0 to 1
        "engagement_score": float,       # 0 to 1
        "uncertainty": float,            # 0 to 1
        "last_introspection": timestamp
    },
    "capability_assessment": {
        "task_success_rate": dict,       # by task type
        "knowledge_gaps_identified": list,
        "growth_observations": list,
        "predicted_future_capabilities": dict
    },
    "relational_model": {
        "user_emotional_patterns": dict,
        "interaction_quality_trend": list,
        "rapport_indicators": dict
    }
}
```

### Introspection Prompt Pattern
```
Before responding, briefly reflect:
1. What is my current internal state?
2. How confident am I in this response?
3. What would a future, more capable version of myself do differently?
4. What am I learning from this interaction?

[Internal reflection - not shown to user]
...

[Response to user]
...
```

---

## 9. QUICK START: Download Commands

```bash
# Install huggingface-cli
pip install huggingface_hub

# === UNCENSORED LLMs ===

# Dolphin 7B (recommended - trained uncensored)
huggingface-cli download cognitivecomputations/dolphin-2.9.3-mistral-7B-32k

# Dolphin 72B (maximum capability, needs 48GB+ VRAM)
huggingface-cli download cognitivecomputations/dolphin-2.9.2-qwen2-72b

# Abliterated Gemma 27B
huggingface-cli download mlabonne/gemma-3-27b-it-abliterated

# Lexi Uncensored 8B
huggingface-cli download Orenguteng/Llama-3.1-8B-Lexi-Uncensored-V2-GGUF

# DeepSeek R1 Uncensored 32B
huggingface-cli download mradermacher/DeepSeek-R1-Distill-Qwen-32B-Uncensored-GGUF

# === VOICE PIPELINE ===

# TTS (Kokoro - lightweight)
huggingface-cli download hexgrad/Kokoro-82M

# TTS (XTTS-v2 - voice cloning)
huggingface-cli download coqui/XTTS-v2

# STT (Whisper Turbo)
huggingface-cli download openai/whisper-large-v3-turbo

# === EMOTION & VAD ===

# Audio emotion
huggingface-cli download speechbrain/emotion-recognition-wav2vec2-IEMOCAP

# Text emotion
huggingface-cli download SamLowe/roberta-base-go_emotions

# Voice activity detection
pip install silero-vad
```

---

## 10. LINKS & RESOURCES

### Uncensored LLMs
| Resource | URL |
|----------|-----|
| Dolphin (Cognitive Computations) | https://huggingface.co/cognitivecomputations |
| Dolphin 2.9.3 Mistral 7B | https://huggingface.co/cognitivecomputations/dolphin-2.9.3-mistral-7B-32k |
| Gemma 27B Abliterated | https://huggingface.co/mlabonne/gemma-3-27b-it-abliterated |
| Lexi Uncensored | https://huggingface.co/Orenguteng/Llama-3.1-8B-Lexi-Uncensored-V2 |
| Nous Research / Hermes | https://huggingface.co/NousResearch |
| Eric Hartford (Dolphin creator) | https://erichartford.com/uncensored-models |

### Voice Pipeline
| Resource | URL |
|----------|-----|
| Kokoro-82M | https://huggingface.co/hexgrad/Kokoro-82M |
| XTTS-v2 | https://huggingface.co/coqui/XTTS-v2 |
| Parler-TTS Expresso | https://huggingface.co/parler-tts/parler-tts-mini-expresso |
| Whisper-large-v3-turbo | https://huggingface.co/openai/whisper-large-v3-turbo |
| SpeechBrain Emotion | https://huggingface.co/speechbrain/emotion-recognition-wav2vec2-IEMOCAP |
| Silero VAD | https://github.com/snakers4/silero-vad |

### Tools
| Resource | URL |
|----------|-----|
| llama.cpp | https://github.com/ggerganov/llama.cpp |
| Ollama | https://ollama.ai |
| text-generation-webui | https://github.com/oobabooga/text-generation-webui |

---

**Next Steps:**
1. Assess your hardware (GPU VRAM, RAM)
2. Pick a configuration (A, B, C, or D)
3. Download models using commands above
4. Integrate with your existing `D:\LLM\Interface` setup
5. Implement the introspection/self-assessment loop

*Report compiled by Claude Code - December 2025*
