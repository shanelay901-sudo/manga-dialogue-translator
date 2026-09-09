# Manga Dialogue Translator

A Streamlit application that extracts English dialogue from images, PDFs, and UTF-8 text files, localizes it into natural Burmese with Gemini, and exports an editable `.txt` file.

## Project structure

```
.
├── app.py                  # Streamlit UI, extraction, OCR, translation, download
├── requirements.txt        # Python dependencies
├── .env.example            # Environment-variable template (never commit .env)
├── .gitignore
└── .streamlit/
    └── config.toml         # Dark theme and upload/server settings
```

## Run locally

1. Install Python 3.10 or newer.
2. Create and activate a virtual environment:

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

3. Install dependencies:

   ```powershell
   py -m pip install -r requirements.txt
   ```

4. Copy `.env.example` to `.env`, then replace the value with a Gemini API key created in [Google AI Studio](https://aistudio.google.com/app/apikey).

   ```powershell
   Copy-Item .env.example .env
   ```

5. Start the app:

   ```powershell
   py -m streamlit run app.py
   ```

Open the local URL Streamlit displays (normally `http://localhost:8501`). You can also paste a key in the sidebar for the current session.

## How it works

- **PNG/JPG/JPEG:** Gemini Vision OCR reads visible English dialogue and returns it in panel/bubble reading order when possible.
- **PDF:** selectable text is extracted locally; image-only PDFs render each page and use Gemini Vision OCR. PDFs are capped at 20 pages to control latency and cost.
- **TXT:** expects UTF-8 encoding.
- The translation prompt preserves labels and reading order while adapting tone and context for natural Burmese. Always review the editable result before publishing.

## Deployment and security

For Streamlit Community Cloud, add `GEMINI_API_KEY` to its Secrets settings instead of uploading a `.env` file. The app reads it automatically. `.env` and Streamlit secrets are ignored by Git, uploads are size/type checked, and the API key remains server-side. Configure Google-side quotas before exposing the app publicly.
