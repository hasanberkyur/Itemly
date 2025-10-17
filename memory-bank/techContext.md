# Tech Context

## Stack & Frameworks
- Backend: Python with Flask.
- Templating: Flask Jinja templates (or potential API + frontend decision to be confirmed).
- Database: SQLite (likely using SQLAlchemy or Flask SQLAlchemy for ORM support).
- Styling: TailwindCSS (requires build pipeline via npm or CDN approach).
- Authentication/session management: Flask-Login or manual session handling.

## Tooling & Setup
- Python virtual environment already present at `venv/` (activation steps to be documented).
- Tailwind build toolchain (e.g., PostCSS + autoprefixer) to be configured.
- Local development runs on localhost; no deployment automation yet.

## Constraints
- Network access currently restricted; external dependencies may require pre-download or alternative setup.
- App limited to a single shared password.
- No offline mode; relies on active server session.

## Testing & QA
- No testing strategy defined yet; likely to use pytest or Flask's testing utilities.
- Need to consider fixtures for sample inventory data.

## Future Considerations
- Manual Git-based deployment to Hostinger.
- Potential scalability improvements if multi-user accounts introduced later.
