# CLAUDE.md - AI Assistant Guide for Special Lady

## Project Overview

**Special Lady** (codename: Carmen) is a voice-interactive AI companion built for
emotional modeling, multi-model reasoning, and privacy-conscious deployment. It is
a research project by Justin Long (ronniec03) under the MIT license, focused on
comparing AI model empathy/creativity and exploring voice UX in companion AI.

The repository currently contains **launcher scripts only** (Windows `.bat` files).
The core Python source code (`carmen_v7_fixed.py` and variants) is not yet committed
to the repository.

## Repository Structure

```
/
├── CLAUDE.md                                # This file - AI assistant guide
├── README.md                                # Project overview and setup instructions
├── LICENSE                                  # MIT License (Copyright 2025 ronniec03)
├── Start_Carmen_CPU.bat                     # CPU-only launcher (hides CUDA GPUs)
├── Start_Carmen_GPU.bat                     # GPU launcher (CUDA/llama.cpp)
├── Run_Carmen_LiveMic.bat                   # Live microphone launcher (sounddevice)
├── Run_Carmen_Safe.bat                      # Safe boot: CPU + async video + live mic
└── Launch_Carmen_Companion_With_PyAudio.bat # Full launcher with PyAudio for Python 3.13
```

## Technology Stack

| Layer              | Technologies                                                     |
|--------------------|------------------------------------------------------------------|
| **Platform**       | Windows (all launchers are `.bat` files)                         |
| **Language**       | Python 3.13 (targeted by PyAudio wheel), Batch Script            |
| **AI/LLM**        | gpt4all (local), llama.cpp (CUDA), Claude 3.5 API, GPT-4 API    |
| **Speech Input**   | SpeechRecognition, sounddevice, PyAudio                          |
| **Speech Output**  | pyttsx3, edge-tts, gtts                                          |
| **Audio Playback** | pygame                                                           |
| **Vision**         | opencv-python, pillow                                            |
| **ML Framework**   | PyTorch (CPU builds: torch, torchvision, torchaudio)             |
| **Data Storage**   | SQLite (local memory, mentioned in README)                       |
| **Environment**    | Python venv (auto-created by launchers)                          |

## Launcher Variants

Each `.bat` file targets a different hardware/capability profile:

| Launcher | GPU | Mic Library | Python Module | Key Difference |
|----------|-----|-------------|---------------|----------------|
| `Start_Carmen_CPU.bat` | No (CUDA hidden) | N/A | `carmen_v7_fixed.py` | Minimal, CPU-only, installs only gpt4all |
| `Start_Carmen_GPU.bat` | Yes (CUDA GPU 0) | N/A | `carmen_v7_fixed.py` | Adds llama.cpp CUDA path |
| `Run_Carmen_LiveMic.bat` | Optional (CPU torch) | sounddevice | `carmen_v7_micfix.py` | Full audio/vision deps, mic-optimized |
| `Run_Carmen_Safe.bat` | No (CUDA hidden) | sounddevice | `carmen_safevideo_micfix.py` | Safe boot with async video, no PyTorch |
| `Launch_Carmen_Companion_With_PyAudio.bat` | No (CPU torch) | PyAudio | `carmen_v7_fixed.py` | Downloads PyAudio .whl for Python 3.13 |

## Python Modules (Referenced but Not in Repo)

Three Python entry points are referenced across the launchers:

- **`carmen_v7_fixed.py`** - Main/base implementation (used by CPU, GPU, and PyAudio launchers)
- **`carmen_v7_micfix.py`** - Microphone-optimized variant (used by LiveMic launcher)
- **`carmen_safevideo_micfix.py`** - Safe mode with async video processing (used by Safe launcher)

These files are **not yet committed** to the repository.

## Application Architecture (Inferred)

```
┌─────────────────────────────────────────────────────┐
│            Carmen Voice-Interactive Companion         │
├─────────────────────────────────────────────────────┤
│  INPUT:                                              │
│  ├─ Speech-to-Text (SpeechRecognition / sounddevice) │
│  ├─ PyAudio (optional advanced audio)                │
│  └─ Computer Vision (opencv-python)                  │
│                                                      │
│  PROCESSING:                                         │
│  ├─ Local LLMs (gpt4all, llama.cpp w/ CUDA)         │
│  ├─ Cloud APIs (Claude 3.5, GPT-4)                  │
│  ├─ Emotional Intelligence Module                    │
│  └─ SQLite Memory/Context                            │
│                                                      │
│  OUTPUT:                                             │
│  ├─ Text-to-Speech (pyttsx3, edge-tts, gtts)        │
│  ├─ Audio Playback (pygame)                          │
│  └─ Visual Display (pillow, opencv)                  │
└─────────────────────────────────────────────────────┘
```

