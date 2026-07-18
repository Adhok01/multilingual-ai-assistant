# Multilingual AI Assistant 🎙️

A voice-based AI assistant built with Streamlit that listens to your speech, responds intelligently using Google's Gemini model, and speaks the answer back — in the language you spoke in.

## Features

- 🎤 **Voice input** via microphone (speech-to-text using Google Speech Recognition)
- 🧠 **AI-powered responses** using Gemini (`gemini-3.1-flash-lite`)
- 🌐 **Multilingual support** — responds naturally in Hindi, Kannada, English, and other languages based on how you speak
- 🔊 **Text-to-speech playback** of the AI's response
- ⬇️ **Downloadable audio** of every response
- 📝 **Logging** of all interactions to `logs/application.log`

## Demo

| Language | Example |
|---|---|
| English | Asked "How are you?" → *"I'm doing well, thank you! How are you? How's everything going?"* |
| Hindi | Asked in Hindi → *"Main bilkul theek hoon, shukriya! Aap kaise hain? Sab kaisa chal raha hai?"* |
| Kannada | Asked "Do you know Kannada?" → *"ಹೌದು, ನನಗೆ ಕನ್ನಡ ಬರುತ್ತದೆ. ನಾನು ನಿಮಗೆ ಹೇಗೆ ಸಹಾಯ ಮಾಡಲಿ?" (Yes, I know Kannada. How can I help you?)* |

See [`DEMO.md`](DEMO.md) for the full walkthrough with more examples.

## Prerequisites

- Python 3.10+
- A working microphone
- macOS users: `portaudio` installed via Homebrew (required for `pyaudio`)
  ```bash
  brew install portaudio
  ```
- A Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/adhok01/multilingual-ai-assistant.git
   cd multilingual-ai-assistant
   ```

2. **Create and activate a conda environment** (or use `venv`)
   ```bash
   conda create -n aiassistant python=3.10
   conda activate aiassistant
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Configuration

This project reads your Gemini API key from an environment variable — **never hardcode it in the source code.**

Set it in your terminal before running the app:
```bash
export GEMINI_API_KEY="your-api-key-here"
```

To make this permanent across terminal sessions, add the line above to your shell profile (`~/.zshrc` for zsh, `~/.bashrc` for bash), then reload it:
```bash
source ~/.zshrc
```

## Running the app

```bash
conda activate aiassistant
streamlit run main.py
```

This opens the app in your browser (typically at `http://localhost:8501`, or the next available port if that one's in use).

Click **"Ask me anything!"**, speak your question, and wait for the response — text, audio playback, and a download link will all appear.

## Project structure

```
.
├── main.py             # Main application: speech recognition, Gemini call, TTS, Streamlit UI
├── requirements.txt     # Python dependencies
├── .gitignore           # Excludes secrets, logs, and generated audio from version control
├── logs/                # Runtime logs (auto-created, git-ignored)
├── samples/             # Example audio outputs for demo purposes
└── README.md
```
## Outputs


<img width="1014" height="755" alt="Screenshot 2026-07-18 at 12 52 13 PM" src="https://github.com/user-attachments/assets/b0db63d7-3020-48d2-b8aa-8e8f725e6fe5" />
<img width="1680" height="1050" alt="Screenshot 2026-07-18 at 12 22 27 PM" src="https://github.com/user-attachments/assets/8a58ae8e-3c78-4f3f-b95e-957ec7736da5" />
<img width="1680" height="910" alt="Screenshot 2026-07-18 at 12 25 52 PM" src="https://github.com/user-attachments/assets/1cd37f8c-1454-4576-a0c9-a885e2e031aa" />

## Notes on rate limits

The free tier of the Gemini API allows a limited number of requests per minute. If you see a message like *"I'm getting a lot of requests right now"*, wait 30–60 seconds before trying again, or enable billing on your Google Cloud project for higher limits.

## Security

- API keys are **never** stored in the codebase — only read via `os.environ.get("GEMINI_API_KEY")`.
- `.gitignore` excludes `.env` files, logs, and generated audio to prevent accidental credential leaks.
- If you ever accidentally commit or expose a key, revoke it immediately at [Google AI Studio](https://aistudio.google.com/apikey) and generate a new one.

## License

This project is provided as-is for educational purposes.
