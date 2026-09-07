# Ellen's Salon

A single-page site for a braiding and hair salon on Dune Route, Richards Bay,
KwaZulu-Natal, operating out of a converted shipping container on the grounds of
Xaba Guest Lodge.

Static HTML and CSS, plus about 30 lines of inline JavaScript for the scroll
reveals. No framework, no build step, no dependencies. Open
`index.html` in a browser, or serve the folder with any static host.

## Business details

These are the facts the page states. Nothing else about the business is invented.

| | |
|---|---|
| Address | Dune Route, Richards Bay – New, Richards Bay, 3900 (at Xaba Guest Lodge) |
| Phone | 063 386 8838 (`tel:+27633868838`) |
| Hours | Open daily, from morning until 7:30 pm |
| Rating | 5.0 on Google |

The opening time is deliberately written as "from morning" — the exact hour is
not known. If you find out what it is, update it in three places: the hero
`<dl class="facts">`, the Hours paragraph in "Finding us", and the footer.

## Design decisions

The palette is taken off the building rather than from a salon template: a
red-oxide container standing on sand, hand-painted white lettering, deep shadow.

| token | hex | what it is |
|---|---|---|
| `--oxide` | `#93291E` | the container's red-oxide paint |
| `--oxide-deep` | `#5C1811` | its shaded ribs; the contact band |
| `--paint` | `#F7F4EE` | the hand-painted white of the sign |
| `--sand` | `#E4DED0` | the ground it stands on; page background |
| `--ink` | `#241A16` | body text |
| `--zinc` | `#5F5B54` | weathered metal; secondary text |
| `--sea` | `#5B7C85` | one cool coastal note, hairlines only — never text |

Type is **Archivo Black** for display and **Karla** for body text. The hero sets
the wordmark — `ellen's` over `SALON` — as one painted lockup. Its hand-painted
quality comes from per-letter baseline offsets and rotations plus an SVG
turbulence filter (`#brush`), not from a script typeface: a sign painter uses a
plain bold letterform and an unsteady hand.

Everything is hard left-aligned. The hero panel and every section below share one
`--wrap` width and one `--pad`, so the left edge is continuous down the page.

The one motif is the cornrow-parting mark (`#cornrow`) used twice, as a section
divider. It is a `<pattern>` with `patternUnits="userSpaceOnUse"` on an SVG with
no `viewBox`, so one tile is always 240×46 real pixels — the mark reads at the
same scale on a phone as on a desktop.

Motion is in two tiers and both follow the same idea — things arrive the way
paint does, wiped on from the left. The hero lettering paints itself on at load.
Below it, a section entering view plays one short sequence: its heading and
parting mark wipe in from the left, then its content rises 8px into place on a
70ms stagger. Which tier an element belongs to is declared in the markup with
`data-reveal="paint"` or `data-reveal="rise"`.

Three things keep that from getting in the way. The hidden state hangs off
`:not([data-reveal-in])` rather than a competing "revealed" rule, so the two
states never race on specificity. It is armed by an inline script in the
`<head>` before first paint, and only when JavaScript is available and motion is
not reduced — so with no JS, or under `prefers-reduced-motion`, every element
simply keeps its normal visible state and nothing animates at all. And whatever
is already on screen at load is shown outright rather than revealed, so the
opening frame is complete and the reveals only ever apply to content you scroll
down to.

## Languages

The page opens in English with an isiZulu toggle at the top of the hero. Most
people walking into a salon in Richards Bay speak isiZulu at home, so it is a
toggle rather than a menu: both languages sit on screen, and the current one is
underlined in sign-paint white.

Each translated string lives on the element itself as a `data-zu` attribute,
next to the English it replaces, so a correction never means hunting through a
separate dictionary. The English is stashed into `data-en` at load, and
switching assigns `textContent` — no markup is ever rebuilt from a string, so
every element carrying a translation is a plain text leaf. That is why the
`<strong>` came off "Xaba Guest Lodge": the isiZulu locative prefix binds onto
the name itself (`egcekeni laseXaba Guest Lodge`), so the name cannot be split
out of the sentence the way it can in English.

Switching also sets `lang` on the root and on each swapped element, updates the
`<title>`, and stores the choice in `localStorage` so it survives a reload.
The wordmark, the phone number and the street address stay as they are.

**The isiZulu has not been checked by a native speaker.** It was written to be
plain and direct rather than formal, and it keeps the style names people
actually use in KZN (`cornrows`, `box braids`) instead of translating them.
Before this goes in front of customers, someone who speaks isiZulu should read
it — particularly the service descriptions, where the noun-class agreements are
the easiest thing to get wrong. Corrections go in the `data-zu` attributes in
`index.html` and nowhere else.

## Fundamentals

- Mobile-first; checked for horizontal overflow from 320px to 1920px.
- Semantic HTML, one `h1`, clean heading order, skip link.
- Visible focus rings that switch colour over red panels.
- All text meets WCAG AA contrast (measured on the rendered page; lowest is
  4.6:1 on the small `Hours`/`Rating`/`Where` labels).
- `LocalBusiness` (`HairSalon`) JSON-LD, limited to facts that are known.
- About 63 KB in four requests, no third-party requests, no dependencies.

## Fonts

Archivo Black and Karla are bundled in `fonts/` (latin subsets, woff2) rather
than loaded from Google Fonts. That removes a third-party round trip on a slow
mobile connection and means the page never renders in a fallback face. Both are
licensed under the SIL Open Font License 1.1 — see `fonts/OFL.txt`.

## Adding WhatsApp

If the salon's number is on WhatsApp, there is a commented-out link in
`index.html` next to the hero buttons that can be uncommented. It was left off
because we could not confirm the number is registered.
