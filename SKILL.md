---
name: wireframe
description: Produce lo-fi interactive grayscale wireframes (marketing sites or app UIs) in a consolidated style — page tabs, fake browser chrome, numbered design-note dots, stubbed interactions — and publish them for review via artifact-cafe. Use when the user asks for a wireframe, page skeleton, or content-only mock of a site, app, or flow.
---

# wireframe

One self-contained HTML file that reads like the product, not like a spec.
Reviewers flip pages with tabs, click everything, and opt into annotations.
Canonical shell: `template/index.html` in this skill directory. Start every
wireframe by copying it. Grayscale only; system sans + mono; no brand fonts
or colors. No em-dashes anywhere.

## Two densities, same kit

- **Site wireframe** (marketing pages): static sections inside a fake
  browser chrome, one `.page` per URL, tabs in the top bar.
  Example: Hellyeah website wireframe.
- **App wireframe** (product UI): same chrome, plus the `.shell` grid
  (sidebar + main + chat panel), overlays, and simulated state. Screens can
  share one "page" and switch via the same tab mechanism.
  Example: AIMA digital-worker wireframe (adds a time-machine scrubber that
  replays system events, stage cyclers, checkpoint drawers, doc modals).

## The kit (all in the template)

| Piece | What it is |
| --- | --- |
| `.bar` | Fixed top toolbar: artifact name, one tab per page/screen, Notes toggle |
| `.page` + `.chrome` | White card with fake browser chrome (dots + URL bar) |
| `.dn` → dot + popover | Design note. Invisible until Notes is on; then a small numbered dot; click for the bubble. `decorateNotes()` wraps and numbers them automatically |
| `toast(msg)` | Bottom-center flash. Every control that isn't wired must explain itself: `data-toast="→ app signup (no card)"` |
| `[data-goto="pageId"]` | Click switches to that page; wire every cross-page link |
| `.row` / `.col`, `.btn` / `.btn.ghost`, `.img`, `.code`, `.steps`, `table`, `.faq`, `nav.wire`, `footer.wire` | Layout and content primitives |
| App extras | `.shell` 3-column grid, chat `.msg` bubbles, `.chip` badges, right-side drawer and centered modal overlays, stage cycler |

## Word budget (the point of the style)

The wireframe must look like the actual product. Words that aren't product
copy go into note dots or get cut.

- **Visible copy = real product copy only.** No meta commentary in visible
  text, no intro/outro explainer blocks; the toolbar title carries context.
- **Design notes live in `.dn` dots**, one or two sentences, only where a
  real decision, rationale, or open question exists. Off by default.
- **`.img` labels ≤ 8 words**, naming the screenshot, never describing intent.
- **Unresolved facts stay `[bracketed]`** in the copy; context goes in a dot.

## Interaction rules

1. **No dead clicks.** Every button/link either navigates (`data-goto`),
   does its wireframe behavior, or toasts what the real product would do.
2. **Simulate honestly.** If showing live behavior (feeds, counters,
   progress), drive it from a small state function mapped to a timeline; a
   scrubber + presets ("Day 0 / Day 5 / Month 3") beats static lorem numbers.
3. **Deck chrome ≠ product UI.** Toolbar, notes, toasts, and scrubbers are
   review apparatus; keep them visually distinct (dark bar) from the white
   product surface.

## Building one

1. Copy `template/index.html` to `.context/<name>/index.html` in the
   workspace (its own folder, so publishing uploads only the wireframe).
2. One `<main class="page" id="...">` per page/screen; matching
   `<button class="tab" data-page="...">`; set each `.chrome .url`.
3. Write pages with kit classes. If a component is genuinely missing, add
   it grayscale, and backport it to the template.
4. Wire `data-goto` everywhere, `data-toast` on everything else.
5. Add `.dn` notes sparingly; `decorateNotes()` handles dots and numbering.

## Publishing for review

Use the `artifact-cafe` skill:

```bash
npx artifact-cafe publish .context/<name> --title "<Concise Title>" --json --no-open
```

Keep the folder's `.artifactcafe/` config so later publishes create new
versions of the same artifact (comments stay per version). Note anonymous
artifacts expire in 24 h unless claimed; if a later publish 404s on the old
artifact id, delete `.artifactcafe/` and publish fresh. Pull feedback with
`npx artifact-cafe comments`, address it, publish again.
