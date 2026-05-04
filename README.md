# Draft to Take Beta

Draft to Take is a local-first AI audio production studio for turning scripts into generated dialogue, reviewed takes, timeline clips, and exported mixes.

This beta release repo contains only deployment files. The source code is not included here. Docker pulls prebuilt beta images from GitHub Container Registry and stores your models, voices, projects, and outputs in a persistent local folder.

## Beta Status

The `v3.0.0-beta.1` container images have been built and pushed, but this repo is not ready to send to testers until the GHCR packages are made public or testers are given registry login access. Anonymous Docker pulls currently receive `denied`.

For a low-friction Reddit beta, make these packages public in GitHub Packages before sharing the link:

- `draft-to-take-backend`
- `draft-to-take-frontend`
- `draft-to-take-script-llm`
- `draft-to-take-omnivoice`
- `draft-to-take-sfx`

## Requirements

- Windows 11 recommended.
- Docker Desktop with WSL2 enabled.
- NVIDIA GPU strongly recommended.
- NVIDIA Container Toolkit / Docker GPU support.
- 32 GB system RAM recommended for the full workflow.
- 12-16 GB VRAM recommended for the smoother local AI path.
- A lot of disk space. First-run model downloads can be many gigabytes.

## Quick Start

1. Download this release repo as a ZIP or clone it.
2. Make sure Docker Desktop is running.
3. Double-click `start.bat`.
4. Open the frontend URL shown in the terminal, usually:

```text
http://localhost:3000
```

On first run, the app may download large model files. Keep the terminal open and be patient.

## Where Your Files Go

The launcher stores shared files outside this release folder:

```text
%USERPROFILE%\DraftToTake\shared
```

That means you can delete and re-download this beta repo without losing downloaded models, voices, projects, or exported audio.

Important folders:

- `shared\models` - downloaded model files.
- `shared\models\checkpoints` - IndexTTS2 checkpoints and Hugging Face cache.
- `shared\models\llm` - Qwen GGUF files.
- `shared\audio\speakers` - prepared speaker WAV files.
- `shared\audio\source_clips` - raw clips you want to prepare.
- `shared\audio\outputs` - exported mixes.
- `shared\data` - app/project data.

## Optional Features

The beta launcher enables the managed Qwen sidecar by default because Qwen supports emotion detection and the optional AI Thread.

The OmniVoice sidecar is enabled by default for beta testing reusable voice design.

SFX/music generation is disabled by default because the current model-backed generators are experimental, heavier, and license-dependent. To test it, edit `.env`:

```text
INDTEXTS_SFX_ENABLED=true
```

Then run `start.bat` again.

## Updating

To update to a new beta:

1. Run `stop.bat`.
2. Download the new release repo ZIP or pull the repo.
3. Run `start.bat`.

Your shared folder under `%USERPROFILE%\DraftToTake\shared` is not deleted.

## Diagnostics

If something breaks, run:

```text
collect-diagnostics.bat
```

It writes a diagnostics text file under:

```text
%USERPROFILE%\DraftToTake\diagnostics
```

Review the file before posting it publicly. Do not share private scripts, voices, tokens, or personal data.

## Reporting Bugs

Use this release repo's Issues tab.

Good bug reports include:

- Windows version.
- GPU model and VRAM.
- System RAM.
- Docker Desktop version.
- Whether Docker GPU support works.
- What you clicked.
- What you expected.
- What happened.
- Diagnostics file excerpt, if safe to share.

## Model And License Notes

This beta does not sell, bundle, or grant rights to third-party model weights. The app may download models from official upstream sources into your local machine.

Read:

- `BETA_TERMS.md`
- `THIRD_PARTY_NOTICES.md`

SFX/music model-backed generation is optional, experimental, and license-dependent.

## Stopping

Run:

```text
stop.bat
```

This stops containers but does not delete shared models, voices, projects, or outputs.
