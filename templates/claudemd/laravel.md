# CLAUDE.md — Laravel Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** PHP 8.3+, Laravel 11.x <!-- add extras: Livewire, Inertia, Filament, Horizon, etc. -->
- **Package manager:** Composer (PHP), npm (frontend assets)
- **Database:** MySQL <!-- or PostgreSQL, SQLite -->
- **Queue driver:** Redis <!-- or database, SQS -->

## Commands

| Action | Command |
|--------|---------|
| Install PHP deps | `composer install` |
| Install JS deps | `npm install` |
| Dev server | `php artisan serve` |
| Vite dev server | `npm run dev` |
| Build assets | `npm run build` |
| Run tests | `php artisan test` |
| Run tests (parallel) | `php artisan test --parallel` |
| Run single test | `php artisan test --filter=TestName` |
| Create migration | `php artisan make:migration create_posts_table` |
| Run migrations | `php artisan migrate` |
| Rollback migration | `php artisan migrate:rollback` |
| Fresh migrate + seed | `php artisan migrate:fresh --seed` |
| Create model (full) | `php artisan make:model Post -mfsc` |
| Create controller | `php artisan make:controller PostController --resource` |
| Create form request | `php artisan make:request StorePostRequest` |
| Create policy | `php artisan make:policy PostPolicy --model=Post` |
| Queue worker | `php artisan queue:work` |
| Clear all caches | `php artisan optimize:clear` |
| Cache config/routes | `php artisan optimize` |
| Tinker (REPL) | `php artisan tinker` |
| List routes | `php artisan route:list` |
| Lint (Pint) | `./vendor/bin/pint` |
| Static analysis | `./vendor/bin/phpstan analyse` |

## Project Structure

```
app/
├── Console/
│   └── Commands/              # Custom artisan commands
├── Exceptions/
│   └── Handler.php            # Exception handling
├── Http/
│   ├── Controllers/
│   │   └── PostController.php # Resource controllers
│   ├── Middleware/             # HTTP middleware
│   └── Requests/
│       └── StorePostRequest.php # Form request validation
├── Models/
│   ├── User.php
│   └── Post.php               # Eloquent models
├── Policies/                  # Authorization policies
├── Providers/
│   └── AppServiceProvider.php # Service providers
├── Services/                  # Business logic layer
├── Actions/                   # Single-purpose action classes
├── Enums/                     # PHP enums
└── Jobs/                      # Queued jobs
bootstrap/
├── app.php                    # Application bootstrap
└── providers.php              # Provider registration
config/                        # Configuration files
database/
├── factories/                 # Model factories (for testing/seeding)
├── migrations/                # Database migrations
└── seeders/                   # Database seeders
resources/
├── views/                     # Blade templates
│   ├── layouts/
│   │   └── app.blade.php
│   ├── components/            # Blade components
│   └── posts/
│       ├── index.blade.php
│       └── show.blade.php
├── css/
│   └── app.css
└── js/
    └── app.js
routes/
├── web.php                    # Web routes
├── api.php                    # API routes
└── console.php                # Console routes (scheduled tasks)
storage/
├── app/                       # Application files
├── framework/                 # Framework cache, sessions, views
└── logs/
    └── laravel.log
tests/
├── Feature/                   # Feature / integration tests
│   └── PostControllerTest.php
├── Unit/                      # Unit tests
│   └── PostServiceTest.php
└── TestCase.php               # Base test class
```

## Conventions

- Eloquent models: singular `PascalCase` (e.g., `Post`, `UserProfile`). Define `$fillable` or `$guarded` on every model. Always declare relationships, casts, and scopes.
- Controllers: use resource controllers (`--resource`) for CRUD. Keep controllers thin — move logic to Services or Actions.
- Form Requests: validate in dedicated `FormRequest` classes, not in controllers. Use `authorize()` for policy checks.
- Migrations: one structural change per migration. Never edit a migration that has been deployed — create a new one.
- Naming: `snake_case` for database columns and routes, `camelCase` for variables and methods, `PascalCase` for classes, `UPPER_CASE` for constants and env vars.
- Routing: use resource routes (`Route::resource`) when possible. Always name routes. Group with middleware.
- Blade templates: use components (`<x-button>`) over `@include`. Extend layouts with `@extends` / `@section` or use component layouts.
- Testing: Feature tests for HTTP/controller flows, Unit tests for isolated logic. Use model factories for test data. Prefer `RefreshDatabase` trait.
- Business logic: use Service classes or single-purpose Action classes. Do not put complex logic in controllers, models, or middleware.
- Eager load relationships to avoid N+1 queries. Use `->with()` in queries or `$with` on models.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `APP_NAME` | Yes | Application name |
| `APP_ENV` | Yes | Environment: `local`, `staging`, `production` |
| `APP_KEY` | Yes | Encryption key (generate with `php artisan key:generate`) |
| `APP_DEBUG` | No | Enable debug mode (default: `false`) |
| `APP_URL` | Yes | Application base URL |
| `DB_CONNECTION` | Yes | Database driver (`mysql`, `pgsql`, `sqlite`) |
| `DB_HOST` | Yes | Database host |
| `DB_DATABASE` | Yes | Database name |
| `DB_USERNAME` | Yes | Database username |
| `DB_PASSWORD` | Yes | Database password |
| `CACHE_STORE` | No | Cache driver (default: `file`) |
| `QUEUE_CONNECTION` | No | Queue driver (default: `sync`) |
| `REDIS_HOST` | No | Redis host |
| `MAIL_MAILER` | No | Mail driver (`smtp`, `ses`, `mailgun`) |
| `AWS_ACCESS_KEY_ID` | No | AWS credentials (S3, SES, SQS) |
| `SENTRY_LARAVEL_DSN` | No | Sentry error tracking DSN |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
