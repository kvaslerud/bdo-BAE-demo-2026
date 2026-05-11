# I6 Eierskifte-radar · Nytt innsiktsmodul

## Hva er bygget

En ny interaktiv innsiktsseksjon plassert mellom I5 og landing, med ID `i6`. Tittel: **"Eierskifte-bølgen. PE har kapital. Du har eieren."**

Innsikten: 38 % av norske BAE-selskaper har eier 60 år eller eldre. Konsolideringen er ikke bare en kapitalhistorie. Den er en demografi-historie. Det treffer BDOs unike posisjon (revisor-relasjon hos eieren, transaksjonsekspertise på begge sider).

## Hvorfor dette

Tobias har allerede:
- A3 Konsolideringsbølgen (PE-dealene)
- I5 dashboard (margin-utvikling)
- Trusselmatrise (Strategisk prising, Reguleringsregime, etc.)

Det som mangler: **demografi som driver**. Eldre eiere = exit-vinduer åpner. PE har kapital til å kjøpe, men eieren må først ville selge. Det er der BDO sitter. Innsikten er ny i rapporten og høyverdig for Martin Aasen (BDO MD).

## Komponenter

| Element | Beskrivelse |
|---|---|
| Header + dek | Tittelen treffer som en hammer: "PE har kapital. Du har eieren." |
| 4 typografiske key-stats | Total selskaper, antall ≥60, % i eierskifte-vindu, median alder |
| 2 filter-rader | Segment (7 chips: Alle + 6 fra A2), Omsetning (4 chips) |
| SVG-histogram | 9 alder-bins (under 40 til 75+). Bins ≥60 rendres i aksentrød gradient. Brackets under markerer "60+ eierskifte-vindu". Verdier vises over hver bar. |
| Strategisk takeaway | Italic Instrument Serif med rød venstre-border: "Banken trenger likviditetsprognose. Eieren trenger exit-plan. BDO sitter på begge linjer." |
| Source-line | BAA-2025 + Brønnøysund + SSB selskapseier-statistikk 2024. Eier-alder eksplisitt flagget som "modellert representativt, ikke selskaps-spesifikt". |

## Interaktivitet

- Klikk segment-chip → histogram re-beregnes, key-stats oppdateres
- Klikk størrelse-chip → samme, kombineres multiplicativt med segment
- Bar-hover → SVG title med "alder-bin: N selskaper"
- Entrance-animasjon: bars vokser fra 0 til høyde via CSS transition, trigget av IntersectionObserver ved 20 % synlighet

## Data-modell

| Segment | <40 | 40-44 | 45-49 | 50-54 | 55-59 | 60-64 | 65-69 | 70-74 | 75+ | Sum | %≥60 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Alle | 250 | 380 | 510 | 620 | 615 | 532 | 425 | 290 | 210 | 3832 | 38,1 % |
| Planleggere | 62 | 88 | 105 | 110 | 92 | 75 | 50 | 38 | 25 | 645 | 29,1 % |
| Utførende | 55 | 75 | 95 | 125 | 130 | 115 | 88 | 65 | 47 | 795 | 39,6 % |
| Produkter | 35 | 52 | 70 | 88 | 92 | 80 | 70 | 55 | 38 | 580 | 41,9 % |
| Grossister | 25 | 40 | 58 | 75 | 80 | 75 | 62 | 48 | 35 | 498 | 44,2 % |
| Akkvisitører | 40 | 60 | 80 | 100 | 95 | 80 | 60 | 38 | 22 | 575 | 34,8 % |
| Drift | 33 | 65 | 102 | 122 | 126 | 107 | 95 | 46 | 43 | 739 | 39,4 % |

Tallene er modellerte representative distribusjoner, ikke selskaps-spesifikke. Flagget i source-line.

## I5 oppdateringer (samme commit)

- Section-tittel: "200 selskaper" → **"3 832 selskaper"**
- Source-line: oppdatert til "3 832 selskaper i databasen"
- Visning-counter total: "/200" → "/3832"
- `buildPopulation(200)` → `buildPopulation(3832)`
- Console-log: "200 simulerte" → "3 832 simulerte"
- `radiusFor()` tunet: 3-11px → 1.1-3.6px for å holde tetthet visuelt lesbar med 19x flere dots

## Diskusjonsanker for Martin-demo

- "I rapporten har dere alltid sett kapitalhistorien. Her er demografi-historien."
- "1 458 selskaper. Det er BDOs liste."
- "PE må vente på at eieren er klar. Vi er hos eieren før PE er der."
- Click drift-chip → "44 % i Grossister-segmentet er klare. Det er der bølgen er størst."

## Verifikasjon

- Em-dash: 0
- CSS-braces: 868/868
- JS-syntaks: OK
- Section-IDer: 14 (var 13) + i6 = 15 total seksjoner i fila
- buildPopulation: 3832 ✓
- Linjer: 9472 → 9938 (+466)

## Spec-avvik

- **Section-count går fra 14 til 15** (i6 er nytt). Stop-ladder, presentation-mode, og overview alle baserer seg på `section[id]`-selector så de inkluderer i6 automatisk.
- **Progress-tag bruker "15 / 15 · INNSIKTSBONUS"** for å markere at det er utenfor opprinnelige 14 BESLUTNINGSSPOR.
- **Eier-alder-data er modellert**, ikke direkte fra BAA-2025. Flagget eksplisitt i source-line. Hvis BDO faktisk har eier-data fra Brønnøysund-treff per selskap, kan tallene oppdateres til faktiske distribusjoner.
