# LiveKit Voice Agent Demo

An upbeat, slightly sarcastic voice AI designed for tech support, built using the [LiveKit](https://livekit.io/) Agents framework. 

This agent uses a highly resilient pipeline configured with fallback providers for Speech-to-Text (STT), Large Language Models (LLM), and Text-to-Speech (TTS), ensuring maximum uptime even if a provider goes down.

## Features

- **Robust Fallback Systems:**
  - **LLM:** Primary `openai/gpt-4.1-mini`, Backup `google/gemini-2.5-flash`
  - **STT:** Primary `assemblyai/universal-streaming:en`, Backup `deepgram/nova-3`
  - **TTS:** Primary `cartesia/sonic-3`, Backup `inworld/inworld-tts-1`
- **Advanced Voice Processing:**
  - **VAD:** Silero Voice Activity Detection
  - **Turn Detection:** Multilingual Model support
  - **Audio Filtering:** Built-in Background Voice Cancellation (BVC)

## Requirements

- Python >= 3.14
- `uv` package manager (recommended for dependency management)

## Setup

1. **Install dependencies:**
   This project uses `uv` for dependency management. Install the required packages by running:
   ```bash
   uv sync
   ```
   *Alternatively, using standard pip: `pip install -r pyproject.toml` or similar.*

2. **Environment Variables:**
   Create a `.env` file in the root directory and add the required API keys for LiveKit and your chosen inference providers:
   ```env
   LIVEKIT_URL=your_livekit_url
   LIVEKIT_API_KEY=your_api_key
   LIVEKIT_API_SECRET=your_api_secret
   ```

## Usage

Start the agent in the console by running:

```bash
uv run agent.py console
```

The agent will connect to your LiveKit room. Whenever a participant joins the room, the `entrypoint` function will automatically launch the voice pipeline, and the tech support AI will begin interacting.

## Project Structure

- `agent.py`: The main entrypoint defining the `Assistant` logic and voice pipeline configuration.
- `pyproject.toml` / `uv.lock`: Project metadata and dependencies.
