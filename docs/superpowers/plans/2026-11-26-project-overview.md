# Project Overview Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** One landing page where classmates see and open all 11 projects.

**Architecture:** A static root `index.html` with hand-written cards. The old
`wbs-exercises/index.html` becomes a redirect to it.

**Tech Stack:** HTML, Tailwind browser CDN (`https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4`)

**Spec:** docs/superpowers/specs/2026-11-26-project-overview-design.md

## Global Constraints
- All links relative; no leading `/`. Same-tab.
- Cards are plain HTML; no JavaScript builds them.
- Descriptions are marked TODO placeholders; Dunn writes the final text.

## Review Focus
- `html-Tailwind CSS`: href uses `%20` and opens.
- Phone width: one column, no horizontal scroll.
- Old `/wbs-exercises/` address lands on the new page, under the `/wbs-coding-school/` prefix.
- Tailwind CDN unavailable: titles and links stay readable.
- Duplicate names (two resumes, two time-travel sites): titles tell them apart.

---

### Task 1: Overview page and redirect

**Files:**
- Create: `index.html`
- Modify: `wbs-exercises/index.html`

- [ ] **Step 1: Branch from the latest main**

Run: `git fetch origin && git switch -c feature/project-overview origin/main`
Expected: `wbs-exercises/index.html` exists.

- [ ] **Step 2: Create `index.html`**

`lang="en"`, viewport meta, page title and `h1` "My WBS Coding School Projects".
A `ul` grid (1 column on phones, more when wider), one `li` per row below, each with
an `h2` title, a `p` with `TODO(Dunn): describe this project`, and a "View live" link
to `wbs-exercises/<folder>/` whose `aria-label` includes the title.

| Folder (as written in href) | Title |
|---|---|
| html-template-ActiveBox | ActiveBox |
| html-coffee-shop | Common Ground Coffee |
| html-dog-adoption | Happy Tails Dog Adoption |
| html-flexbox-layout | Flexbox Navbar |
| html-grid-layout | Grid Image Gallery |
| html-resume | Resume |
| html-resume-tailwind | Resume (Tailwind) |
| html-time-travel-agency | Time Travel Agency |
| html-time-travel-agency-tailwind | Time Travel Agency (Tailwind) |
| html-Tailwind%20CSS | Tailwind CSS Exercise |
| html-windows-nostalgia | Windows Nostalgia |

Check each Tailwind label against that page's source: the `-tailwind` folder name and
the Tailwind script tag disagree for the time-travel pair. Label by what the code uses.

- [ ] **Step 3: Replace `wbs-exercises/index.html` with a redirect**

A minimal page with `<meta http-equiv="refresh" content="0; url=../">` and a fallback
link to `../`.

- [ ] **Step 4: Check links and coverage**

Run:
```bash
python3 - <<'PY'
import re, glob, os, urllib.parse
links = {urllib.parse.unquote(h) for h in re.findall(r'href="(wbs-exercises/[^"]+)"', open('index.html').read())}
want = {os.path.dirname(p) + '/' for p in glob.glob('wbs-exercises/*/index.html')}
assert links == want and len(want) == 11, (links ^ want, len(want))
print('OK')
PY
```
Expected: `OK`

- [ ] **Step 5: Preview**

Serve the repo locally; check desktop and phone width, open every card, and visit `/wbs-exercises/`.

- [ ] **Step 6: Commit (only after Dunn says to)**

```bash
git add index.html wbs-exercises/index.html
git commit -m "Add project overview page" -m "Replaces the starter landing page contributed by Arthag with a redirect."
```
