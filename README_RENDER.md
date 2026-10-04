# Railway Reservation Django - Render Deployment

## Project structure
- `manage.py`
- `RailwayDjango/` - Django project (`settings.py`, `urls.py`, `wsgi.py`)
- `railway/` - application
- `railway/templates/` - HTML templates
- `railway/static/` - static assets
- `media/` - uploaded/local media files

## Render settings
**Build Command**
```bash
pip install -r requirements.txt && python manage.py collectstatic --noinput && python manage.py migrate
```

**Start Command**
```bash
gunicorn RailwayDjango.wsgi:application
```

**Recommended environment variables**
- `SECRET_KEY` - generate a strong secret
- `DEBUG=False`
- `ALLOWED_HOSTS` - Render will also accept the automatic `RENDER_EXTERNAL_HOSTNAME`
- `DATABASE_URL` - supplied by Render PostgreSQL

## Important database note
The local `db.sqlite3` file is intentionally not included in the deployment package. Render should use PostgreSQL in production. After the first deploy, create an admin account and add your train/route data through the deployed site/admin.

## Important media note
Render web-service storage is ephemeral. User-uploaded files stored under `media/` can be lost after a redeploy/restart. For permanent uploaded train images, use object storage such as Cloudinary or Amazon S3.

## Local test
```bash
python manage.py check
python manage.py runserver
```
