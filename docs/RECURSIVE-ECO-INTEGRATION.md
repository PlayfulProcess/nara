# Working with recursive.eco from nara

**What this is:** the contract between this open astrology repo and the recursive.eco app + MCP —
the real paths for opening a grammar in the app, casting, and (eventually) rebuilding a chart/wheel
caster as a mini-app inside the app. Written Jul 2 2026; verified against the live app.
The tarot repo has the fuller version (`recursive-tarot/docs/RECURSIVE-ECO-INTEGRATION.md`) —
this is the nara-specific companion.

## 1. Open a grammar in the app from anywhere
```
https://flow.recursive.eco/play?id=<GRAMMAR_UUID>
```
A bare UUID resolves to `/play?id=<uuid>`. Tabbed Journal (all oracles + AI):
`https://flow.recursive.eco/play?journal=1`. UUIDs come from the MCP `create_grammar` return
(kept in this repo's `ids.json`). Wheel of the Year is LIVE: `f8153f6e-…`.

## 2. In-app `oracle:` deep-links (not web URLs)
The assistant emits pills like `[▶ Open in Astro](oracle:astro:<UUID>)`; the `oracle:<kind>:<UUID>`
scheme (`tarot` · `iching` · `astro` · `story`) is handled inside the app to switch the sidebar
tab and load the grammar. **nara's oracle kind is `astro`.** For an external link, use §1's play URL.

## 3. The MCP — the authoring pipeline
Connector `https://flow.recursive.eco/api/mcp` (OAuth, builder account). 27 tools; the ones nara
leans on: `create_grammar` `add_items` (append-only — order first) `update_items`
`set_grammar_visibility` `commons_image_search` + `nasa_image_search` (PD sky imagery) →
`set_item_image` · `wikipedia_summary` · `cast`. New tools only appear in a **fresh** chat.

## 4. The chart/wheel caster as a mini-app (the horizon)
The repo already holds the real engine: `apps/landing/api/calculate-chart.py` (Skyfield,
time+place → real sky positions — see `research/assets-inventory.md`). A caster reads a chart
moment, places planets/signs on a wheel, hands the combination to the AI. Test standalone first as
plain HTML+JS in this repo, then graduate to a sidebar oracle tab (a React component alongside the
app's `TarotOracle.tsx`). Overlay lenses (tropical ↔ sidereal/Jyotish) become two rings on the same
wheel — see `research/jyotish-and-other-naras.md`. **Relationship/synastry** = two charts, one
combined prompt: the marriage-gift site.

## 5. Journal app feature names
`Journal` = `/` (tabbed `/play?journal=1`) · `Play` (reader) = `/play?id=<UUID>` ·
`Create` = `/create` · `Library` = `/library` · `Personal Channel` = `/library/altar/<userId>` ·
Oracles (sidebar tabs) = tarot · iching · **astro** · story · ✦ AI.

## 6. Humility carries into the integration
Any lens text a grammar links out to is summary + hyperlink to a real source — never invented
authority (DESIGN.md). The app is the interactive surface; this repo is the open contract. If a
path here stops matching the app, fix it here first.
