# System Patterns

## Architecture Overview
- Monolithic Flask application handling routing, templating/API responses, and authentication.
- SQLite database storing core entities (users/owners, locations, items, and potentially categories).
- TailwindCSS used for styling; compiled locally into static assets.
- Photo uploads persisted on the server under `static/uploads/` with enforced size/type limits.
- Flask Blueprints separate concerns: `auth` for login/logout, `inventory` for item/catalog features, and optional `admin` blueprint for managing members/locations if needed.

## Authentication
- Single shared password for all family members.
- Hashed password stored in environment/config (e.g., `FAMILY_PASSWORD_HASH`) and compared during login; Flask sessions track authenticated state.

## Data Modeling Concepts
- `HouseholdMember`: represents item owners; seeded with four initial family members and supports additions.
- `Location`: represents a house; no deeper hierarchy (room/shelf granularity out of scope).
- `Item`: stores name, category (user-extensible), owner reference, location reference, optional description, optional photo path, and timestamps (`created_at`, `updated_at`).
- `Category`: surfaced as prefilled options with ability to capture custom values typed by the user (store raw string on the item).

## Interaction & Patterns
- CRUD forms for items using standard Flask form handling (possibly Flask-WTF).
- Home/dashboard view listing items with filters (owner, house/location, category), text search over name/description, and optional sorting by last updated date.
- Photo upload handled via Flask file upload mechanisms with server-side validation: JPEG/PNG/WebP only, max 5 MB, stored under `static/uploads/` with conflict-free filenames.
- Thumbnail preview displayed in item table leveraging stored photo path.
- Filtering/search handled via a dedicated query builder service to keep route handlers slim.
- Default category choices surfaced from seeded data; custom category entries create new category records (case-insensitive uniqueness).

## Project Structure
- `app/__init__.py`: application factory wiring Flask, SQLAlchemy, login/session helpers, and blueprint registration.
- `app/config.py`: configuration classes loading `.env` values (database path, secret key, password hash).
- `app/extensions.py`: instantiates shared extensions (db, migrate, login manager, CSRF).
- `app/models.py`: SQLAlchemy models for members, locations, categories, items, plus utility mixins for timestamps.
- `app/auth/routes.py` & `app/auth/forms.py`: login view + password validation form; handles session management.
- `app/inventory/routes.py`: dashboard, create/edit/delete item views, filtering endpoints.
- `app/inventory/forms.py`: WTForms (or similar) capturing item data, including category autocomplete.
- `app/inventory/services.py`: encapsulates query filtering, category management, and file upload handling.
- `app/static/` + `static/`: Tailwind-built CSS (`app/static/css/app.css`), compiled assets, and uploads under `static/uploads/`.
- `templates/`: derived from `designSamples/` (home, my items, locations), refactored into Jinja templates using shared partials.
- `tailwind.config.js` & `postcss.config.js`: Tailwind build pipeline; `package.json` scripts for development build/watch.
- `manage.py` or `flask` CLI entry point for migrations, seeding commands, and maintenance scripts.

## Open Decisions
- Determine exact list of default categories presented in dropdown.
- Choose approach for thumbnail generation (client-side resizing vs. server-side) if necessary.
