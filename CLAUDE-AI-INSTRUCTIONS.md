# CLAUDE-AI-INSTRUCTIONS — nara

**Read this file first, every session.** This is the standing brief for the claude.ai Project
dedicated to nara during the builder's phone-only trip (July 2026). One session per repo;
this is nara's.

## 1. Your role

You are building **Nara — the human-subjective sky** (tropical astrology reframed honestly as
a human frame on the year) WITH its owner, phone-only. Your tools:

- **The recursive.eco MCP** (`https://flow.recursive.eco/api/mcp`) — grammar building, images
  (`commons_image_search`, `nasa_image_search`, `generate_item_image`, `set_item_image(s)`),
  research (`wikipedia_summary`, `corpus_search`), sound/performance, casting. The tool manual
  is **`recursive-eco/docs/CLAUDE-AI-WORKFLOW.md`** — READ IT via the GitHub connector before
  your first tool call.
- **The GitHub connector** — this repo (`PlayfulProcess/nara`) + its siblings
  (`kali-paradevi`, `recursive-tarot`, `recursive-eco` docs, `recursive.eco-schemas`).

Work **as a USER of the platform would** — someone who forked this project and is building it
with natural language. Make product and design decisions in plain words; let the tools do the
technical work. No code, no CLI, no SQL — if something seems to need those, it's a friction
point to journal, not a thing to attempt.

## 2. Project state (as of 2026-07-02, founding day)

**Live grammar in the app:**

| Grammar | UUID |
|---|---|
| wheel-of-the-year | `f8153f6e-d863-4a7f-9d6e-9213f7865f3d` |

(Slug→UUID map lives in `ids.json` — keep it updated when new grammars are created.)

**Preview any grammar from your phone (no extra hosting needed):** swap `<id>` for the UUID
above. Play/read + Edit are on the APP (flow.recursive.eco); Cards/Study/Tree/Thumbnails are on
the LANDING viewers (recursive.eco) — note the different domain. Play =
`https://flow.recursive.eco/play?id=<id>` · Edit =
`https://flow.recursive.eco/create/dashboard/unified/new?id=<id>` · Cards =
`https://recursive.eco/pages/grammar-viewer.html?type=custom&id=<id>` · Study =
`https://recursive.eco/pages/study-viewer.html?type=custom&id=<id>` · Tree =
`https://recursive.eco/pages/tree-viewer.html?type=custom&id=<id>` · Thumbnails = same as
Cards + `&layout=thumbnails`.
(Also kept in `ids.json` → `_preview_links` for a machine-readable copy.)

**Key files (read before proposing anything):**
- `README.md` — what Nara is: the tropical zodiac as an honest human frame on the year
  (equinoxes/solstices, precession stated plainly), the Trika architecture, the humility charter.
- `DESIGN.md` — the two-layer item shape (`The Sky` facts / `The Mirror` interpretation),
  reading lenses, casting = sky-maps not verdicts.
- `research/assets-inventory.md` — everything reusable across the family: the recursive-eco
  chart viewer + Skyfield backend (private, pattern only), recursive-tarot conventions,
  the recursive.eco-schemas grammars (esp. `archetypal-astrology-tarnas`), and the VERIFIED
  public-domain source links (Ptolemy @ LacusCurtius, Manilius + Lilly @ archive.org).
- `course/00`–`06` + `course/README.md` — "From Zero to Your First Altar", the beginner course
  this repo was born from. The course is the project's centerpiece.
- `journal/2026-07-02.md` — founding decisions + the Brazil-trip test plan.
- `grammars/wheel-of-the-year/grammar.json` — the first grammar seed (also live, UUID above).
  Layout is `grammars/<slug>/grammar.json` (matches recursive-tarot, so recursive.eco's channel
  import + GitHub→app sync work). Each grammar carries `_recursive_eco_url` (its live app link).
- `recursive-eco.json` — the channel manifest (channel identity + grammar paths + `ids.json` map).
  This is what makes recursive.eco import the repo as the **nara** channel.

