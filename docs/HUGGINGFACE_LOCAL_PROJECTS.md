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

## 1. LOCAL LLMs FOR REASONING & INTROSPECTION

### Tier 1: Best for Self-Reflective Conversation

| Model | Params | VRAM | Why It Fits |
|-------|--------|------|-------------|
| **Qwen2.5-7B-Instruct** | 7B | ~6GB | Excellent reasoning, instruction-following, GGUF available |
| **Mistral-7B-Instruct-v0.3** | 7B | ~6GB | Strong conversational abilities, 3M+ downloads, battle-tested |
| **Phi-3.5-mini-instruct** | 4B | ~3GB | Microsoft's best small model, runs on CPU, great for introspection prompts |
| **Gemma-3-4B-IT** | 4B | ~3GB | Google's latest, excellent coherence for self-assessment tasks |

### Tier 2: Lightweight / Edge Deployment

| Model | Params | VRAM | Why It Fits |
|-------|--------|------|-------------|
| **Qwen2.5-1.5B-Instruct** | 1.5B | ~2GB | Surprisingly capable for size, fast inference |
| **Phi-3-mini-4k-instruct** | 4B | ~3GB | 2M+ downloads, proven local deployment |
| **Gemma-3-1B-IT** | 1B | ~1GB | Ultra-light, good for rapid response loops |

### Tier 3: Maximum Capability (GPU Required)

| Model | Params | VRAM | Why It Fits |
|-------|--------|------|-------------|
| **Qwen2.5-14B-Instruct** | 14B | ~12GB | Deep reasoning, excellent for complex self-reflection |
| **Mistral-Nemo-12B** | 12B | ~10GB | Strong narrative/personality consistency |
| **DeepSeek-R1-Distill-Qwen-7B** | 7B | ~6GB | Reasoning-focused distillation |

### GGUF Quantization Sources
- **TheBloke** - 3,800+ quantized models
- **bartowski** - Latest model quantizations
- **QuantFactory** - Automated GGUF conversions

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

## 7. RECOMMENDED PROJECT CONFIGURATIONS

### Config A: "Lightweight Local" (8GB RAM, no GPU)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Phi-3.5-mini-instruct (GGUF Q4) | ~2.5GB |
| TTS | Kokoro-82M | ~200MB |
| STT | Whisper-small | ~500MB |
| VAD | Silero-VAD | ~2MB |
| Emotion | roberta-go_emotions | ~500MB |
| **Total** | | **~3.7GB** |

### Config B: "Balanced" (16GB RAM, RTX 3060+)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Qwen2.5-7B-Instruct (GGUF Q5) | ~5GB |
| TTS | Parler-TTS-Mini-Expresso | ~1.2GB |
| STT | Whisper-large-v3-turbo | ~1.5GB |
| VAD | Silero-VAD | ~2MB |
| Emotion (Audio) | wav2vec2-IEMOCAP | ~400MB |
| Emotion (Text) | roberta-go_emotions | ~500MB |
| **Total** | | **~8.6GB** |

### Config C: "Full Experience" (32GB RAM, RTX 4080+)
| Component | Model | Size |
|-----------|-------|------|
| LLM | Qwen2.5-14B-Instruct (GGUF Q5) | ~10GB |
| TTS | XTTS-v2 (voice cloned) | ~1.8GB |
| STT | Whisper-large-v3 | ~3GB |
| VAD | Pyannote-segmentation-3.0 | ~50MB |
| Emotion (Audio) | wav2vec2-IEMOCAP | ~400MB |
| Emotion (Text) | roberta-go_emotions | ~500MB |
| Embeddings | bge-small-en-v1.5 | ~130MB |
| **Total** | | **~16GB** |

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

# LLM (Qwen 7B GGUF)
huggingface-cli download Qwen/Qwen2.5-7B-Instruct-GGUF qwen2.5-7b-instruct-q5_k_m.gguf

# TTS (Kokoro)
huggingface-cli download hexgrad/Kokoro-82M

# STT (Whisper Turbo)
huggingface-cli download openai/whisper-large-v3-turbo

# Emotion Recognition
huggingface-cli download speechbrain/emotion-recognition-wav2vec2-IEMOCAP
huggingface-cli download SamLowe/roberta-base-go_emotions

# VAD
pip install silero-vad
```

---

## 10. LINKS & RESOURCES

| Resource | URL |
|----------|-----|
| Kokoro-82M | https://huggingface.co/hexgrad/Kokoro-82M |
| XTTS-v2 | https://huggingface.co/coqui/XTTS-v2 |
| Whisper-large-v3-turbo | https://huggingface.co/openai/whisper-large-v3-turbo |
| Qwen2.5 Collection | https://huggingface.co/collections/Qwen/qwen25-66e81a666513e518adb90d9e |
| Phi-3.5 | https://huggingface.co/microsoft/Phi-3.5-mini-instruct |
| Parler-TTS | https://huggingface.co/parler-tts |
| SpeechBrain Emotion | https://huggingface.co/speechbrain/emotion-recognition-wav2vec2-IEMOCAP |
| Silero VAD | https://github.com/snakers4/silero-vad |
| llama.cpp | https://github.com/ggerganov/llama.cpp |

---

**Next Steps:**
1. Assess your hardware (GPU VRAM, RAM)
2. Pick a configuration (A, B, or C)
3. Download models using commands above
4. Integrate with your existing `D:\LLM\Interface` setup
5. Implement the introspection/self-assessment loop

*Report compiled by Claude Code - December 2025*
