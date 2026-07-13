# wireframe-skill

A agent skill for producing lo-fi, interactive grayscale wireframes (marketing sites or app UIs) as a single self-contained HTML file, then publishing them for review via [artifact.cafe](https://artifact.cafe).

## What it produces

- One HTML file that reads like the product, not like a spec
- Fake browser chrome per page, page tabs in a dark deck bar
- Design notes as numbered dots with click-to-open popovers, hidden behind a Notes toggle
- No dead clicks: every control navigates (`data-goto`) or explains itself with a toast (`data-toast`)
- Two densities: site wireframes (static sections) and app wireframes (3-column shell, chat panel, overlays, simulated state)

## Install

```bash
npx skills add yulonghe97/wireframe-skill --skill wireframe -g
```

Drop `-g` for a repo-local install.

## Contents

- `SKILL.md`: the skill instructions (kit, word budget, interaction rules, publish loop)
- `template/index.html`: the canonical shell every wireframe starts from
