# Project overview page

**Why:** classmates visit one landing page, see all my projects, and open them.

**Goals:** all 11 projects, each a card with a title, one-line description and "View live" link.
**Non-goals:** auto-discovery, search, filtering, screenshots.
**Anti-goal:** a missing project or a broken link.

**Constraints:** GitHub Pages serves the root of `main`; links must be relative
(`wbs-exercises/<folder>/`, with the space in `html-Tailwind CSS` written as `%20`).

## Approaches
- **A. Hand-written HTML (picked):** simple and fully controlled; new cards are added by hand.
- B. List from the GitHub API: automatic, but needs separate descriptions and is rate-limited.
- C. README links: quickest, little control over the look.

## Design (proposed)
- One static `index.html` at the repo root. Cards are plain HTML, so no script builds them.
- Responsive grid, styled with the Tailwind browser CDN already used in this repo.
- Same-tab links.
- Titles are written by hand: some page titles are missing, generic or duplicated.
  Tailwind versions are labelled as such.
- I write placeholder descriptions as TODOs; Dunn writes the final wording.
- Start from current `origin/main` (`dev` is 3 commits behind).
- `wbs-exercises/index.html` (a classmate's 3-project starter): replace its contents with a
  redirect to the root page, so the old address still works and there is only one list.
  Credit the classmate in the commit message.

**Check:** every card link resolves to an `index.html`, and all 11 folders are listed.

**Left to the builder:** colours, spacing, markup details.
