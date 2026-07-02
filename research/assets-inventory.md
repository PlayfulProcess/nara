# Nara — Assets Inventory

**Purpose:** What already exists across Fernanda's repos + the public web that Nara (tropical astrology as "the human-subjective sky", sibling of kali-paradevi) can reuse. Written for future sessions **including phone-only claude.ai sessions** — every asset has a concrete path, UUID, or URL. All local paths, repo URLs, and external links below were verified on **2026-07-02** (verification method noted where it matters).

**Companion docs:** `nara/DESIGN.md` (the two-layer sky/mirror item shape), `kali-paradevi/DESIGN.md` ("the caster casts MAPS, not cards", lines 105–109).

---

## 1. The astrological map already drawn in recursive-eco

recursive-eco is **PRIVATE** (Next.js monorepo, `C:\Users\ferna\OneDrive\Documentos\GitHub\recursive-eco`). Nara copies the *pattern*, never the platform code. Phone sessions cannot read these files — the essentials are captured here.

### 1a. The full chart viewer (the big one)

**`recursive-eco/apps/landing/pages/astrology-viewer.html`** — 8,472 lines, single-file static app.
Live and verified (HTTP 200): **https://recursive.eco/pages/astrology-viewer.html**

What it renders:
- **Full natal chart wheel** — custom SVG drawn in-page (no chart library), pan/zoom, scales to ~1500px.
- **Tropical / Sidereal toggle** with ayanamsa section for sidereal (≈24° Lahiri offset) — the tropical default is *exactly* Nara's "human-subjective sky" framing, already built.
- **House systems**: Placidus (default), Whole Sign, equal-house fallback when cusps fail.
- **Aspects + transits** — `calculateTransitAspects()` compares transit planets vs natal bodies.
- **Human Design mandala** — a second view: 64-gate wheel, centers, `calculateHumanDesign()` (planets incl. Earth + nodes, `HD_PLANETS` at line ~6274).
- **Interpretation text inline** — per-planet story/shadow entries hardcoded in the page (e.g. Moon at line ~1856) PLUS grammar-driven interpretations loaded from Supabase.

What it consumes:
- **`recursive-eco/apps/landing/api/calculate-chart.py`** — Vercel Python serverless function. Uses **Skyfield + JPL ephemeris (de421.bsp, ~17MB, auto-downloaded to `/tmp/skyfield_cache`)**, `timezonefinder` + `pytz` for birth-time zone resolution. POST `/api/calculate-chart` with `{year, month, day, hour, minute, latitude, longitude, houseSystem, zodiac}`. Requirements: `skyfield>=1.46, timezonefinder>=6.0.0, pytz>=2023.0`. **This is real astronomy, not table lookup** — directly reusable as the computation backend for Nara's sky-map casting.
- Supabase (`user_documents`) for saving charts (`document_type: astrology_chart`) and loading interpretation grammars; `config.js` + `auth-init.js` for env/auth.

### 1b. The Journal-embedded oracle (React side)

All under `recursive-eco/apps/flow/src/`:

