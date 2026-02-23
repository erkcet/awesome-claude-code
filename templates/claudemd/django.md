# CLAUDE.md — Django Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** Python 3.12+, Django 5.x, Django REST Framework <!-- add extras: Celery, Redis, etc. -->
- **Package manager:** pip <!-- or poetry, uv, pdm -->
- **Virtual env:** `.venv/` (activate with `source .venv/bin/activate`)
- **Database:** PostgreSQL <!-- or SQLite, MySQL -->

## Commands

| Action | Command |
|--------|---------|
| Create venv | `python -m venv .venv` |
| Activate venv | `source .venv/bin/activate` |
| Install deps | `pip install -r requirements.txt` |
| Run dev server | `python manage.py runserver` |
| Run tests | `python manage.py test` |
| Run tests (specific app) | `python manage.py test myapp` |
| Run tests (pytest) | `pytest` |
| Make migrations | `python manage.py makemigrations` |
| Apply migrations | `python manage.py migrate` |
| Create superuser | `python manage.py createsuperuser` |
| Collect static files | `python manage.py collectstatic --noinput` |
| Open Django shell | `python manage.py shell_plus` <!-- or shell -->
| Create new app | `python manage.py startapp myapp` |
| Check for issues | `python manage.py check --deploy` |
| Lint | `ruff check .` |
| Format | `ruff format .` |
| Type check | `mypy .` |

## Project Structure

```
project_name/
├── manage.py                 # Django management entry point
├── config/                   # Project-level configuration
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py           # Shared settings
│   │   ├── development.py    # Dev overrides
│   │   └── production.py     # Production overrides
│   ├── urls.py               # Root URL configuration
│   ├── wsgi.py               # WSGI application
│   └── asgi.py               # ASGI application
├── apps/
│   └── myapp/
│       ├── __init__.py
│       ├── admin.py           # Admin site registration
│       ├── apps.py            # App configuration
│       ├── models.py          # Database models
│       ├── views.py           # View functions / class-based views
│       ├── urls.py            # App-level URL patterns
│       ├── serializers.py     # DRF serializers (if using REST framework)
│       ├── forms.py           # Django forms
│       ├── signals.py         # Signal handlers
│       ├── managers.py        # Custom model managers
│       ├── services.py        # Business logic (keep views thin)
│       ├── management/
│       │   └── commands/      # Custom manage.py commands
│       ├── migrations/        # Auto-generated migration files
│       ├── templates/
│       │   └── myapp/         # App-namespaced templates
│       ├── static/
│       │   └── myapp/         # App-namespaced static files
│       └── tests/
│           ├── __init__.py
│           ├── test_models.py
│           ├── test_views.py
│           └── test_services.py
├── templates/                 # Project-level templates
│   └── base.html
├── static/                    # Project-level static files
├── media/                     # User-uploaded files (dev)
└── requirements/
    ├── base.txt
    ├── development.txt
    └── production.txt
```

## Conventions

- Use class-based views (CBVs) for standard CRUD; function-based views (FBVs) for simple or highly custom logic.
- Model naming: singular `PascalCase` (e.g., `Article`, `UserProfile`). Use `related_name` on all ForeignKey/M2M fields.
- Keep views thin — move business logic into `services.py` or model methods.
- Migration workflow: always run `makemigrations` after model changes, review the generated file, then `migrate`. Never edit migrations by hand unless squashing.
- URL naming: use `app_name` namespace and `name` kwarg on every path (e.g., `myapp:article-detail`).
- Templates: extend a shared `base.html`, use `{% block %}` for sections, namespace templates under `templates/myapp/`.
- Settings: split into `base.py`, `development.py`, `production.py`. Select via `DJANGO_SETTINGS_MODULE`.
- Use Django's built-in `User` model or `AbstractUser` for customization — decide before the first migration.
- Signals: use sparingly; prefer explicit service-layer calls.
- Tests: use `django.test.TestCase` or pytest-django. Use factories (`factory_boy`) over fixtures.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `SECRET_KEY` | Yes | Django secret key (50+ random chars) |
| `DEBUG` | No | Enable debug mode (default: `False`) |
| `DATABASE_URL` | Yes | Database connection string (parsed by `dj-database-url`) |
| `ALLOWED_HOSTS` | Yes (prod) | Comma-separated list of allowed hostnames |
| `DJANGO_SETTINGS_MODULE` | Yes | Settings module path (e.g., `config.settings.production`) |
| `REDIS_URL` | No | Redis connection string (cache / Celery broker) |
| `EMAIL_HOST` | No | SMTP server for outgoing email |
| `CORS_ALLOWED_ORIGINS` | No | Comma-separated allowed CORS origins |
| `SENTRY_DSN` | No | Sentry error tracking DSN |
| `AWS_STORAGE_BUCKET_NAME` | No | S3 bucket for static/media files |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
