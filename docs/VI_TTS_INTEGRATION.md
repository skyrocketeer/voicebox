# VieNeu-TTS-v3-Turbo integration notes

Model Space: https://huggingface.co/spaces/pnnbao-ump/VieNeu-TTS-v3-Turbo

This file documents the minimal steps taken to attach the Vietnamese TTS model to the project and how to use it.

What I added:
- config/tts_models.yml with an entry `vi: pnnbao-ump/VieNeu-TTS-v3-Turbo`
- backend/vi_tts_loader.py: a small wrapper that calls the Hugging Face Inference API to synthesize Vietnamese audio.

How it works:
- The loader uses `huggingface_hub.InferenceApi` to call the model hosted on Hugging Face.
- The function `synthesize(text, out_path)` writes a WAV file with the audio returned by the model.

Usage:
1. Install dependency: `pip install huggingface-hub`
2. (Optional but recommended) Set HF token: `export HUGGINGFACE_HUB_TOKEN=...` if required by the model or to avoid rate limits.
3. Run a quick test:
   python backend/vi_tts_loader.py

Notes & next steps:
- Verify the model license on the Space page and record it here if acceptable for the project.
- For production use, consider downloading the model to the deployment environment (using `huggingface_hub.snapshot_download`) and running inference locally (Coqui TTS, VITS runtime, etc.) to avoid runtime network calls and rate limits.
- Add a CI smoke test to synthesize a few short phrases and store the generated artifact or verify its existence.

License and attribution:
- Check: https://huggingface.co/spaces/pnnbao-ump/VieNeu-TTS-v3-Turbo (see model card / license section on that page)