| File | Lines | What it does |
|---|---|---|
| `components/AstrologyOracle.tsx` | 1,080 | Journal oracle panel. Embeds the viewer in an **iframe** and receives calculated charts via **postMessage** (`CalculatedChartData`: planets, houses, aspects, ascendant, midheaven). Chart picker + grammar picker + "Interpret" (AI) with idle/loading/ready states. |
| `types/astrology.types.ts` | 447 | The data model: `BirthChart`, `PlanetPosition`, `ChartAspect`, `AstrologyInterpretation` (type: planet / sign / house / planet_sign / planet_house / aspect; fields: keywords, story, shadow, light, questions, affirmation), `AstrologyReading`. **Steal this schema for Nara items.** |
| `lib/astrology-grammars.ts` | 204 | Fetches astrology grammars from Supabase: `user_documents` filtered by `document_type astrology_interpretations/astrology_set/unified_grammar` + `tools` where `channel_slug='astrology'`. Category detection list: `['planet','sign','house','graha','rashi','nakshatra','aspect','transit']`. |
| `components/AstrologyGrammarSelector.tsx` | 61 | Grammar dropdown. |
| `components/AspectDetailModal.tsx` | 308 | Detail modal for a selected aspect/placement with stacked interpretations. |
| `components/offer/universal-editor/meaning-objects/BirthChartFields.tsx` | 361 | Editor fields for birth-chart meaning objects. |
| `channels/astrology.mdx` | — | The astrology channel page ("contemplative astrology... chart as mirror" — language already aligned with Nara's non-consent axiom). |

### 1c. Reusability verdict for Nara's sky-map casting

Per `kali-paradevi/DESIGN.md` §"The caster casts MAPS, not cards" (lines 105–109): the caster resolves **a time + place into what was actually overhead**. The recursive-eco stack already does the hard half:

- **Reusable as-is:** `calculate-chart.py` (Skyfield, time+place → planet longitudes/houses/aspects; tropical or sidereal). A Nara caster could call the same endpoint or vendor a copy of the ~one-file Python function.
- **Reusable as pattern:** iframe + postMessage handoff (viewer computes, oracle interprets), grammar-driven interpretation lookup keyed by placement, tropical/sidereal honesty toggle.
- **NOT what Nara renders:** the viewer draws a conventional zodiac wheel. Nara/kali-paradevi's cast shape is a **sky MAP** (each object flippable through its layers), so the wheel SVG is a reference, not the deliverable. The wheel code is also entangled with Human Design views — extract concepts, not the file.
- **Access note:** recursive-eco is private; Nara is meant to be public like recursive-tarot. Don't copy platform code verbatim into a public repo without the builder's say-so — the Skyfield API function is the one piece worth asking to liberate (it contains no platform secrets).

---

## 2. recursive-tarot — the structural pattern Nara copies

Local clone: `C:\Users\ferna\OneDrive\Documentos\GitHub\recursive-tarot` (public repo: https://github.com/PlayfulProcess/recursive-tarot, GitHub Pages via `CNAME` → tarot.recursive.eco; **Pages serves the `dev` branch** per memory). Raw grammar URL verified 200: `https://raw.githubusercontent.com/PlayfulProcess/recursive-tarot/main/tarot/tarot-de-marseille-conver/grammar.json`.

**License:** README declares **CC-BY-SA-4.0** for everything, built from public-domain sources. **No standalone LICENSE file at repo root** (checked — worth adding to Nara from day one).

### 2a. Folder conventions (copy these)

```
tarot/<deck-slug>/grammar.json    # one grammar per deck/course — 57 folders currently
tarot/_collection.json            # the collection manifest
tarot/_eco_ids.json               # slug → recursive.eco grammar UUID map (see 2c)
viewers/*.html                    # standalone viewers, all load grammar.json via grammar-loader.js
viewers/spreads.json              # spread definitions for the caster
viewers/voices.json               # reading-lens texts (NOTE: attributed lenses flagged for fix per kali-paradevi DESIGN.md lines 115–121 — Nara lenses are OURS, unattributed)
scripts/build_meta_grammar.py     # + ~30 build/enrich/audit scripts (build_tarot_collection.py, enrich_from_research.py, audit_image_usage.py ...)
site-header.js / theme.css / style.css   # shared shell (bump ?v=N on ALL pages when changing site-header.js)
course/*.mdx                      # course content → grammars via scripts/course_to_grammar.py
```

### 2b. The viewers (each ≈ one standalone HTML file in `viewers/`)

| Viewer | What it does |
|---|---|
| `cards.html` | Card browser — grid of a deck's cards with detail panel. |
| `explorer.html` | "Emergence Explorer — Pivot the Tarot": multi-deck pivot/compare, hover floating preview (`#hovprev`). |
| `genealogy-tree.html` | "Tree of Tarot" radial genealogy — how decks descend from one another. **Nara's lineage-layer model** (constellation myths / astrology traditions as a genealogy). |
| `tree-viewer.html` | Hierarchical tree view of a grammar. |
| `timeline.html` | Decks through time. |
| `sequence.html` / `sequence-v2.html` | Sequential reading of items. |
| `caster.html` | Redirect → caster-studio. |
| `caster-studio.html` | **Spread Caster** — the casting machinery Nara adapts from spreads-of-cards to cast SKY MAPS. |
| `perform.html` | Performance / karaoke playback of a grammar item. |
| `grammar-course.html` | Renders a grammar as a course. |
| Support JS: `grammar-loader.js` (fetch + normalize grammar.json), `deck-picker.js`, `dimension-engine.js`, `eco-links.js` (builds recursive.eco open/fork links from `_eco_ids.json`), `course-assistant.js`. |

### 2c. Grammar UUIDs (from `tarot/_eco_ids.json`, sourced from the recursive.eco DB)

Link patterns: open/read = `https://flow.recursive.eco/?deckId=<uuid>` ; fork = `https://flow.recursive.eco/create/dashboard/unified/new?forkId=<uuid>`.
Most relevant to Nara:

- `tree-of-tarot` (the genealogy meta-grammar): `1aa29bd2-eb06-4cf4-b53d-ab46da5e2d43`
- `people-of-tarot`: `a284fa37-694f-48dc-b977-f093658bc2b7`
- `books-of-tarot`: `7ff3ad23-6ceb-4b20-8c27-8bb04d0876ef`
- `all-decks-many-lenses`: `b03937bf-92be-414b-bd23-a85fe9be39eb`
- `how-to-contribute`: `368974ce-0718-4e9a-9351-bce7b2c053e4`
- `tarot-de-marseille-conver` (reference deck grammar shape): `ac47f7af-ac80-4942-a422-dd4a15614738`
- Full 37-entry map lives in `recursive-tarot/tarot/_eco_ids.json`.

**Source-text policy carried over** (memory: recursive-tarot-source-text-policy): render historical commentary only on tradition-native items; always attribute author + date + "later interpretation". This is already restated in `nara/DESIGN.md`.

---

## 3. Mythology / cosmology grammars already built (recursive.eco-schemas)

Public repo, `main` branch: https://github.com/PlayfulProcess/recursive.eco-schemas — local at `C:\Users\ferna\OneDrive\Documentos\GitHub\recursive.eco-schemas\grammars\<slug>\grammar.json`. Raw fetch verified 200: `https://raw.githubusercontent.com/PlayfulProcess/recursive.eco-schemas/main/grammars/<slug>/grammar.json`. These grammar.json files carry **no Supabase UUID** (keys: `_grammar_commons, name, description, grammar_type, ... items`) — to use one in the platform, import/fork it from the raw GitHub URL; to link a live copy, look it up via the recursive.eco MCP (`list_grammars`) in a desktop session.

### Best fits for Nara (verified names + item counts)

| Slug | Name (items) | Fitness for Nara |
|---|---|---|
| **`archetypal-astrology-tarnas`** | Archetypal Astrology — Richard Tarnas (23) | **The single most Nara-ready grammar that exists.** Planetary archetypes (Sun—Central Self, Moon—Receptive Soul, Mercury—Messenger, Venus, Mars, Jupiter—King, Saturn—Elder, Uranus—Awakener...) from *Cosmos and Psyche*. Nara's mirror layer for planets, essentially pre-drafted — needs the sky-layer facts added and Tarnas properly attributed as a modern interpretive source. |
| `myth-greece-rome` | Myths of Greece and Rome (87) | The lineage layer for constellation/planet name-myths (gods the planets are named after). Guerber-era PD source. |
| `metamorphoses-ovid` | Ovid's Metamorphoses (86) | Transformation myths incl. catasterisms (people → stars); pairs with the existing Ovid PD-art streams (Arachne, Narcissus). |
| `bulfinch-s-classical-mythology` | Bulfinch's Classical Mythology (19) | Compact classical-myth reference layer. |
| `timaeus-plato` | Timaeus (12) | "Time and the Heavenly Bodies", World Soul, Demiurge — THE ancient cosmology text behind astrology's worldview; Jowett PD translation. |
| `cosmic-unfolding` | Cosmic Unfolding (40) | Big Bang → now in 30+ milestones — the **objective-sky counterweight**; this is kali-paradevi's register, useful for cross-linking sibling projects. |
| `myths-babylonia-assyria` | Myths of Babylonia and Assyria (26) | Where the zodiac actually began (MUL.APIN culture) — origin-lineage layer. |
| `egyptian-mythology` | Myths and Legends of Ancient Egypt (14) | Decans / Egyptian sky-religion adjacency. |
| `prose-edda` | The Prose Edda (30) | Norse cosmology — non-Greek sky stories for the "many skies" framing. |
| `popol-vuh` | The Popol Vuh (37) | Maya creation/cosmology — same. |
| `myths-through-many-eyes` | 43 world myths × 13 interpreters (43+) | The multi-lens pattern (Jung, Campbell...) Nara's reading lenses can copy structurally. |
| `eleusinian-mysteries` | The Eleusinian Mysteries and Rites (12) | Seasonal/agrarian mystery religion — resonates with tropical = seasonal zodiac. |
| `consciousness-of-the-atom` / `seven-rays-ancient-roots` (29) / `seven-rays-bailey-expressions` | Bailey esoterica (27/29) | Esoteric-astrology lineage (Bailey) — later interpretive layer, attribute as such. |
| `zhouyi-legge` / `repair-iching` | Zhouyi (64) | I Ching cosmology adjacents — pattern reference for "cast a moment, read a structure". |

Also in the repo, same folder: `alchemy-ancient-modern`, `book-of-the-dead-egyptian`, `plutchik-wheel-of-emotions`, plus the whole tarot mirror set. Nara already has its first grammar seed: **`nara/grammars/wheel-of-the-year.json`**.

---

## 4. Public-domain source texts for tropical astrology (link, don't host)

Format rule (from `nara/DESIGN.md`): each card's mirror layer carries a **SHORT summary + hyperlink to the passage** in a PD edition, with author + date + "a later interpretation" flag. Never host whole books unless one is later adopted for RAG.

### Ptolemy — *Tetrabiblos* (2nd c. CE; the founding text of TROPICAL astrology)

- **Primary link (verified HTTP 200 on 2026-07-02):** LacusCurtius, F.E. Robbins translation (Loeb 1940, unrenewed copyright — PD in the US):
  `https://penelope.uchicago.edu/Thayer/E/Roman/Texts/Ptolemy/Tetrabiblos/home.html`
- **Secondary:** sacred-texts.com Ashmand (1822) rendering: `https://www.sacred-texts.com/astro/ptb/` — **NOTE: sacred-texts returned 403 to curl (bot-blocking); it loads fine in browsers.** Phone sessions: prefer the LacusCurtius link for anything automated.
- **Maps to grammar items:** Book I chs. 4–8 (planet natures — pairs with the Tarnas grammar), Book I chs. 10–13 (**why the zodiac starts at the equinox — THE tropical-sky argument, quote for the Aries item**), Book I chs. 17–24 (houses/exaltations/triplicities), Book II (mundane), Book III–IV (natal topics). LacusCurtius URL pattern per book: `.../Tetrabiblos/1A*.html` etc. — link to the book page + section anchor.

### Manilius — *Astronomica* (1st c. CE; earliest surviving astrological poem)

- **Verified (HTTP 200):** Thomas Creech's 1697 English verse translation, *The Five Books of M. Manilius*: `https://archive.org/details/TheFiveBooksOfM.ManiliusAncientAstronomy` (a second scan of the 1700 printing exists: item `bim_early-english-books-1641-1700_the-five-books-of-m-man_manilius-marcus_1700`).
- **The Loeb (G.P. Goold, 1977) is NOT public domain — do not link or excerpt it.**
- **Maps to items:** Book 2 (signs' characters, aspects, the 12 athla), Book 3 (houses/lots), Book 4 (**sign-by-sign meanings — the richest per-sign source**), Book 5 (extra-zodiacal constellations rising with degrees — lineage layer for constellation myths).

### William Lilly — *Christian Astrology* (1647; the English horary classic)

- **Verified (HTTP 200):** `https://archive.org/details/christian-astrology-1647` (item title: "Christian Astrology, Editions from 1647–2022" — link the 1647 scan inside it; alternate item: `ChristianAstrologyByWilliamLilly`).
- **Maps to items:** Book 1 chs. on the 12 houses and the 7 planets (temperament, significations — extremely quotable per-planet/per-house), Book 1 sign descriptions (body/temperament per sign). Flag as 17th-century horary tradition, not "what astrology is".

### Al-Biruni — *The Book of Instruction in the Elements of the Art of Astrology* (1029; R. Ramsay Wright trans. 1934)

- **Status: NOT verified this session.** Archive.org search (multiple queries: title, "tafhim", creator:biruni) did not surface the Wright 1934 scan — it may exist under a nonstandard identifier or on another host. **Do not paste a guessed URL into a grammar; locate and verify first** (a desktop session with browser can find it — it circulates widely as a PDF).
- Verified adjacent (HTTP 200 via search result): *Alberuni's India* — `https://archive.org/details/alberunisindiaac01brnm` (1888) — has cosmology/astronomy chapters but is NOT the astrology manual.
- **Maps to items (once located):** its numbered-paragraph format (§§ on signs, planets, lots, aspects) is the most grammar-shaped of all four sources — one paragraph ≈ one card note.

### Strategy summary

| Source | Century | Verified URL | Best for |
|---|---|---|---|
| Ptolemy (Robbins @ LacusCurtius) | 2nd | YES | Tropical rationale, planet natures, dignities |
| Manilius (Creech @ archive.org) | 1st | YES | Per-sign poetry, constellation lore |
| Lilly (archive.org) | 17th | YES | Houses, planet significations, horary voice |
| Al-Biruni (Wright 1934) | 11th | **NO — locate before linking** | Numbered sign/planet/aspect definitions |

---

## Quick-pull cheatsheet for phone sessions

- Nara design: `https://github.com/PlayfulProcess/nara` → `DESIGN.md` (if pushed) — item = sky layer (facts) + mirror layer (interpretation).
- Tarot pattern: `https://github.com/PlayfulProcess/recursive-tarot` — copy `tarot/<slug>/grammar.json` + `viewers/` + `scripts/build_meta_grammar.py` conventions; CC-BY-SA-4.0.
- Grammar seeds: `https://raw.githubusercontent.com/PlayfulProcess/recursive.eco-schemas/main/grammars/archetypal-astrology-tarnas/grammar.json` (and siblings per §3).
- Chart math: private `recursive-eco/apps/landing/api/calculate-chart.py` (Skyfield); live UI `https://recursive.eco/pages/astrology-viewer.html`.
- PD texts: LacusCurtius Tetrabiblos, archive.org Creech Manilius + Lilly 1647 (all verified); Al-Biruni pending.
