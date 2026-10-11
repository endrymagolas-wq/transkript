# Transkript

Paste a link to a video, get a transcript with speaker labels and timestamps.

The back end downloads the audio with yt-dlp, sends it to AssemblyAI with speaker labels and language detection on, and returns the text plus a list of utterances (speaker, text, start, end). The front end is a small React app that takes the link and shows the result.

## Run it

Back end (Python 3.12, ffmpeg on PATH):

```bash
cd backend
pip install -r requirements.txt
ASSEMBLYAI_API_KEY=your_key uvicorn main:app --port 8001
```

Front end:

```bash
cd frontend
npm install
VITE_API_URL=http://localhost:8001 npm run dev
```

The AssemblyAI key can also be passed per request in the `api_key` field. A `Dockerfile` and a `Procfile` are included for container or Cloud Run style hosting.

## Endpoints

| Method | Path | What it does |
| --- | --- | --- |
| `POST` | `/transcribe` | `{ "url": "...", "api_key": "optional" }` → transcript text and utterances |
| `GET` | `/audio_url?url=...` | Resolves the direct audio URL for a link |

Keys live in environment variables or in the request, never in the repository.