## Development Conventions

### Environment Setup Pattern

All launchers follow the same venv bootstrap pattern:
1. Set working directory to script location (`cd /d %~dp0`)
2. Configure GPU visibility via `CUDA_VISIBLE_DEVICES`
3. Create Python venv if it does not exist
4. Activate the venv
5. Upgrade pip and install dependencies
6. Run the target Python module

### Dependency Management

- No `requirements.txt` or `pyproject.toml` exists yet -- dependencies are installed
  inline within each `.bat` launcher via `pip install` commands.
- PyTorch is installed as CPU-only builds from the official PyTorch wheel index.
- PyAudio requires a pre-built wheel downloaded via `curl` (targeting Python 3.13/Win64).

### GPU Configuration

- **CPU mode**: Set `CUDA_VISIBLE_DEVICES=` (empty) to hide all GPUs
- **GPU mode**: Set `CUDA_VISIBLE_DEVICES=0` and add llama.cpp CUDA build to PATH
- GPU launcher has a **hardcoded path** (`C:\Users\Justin\llama.cpp\build\bin\Release`)
  that should be parameterized for other developers

### File Naming

- Launcher scripts: `{Action}_{Name}_{Variant}.bat` (PascalCase with underscores)
- Python modules: `carmen_{version}_{variant}.py` (lowercase with underscores)

## Known Gaps and Issues

1. **Missing source code**: The core Python files (`carmen_v7_fixed.py`,
   `carmen_v7_micfix.py`, `carmen_safevideo_micfix.py`) are not in the repository
2. **Missing config directory**: README references `config/` for API keys but it
   does not exist
3. **Missing documentation**: README references `docs/research_methodology.md`
   which does not exist
4. **Missing install script**: README references `install_enhanced_deps.bat` and
   `launch_enhanced.bat` which do not exist
5. **No `requirements.txt`**: Dependencies are scattered across launcher scripts
   with no single source of truth
6. **Hardcoded paths**: `Start_Carmen_GPU.bat` contains a user-specific path
7. **No tests**: No test files, test framework, or CI/CD configuration
8. **No `.gitignore`**: The `venv/` directory and other generated artifacts are
   not excluded

## Guidelines for AI Assistants

### When Making Changes

- This is an **early-stage research project** with only 3 commits. Expect incomplete
  structure and missing files.
- The target platform is **Windows** -- all scripts are `.bat` files. Do not
  introduce Unix-only tooling without providing Windows equivalents.
- The target Python version is **3.13** (inferred from PyAudio wheel in
  `Launch_Carmen_Companion_With_PyAudio.bat`).
- If adding Python source files, follow the existing naming convention:
  `carmen_{version}_{variant}.py`.
- Preserve the multi-launcher pattern -- different hardware profiles need different
  entry points.

### Priority Improvements

If asked to improve the project structure, consider:
1. Adding the core Python source files to the repository
2. Creating a `requirements.txt` (or `pyproject.toml`) consolidating all dependencies
3. Adding a `.gitignore` for `venv/`, `__pycache__/`, `*.whl`, `.env`, etc.
4. Creating a `config/` directory with template/example config files
5. Replacing hardcoded paths with environment variables or config
6. Adding the referenced `docs/research_methodology.md`

### Security Considerations

- API keys (Claude, GPT-4) should **never** be committed. Ensure a `.gitignore`
  excludes `config/` secrets and `.env` files.
- The PyAudio launcher downloads a `.whl` from an external URL -- verify integrity
  if modifying this step.
- SQLite database files containing conversation history should also be gitignored.

## Build and Run

There is no formal build system. To run the application on Windows:

```batch
:: CPU-only (minimal)
Start_Carmen_CPU.bat

:: With GPU support (requires CUDA + llama.cpp build)
Start_Carmen_GPU.bat

:: With live microphone (sounddevice)
Run_Carmen_LiveMic.bat

:: Safe mode (CPU + async video)
Run_Carmen_Safe.bat

:: Full setup with PyAudio (Python 3.13)
Launch_Carmen_Companion_With_PyAudio.bat
```

Each launcher auto-creates a `venv/` and installs dependencies on first run.

## Git Workflow

- **License**: MIT
- **Primary author**: ronniec03 (Justin Long)
- No branch protection, PR templates, or CI/CD pipelines are configured.
- Commit messages have been brief and informal (e.g., "Add files via upload").