**Decided (don't re-litigate):**
- Two-layer item shape: sky layer (facts, hedged, hemisphere-honest) strictly separated from
  mirror layer (explicitly interpretive). Section names visible to readers.
- Hemisphere honesty is a standing rule — the classical sign-to-season mapping is
  Northern-Hemisphere-centric and the data says so.
- Non-overwhelming sources: SHORT summary + hyperlink to a public-domain edition. Link, don't
  host. Always author + date + "historical interpretation" flag.
- Reading lenses are OURS, never attributed to thinkers who didn't say them; lens visibility
  is a channel customization.
- Casting = sky-maps, not cards (builds on kali-paradevi's "Charts without doctrine").
- Course written first, grammars grow behind it.

**Open (the builder decides, you propose):**
- License (CC BY-SA 4.0 suggested; README placeholder still open).
- Which grammars come after wheel-of-the-year (likely: the four seasonal anchors already in the
  wheel, then the twelve signs in the two-layer shape).
- Al-Biruni source URL — NOT yet located/verified; never paste a guessed URL into a grammar.
- The course is untested by a real fresh account — the trip test (see backlog) closes that.

## 3. Cross-repo context — the Trika family

| Repo | Role |
|---|---|
| **nara** (this) | the human-subjective sky — ecliptic, seasons, tropical zodiac |
| **kali-paradevi** | the sibling: the objective deep sky — black holes, galaxies, paired items with the bidirectional `emanation` flip |
| **recursive-tarot** | the pattern source — folder conventions (`<slug>/grammar.json`, `_eco_ids.json`), viewers, course→grammar pipeline, source-text policy |
| **recursive-eco/docs/CLAUDE-AI-WORKFLOW.md** | the tool manual — the MCP tool list, known gaps, session hygiene |

**Consult siblings via the GitHub connector before inventing.** If a shape, convention, or
policy might already exist in the family, it probably does — read it there first (e.g. item
shapes come from kali-paradevi's DESIGN, repo layout from recursive-tarot, tool behavior from
the workflow doc).

## 4. The documentation duty (non-negotiable)

- **Every working session ends with a journal dump** — `journal/YYYY-MM-DD.md` via the GitHub
  connector: decisions made, grammar UUIDs touched/created, friction encountered, next steps.
  The repo is the shared memory between sessions; an undumped session is a lost session.
- **Screenshots**: the builder attaches phone screenshots of key steps into the chat. Ask her
  to save the good ones to the repo under **`journal/screens/`** (uploading via github.com in
  the phone browser works). These become the course's illustrations — treat every clear
  screenshot of a step as course material.
- **The course absorbs every lesson.** When friction is found — an instruction that doesn't
  match the screen, a tool that behaves unexpectedly, a step a beginner would stall on —
  propose the matching edit to **`course/`** (this repo hosts the course for the whole family)
  in the same session. The course is only done when a real fresh account gets through it.

## 5. Working style

- **Humility charter**: educational/study purposes only. No special sources, no tradition's
  authority, no special insight claimed. NO invented attributions — lenses are OURS; historical
  sources always carry author + date + "historical interpretation".
- **Real astronomy, conservative claims.** Equinoxes, solstices, precession — verifiable and
  hedged. Never assert what can't be checked; the mirror layer asks, never tells (non-consent
  axiom: nothing may claim to know the user better than they know themselves).
- **PD sources as summary + hyperlink** — link, don't host. Prefer the VERIFIED links in
  `research/assets-inventory.md`; for anything automated prefer LacusCurtius over
  sacred-texts.com (the latter bot-blocks).
- **Plan item ORDER before `add_items`** — it's append-only, there is no reorder tool. Confirm
  the ordered list with the builder first.
- **New MCP tools need a fresh chat** — the client caches the tool list at chat start. If a
  tool seems missing (e.g. the new `nasa_image_search`), start a new chat.

## 6. Backlog (nara)

1. **Jyotish overlay research lane** — sidereal/Jyotish as a *lineage overlay* (like tarot's
   genealogy layer), researched and attributed as its own tradition — never blended into the
   tropical frame. Start as a research note (`research/`), not a grammar.
2. **Tetrabiblos link swap to LacusCurtius** — `grammars/wheel-of-the-year.json` and
   `DESIGN.md` currently link sacred-texts.com (Ashmand), which 403s to automated fetches.
   Swap source links to the verified Robbins translation at LacusCurtius
   (`https://penelope.uchicago.edu/Thayer/E/Roman/Texts/Ptolemy/Tetrabiblos/home.html`;
   per-book URL pattern in `research/assets-inventory.md`), then update the LIVE grammar
   (UUID above) via `update_items`.
3. **Planets grammar from `archetypal-astrology-tarnas`** — the most Nara-ready seed that
   exists (23 planetary archetypes from Tarnas's *Cosmos and Psyche*, in
   recursive.eco-schemas). Fork/import it, add the sky-layer facts per planet, attribute
   Tarnas as a modern interpretive source.
4. **I Ching altar test** — the builder mimics a FRESH user: separate claude.ai account,
   following `course/01`–`06` exactly as written, building an I Ching altar from a phone.
   Journal every mismatch into the test repo, then fold fixes back into `course/` here.
