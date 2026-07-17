# LETR Lab Website — CLAUDE.md

## Project overview

Quarto-based academic website for the **LETR Lab** (Learning & Educational
Technology Research Lab), directed by Dr. Anisha Singh, Department of
Psychology, San Francisco State University.

Hosted on **GitHub Pages** from the `docs/` folder of the `master` branch.
GitHub repo: `https://github.com/anishaessingh-8/letr-lab.git`

---

## Key commands

All commands must run from the **main project directory**:
```
/Users/anishasingh/Documents/psych-stats-courses
```
Never run git or quarto commands from a worktree directory.

### Render (required before every commit)
```bash
# Render a single page
/Applications/RStudio.app/Contents/Resources/app/quarto/bin/quarto render <file>.qmd

# Render the entire site
/Applications/RStudio.app/Contents/Resources/app/quarto/bin/quarto render
```

### Commit and deploy
```bash
git add docs/ <changed-source-files>
git commit -m "Description of change"
git push origin master
```
Site goes live ~60 seconds after push.

---

## File structure

```
_quarto.yml          # Site config, navbar, footer, theme
custom.scss          # SCSS theme (Bootstrap/Quarto variables + rules)
styles.css           # CSS custom properties and component styles
index.qmd            # Homepage (hero, research cards, recent pubs, contact)
research.qmd         # Research areas + methods + working with students
publications.qmd     # Publications list + conference presentations
team.qmd             # PI card, lab alumni, collaborators, working with students
teaching.qmd         # Course cards (PSY 371, 531, 771)
psy371/              # PSY 371 course materials
psy771/              # PSY 771 course materials
docs/                # Rendered output served by GitHub Pages
```

---

## Design system

**Colors (dark aubergine / magenta palette)**
- Page background: `#1a1320`
- Card surface: `#1f1526`
- Deep background: `#120d17`
- Magenta accent: `#ff5ea8`
- Primary text: `#f3eaf0`
- Muted text: `#c3b6c8` / `#9d8aa3`

**Fonts**
- Headings: Newsreader (serif, weight 300–500) — Google Fonts
- Body / UI: Space Grotesk (sans-serif) — Google Fonts

**CSS architecture**
- `custom.scss` — Bootstrap/Quarto SCSS variables (`$body-bg`, `$primary`,
  font stacks, etc.) and component rules (navbar, buttons, cards)
- `styles.css` — CSS custom properties (`:root` tokens) and all page
  component classes (`.pub-item`, `.team-card`, `.page-header`, etc.)
- Both files are loaded via `_quarto.yml`:
  ```yaml
  theme:
    - cosmo
    - custom.scss
  css: styles.css
  ```
  > ⚠️ `styles.css` must be a separate `css:` key — listing it inside
  > `theme:` causes a Quarto SCSS layer error.

---

## Content structure

### Publications page (`publications.qmd`)
Organized into year groups (`.pub-year-group`). Each entry uses:
- `.pub-authors` — bold `<strong>` for Singh and lab members
- `.pub-title` — wrap in `<a>` if there's a link
- `.pub-venue` — journal/publisher name
- `.pub-tags` — **only four allowed tags:**
  - `<span class="pub-tag">Journal Article</span>`
  - `<span class="pub-tag">Chapter</span>`
  - `<span class="pub-tag pub-tag-in-press">Preprint</span>`
  - `<span class="pub-tag pub-tag-in-press">Working Paper</span>`

Sections (in order): Preprints & Working Papers → 2026 → 2025 → 2023 →
2022 → 2021 → 2019 → 2018, followed by `<hr>` and Selected Conference
Presentations (also in reverse-year groups).

### Team page (`team.qmd`)
- PI: Dr. Anisha Singh
- Lab Alumni: Kayla King, Dylan (Sophia) Mattioda
- Collaborators: Alexander, Bharaj, Sun, Zhao, Javadizadeh
- Office: EP Building, Room 319, SFSU

### Teaching page (`teaching.qmd`)
- PSY 371 — Psychological Statistics (Undergraduate)
- PSY 531 — Psycholinguistics (Upper Division)
- PSY 771 — ANOVA and Experimental Design (Graduate)

---

## Common tasks

### Add a publication
Copy an existing `.pub-item` block in `publications.qmd`, update authors,
title (with link if available), venue, and tag. Place in the correct year
group. Render `publications.qmd` and commit.

### Add a conference presentation
Copy an existing `.pub-item` block in the presentations section of
`publications.qmd`. No tags needed. Render and commit.

### Update team members
Edit `team.qmd`. Current members go under Graduate Students; former
members go under Lab Alumni. Render and commit.

### Update the homepage recent pubs
Edit the `.recent-pubs` section in `index.qmd`. Keep it to 4 entries,
newest first. Render `index.qmd` and commit.

### Update research topics
Edit the `.research-card` blocks in `research.qmd`. Each card has:
- `.research-card-icon` — an emoji
- `.research-card-title` — the area name
- `.research-card-desc` — a short paragraph description

The same three cards are also mirrored on the homepage (`index.qmd`) under
"What We Study" — update both files if the topic names or descriptions
change. Render both files and commit.

### Add material to a course
1. Place the file (`.qmd`, `.pdf`, `.csv`, etc.) in the relevant course
   folder (`psy371/`, `psy531/`, or `psy771/`).
2. Open that course's `index.qmd` and add a link where it fits, e.g.:
   ```markdown
   [Week 5 — Correlation tutorial](week5-correlation.html)
   ```
3. To add a new course entirely: create a new subfolder with an
   `index.qmd`, then add a `.course-card-v2` block to `teaching.qmd`
   pointing to it.
4. Render and commit. Non-`.qmd` files (PDFs, CSVs) are copied as-is and
   do not require a render step — but do still need to be committed.

---

## Important notes

- The `quarto` binary is at:
  `/Applications/RStudio.app/Contents/Resources/app/quarto/bin/quarto`
  (not in system PATH — always use the full path)
- Always **render before committing** — `docs/` is what GitHub Pages serves
- The `[WARNING] nonempty <title>` messages during render are expected and
  harmless (pages use `title: ' '` intentionally)
- `*` in presentations = student author; `†` = equal contribution
