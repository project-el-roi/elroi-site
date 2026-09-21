# Project El Roi — site context

A single static page for a Ugandan-led hunger response in Logoole Village,
Kotido Rural Parish, Kotido Municipality, Karamoja. Hosted on Vercel from
this repo. Slogan: "God sees. We act."

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
cream background `#F8F5ED`, paper `#FFFDF8`, ink `#18251D`, forest green
`#123B29` (`--forest`, the impact card and footer), leaf green `#1F6B47`
(`--green`, text accents and links), rust `#B9431F` (`--rust`, and `--cta`
for the Donate button), muted gold `#D49A2D` (`--gold`, icon tints only).
Dark mode is a deep green-black. The design brief is `design.md` (kept out of
the repo); the visual reference is the mockup it names.

The accents carry a rule: **rust is action, green is information and
outcome.** Rust marks what the project or a donor does: the Donate button,
the "The work", "What a gift buys" and "Get involved" labels, running items
on the map. Green marks explanation and result: the "Why now", "How it
connects", "About" and "Reports" labels, body links, the meal count in the
slider. Gold is decoration only, never text. Keep new elements consistent
with that split rather than adding another accent.

Type is Source Serif 4 for headlines and figures, Archivo for body and UI.
Small uppercase labels (eyebrows, kickers) are part of the design; headlines
are sentence case. The slogan is written "God sees. We act." everywhere.

The homepage is one file with two views, switched by the URL hash: the main
page, and "Our Work" (`#work`, with `#map` inside it), which holds the work
list and the interconnection map. Every header link is an anchor on the main
page except Our Work. The carousel below the hero is built from the `photos`
list in `data.json`; the first photo dated the same as `feeding.date` gets the
latest-feeding-report panel, the rest show their own date and caption only.

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
rust — something the project is already doing) or `planned`.

## Things that are deliberately absent

There is **no payment button.** The Donate button in the header (and in the
Get involved section) opens a form that builds a message and hands it to the
visitor's own email or WhatsApp app, addressed to the details in `data.json`;
nothing is sent from the page and no payment is taken. The Get involved
section explains that money currently moves as mobile money to the pastor,
that there is no registered account, independent bookkeeping or audited
trail, and that a payment button before those exist would be asking for
unearned trust. It then names the three things being built first. Do not add
a payment widget until the user says those exist, and when the section
changes, say the date it changed (last changed 20 September 2026, when the
Donate button was added).

Seven of the nine initiatives are listed as "Not started" and most say "Not
yet costed". That honesty is the point, not an omission to fill in.

## Photographs

Shrink to ~1400px wide and strip EXIF before committing — phone photos carry
GPS coordinates, and this repo is public and permanent:

    mogrify -strip -resize 1400x -quality 78 photos/*.jpg

Captions carry place and date only. No beneficiary names, no children's
names, no phone numbers. The same applies to commit messages and to
`data.json`.
