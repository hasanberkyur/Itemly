# Active Context

## Current Focus
- Project kickoff: establish comprehensive documentation in the memory bank.
- Incorporate clarified functional requirements into planning for implementation, including file structure and schema.

## Recent Actions
- Created initial memory bank with core context files summarizing Itemly goals, product needs, architecture, and tech stack.
- Captured user decisions regarding categories, locations, photo handling, filtering, and design references.

## Next Steps
- Translate design samples (`designSamples/`) into Flask templates styled with TailwindCSS.
- Scaffold Flask application package with blueprints, models, and shared extensions.
- Configure Tailwind build pipeline (`tailwind.config.js`, `postcss.config.js`, npm scripts) and integrate compiled CSS.
- Finalize default category list and seed data for members and houses.
- Implement database migrations covering members, locations, categories, items (with timestamps and uploads).
- Outline filtering/search service methods and corresponding form/query parameters.

## Open Questions
- Determine how new family members and houses will be added via UI (dedicated CRUD vs. simple forms).
- Decide if text search should be case-insensitive and partial-match capable.
- Confirm whether thumbnails should be generated server-side or rely on CSS-resized originals.
- Clarify default list of categories beyond core examples (Clothing, Electronics, Kitchenware).
