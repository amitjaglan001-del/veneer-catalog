# Revamp Assortment

**Project:** Revamp Assortment Exercise — Urban Company
**Repo:** `git@github.com:amitjaglan001-del/veneer-catalog.git`
**Purpose:** Evaluate and catalog premium decorative surface materials (veneer films, stone panels, marble films) for Urban Company's assortment in the Indian market.

---

## Workflow

1. **Analyse** — User provides a product image (+ optional species/stone name). Use the `panel-expert` skill to run a full analysis.
2. **Score** — Each product gets a composite score (demand × mimicry for films; 7-dimension weighted score for stones/marbles).
3. **Save** — Write outputs:
   - **JSON entry** → append to `films.json`, `stones.json`, or `marbles.json`
   - **Markdown file** → individual deep-analysis file in `films/`, `stones/`, or `marbles/`
   - **Image** → save product image in `films/images/`, `stones/images/`, or `marbles/images/`
   - **Catalog index** → update `veneer-catalog.md` or `stone-catalog.md` leaderboard
4. **Push** — After every analysis, commit all changes and `git push` to origin/main.

---

## File Structure

```
├── index.html              # Interactive web catalog (vanilla HTML/CSS/JS)
├── films.json              # Veneer film catalog data
├── stones.json             # Stone panel catalog data
├── marbles.json            # Marble film catalog data
├── veneer-catalog.md       # Veneer leaderboard & index
├── stone-catalog.md        # Stone/marble leaderboard & index
├── films/                  # Individual veneer analysis markdown files
│   └── images/             # Veneer product images
├── stones/                 # Individual stone analysis markdown files
│   └── images/             # Stone product images
└── marbles/                # Individual marble analysis markdown files
    └── images/             # Marble product images
```

## Scoring

### Veneer Films
- **Score** = weighted average of Demand (market pull) + Mimicry (quality of wood replication)
- Scale: 0–10
- Tiers: Top 3 Candidate (≥8.5) · Strong Contender (7.0–8.4) · Niche (5.0–6.9) · Low Priority (<5.0)

### Stone & Marble Panels
- **Score** = 7-dimension composite out of 100: Fidelity×25 + Colour×20 + Veining×18 + Finish×12 + Versatility×10 + Texture×8 + Trend×7
- Tiers: Ultra-Premium (80–100) · Premium (65–79) · Mid-Premium (50–64) · Value (35–49) · Not Recommended (<35)
- JSON scores are normalized to /10 scale for the website display.

## JSON Schema (key fields per entry)

All entries include: `rank`, `name`, `code`, `brand`, `score`, `tier`, `topApplication`, `bestSegments`, `bestCities`, `keyStrength`, `keyWeakness`, `priorityFix`, `image`, `file`

Films add: `species`, `speciesLatin`, `cut`, `finish`, `demand`, `mimicry`
Stones/Marbles add: `stoneReference`, `colourFamily`, `finish`, `demand`, `mimicry`

## Important Rules

- Always sort JSON arrays by score descending and re-rank after adding new entries.
- Always push to git after analysis (json + md + image + commit + push).
- Use the `panel-expert` skill for all panel/film analyses.
- Images go in the category-specific `images/` subdirectory.
