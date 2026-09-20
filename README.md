# Project El Roi — website

A single static page. No build step, no framework, no server. Three things
live here:

    index.html    the whole site
    data.json     every figure the page displays
    photos/       photographs from the feedings

## Putting it online

1. Create a new repository on GitHub and upload these three items to it
   (keep the folder structure — `data.json` and `photos/` must sit beside
   `index.html`, not inside a subfolder).
2. Go to vercel.com, sign in with GitHub, and choose "Add New — Project".
3. Pick the repository. Vercel will detect a static site; leave every build
   setting untouched and press Deploy.
4. It goes live at a `.vercel.app` address in about a minute. Every future
   push to the repository redeploys it automatically.

To use your own domain, open the project in Vercel, go to Settings then
Domains, and follow the instructions there for pointing the domain's DNS at
Vercel.

## Updating the figures

Open `data.json` on GitHub, press the pencil icon, change the numbers, and
commit. The site redeploys within a minute.

    "feeding"     the most recent feeding report: date (YYYY-MM-DD),
                  children fed, adults fed. The headline adds these two.
    "cumulative"  running totals across every report: meals, reports
    "cost"        perMealUgx, dailyUgx, poshoUgx, beansUgx, usdRate.
                  These drive the slider, so keep usdRate roughly current.
    "org"         contactEmail and contactPhone. Leave either blank and the
                  page shows a placeholder line instead.
    "updated"     the date shown under the figures. Change it when you
                  change anything else.

If `data.json` is ever malformed, the page quietly falls back to the figures
baked into `index.html` rather than breaking. That is a safety net, not a
second place to edit — always edit `data.json`.

## Adding photographs

1. Shrink each photograph before uploading it. Roughly 1400 pixels wide and
   under 300 KB is plenty; anything larger only makes the page slow on the
   phone connections most of your visitors will use.
2. Put the files in `photos/` with plain lowercase names and no spaces, for
   example `feeding-2026-09-16-a.jpg`.
3. Add an entry to the `photos` list in `data.json`:

    "photos": [
      {
        "src": "photos/feeding-2026-09-16-a.jpg",
        "caption": "Serving at the homestead",
        "date": "2026-09-16"
      }
    ]

The gallery section stays hidden while that list is empty, and appears as
soon as it has something in it. Keep captions to a place and a date; that is
what makes them credible.

## A note on the photographs

Most of these pictures are of children in a vulnerable moment. Get verbal
consent from parents, through the pastor, for any photograph published here,
and prefer wide shots of the serving line to close portraits of individual
faces. Funders will ask about this eventually, and it is easier to have done
it from the start than to go back.

## Adding a donate button later

The giving section of `index.html` currently explains, deliberately, that
there is no donate button yet and what has to exist first: an account the
project holds rather than a person, a second signature on withdrawals, and a
published monthly statement set against the feeding reports. When those
exist, replace that section — search `id="give"` in `index.html` — and say
the date it changed.
