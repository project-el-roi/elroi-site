# Project El Roi — website

A single static page. No build step, no framework, no server. Three things
live here:

    index.html    the whole site
    data.json     every figure the page displays
    photos/       photographs from the feedings
    vercel.json   security headers Vercel sends with every response

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

`vercel.json` tells Vercel to send a Content Security Policy and a few other
security headers with every page. It only allows the fonts, styles and
scripts the site already uses, so nothing needs to change there when you
edit `data.json` or the photos.

## Updating the figures

Open `data.json` on GitHub, press the pencil icon, change the numbers, and
commit. The site redeploys within a minute.

    "reports"     one entry per day. Written report: date (YYYY-MM-DD),
                  "status":"reported", children, adults, challenges (what
                  the kitchen reported; write "None" if none), and
                  optionally reportedTotal (the total the report itself
                  states, used only to flag a mismatch). A day with no
                  written report but a recalled figure: "status":"estimated"
                  and estimatedTotal. One entry per date.
                  Nothing else is typed: meals served, the daily averages,
                  the date range and the report log are all worked out from
                  this list. Adding a day is one new entry.
    "programmeStarted"  the date feeding began (YYYY-MM-DD).
    "site"        village, parish, municipality.
    "cost"        perMealUgx, dailyUgx, poshoUgx, beansUgx, usdRate.
                  These drive the slider, so keep usdRate roughly current.
    "org"         contactEmail, contactWhatsapp (or contactPhone) and
                  contactNote. The Donate form sends to these: email opens
                  the visitor's mail app, WhatsApp opens wa.me/<number>. Give
                  the WhatsApp number with its country code, for example
                  +256 700 123 456; spaces and the plus sign are ignored.
                  Leave either blank and that send button is switched off,
                  and the page shows a placeholder line instead.
    "updated"     the date shown under the figures. Change it when you
                  change anything else. The report log lists every day up to
                  the day before this date.

If `data.json` is ever malformed, the page quietly falls back to the figures
baked into `index.html` rather than breaking. That is a safety net, not a
second place to edit — always edit `data.json`.

### Meals, not people

The same community is fed every day, so daily counts must never be added up
and shown as people. The headline is **meals served**: the sum of children and
adults over the written reports only. "People fed" is only ever one day, or a
daily average. Estimates are never in the total; they are shown separately.

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

The Our Work page has its own filmstrip at the top, fed by a second list,
`workPhotos`, with the same shape (`src`, `caption`, and an optional `date`),
plus an `alt` that describes what is literally in the photo, for screen readers.
The caption can be thoughtful and general; the alt should stay plain.
Photos there keep their own proportions and scroll sideways; it stays hidden
while the list is empty.

The carousel under the hero stays hidden while that list is empty, and
appears as soon as it has something in it. Photos rotate in the order listed.
The first one dated the same as the most recent written report also shows
the feeding report panel (if none matches, the first photo shows it with a note
of the photo's own date); the others show their own date and caption.
Keep captions to what is visible, plus a date; that is what makes them
credible.

## A note on the photographs

Most of these pictures are of children in a vulnerable moment. Get verbal
consent from parents, through the pastor, for any photograph published here,
and prefer wide shots of the serving line to close portraits of individual
faces. Funders will ask about this eventually, and it is easier to have done
it from the start than to go back.

## The Donate button, and taking payments later

The Donate button opens a message form, not a payment page. The giving
section of `index.html` explains, deliberately, that there is no payment
button yet and what has to exist first: an account the project holds rather
than a person, a second signature on withdrawals, and a published monthly
statement set against the feeding reports. When those exist, change that
section (search `id="give"` in `index.html`) and say the date it changed.
