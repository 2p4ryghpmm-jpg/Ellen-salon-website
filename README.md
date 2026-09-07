# Ellen's Hair Salon

A single-page site for a braiding and hair salon on Dune Route, Richards Bay,
KwaZulu-Natal, operating out of a converted shipping container on the grounds of
Xaba Guest Lodge.

Static HTML and CSS. No framework, no build step, no JavaScript. Open
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

The one motion moment on the page is the hero lettering painting itself on at
load. Nothing else animates, and that is disabled under `prefers-reduced-motion`.

## Fundamentals

- Mobile-first; checked for horizontal overflow from 320px to 1920px.
- Semantic HTML, one `h1`, clean heading order, skip link.
- Visible focus rings that switch colour over red panels.
- All text meets WCAG AA contrast (measured on the rendered page; lowest is
  4.6:1 on the small `Hours`/`Rating`/`Where` labels).
- `LocalBusiness` (`HairSalon`) JSON-LD, limited to facts that are known.
- About 59 KB in four requests, no JavaScript and no third-party requests.

## Fonts

Archivo Black and Karla are bundled in `fonts/` (latin subsets, woff2) rather
than loaded from Google Fonts. That removes a third-party round trip on a slow
mobile connection and means the page never renders in a fallback face. Both are
licensed under the SIL Open Font License 1.1 — see `fonts/OFL.txt`.

## Adding WhatsApp

If the salon's number is on WhatsApp, there is a commented-out link in
`index.html` next to the hero buttons that can be uncommented. It was left off
because we could not confirm the number is registered.
