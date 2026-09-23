# Social Media Django — Deployment Ready

This copy has been prepared for a simple Render deployment. The application code/features have not been redesigned.

## Files added/updated for deployment
- `requirements.txt` — production dependencies
- `build.sh` — collects static files and runs migrations
- `render.yaml` — Render build/start configuration
- `socialmedia/settings.py` — production-friendly environment variables, database configuration, and WhiteNoise
- `socialmedia/urls.py` — media URL handling retained for the demo
- `.gitignore` — ignores local Python/deployment files

## Deploy on Render
1. Extract this ZIP.
2. Create a GitHub repository and upload the contents of this folder. The repository root should contain `manage.py`.
3. In Render, create a **Web Service** from that GitHub repository.
4. Build command: `bash build.sh`
5. Start command: `gunicorn socialmedia.wsgi:application`
6. Render can generate `SECRET_KEY` from the included `render.yaml`; if you configure the service manually, create a `SECRET_KEY` environment variable.
7. After you receive your Render URL, add `CSRF_TRUSTED_ORIGINS` with the full URL, e.g. `https://your-app.onrender.com`.

## Database
The project uses PostgreSQL automatically when `DATABASE_URL` is supplied, and falls back to the included SQLite database when it is not. For a real multi-user production app, use PostgreSQL.

## Media uploads
The project contains existing images in `media/`. Render web-service disks are ephemeral, so newly uploaded profile/post images are not guaranteed to survive a restart/redeploy. For long-term production use, move media to persistent object storage.

## Local run
```bash
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```
