# Tech Context

## Stack & Frameworks
- Backend: Python with Flask.
- Templating: Flask Jinja templates (or potential API + frontend decision to be confirmed).
- Database: SQLite (likely using SQLAlchemy or Flask SQLAlchemy for ORM support).
- Styling: TailwindCSS (requires build pipeline via npm or CDN approach).
- Authentication/session management: Flask-Login or manual session handling.
- Static uploads: Flask serves files from `static/uploads/`; ensure directory creation and secure filename handling.

## Tooling & Setup
- Python virtual environment already present at `venv/` (activation steps to be documented).
- Tailwind build toolchain (e.g., PostCSS + autoprefixer) to be configured.
- Local development runs on localhost; no deployment automation yet.
- Need utility helpers for file validation (MIME/type, size) and unique filename generation.
- `package.json` scripts:
  - `tailwind:build` for production CSS generation.
  - `tailwind:watch` for local development watching `templates/` and `app/static/src/`.
- Use `npm` (or `pnpm`) for Tailwind dependencies; compiled CSS emitted to `app/static/css/app.css`.
- Flask CLI command set for database migrations (`flask db upgrade`) and seeding defaults.

## Constraints
- Network access currently restricted; external dependencies may require pre-download or alternative setup.
- App limited to a single shared password.
- No offline mode; relies on active server session.
- File uploads limited to JPEG/PNG/WebP formats with a 5 MB cap.
- Shared password hash injected via environment variable (`FAMILY_PASSWORD_HASH`) to avoid storing plain text in repo.

## Testing & QA
- No testing strategy defined yet; likely to use pytest or Flask's testing utilities.
- Need to consider fixtures for sample inventory data.
- Include tests for filtering/search logic and upload validation when implemented.
- Write integration tests covering category creation from custom input and ensuring filters respond correctly.

## Future Considerations
- Manual Git-based deployment to Hostinger.
- Potential scalability improvements if multi-user accounts introduced later.
