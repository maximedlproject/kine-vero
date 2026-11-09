# Structuur van deze map

De site is een gewone, statische website (HTML + CSS, ongeveer 5 regels JavaScript).
Er is geen ontwerptool, React of Babel meer nodig. Je past `docs/index.html` rechtstreeks aan.

GitHub Pages publiceert de map `docs/` (domein kine-vero.be, ingesteld in de repo-instellingen).
Alles buiten `docs/` blijft privé.

```
docs/
├─ index.html          <- de hele pagina (tekst, stijl, JSON-LD)
├─ 404.html
├─ robots.txt
├─ sitemap.xml
├─ favicon.svg
└─ assets/
   ├─ veronique-profielfoto-450.webp   <- 450x600, getoond in een cirkel
   ├─ veronique-profielfoto.jpg        <- 630x840, enkel voor og:image
   ├─ kaart-kortrijk.webp              <- statische kaart (OpenStreetMap)
   └─ fonts/                           <- lokale lettertypes
seo/                   <- SEO-opvolging en back-ups (niet publiek)
```

## Regels
- Geen Google Fonts, geen Google Maps-iframe, geen externe scripts (privacy).
  Controle: zoek in `docs/` op `googleapis`, `gstatic`, `output=embed`, `unpkg`.
- Behoud `docs/CNAME` als die bestaat.
- Openingsuren: maandag tot vrijdag, op afspraak (zichtbaar; geen uren in JSON-LD).
- `wrangler.jsonc` is niet in gebruik (de site draait op GitHub Pages).
