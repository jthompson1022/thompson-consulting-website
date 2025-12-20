# Thompson Consulting — Copilot / AI Agent Instructions

Short summary
- Small static marketing site (HTML + CSS, light JS). No build system or test runner present.
- Key pages: `index.html`, `executive-recruiting.html`, `technical-consulting.html`.
- Main stylesheet: `css/main.css` (design tokens in `:root`).

Big-picture architecture (what to know)
- Single-repo, static frontend only. No backend services, APIs, or bundlers to update.
- External assets: Google Fonts loaded from `fonts.googleapis.com` (network-dependent).
- Minimal JS: the only script sets the copyright year in `index.html` (line near bottom).
- Responsive behavior and access patterns are implemented in CSS (e.g., dropdown via `:focus-within` rather than JS).

Files & patterns to reference
- `index.html` — landing page, hero, contact, and site navigation (note commented CTA section).
- `executive-recruiting.html`, `technical-consulting.html` — subpage structure using `.hero-subpage`, `.two-column`, and `.focus-grid`.
- `css/main.css` — contains: design tokens in `:root` (e.g., `--color-primary`, `--color-secondary`), responsive breakpoints (880px/720px/540px), and component classes like `.hero`, `.service-card`, `.hero-badge--recruiting`.

Project conventions and patterns (concrete, discoverable)
- Design tokens: theme colors live in `:root`. Prefer using `var(--color-...)` when introducing color changes.
  Example: `.hero-badge--recruiting { border-left: 4px solid var(--color-secondary); }`
- Class naming: semantic classes with modifier suffixes (e.g., `--recruiting`, `--tech`) rather than a formal BEM toolchain.
- Layout utilities: `.page` sets the max-width and padding; `.two-column` and `.services-grid` are used for responsive grids.
- Accessibility: dropdown menus are shown via `:focus-within` on `.nav-dropdown` — preserve keyboard focus behavior when modifying navigation.

Developer workflows (how to be productive now)
- Local preview: open `index.html` in a browser for a quick check, or serve over HTTP (preferred) to mimic font loading:
  - Python: `python -m http.server 8000` (then open `http://localhost:8000/`)
  - Node: `npx serve` or similar static server.
- Visual QA checklist for PRs:
  - Check visual layout at key breakpoints (<=960px / 880px / 720px / 540px).
  - Verify fonts load (network) and fallback fonts look acceptable.
  - Confirm navigation is keyboard-accessible and dropdown still opens via focus.
  - Confirm contact email (`mailto:`) is correct and the footer year updates automatically.

Tests & CI
- No automated tests or CI workflows exist in the repository. If adding a build step (tooling, preprocessors, bundlers), include an accompanying GitHub Actions workflow and document the commands in `README.md`.

When to change or add JS
- Small, non-invasive JS is OK (e.g., analytics snippet). Avoid replacing CSS-driven interactions (like the nav dropdown) with JS unless it maintains keyboard/focus accessibility.

PR checklist (quick, copyable)
- [ ] Visual check at desktop + tablet + mobile breakpoints.
- [ ] Keyboard navigation and dropdown focus behavior preserved.
- [ ] Color changes use `:root` tokens or documented new tokens.
- [ ] No external dependencies added without documenting why and adding a deployment/build step if needed.

Notes & quick reminders
- The CTA buttons in `index.html` are currently commented out — review intent before re-enabling.
- If you add tooling (Sass, PostCSS, bundler), document how to run/build and add CI.

If anything above is unclear or you want the instructions to emphasize other workflows (e.g., deploy steps for GitHub Pages), tell me which areas to expand and I will update this file.