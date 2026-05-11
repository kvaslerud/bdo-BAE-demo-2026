# ENDRINGSLOGG v37

## Utgangspunkt og avvik fra spec

Speccen refererer til **`bdo_demo_2026_v2.html`, 8156 linjer**, og en design-token-palette med `--accent: #E30613`. Faktisk utgangspunkt i repo:

| Felt | Spec antar | Faktisk |
|---|---|---|
| Filnavn | `bdo_demo_2026_v2.html` | `bdo_demo_2026_v2 (2).html` |
| Linjeantall | 8156 | 8513 (etter v6 + kannede svar) |
| `--accent` | `#E30613` | `#e81a3b` |
| Em-dash count | 0 (antatt) | 20 (i CANNED_RESPONSES fra forrige sprint) |

**Beslutninger:**

1. **Filnavn:** v37-utdataene lagt i `bdo_demo_2026_v37.html` (ny fil, kopi fra `bdo_demo_2026_v2 (2).html`). Den eksisterende v2-fila er **ikke rørt** per spec ("Ikke endre noe annet i v2").
2. **`--accent` farge:** Beholdt på `#e81a3b` siden spec sier "DESIGN-SYSTEM (LÅST, IKKE ENDRE)". Fargen ble flippet i v6-sprinten på Tobias' egen instruks. Hvis intensjonen er å gå tilbake til `#E30613`, krever det eksplisitt bekreftelse.
3. **20 eksisterende em-dashes:** Fjernet i v37 siden spec sier "Em-dash (—) er forbudt overalt". Alle treff var i CANNED_RESPONSES-strengene i `sendMessage`-fallbackene. Erstattet med `:` (etter bold-titler) eller `,` (inline). Ingen meningsendring.
4. **BCG-referansen:** Ikke vedlagt. Implementeringen fulgte spec uten visuell referanse.

## SPOR 1 · A-seksjons recency (4 endringer)

### A1 (linje 4598, section-dek)
- **Lagt til:** `<span class="recency-stamp">SSB Q1 2026: −0,2 % kvartal, −1,4 % mars YoY.</span>` i slutten av eksisterende section-dek.
- **Source-line oppdatert** (linje 4663): `BAA-2025, BDO. Indekseringer 2019 = 100.` → `BAA-2025, SSB produksjonsindeks Q1 2026. Indekseringer 2019 = 100.`

### A3 (linje 4906, etter .a3-pe-meta)
- **Ny blokk:** `.a3-deal-callout` med "4 mrd", AECOM/Consigli-tekst og rød `recency-stamp.is-accent`-merkelapp ("Markeds-deal · nov 2025").
- **Source-line oppdatert** (linje 4915): `Plattformer er eksempler, ikke uttømmende rangering.` → `Consigli/AECOM-deal: PropTech Connect nov 2025.`
- Hovedtittelens "125" beholdt. Plattform-listen rørt ikke.

### A5 (linje 5071, mini-stats + ny recency)
| Element | Gammel | Ny |
|---|---|---|
| Mini-stat 1 | `2,0x · Konkurser 2024 vs 2020` | `1 104 · Konkurser i byggenæringen 2025` |
| Mini-stat 2 | `20 % · Selskaper i høyrisiko-sjikt` | `5 000 · Forsvunne bedrifter 2023 til 2025` |
| Ny `.a5-recency` | (ny) | `Ferskeste · mai 2026` + Bertelsen og Garpestad-detalj |
| Section-dek | "Konkursene har doblet seg på fire år. Nyetableringene faller. Avstanden mellom dem er halvert siden 2020." | "Konkursene har doblet seg på fire år. 1 104 i byggenæringen i 2025. Nær 5 000 bedrifter forsvunnet på tre år." |
| Source-line | `+ Creditsafe. NACE 41-43.` | `+ Bygghåndverk Norge (jan 2026) + Aftenbladet (mai 2026). NACE 41-43.` |

SVG-graf, path-data og endpoint-typografi rørt ikke (spec: "Rør IKKE SVG-grafens path-data").

### A6 (linje 5119, bolig-driver)
- **Ny blokk** `.driver-recency` rett etter `<p class="driver-text">` om 17–20 000 igangsettinger: `Q1 2026` + "Salg −31 % januar, igangsetting −20 % Q1 mot fjoråret."
- **Source-line oppdatert** (linje 5093): `+ EU-kommisjonen.` → `+ EU-kommisjonen, Boligprodusentene (feb/apr 2026).`

## CSS-tillegg (én ny blokk)

Spec ber om CSS "innenfor eksisterende A3/A5/A6-blokker". For å holde diff-flaten oversiktlig la jeg alle nye selektorer i én samlet blokk merket `/* ═══ v37 RECENCY-STAMP og A-seksjons recency-blokker ═══ */` rett etter `.source-line`-mobile-query (linje 470). Cascade-effekt er identisk. Selektorer er kun nye:

