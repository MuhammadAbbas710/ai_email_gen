# ✉️ AI Professional Email Generator

A small Streamlit app that drafts professional emails with Google's Gemini Flash model.
Enter the **purpose**, the **recipient**, and the **tone** you want, and get a ready-to-send email
(subject line included). You can also choose a length and add your name for the sign-off.

## Features

- Purpose, recipient, and tone inputs (10 preset tones plus a custom tone)
- Short / medium / long length options
- Copy-friendly output box and a "Download as .txt" button
- Input validation and friendly error messages (bad key, quota, blocked response, network)
- API key kept in secrets, never in the code

## Project structure

```
.
├── app.py                          # the Streamlit app
├── requirements.txt                # Python dependencies
├── README.md
├── .gitignore                      # keeps your real secrets out of GitHub
└── .streamlit/
    └── secrets.toml.example        # template for your API key
```

## Run it locally

1. **Get a Gemini API key** (free tier available) from [Google AI Studio](https://aistudio.google.com/apikey).
2. **Create a virtual environment and install dependencies** (Python 3.9+):

   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Add your key.** Copy the example file and edit it:

   ```bash
   cp .streamlit/secrets.toml.example .streamlit/secrets.toml
   ```

   Then set `GEMINI_API_KEY = "your-real-key"` inside `.streamlit/secrets.toml`.
   (Alternatively, set a `GEMINI_API_KEY` environment variable.)

4. **Start the app:**

   ```bash
   streamlit run app.py
   ```

## Choosing the model

By default the app uses the `gemini-flash-latest` alias, which always points to Google's newest Flash model.
To pin a specific model, add this to your secrets:

```toml
GEMINI_MODEL = "gemini-2.5-flash"
```

Check [Google's model list](https://ai.google.dev/gemini-api/docs/models) for the names available to you.

## Upload to GitHub

1. Create a new **empty** repository on [github.com/new](https://github.com/new) (no README, no .gitignore).
2. From the project folder, run:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: AI email generator"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
   git push -u origin main
   ```

3. Confirm `.streamlit/secrets.toml` does **not** appear in the repository. The `.gitignore` excludes it,
   but only `secrets.toml.example` should be on GitHub.

## Deploy on Streamlit Community Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
2. Click **Create app** and choose to deploy from an existing repo.
3. Select your repository, the `main` branch, and `app.py` as the main file.
4. Open **Advanced settings**, and in the **Secrets** box paste:

   ```toml
   GEMINI_API_KEY = "your-real-key"
   ```

5. Click **Deploy**. The first build takes a minute or two. Every later `git push` redeploys automatically.

## Troubleshooting

| Problem | Fix |
|---|---|
| "No Gemini API key found" | Add `GEMINI_API_KEY` to `.streamlit/secrets.toml` (local) or the app's Secrets (cloud). |
| "API rejected the request" | The key is invalid or the model name is wrong. Re-copy the key; remove `GEMINI_MODEL` to use the default. |
| "Model ... was not found" | Set `GEMINI_MODEL` to a model name listed in Google's docs. |
| "Rate limit or quota reached" | Wait a minute and retry, or check your quota in Google AI Studio. |
| Build fails on Streamlit Cloud | Make sure `requirements.txt` is in the repo root and `app.py` is selected as the main file. |

## Privacy note

The text you enter is sent to Google's Gemini API to generate the email. Don't enter passwords or highly sensitive data.# ai_email_gen
