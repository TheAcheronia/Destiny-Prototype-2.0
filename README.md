# Destiny (Assistant Prototype 2.0) (Modular, Cross‑Platform, Open/Free Stack)

A highly‑modular voice+GUI assistant scaffold designed for Windows, Linux, macOS and Android (via Kivy).
Switch LLM/STT/TTS/Wake‑word engines via a single config file—local or API—plus a plugin system for skills
and system control.

> This repo is a **clean, production‑style scaffold** with working defaults that run **without internet**:
> - GUI: Kivy
> - TTS: pyttsx3 (offline)
> - STT: (mock) keyboard input; Vosk/Whisper optional
> - Wake Word: simple keyword ("destiny") in mock mode; openwakeword optional
> - LLM: local simple rule engine by default; plug OpenAI/Gemini or llama.cpp later
>
> Perfect for extending into your own advanced assistant ("Destiny").

## Features

- 🔌 **Hot‑swappable engines** (LLM, STT, TTS, Wake‑word) via `config.yaml`
- 🧩 **Skills**: drop a Python file in `src/destiny/skills/` to add capabilities
- 🖥️ **Modern GUI** (Kivy) with conversation stream, VU meter placeholder, interrupt button
- 🗣️ **Realtime-ish** pipeline with cooperative async tasks & interruption
- 🧠 **Function/Tool calls**: skills can be called by the LLM router
- 🧰 **System control** examples (open URLs, volume, brightness placeholders)
- 📱 **Android support** (build with `buildozer`); desktop works with Python
- 🧪 **Tests**: smoke test for config + plug loading

## Quick Start (Desktop)

```bash
# 1) Create venv (Python 3.10–3.12 recommended)
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
# source venv/bin/activate

# 2) Install deps
pip install -r requirements.txt

# 3) Run GUI
python main.py
```

- Click the mic icon (mock) to simulate wake, type text (mock STT), and see responses.
- Click "Stop" to interrupt current TTS.

## Switching Engines

Open `config.yaml` and change blocks like:

```yaml
llm:
  engine: simple # options: simple | openai | gemini | llama_cpp
stt:
  engine: mock   # options: mock | vosk | whisper_api
tts:
  engine: pyttsx3 # options: pyttsx3 | coqui
wakeword:
  engine: mock    # options: mock | openwakeword
```

Each engine has its own settings section. Add your API keys in env vars (`.env`) or directly in config (not recommended).

## Android (Kivy)

- Install `buildozer` (Linux) or use a Docker image.
- Ensure your chosen engines are compatible on Android (e.g., pyttsx3 may not work; prefer Coqui TTS on-device or Android TTS bridge).
- Replace mock STT with Vosk/Whisper tiny (convert model paths).

## Security & Privacy

- No telemetry. All local unless you enable API engines.
- Use the `skills/` folder to limit what the assistant is allowed to execute.

## Roadmap ideas

- Realtime streaming TTS/STT (Coqui + VAD)
- Screen reading, OCR, RAG with local embeddings
- On‑device wake word via openwakeword model bundle
- Fine‑grained permissions per skill

Enjoy building Destiny. 💫

Kindly use another name instead of "Destiny" in case you want to publish.
