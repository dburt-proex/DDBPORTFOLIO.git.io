# CLAUDE.md

Guidance for Claude Code and other AI assistants working in this repository.

## What this repository is

This is **not** the public portfolio website. It is the **versioned documentation and evidence layer** behind Drew Burt's public portfolio.

| Scope | Canonical authority |
| --- | --- |
| Public positioning, navigation, assessment, lab, contact | [ChatGPT Sites portfolio](https://drew-burt-portfolio.dburt-proex.chatgpt.site) |
| Evidence map, claim boundaries, maturity classifications, change history | **This repository** |
| Code, tests, releases, implementation status | Each project's own repository |

`docs/source-of-truth.md` is the governing record for this split. Read it before changing any claim, route, or evidence link — it contains the authority matrix, the public route registry, the project evidence registry, the publishing workflow, and the change log.

The GitHub Pages root (`index.html`) is a **redirect bridge** to the Sites portfolio, not a second homepage. Do not rebuild it into a full landing page.

## The core convention: evidence discipline

This repository is a portfolio *about* AI governance, and it holds itself to the same standard. This is the most important thing to get right — it matters more than code style.

**Every public claim must be traceable to inspectable evidence, and every claim must state its boundary.**

Concrete rules when writing or editing content here:

- Only describe capability that exists on a project's **default branch**. Work in an open PR is "active review" and must never be presented as merged or released.
- Use the established maturity vocabulary from `docs/ai-governance-developer-tooling.md`: *Validated implementation*, *Documented runnable implementation*, *Documented framework*, *Active review*. Their definitions are in that file's "Evidence interpretation rules" — do not invent new tiers.
- Never claim enterprise production readiness, independent certification, broad deployment, or third-party endorsement without separate explicit evidence.
- Date-stamp evidence. Briefs carry an "Evidence snapshot <date>" in the hero eyebrow and the footer; keep both in sync when content changes.
- Keep boundary language. Pages end with a `.boundary-note` stating what the page does *not* claim, plus a `.source-list` linking the canonical repositories. Do not drop these when editing.
- Projects stay independent. Portfolio pages summarize other repositories; they never absorb them or imply a merged platform.
- When sources disagree, **narrow the claim** until the discrepancy is resolved.

If asked to strengthen a claim, verify it in the canonical project repository first. If it can't be verified, say so rather than upgrading the wording.

## Layout

```
index.html                          Redirect bridge → Sites portfolio (self-contained, inline CSS)
styles.css                          Single shared stylesheet for all brief/case-study pages
script.js                           Shared progressive-enhancement JS (nav toggle, year, reveal)
governance-developer-tooling.html   Rendered capability brief
agentic-sdlc-governance.html        Case study: governing AI-generated changes
diffwall-v0.2.0-release.html        Case study: DiffWall v0.2.0 release evidence
docs/source-of-truth.md             Governance record — authority matrix, registries, workflow, change log
docs/ai-governance-developer-tooling.md   Source brief + repository-verified maturity appendix
.github/ISSUE_TEMPLATE/work-log.yml Structured Work Log submission form
.nojekyll                           Disables Jekyll so GitHub Pages serves files verbatim
README.md                           Public entry point: source-of-truth model, routes, systems, publishing rule
```

## Stack and build

Static HTML, CSS, and vanilla JS. **There is no site build step, package manager, or product test suite.** Files are served verbatim by GitHub Pages. The sole repository CI workflow is `.github/workflows/diffwall.yml`, which runs the deterministic DiffWall gate on pull requests and does not build or publish the site.

Do not introduce a framework, bundler, or dependency manifest unless explicitly asked. Adding one changes the deployment model.

Preview locally:

```bash
python3 -m http.server 8000
```

Site verification is manual: open the affected pages, check that links resolve, and check the layout at desktop and mobile widths (breakpoints are 900px and 720px). DiffWall separately evaluates pull-request change risk.

## Page conventions

Brief and case-study pages share one template. When adding a page, copy an existing one — `agentic-sdlc-governance.html` is the cleanest reference — and keep this structure:

1. `<head>`: title `<Page name> | Drew Burt`, `meta description`, `og:title` / `og:description` / `og:type=article`, `twitter:card`, `theme-color` `#07100d`, Google Fonts preconnect + Manrope/DM Mono, then `styles.css`.
2. `<div class="noise" aria-hidden="true">` immediately inside `<body>`.
3. `header.site-header` with the `DB` brand mark linking to `index.html`, a `.menu-toggle` button carrying `aria-expanded` / `aria-controls`, and `nav#site-nav.site-nav` with in-page anchors.
4. `main` containing `section.brief-hero` then `section.brief-section` blocks, alternating `.section-dark` for rhythm. Each section wraps content in `.container` and adds `.reveal`.
5. A closing source section with `.boundary-note` and `.source-list`.
6. `footer.site-footer` with `<span id="year">`, an evidence-snapshot date, and a back link.
7. `<script src="script.js"></script>` as the last element before `</body>`.

Other conventions:

- **Styling goes in `styles.css`**, never inline and never in a per-page `<style>` block. `index.html` is the one exception — it is deliberately self-contained so the redirect renders with zero extra requests.
- Use the existing CSS custom properties (`--bg`, `--surface`, `--text`, `--muted`, `--line`, `--accent`, `--accent-2`, `--ink`, `--max`, `--shadow`) rather than hard-coded colors.
- Reuse existing component classes before writing new ones: `.signal-table` + `.matrix-wrap` for evidence tables, `.lifecycle` / `.lifecycle-step` for staged flows, `.maturity-grid` / `.maturity-card` for status classifications, `.evidence-grid` / `.evidence-card` for link cards, `.proof-callout` for a headline metric, `.role-grid` / `.role-card` for role relevance.
- `styles.css` is written in a dense one-rule-per-line style grouped by page region. Match it.
- Accessibility is not optional here: `lang="en"`, `aria-label` on nav landmarks and the brand link, `aria-expanded` kept in sync on the menu toggle, `rel="noopener noreferrer"` on `target="_blank"` links, and a `prefers-reduced-motion` path (already handled at the bottom of `styles.css` — new animations must respect it).
- `.reveal` elements start at `opacity: 0` and are shown by the IntersectionObserver in `script.js`. Any page using `.reveal` **must** load `script.js` or its content will be invisible.

### Known dead code

`styles.css` and `script.js` still carry rules and handlers for the retired v2 homepage — the `.hero`/`.project-card`/`.proof-grid`/`.notes-grid` blocks, and the `.filter` / `.note-card` filtering logic in `script.js`. No current page uses them. Leave them alone unless asked to clean up; if you do remove them, remove the CSS and JS together.

## Content conventions

- Markdown in `docs/` uses tables heavily for registries and matrices. Follow the existing column shapes rather than inventing new ones.
- Prose is declarative and unhedged, without marketing intensifiers. Short sentences.
- Punctuation splits by file: `README.md` uses em dashes to gloss link list items (`[Home](...) — positioning and ...`), while the `docs/` prose and the HTML pages use none, relying on periods and commas. HTML eyebrow and footer lines separate segments with a middot (`Case study · Evidence snapshot July 19, 2026`).
- Backtick the control-gate names: `ALLOW`, `REVIEW`, `HALT`.
- Cross-link generously: briefs link to `docs/source-of-truth.md`, to each other, and out to canonical project repositories.

## Git workflow

- Default branch is `main`. All work lands through pull requests; direct pushes to `main` are not the pattern here.
- Branch naming follows a prefix convention seen in history: `leverage/<YYYY-MM-DD>-<slug>` for evidence and content increments, `signal/<slug>` for positioning changes, `agent/<slug>` for agent-authored work.
- Commit subjects are imperative and sentence-case: `Add DiffWall v0.2.0 release evidence case study`, `Define work log governance`. A few older commits use Conventional Commit prefixes; the recent, dominant style is plain imperative — match that.
- Keep commits scoped to one governance change so the evidence history stays reviewable.

## Publishing checklist

Follow this order for any technical or maturity change (full version in `docs/source-of-truth.md`):

1. Verify the new state in the system's canonical repository.
2. Update the evidence registry or supporting brief here.
3. Review the wording for evidence strength, maturity, and unsupported inference.
4. Update the corresponding public Sites content.
5. Confirm the public link resolves to the correct evidence.
6. Add a row to the change log table at the bottom of `docs/source-of-truth.md` with the date, change, GitHub record, and public deployment.

When a new page is added, link it from **both** `README.md` ("Supporting evidence") and the GitHub Pages role section of `docs/source-of-truth.md`.

**There is deliberately no automatic two-way sync with the Sites portfolio.** Do not build one. Read-only parity checks, broken-link detection, and change reminders are acceptable automation; anything that publishes a claim without human review is not.

## Work Log flow

Work Log entries are GitHub issues created from `.github/ISSUE_TEMPLATE/work-log.yml`, titled with the `[Work Log]` prefix.

The publication gate is the issue state:

- **Open issue = unpublished draft.**
- **Closed issue = published** to the public Work Log feed.
- **Reopened = withdrawn** from the feed.

An automated process may create open drafts through this form. It must never close or publish one — closing is the human review gate. Before an entry is closed, its claims, evidence links, dates, and project attribution are verified and secrets, personal data, private client information, and unsupported claims are removed.
