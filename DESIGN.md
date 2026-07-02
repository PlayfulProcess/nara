# DESIGN — nara

Author: PlayfulProcess. Status: seed, 2026-07-02.

This document seeds the data shapes for Nara's tropical grammars and its casting layer. It deliberately mirrors the design of the sibling project, [kali-paradevi/DESIGN.md](https://github.com/PlayfulProcess/kali-paradevi/blob/main/DESIGN.md) — same two-layer honesty structure, same casting philosophy — adapted to the subjective sky.

## 1. What a Nara item is

An item is a human frame on the year: a sign, a season marker, an element grouping, a cross-quarter day, a planet-as-symbol. The key design commitment, inherited from kali-paradevi and enforced in the data:

**Two layers per item, kept strictly separate, so a reader always knows which register they are in.**

### Sky layer (facts — verifiable, hedged, hemisphere-honest)

The sky layer states what actually happens, from Earth. Not "Aries makes you bold" but "the Sun crosses the celestial equator heading north." Examples of honest framings:

- **Aries (tropical):** "Begins at the March equinox — the moment the Sun crosses the celestial equator moving north. Day and night are near-equal everywhere on Earth. In the Northern Hemisphere this opens spring; in the Southern Hemisphere, autumn."
- **Cancer (tropical):** "Begins at the June solstice — the Sun's northernmost point on the ecliptic. Longest day in the north, shortest in the south."
- **Precession note (carried wherever a sign is named):** the tropical sign no longer overlaps the constellation of the same name; the offset is currently around 24 degrees and grows about one degree every 72 years.

Hemisphere honesty is a standing rule: the classical season-to-sign mapping is Northern-Hemisphere-centric, and Nara says so rather than presenting it as universal. (The builder is Brazilian; half the audience lives in the other half of the year.)

```json
{
  "id": "sign-aries",
  "name": "Aries",
  "sky": {
    "anchor": "March equinox",
    "what_happens": "The Sun crosses the celestial equator moving north; day and night are near-equal worldwide.",
    "dates_approx": "about March 20 to April 19 (tropical; varies by year)",
    "hemisphere_note": "Opens spring in the Northern Hemisphere, autumn in the Southern.",
    "precession_note": "The tropical sign Aries no longer overlaps the constellation Aries.",
    "element_frame": "Fire (a classical human grouping, not a physical property)"
  }
}
```

Elements (fire, earth, air, water) and modalities (cardinal, fixed, mutable) are carried as **classical human groupings** — labeled as frames people used, never as properties of the sky.

### Mirror layer (meaning — explicitly interpretive, non-overwhelming)

```json
{
  "mirror": {
    "theme": "the year begins wherever you decide to start counting",
    "prompt": "What in your life is at its equinox — poised between two seasons, belonging to neither yet?",
    "sources": [
      {
        "summary": "Ptolemy places the zodiac's start at the spring equinox and builds the signs' qualities from the seasons, not the stars.",
        "attribution": "Ptolemy, Tetrabiblos, 2nd century CE — a later systematization, itself one interpretation among many",
        "link": "https://www.sacred-texts.com/astro/ptb/"
      }
    ]
  }
}
```

**Non-overwhelming is a design rule, not a taste.** The centuries of interpretive literature on each sign could bury a card. So a card carries a SHORT summary of what a historical source says, plus a hyperlink to the source passage in a public-domain edition online — we **link, we do not host**. Good homes for links: [sacred-texts.com](https://www.sacred-texts.com/astro/) (Ptolemy's Tetrabiblos in the public-domain Ashmand rendering), [archive.org](https://archive.org) (Manilius's Astronomica and other public-domain editions). Every source line carries author, date, and a flag that it is historical interpretation — the same source-text policy as recursive-tarot.

In grammar JSON the two layers merge into one item with clearly named sections (e.g. `The Sky` for facts, `The Mirror` for reflection), so the register is visible to the reader, not just to the schema.

## 2. Reading lenses

A lens is a way a person relates to a reading — "read the sign as the season your question is in," "read the chart as a snapshot you chose to keep." Two rules, inherited verbatim from the Trika family:

- **Lenses are OURS.** A lens is our own creation, possibly influenced by depth psychology or by historical practice, and it is presented as ours. Never attribute lens text to thinkers who did not say it — no quotation-shaped paraphrases with a famous name attached.
- **Lens visibility is a channel customization.** Each channel (and possibly each page) chooses whether lenses render, which ones, or none. A kids channel might show no lenses; a study channel might show all of them. The data carries the lenses; the surface decides.

## 3. Casting: sky-maps, not verdicts

Nara's casting shape follows kali-paradevi's "Charts without doctrine" design directly: **the caster casts MAPS, not cards.** Where tarot's casting shape is a spread of card positions, Nara's is a cast sky-map — a time and a place resolved into how the ecliptic actually stood from there: what was rising, where the Sun sat in the year, which tropical frame was overhead.

- **The chart is an invitation, not a claim.** The system never asserts that the moment was deterministic. If YOU choose to hold a moment as meaningful — a birth, a meeting, a decision — you can investigate it as a chart. The belief is the user's to bring; the system supplies an honest sky (the non-consent axiom applied to astrology).
- **The map is honest astronomy.** Positions are computed, not vibed; the tropical frame is labeled as the tropical frame; the constellations, if shown, are shown where they actually are.
- **Reading a chart is contemplation, not lookup.** Meaning renders through the mirror layer and the channel's chosen lenses — short, linked, never a wall of doctrine.
- Casting shapes are **inferred data shapes, never stored types**, matching the platform's design rule.

## 4. Where the Trika projects meet

A Nara sky-map and a kali-paradevi draw can eventually share a surface: the same moment viewed subjectively (the ecliptic from your place, Nara) and objectively (what actually sits in that direction — a galaxy, a void, kali-paradevi's paired items). That junction is the Trika metagrammar's reason to exist. Design later; name it now.

## 5. Values (inherited, enforced in design)

- **Meaning-making over fortune-telling** — the mirror layer asks, never tells.
- **Non-consent axiom** — no item text may claim authority over the user ("you are…", "you will…"). Prompts are questions; readings are offered framings.
- **Honesty about what it is** — sky and mirror kept in separate, labeled layers; no astronomy claim without a verifiable basis; precession and hemisphere caveats carried in the data, not buried in a footnote.
- **Humility charter** — educational and study purposes only; no special sources, no tradition's authority, no special insight claimed. Sources are linked and attributed; lenses are owned.
