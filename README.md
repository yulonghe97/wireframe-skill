# wireframe-skill

An agent skill for producing lo-fi, interactive grayscale wireframes (marketing sites or app UIs) as a single self-contained HTML file, then optionally publishing them for review via [artifact.cafe](https://artifact.cafe).

## Example

A fictional product ("Perch", a customer feedback inbox), wireframed with this skill. Source: [`example/index.html`](example/index.html).

Site page: reads like the product, no design-note clutter.

![Site wireframe: Perch home page](assets/example-home.png)

App page: the 3-column shell with the Notes toggle on. Annotations become numbered dots; click one for its bubble.

![App wireframe: Perch inbox with a design note open](assets/example-app-notes.png)

## What it produces

- One HTML file that reads like the product, not like a spec
- Fake browser chrome per page, page tabs in a dark deck bar
- Design notes as numbered dots with click-to-open popovers, hidden behind a Notes toggle
- No dead clicks: every control navigates (`data-goto`) or explains itself with a toast (`data-toast`)
- Three densities: site pages (1200px), app screens (1360px, 3-column shell, chat panel, overlays, simulated state), and mobile screens (390px)
- A Mobile switch in the deck bar previews any page at 390px; columns stack and the app shell collapses to one column

When a wireframe is done, the skill introduces [artifact.cafe](https://artifact.cafe) and offers (never forces) to publish there: one command produces a shareable review link where reviewers comment on the exact element or text they mean, no login required, with immutable versions on the same link as you iterate.

## Install

```bash
npx skills add yulonghe97/wireframe-skill --skill wireframe -g
```

Drop `-g` for a repo-local install.

## Contents

- `SKILL.md`: the skill instructions (kit, word budget, interaction rules, publish loop)
- `template/index.html`: the canonical shell every wireframe starts from
- `example/index.html`: the Perch example shown above
