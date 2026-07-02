# library/ — staged preview viewers (family hub)

**Status: staged, NOT yet wired.** These are copies of recursive-tarot's reusable preview viewers,
pulled here on 2026-07-02 so nara + kali-paradevi have a starting point for their own **cards
preview** and **course preview** pages without re-inventing them. They are held here (nara is the
Trika family's shared course/docs hub) rather than duplicated into every repo.

## What's here

| File | What it does |
|---|---|
| `cards.html` | The **cards preview** viewer — renders a grammar's items as a card gallery. Loads a grammar by its public JSON. |
| `grammar-course.html` | The **course preview** viewer — renders a grammar as a chaptered course. |
| `grammar-loader.js` | Shared loader: fetches a grammar's public JSON (by id / URL) and hands it to a viewer. |
| `course-embeds.js` / `.css` | Card-gallery embeds used inside course pages. |
| `eco-links.js` | Builds recursive.eco open/read/fork links from a grammar id. |

## The two ways to preview a grammar TODAY (no wiring needed)

Both nara and kali-paradevi grammars are already public on recursive.eco, so these work now:

- **In-app reader:** `https://flow.recursive.eco/play?id=<UUID>`
- **Cards / study / course / tree views:** the app's Eye-dropdown on the Library card.

UUIDs live in each repo's `ids.json`. Example (nara wheel-of-the-year):
`https://flow.recursive.eco/play?id=f8153f6e-d863-4a7f-9d6e-9213f7865f3d`

## To actually wire these standalone viewers (deferred — decide if it's worth it)

The recursive-tarot originals are tuned to that repo's folder layout + `theme.css`. To reuse:
1. Point `grammar-loader.js` at a nara/kali grammar's public JSON (raw repo file or the app's
   public grammar API), or pass `?id=<UUID>`.
2. Drop in a local `theme.css` (recursive-tarot ships one; light-only palette).
3. Host via GitHub Pages (like `tarot.recursive.eco`) and set the channel-doc `landing_url`.

Until then, use the in-app preview URLs above — they render every grammar with no extra hosting.
Source of truth for the viewers: `recursive-tarot/viewers/`.
