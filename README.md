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
| Races | Complete |
| Artifacts | Complete (dig times need verification) |
| Ships | Stub — needs formatting |
| Battle Mechanics | Incomplete — needs dedicated session |
| Federations | Complete |
| Index | Stub |

## Known gaps

- Combat depth: weapon types, shield interactions, stack tactics
- Missions: not yet documented
- Dig times: verify Malaysian server time windows with devs
- Ship list: CSV imported but needs per-race formatting
- PR system: partial, needs expansion

## Source notes

- Ship list CSV dated Feb 2023, confirmed current at wiki creation
- Artifact formulas from ucguides.weebly.com and theflyingcircus.weebly.com
- Battle mechanics from gcc.wrindustries.com HEF guide (2008, last edited 2022)
- Enslaving mechanic is **disabled** — do not document until reworked
- UW ships are **trophies only** — 0 build rate, no active fleet copies
