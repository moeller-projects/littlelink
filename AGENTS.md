# Repository Guidelines

## Project Structure & Module Organization
- Root HTML entry points live in `index.html` and `privacy.html`; edit these for content updates.
- Core styling is split across `css/reset.css`, `css/style.css`, and `css/brands.css`; brand-specific button overrides belong only in `css/brands.css`.
- Static assets sit under `images/` and `fonts/`; keep file names lowercase and descriptive (e.g., `images/icons/service.svg`).
- Docker resources reside in `docker/` and provide both production and development configurations.

## Build, Test, and Development Commands
- Serve locally without tooling: `python3 -m http.server 8000` from the repository root.
- Containerized preview: `docker compose -f docker/compose.yaml up` mounts the workspace into nginx with live reloads.
- Production image build: `docker build -f docker/Dockerfile -t littlelink:latest .` packages the site onto the static website base image.

## Coding Style & Naming Conventions
- Use two-space indentation in HTML and CSS; keep attributes on individual lines when they aid readability.
- Favor semantic HTML elements (`section`, `nav`, `ul`) and maintain ARIA labels already present.
- In CSS, define reusable values via custom properties on `:root`; group related declarations (layout, typography, color) together.
- Prefix new button classes with `button-<service>` and store their assets under `images/icons/`.

## Testing & Quality Checks
- There is no automated unit test suite; manually verify layout across light, dark, and auto themes.
- Run the contrast workflow on demand with `gh workflow run contrast-check.yml` to confirm button accessibility.
- Before submitting, audit with browser dev tools or Lighthouse to ensure 100/100 targets remain plausible.

## Commit & Pull Request Guidelines
- Write concise, imperative commit subjects (e.g., `Add mastodon button style`).
- Squash unrelated changes; large updates benefit from multiple focused commits.
- Pull requests should describe the change, list manual verification steps, and include screenshots for UI adjustments when possible.
- Reference any accessibility findings and note if the contrast workflow raised warnings.

## Accessibility & Asset Hygiene
- Keep SVGs optimized (e.g., via `svgo`) and remove inline dimensions when CSS controls sizing.
- Preserve descriptive `alt` text and update it whenever swapping imagery.
- Ensure new buttons meet WCAG AA contrast ratios—add a stroke via `--button-border` when backgrounds are high-chroma.