- `.recency-stamp` + `.recency-stamp.is-accent`
- `.a3-deal-callout`, `.a3-deal-callout .a3-deal-num`, `.a3-deal-callout .a3-deal-label`
- `.a5-recency`, `.a5-recency-text`
- `.driver-recency`
- `.i4-frontier-note`

Ingen eksisterende selektorer endret. Ingen nye `--variabler` (var-count uendret: 82 i v2, 82 i v37).

## SPOR 2 · SYSTEM_PROMPT (linje 6133, mellom AI-VERKTØY og CASESTUDIER)

Tre nye seksjoner lagt inn ordrett fra spec:

1. **NORSK 2025-2026 RECENCY** (11 punkter: Volvo/Brønnøy Kalk, Bane NOR x2, Statsbygg x2, Consigli/AECOM, Bertelsen og Garpestad, Bygghåndverk Norge, Boligprodusentene, SSB Q1 2026, NHO mai 2026)
2. **GLOBAL FRONTIER SELEKTIVT** (4 punkter: Trunk Tools/Suffolk, Procore Agent Builder, Meta/Amrize/Mortenson, Pronto/Heidelberg)
3. **STRUKTURELLE SKIFTER** (6 punkter: Brookfield, NBIM, BR25 Danmark, Net-Zero Industry Act, CSRD, owner-operator-skifte)

Resten av SYSTEM_PROMPT (SKRIVESTIL, KRITISKE REGLER, FORMATERING) uendret.

## SPOR 3 · I4 mikro-note (linje 5330)

Lagt til som siste `<li>` i Prosess-AI-cellens `.i4-list`:
```html
<li class="i4-frontier-note">Volvo Brønnøy Kalk · 1M tonn autonomt · norsk drift på globalt frontier-nivå</li>
```

CSS i samlet v37-blokk.

## SPOR 4 · narrativ-arsenal.md

Ny fil opprettet ved siden av v37-html-fila. Innholdet er ordrett fra spec, alle seks våpen.

## Verifisering (alle fem passerer)

```
1. Em-dash (forventet 0):                          0  ✓
2. recency-stamp (forventet ≥4):                   6  ✓
3. CSS-variabler --xxx (v37 vs v2):              82 = 82  ✓ (ingen økning)
4. Consigli/AECOM (forventet ≥2 HTML + ≥1 prompt): 4  ✓
5. SYSTEM_PROMPT seksjoner (forventet 3):          3  ✓
```

Bonus-sjekker:
- CSS-braces balansert (752/752)
- JS-syntaks: `node --check` OK
- Linjeantall: 8513 → 8620 (+107)

## Tall byttet ut (kilde i source-line eller SYSTEM_PROMPT)

| Felt | Gammel | Ny | Kilde |
|---|---|---|---|
| A5 mini-stat 1 | 2,0x | 1 104 | Bygghåndverk Norge (jan 2026) |
| A5 mini-stat 2 | 20 % | 5 000 | Bygghåndverk Norge (jan 2026) |
| A1 recency-stempel | (ny) | −0,2 % / −1,4 % | SSB Q1 2026 produksjonsindeks |
| A3 callout | (ny) | 4 mrd | PropTech Connect nov 2025 |
| A5 recency | (ny) | 3,2 mrd / 451 / 12 | Aftenbladet mai 2026 |
| A6 driver-recency | (ny) | −31 % / −20 % | Boligprodusentene feb/apr 2026 |

## Endringer utenfor scope (flagget, ikke fikset)

1. **`bdo_demo_2026_v2 (2).html`** beholdt em-dashes i CANNED_RESPONSES. Disse er ikke fjernet der per "ikke endre noe annet i v2". Hvis fila skal beholdes som referanse, anbefales at de fjernes der også i en separat sprint.
2. **`--accent` token-verdi** står på `#e81a3b` (v6-flippet) og ikke spec'ens `#E30613`. Beholdt per "ikke endre design-system".
3. **A3 hovedtittelens "125"** rørt ikke per spec, men ny callout introduserer "4 mrd" som risikerer å konkurrere visuelt om Martin's blikk. Bør sjekkes mot BCG-referanse ved hands-on (referansen var ikke vedlagt denne sprinten).

## Leveranse i repo

| Fil | Status |
|---|---|
| `bdo_demo_2026_v37.html` | Ny, 8620 linjer |
| `narrativ-arsenal.md` | Ny |
| `ENDRINGSLOGG_v37.md` | Denne fila |
| `bdo_demo_2026_v2 (2).html` | Urørt |

## BCG-referanse

Ikke vedlagt sprinten. Implementeringen følger v2-design-system uten visuell sammenligning mot BCG-rapport.
