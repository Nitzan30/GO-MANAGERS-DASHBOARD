<!-- .github/copilot-instructions.md - Guidance for AI coding agents -->
# Copilot instructions — GO-MANAGERS-DASHBOARD

Purpose
- Short, actionable guidance so AI coding agents can be immediately productive editing this repo.

Quick summary
- This is a single-page static HTML dashboard: all styling and JS are inline in `index.html`.
- There is no build tool, package.json, or tests. Edit and preview directly in a browser or with a VS Code Live Server.

Big picture
- Primary file: `index.html` — contains the UI, CSS variables under `:root`, the `dashboardData` JS array, rendering helpers (`renderCards`, `getIconData`, `filterDashboards`, `init`) and small interactive logic.
- Data flow: update `dashboardData` (array of objects) to add/remove dashboards; `init()` populates domain/region selects, and `filterDashboards()` drives the visible cards.
- External integrations are simple outbound links inside `dashboardData` (PowerBI, Tableau, ServiceNow, Monday.com). The project does not host those services.

Imperatives for edits
- When adding/updating dashboards, edit the `dashboardData` entries in `index.html` (preserve object keys: `pinned`, `domain`, `region`, `name`, `url`). Example entry:

  { "pinned": true, "domain": "GO Ping", "region": "Global", "name": "GO Ping", "url": "https://app.powerbi.com/..." }

- To change visual tokens, update the CSS variables in `:root` (colors like `--brand-magenta`, `--brand-yellow`, and glass variables). Keep the glassmorphism variables and border values to preserve layout.
- To add a new icon mapping, update `getIconData(item)` in `index.html` (it classifies URLs for icon + class). Follow existing pattern: check `lowerUrl.includes('powerbi')` etc.

Developer workflows & preview
- No build: open `index.html` directly in a browser, or use VS Code Live Server (`Live Server` extension) for auto-refresh.
- Typical quick edit flow:
  - Update `dashboardData` or inline CSS.
  - Save file and refresh browser (or rely on Live Server auto-reload).

Conventions & patterns
- Single-file structure: prefer small, focused edits inside `index.html` rather than splitting files unless requested.
- Keep JS functions small and pure where possible — e.g., `renderCards` should only mutate the DOM inside `#gridContainer` and not alter global data.
- Preserve existing DOM ids: `gridContainer`, `domainSelect`, `regionSelect`, `searchInput`, `countDisplay`, `viewModeText` are referenced by JS.

Testing & validation
- Manual validation: confirm new/edited links open in a new tab, filters work (domain/region/search), and pinned/default state renders as expected.
- Check footer `Last updated` date when making content changes — it is static text in the footer.

Files to inspect
- `index.html` — primary implementation (UI, styles, data and logic).
- `index_old.html` — legacy/backup copy; consult for previous versions or alternate markup.

Notes / gotchas
- There is no server-side code here; do not attempt to add server routes expecting a backend.
- External links in `dashboardData` must remain valid; updating a link affects users immediately when they open the page.

If anything is unclear or you want additional examples (e.g., a small refactor into modular JS/CSS or adding a local dev server), tell me which direction and I will update this file.
