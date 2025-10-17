# System Patterns

## Architecture Overview
- Monolithic Flask application handling routing, templating/API responses, and authentication.
- SQLite database storing core entities (users/owners, locations, items, and potentially categories).
- TailwindCSS used for styling; compiled locally into static assets.
- Optional photo uploads stored locally (exact storage path and limits to be confirmed).

## Authentication
- Single shared password for all family members.
- Likely implementation: hashed password stored in the database or configuration; session-based auth after successful login.

## Data Modeling Concepts
- `HouseholdMember`: represents item owners; seeded with four initial family members and supports additions.
- `Location`: represents houses/rooms where items are stored.
- `Item`: tracks name, category, owner reference, location reference, optional photo path/URL, and timestamps.
- Potential `Category` table or enum; clarification needed.

## Interaction & Patterns
- CRUD forms for items using standard Flask form handling (possibly Flask-WTF).
- Simple dashboard/home view listing items with filtering controls.
- Photo upload handling via Flask file upload mechanisms with validation for size and type.

## Open Decisions
- Whether categories are free-text or managed as a controlled list.
- Storage strategy for photos (filesystem path, database blob, or external storage).
- Desired filtering/search capabilities (by owner, house, category, keyword, etc.).
- Any audit trail requirements for edits.
