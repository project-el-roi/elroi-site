# Project El Roi — site context

A single static page for a Ugandan-led hunger response in Logoole Village,
Kotido Rural Parish, Kotido Municipality, Karamoja. Hosted on Vercel from
this repo. Slogan: "God sees, We act."

## Structure

    index.html    the entire site — markup, styles and script in one file
    data.json     every figure and photo the page displays
    photos/       image files referenced from data.json
    README.md     deploy and maintenance instructions

No build step. Vercel serves the files as they are. Preset is "Other",
root `./`, all build commands empty.

## How data flows

`index.html` carries a baked-in copy of the figures as a fallback, then
fetches `data.json` at load and re-renders from it. Always edit
`data.json` — the baked-in copy is only there so the page still renders if
the fetch fails. Never introduce a second source of truth.

## Design decisions to preserve

Palette, as CSS custom properties on `:root` with a dark-mode counterpart:
sand background `#F7F2E9`, clay `#C2410C` (`--ochre`), water teal `#0E6A7D`
(`--sky`), ink `#1A1F22`. Dark mode is a warm brown-black, not a cold one.

The two accents carry a rule: **clay is action, teal is information and
outcome.** Clay marks what the project or a donor does — the "The work",
"What a gift buys" and "Giving" section headers, the dollar amount in the
slider, "God sees". Teal marks explanation and result — the "Why now",
"How it connects" and "From the ground" headers, body links, the meal count
in the slider, "We act". Keep new elements consistent with that split
rather than adding a third accent.

Type is Archivo for display and UI, Source Serif 4 for body. Sentence case
throughout, except the slogan's "We act."

The page is written as a dated ledger, not a brochure. Figures are tied to
specific feeding reports and dates. The tone is deliberately sober and
specific; resist adding promotional copy, exclamation marks, or claims that
are not backed by a dated report.

## The interconnection map

An SVG built in JS from `NODES` and `EDGES` arrays near the top of the
script. Nine nodes, fourteen directed edges. Node positions are hand-tuned
against a `0 0 920 660` viewBox; edges take a signed curvature `k` so they
bow around nodes they would otherwise cross. If you move a node, re-check
the edges near it for overlap.

`kind` is `root` (dashed — a condition nobody can change), `live` (solid
clay — something the project is already doing) or `planned`.

## Things that are deliberately absent

There is **no donate button.** The giving section explains that money
currently moves as mobile money to the pastor, that there is no registered
account, independent bookkeeping or audited trail, and that a button before
those exist would be asking for unearned trust. It then names the three
things being built first. Do not add a payment widget until the user says
those exist, and when the section changes, say the date it changed.

Seven of the nine initiatives are listed as "Not started" and most say "Not
yet costed". That honesty is the point, not an omission to fill in.

## Photographs

Shrink to ~1400px wide and strip EXIF before committing — phone photos carry
GPS coordinates, and this repo is public and permanent:

    mogrify -strip -resize 1400x -quality 78 photos/*.jpg

Captions carry place and date only. No beneficiary names, no children's
names, no phone numbers. The same applies to commit messages and to
`data.json`.
