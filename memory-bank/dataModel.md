# Data Model

## Overview
SQLite database with SQLAlchemy models representing family members, houses, categories, and items. Timestamp mixin ensures `created_at` and `updated_at` are maintained automatically. Soft deletes are not required; rows removed via hard delete.

## Tables
- **household_members**
  - `id` (PK, integer)
  - `name` (string, unique)
  - `created_at` (datetime)
  - `updated_at` (datetime)

- **locations**
  - `id` (PK, integer)
  - `name` (string, unique) — represents a house
  - `is_active` (boolean, default true)
  - `created_at` (datetime)
  - `updated_at` (datetime)

- **categories**
  - `id` (PK, integer)
  - `name` (string, unique, case-insensitive)
  - `is_default` (boolean, default false)
  - `created_at` (datetime)
  - `updated_at` (datetime)

- **items**
  - `id` (PK, integer)
  - `name` (string, required)
  - `description` (text, optional)
  - `owner_id` (FK → household_members.id, required)
  - `location_id` (FK → locations.id, required)
  - `category_id` (FK → categories.id, nullable — item retains link even if category not default)
  - `photo_filename` (string, stored sanitized filename under `static/uploads/`)
  - `photo_original_name` (string, optional)
  - `photo_mime_type` (string, optional)
  - `created_at` (datetime)
  - `updated_at` (datetime)

## Relationships
- `HouseholdMember` has many `Item`s (`items` backref).
- `Location` has many `Item`s.
- `Category` has many `Item`s. When a user types a new category, the system upserts into `categories` ensuring uniqueness.

## Indices & Constraints
- Unique indices on `household_members.name`, `locations.name`, and `LOWER(categories.name)`.
- Index on `items.updated_at` to support sorting by last updated.
- Composite index on `items.name`/`items.description` via FTS or standard index depending on search needs (initially rely on `LIKE` queries; consider SQLite FTS5 later if performance requires).

## Seeding Strategy
- Default members: Hasan, Mom, Dad, Sister.
- Default locations: Greenköy House, Bodrum House (extendable via UI later).
- Default categories (all with `is_default = true`): Clothing, Electronics, Kitchenware, Documents, Tools, Sports, Toys, Miscellaneous.
- Family password hash stored in environment; provide CLI command (`flask auth set-password`) to update hash if the password changes.

## File Upload Handling
- Uploaded files saved to `static/uploads/{uuid4}.{ext}` to avoid collisions.
- Validation ensures MIME type is JPEG/PNG/WebP and file size ≤ 5 MB before saving.
- Store metadata (original filename, MIME type) to support download or replacement later.
