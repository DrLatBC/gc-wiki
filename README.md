# Galactic Conquest Wiki

Community wiki for the web-based text MMO **Galactic Conquest (GC)**, documenting game systems for both developers and players.

**Live site:** https://drlatbc.github.io/gc-wiki/

## Local development

```bash
pip install mkdocs-material
mkdocs serve
```

Then open http://127.0.0.1:8000.

## Deploy

GitHub Pages is built automatically by the workflow in `.github/workflows/deploy.yml` on every push to `main`.

To deploy manually:

```bash
mkdocs gh-deploy
```

## Status

| Page | Status |
|------|--------|
| Turns | Complete |
| Resources | Complete |
| Income Types | Complete |
| Colonies | Complete |
| Exploration | Complete |
| Planet Types | Complete |
| Formulas | Complete |
| Races | Complete |
| Artifacts | Complete (dig times need verification) |
| Ships | Complete — stats deferred to Vigi's live shiplist |
| Battle Mechanics | Complete |
| Missions | Complete (Terran, Aspha Miner, Guardian) |
| Federations | Complete |
| Index | Complete |

## Known gaps

- Combat depth: specific ship matchups and per-race counter picks (weapon/shield interaction, stack mechanics, and composition R/P/S are now covered)
- Dig times: verify Malaysian server time windows with devs
- T./A. U-class variants: gordo land/planet thresholds not yet documented
- Ship stats: deferred to Vigi's live shiplist by design — not duplicated here

## Source notes

- Ship list CSV dated Feb 2023, confirmed current at wiki creation
- Artifact formulas from ucguides.weebly.com and theflyingcircus.weebly.com
- Battle mechanics from gcc.wrindustries.com HEF guide (2008, last edited 2022)
- Enslaving mechanic is **disabled** — do not document until reworked
- UW ships are **trophies only** — 0 build rate, no active fleet copies
