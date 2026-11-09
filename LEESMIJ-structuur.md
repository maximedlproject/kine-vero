# Structuur van deze map

Cloudflare Workers serveert **alleen** wat in `public/` staat. Dat is bewust:
alles in de root blijft privé, ook `wrangler.jsonc` zelf.

```
kine-vero-main/
├─ wrangler.jsonc          <- config, NIET publiek
├─ LEESMIJ-structuur.md    <- dit bestand, NIET publiek
└─ public/                 <- alles hierin is wel publiek
   ├─ index.html
   ├─ robots.txt
   ├─ sitemap.xml
   ├─ favicon.svg
   ├─ support.js
   ├─ image-slot.js
   ├─ .image-slots.state.json
   └─ assets/
      ├─ veronique-profielfoto.jpg        <- 285 KB, enkel voor og:image
      └─ veronique-profielfoto-450.webp   <- 36 KB, wat de site toont
```

## Let op bij een nieuwe export uit de Design-editor

Een export dropt bestanden in de **root**, niet in `public/`. Doe daarna:

1. Verplaats de geexporteerde bestanden naar `public/`.
2. Zet de SEO-blok in `<head>` terug (title, meta description, canonical,
   Open Graph, JSON-LD) - een export bevat die niet.
3. Zet `lang="nl-BE"` terug op de `<html>`-tag.
4. Controleer dat `<image-slot>` naar de webp wijst, niet naar de jpg.
5. Controleer dat de telefoonlinks `tel:+32478516265` gebruiken.
6. **Privacy:** verwijder de Google Fonts-regels (`fonts.googleapis.com`,
   `fonts.gstatic.com`) uit `<helmet>`/`<head>`. De lettertypes staan lokaal in
   `public/assets/fonts/` en worden geladen via `/assets/fonts/fonts.css`.
7. **Privacy:** zet het Google Maps-`<iframe>` in de contactsectie niet terug.
   Daar staat een statische kaart (`assets/kaart-kortrijk.webp`, OpenStreetMap)
   met bronvermelding, die bij een klik Google Maps opent.

8. **Privacy:** als een export een nieuwe `support.js` meebrengt, zet daarin
   `REACT_URL`, `REACT_DOM_URL` en `BABEL_URL` terug naar de lokale kopieën in
   `/assets/vendor/` (de SRI-hashes mogen blijven staan). Verandert de versie,
   download dan die nieuwe versie naar `assets/vendor/`.

Controle: zoek in `public/` op `googleapis`, `gstatic`, `output=embed` en `unpkg`.
Je mag geen resultaten krijgen.

Laat `wrangler.jsonc` op `"directory": "./public"` staan.

## Deployen

```
wrangler deploy
```

Uitvoeren vanuit deze map, niet vanuit `public/`.

## Nog open

- `openingHoursSpecification` in de JSON-LD van `public/index.html`
  wacht op de echte openingsuren.
- Er is nog geen `404.html`. Wil je die, zet hem in `public/` en voeg
  `"not_found_handling": "404-page"` toe aan het assets-blok in `wrangler.jsonc`.
