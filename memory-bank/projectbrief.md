# Project Brief: Itemly

## Mission
Create a simple, family-friendly web app that helps household members keep track of where items are stored across multiple homes.

## Primary Objectives
- Provide a single shared login with one correct password for all family members.
- Allow users to add, view, edit, and delete catalog entries for household items.
- Record item attributes including name, category, owner, location, optional photo, and last updated date.
- Support multiple houses and evolving lists of family members as item owners.

## Scope
- Implement a Flask-based web application served locally.
- Use SQLite for persistent storage of users, households, and items.
- Style the interface with TailwindCSS, emphasizing a modern, approachable family aesthetic.
- Support photo upload per item (storage approach to be finalized).
- Desktop-first experience, with consideration for tablet/mobile usage later.

## Constraints & Assumptions
- Application runs on localhost only; deployment to Hostinger will be handled later.
- Offline support is explicitly out of scope.
- Authentication is password-only with a single shared credential (no multi-user accounts for now).
- No integration with external services has been requested yet.

## Success Criteria
- Family members can log in with the shared password and manage the inventory without errors.
- Item records persist reliably between sessions.
- UI clearly communicates item ownership and storage locations across houses.
- Codebase is organized for future expansion (e.g., adding more family members or locations).
