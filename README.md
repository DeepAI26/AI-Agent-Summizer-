# YouTube Video Summarizer

AI-powered Flask web app that transcribes YouTube videos, generates smart summaries, and prepares platform-tailored posts for Telegram and Discord, with search, scheduling, and an admin dashboard.

## Overview
- Transcribe audio with Whisper and summarize with BART.
- Search YouTube videos via keywords and filters.
- Generate platform-optimized content (Telegram, Discord; general summary).
- Schedule posts with a background scheduler (SQLite-backed).
- Secure login (Google OAuth) and admin panel for content management.

## Tech Stack
- Backend: Flask, PyTorch, Whisper (STT), BART (summarization), yt-dlp, SQLite.
- Frontend: HTML, CSS, JavaScript (templates + static assets).
- Integrations: YouTube Data API v3, Google OAuth 2.0, Telegram Bot API, Discord Webhooks.

## Project Structure
- [app.py](app.py) — main Flask app (routes, pipeline, scheduling, integrations)
- [ai_agent.py](ai_agent.py) — coordinates AI workflow (transcribe, summarize, format)
- [templates/](templates/) — Jinja2 HTML templates (home, search, admin, docs, features)
- [static/](static/) — CSS/JS assets
- [audio/](audio/) — working directory for downloaded/processed audio
- [video_data.json](video_data.json) — processed video metadata and summaries
- [users.json](users.json) — basic user records for sessions/admin

## Environment Variables
Create a `.env` file with the following keys and your values:
- `FLASK_SECRET_KEY`
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`
- `YOUTUBE_API_KEY`
- `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`
- `DISCORD_BOT_TOKEN`, `DISCORD_CHANNEL_ID`
- `ADMIN_PIN` (for admin actions)
- Optionally: `OAUTHLIB_INSECURE_TRANSPORT=1` for local development

Never commit real secrets; use local `.env` or your deployment secret store.

## Quick Start
1) Clone the repo and create a virtual environment (Windows example):

```powershell
git clone <your-repo-url>
cd agentic_summarizer
python -m venv .venv
./.venv/Scripts/Activate.ps1
```

2) Configure environment variables: copy `.env` and fill in your keys.

3) Run the server:

```powershell
python app.py
```

Open http://localhost:5000 and sign in. The scheduler runs in the background; admin tools are available via the admin pages.

## Core Features
- YouTube search with filters and batch selection
- Audio download (yt-dlp) and Whisper transcription
- BART-based summarization with long-text chunking
- Per-platform formatting (Telegram captions, Discord embeds)
- Scheduler with status tracking and manual run
- Admin dashboard for viewing, editing, and deleting entries

## Notes
- GPU (CUDA) accelerates Whisper/BART but is optional.
- Ensure FFmpeg is available for yt-dlp post-processing.
- API quotas (YouTube, etc.) apply; caching reduces redundant processing.

## Roadmap Ideas
- Switch JSON storage to Postgres for scalability
- Multi-language UI + improved non-English summaries
- Additional platforms (LinkedIn, Twitter) and analytics
- Real-time/live stream support

## Disclaimer
This project uses third-party APIs and models. Make sure your usage complies with each provider’s terms and local regulations.
