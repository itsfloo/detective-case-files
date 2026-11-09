# CLAUDE.md: Case Files (Detective Mystery Site)

Read this file fully before creating or editing anything in this repository.

## 1. Project purpose

Case Files is a small static website that publishes short detective mysteries.
Each mystery is one page with a fixed structure: scenario, suspects, clues, and a hidden solution.
The goal is to let new cases be added quickly and consistently, so every page must follow the rules below.

Audience: classmates and friends who like mysteries. Tone: playful, light noir, easy to read.
Language: English for all page content unless the user asks otherwise.

## 2. Technical constraints

- Static site only: plain HTML, CSS, and a little vanilla JavaScript. No frameworks, no build step.
- Must work when hosted on GitHub Pages (no server code, no API keys, no secrets in the repo).
- Every page links the shared stylesheet `assets/style.css`. Do not write large inline styles.
- No external requests (no CDN scripts, no remote images). Use files inside `assets/`.
- Pages must be readable on a phone (responsive, no horizontal scrolling).

## 3. Folder structure

```
/
├── index.html              # home page: list of case cards
├── CLAUDE.md               # this file
├── README.md               # short project description + live site link
├── assets/
│   ├── style.css           # the only shared stylesheet
│   └── cases/              # images for cases, named <case-slug>-<name>.png
└── cases/
    └── <case-slug>/
        └── index.html      # one page per case
```

## 4. Naming rules

- Case folder name (`<case-slug>`): lowercase English letters, numbers, and hyphens only. Example: `rosewood-mansion`.
- No spaces, no uppercase, no non-English characters in any file or folder name.
- Image names: `<case-slug>-<short-name>.png`, for example `rosewood-mansion-clara.png`.
- Links between pages use relative paths (`../../index.html`, `../../assets/style.css`).

## 5. Visual style

- Theme: dark, moody "case file" look with a warm accent. Colors must come from CSS variables in `assets/style.css`:
  `--bg`, `--card`, `--text`, `--muted`, `--accent`. Never hard-code new colors in a page.
- Fonts: one serif for headings, one sans-serif for body text (system fonts with fallbacks).
- Cards have rounded corners (12px) and a thin border.
- Keep pages simple. No animations that are required to understand the content.

## 6. Home page rules (`index.html`)

The home page has: a header with the site title, a one-line intro, a grid of case cards, and a footer.
Every case card has exactly these parts, in this order:

1. Difficulty tag (`Easy`, `Medium`, or `Hard`)
2. Case title
3. Two-sentence hook (no spoilers)
4. Info line: number of suspects and number of clues
5. A "Open case" link to `cases/<case-slug>/index.html`

New cards are added at the top of the grid (newest first). Keep the "More cases coming soon" card as the last item.

## 7. Case page template (`cases/<case-slug>/index.html`)

Every case page contains these sections, in this exact order, each with an `<h2>`:

1. **Header**: case title, difficulty tag, one-line hook, link back to the home page.
2. **Scenario**: 1 to 3 short paragraphs (who, where, when, what was found).
3. **Suspects**: exactly 3 suspect cards. Each card shows name, role, personality, and alibi.
4. **Clues**: 5 to 8 clues. Each has an id (`c1`, `c2`, ...), a name, and where it was found.
5. **Questions to think about**: 3 guiding questions (who, how, why).
6. **Solution**: hidden inside a `<details>` element, closed by default. Contains the culprit, motive, method, and which clues prove it.
7. **Endings**: three short endings: correct culprit with good reasoning, correct culprit with weak reasoning, wrong culprit.

Use `class="suspect-card"`, `class="clue"`, and `class="tag"` for these elements so the shared CSS applies.

## 8. Content rules

- Every case must be solvable using only the clues listed on the page.
- Exactly one culprit. Each suspect has a believable motive. At least one suspect is a red herring.
- The solution and the culprit's name must appear only inside the `<details>` block (Section 6 of the page) and the endings. Never in the title, hook, scenario, or card text.
- Do not use real people, real brands, or real crimes. Keep violence mild and non-graphic.

## 9. How to add a new case (follow in order)

1. Choose a slug following Section 4.
2. Create `cases/<slug>/index.html` by copying the structure in Section 7. Do not copy text from other cases.
3. Fill every section. Check the counts: 3 suspects, 5 to 8 clues, 3 questions, 3 endings.
4. Add one card to the top of the grid in `index.html` following Section 6.
5. Run the checklist in Section 10.
6. Summarize for the user what was added (files created and changed).

## 10. Definition of done (check before finishing)

- [ ] The new page opens correctly from the home page and links back.
- [ ] Sections appear in the required order, with the required counts.
- [ ] The solution is hidden in a closed `<details>` and does not appear anywhere else except the endings.
- [ ] File and folder names follow the naming rules.
- [ ] Only `assets/style.css` variables are used for colors. No external requests.
- [ ] The home page card has all five parts and no spoilers.

## 11. Do not

- Do not rename or delete existing cases, or change `assets/style.css` variables, unless the user asks.
- Do not add libraries, frameworks, or build tools.
- Do not put API keys or personal information in any file.
- Do not change the page structure of existing cases when adding a new one.
