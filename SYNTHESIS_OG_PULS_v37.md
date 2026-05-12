# v37 sluttspurt · Synthesis, Slide-mode, Bransje-pulsen

## Hva som ble bygget mens du var ute

Tre store endringer, fullført i én sesjon med push-til-GitHub etter hver fase. Alt på `claude/analyze-bdo-html-gYFUj`.

### Phase 1: Synthesis-pilar (klimakset)

Plassert mellom I7 (Bransje-pulsen, ny) og Landing.

**Layout:**
- Full viewport-høyde (min-height: 100vh, vertikalt sentrert)
- 92px italic Instrument Serif display-tittel: "Fire tall. Én bransje. **BDOs marked.**"
- 4 stat-celler i grid (4 kolonner), hver med:
  - 96px italic stat-tall med aksentrød på det dramatiske
  - 14px label (kort fakta-tekst)
  - 19px italic strategisk implikasjon med rød BDO-position
- Avsluttende linje med høyre-justert serif italic: *"Fire tall. Én bransje. Ett rådgivermandat."*

**Innhold (de fire tallene som binder rapporten sammen):**
| Tall | Fakta | BDO-posisjon |
|---|---|---|
| **3,3 %** | Bransjens driftsmargin 2024, laveste på fem år | BDO rådgir på prising |
| **408** | Transaksjoner i Norden 2025, all-time high | BDO sitter på begge sider |
| **1 458** | Selskaper med eier 60 år eller eldre | BDO har relasjonen |
| **−13 %** | Produktivitet bygg/anlegg siden 2000 | AI starter nå, hos oss |

**Reveal-animasjon:** Hver celle har staggered entrance via IntersectionObserver (0/120/240/360ms forsinkelse). Rød hairline-streket vokser fra 0 til 28 % bredde over toppen av hver celle når den blir synlig.

### Phase 2: Slide-mode (scroll-snap som default)

Aktiveres automatisk 600ms etter sidelast (gir tid til init-animasjoner). Body får class `slide-mode`.

**Implementasjon:**
- `scroll-snap-type: y proximity` (soft snap — tillater fri scroll, antyder slide-snap)
- Korte seksjoner: `scroll-snap-align: start` (hero, A1-A6, I1, I3, I4, Synthesis, Landing)
- Tall seksjoner opt-out: `scroll-snap-align: none` (TOC, I2 chat, I5 dashboard, I6 radar, Trusselmatrise — har egen scroll-mengde)
- Sub-elementer i ikke-aktiv seksjon dimmes til 0.45 opacity for fokus
- Scroll-progress-bar (1px rød) øverst på skjermen viser hvor i rapporten du er
- Smooth scroll-behavior aktivt globalt

**Tastatur-shortcuts fungerer (Presentasjonskontroll-modulen):**
- Piltaster / PageUp / PageDown: forrige/neste seksjon
- Home / End: første/siste
- M: oversiktsmodus (alle seksjoner som tiles)
- F: fokus-modus
- ?: hjelp

`prefers-reduced-motion`: slide-mode deaktiveres automatisk (faller tilbake til normal scroll).

### Phase 3: Bransje-pulsen (I7 — ny state-of-the-art innsiktsmodul)

Plassert mellom I6 (Eierskifte-radar) og Synthesis-pilar.

**Innsikt:** Animert timeline 2020 til Q1 2026 (25 kvartaler) med tre kanaler synkronisert i tid:
- **Konkurser** (rød linje, stiger fra 150 til 315 i Q1 2024)
- **Etableringer** (grå linje, faller fra 290 til 210)
- **Oppkjøp** (oransje bars, tredobles fra 22 til 66+)

**Aha-moment:** Konkurslinjen krysser etableringslinjen i Q1 2023. Annotering på SVG markerer dette punktet med rød stiplet vertikal linje + "KRYSS · Q1-23"-label.

**Auto-play:** Starter automatisk når seksjonen kommer 40 % i syne. 220ms per kvartal på 1× speed (5,5 sek total). Brukeren kan:
- Pause / Spille av (Spill-knapp med SVG-trekant)
- Tilbake til start
- Hastighet: 1× / 2× / 4×

**Live key-stats over chart:** 4 typografiske tall som oppdateres mens animasjonen kjører:
- Konkurser dette kvartalet (aksentrød)
- Etableringer dette kvartalet
- Oppkjøp dette kvartalet
- Aktivt kvartal (JetBrains Mono 30px, f.eks. "Q3-23")

**Strategisk takeaway:** "Konkurslinja krysser etableringslinja andre kvartal 2023. Oppkjøp-pulsen tredobles fra start til slutt. Vi går ikke gjennom en konjunktur. Vi går gjennom en strukturell utvasking."

### Bonus-polish (mine egne tillegg)

- **TOC-headline oppdatert:** "Tretten seksjoner" → "Seksjoner som *lever*. Mini-previews aktive." (fjernet faktisk feil count)
- **Stop-ladder utvidet fra XIV til XVIII:** Lagt til IX (Trusselmatrise), XV (I6 Eierskifte), XVI (I7 Bransje-pulsen), XVII (Synthesis). Numrene er romerske og hopper konsistent.
- **Scroll-progress bar:** Slim rød linje (2px) øverst på viewport, glir fra 0 til 100 % mens du scroller. Subtilt glow-effekt (rgba accent shadow).
- **Console-melding oppdatert:** "17 seksjoner aktive" i finale-melding.

## Total endring i v37

| Felt | Før | Etter |
|---|---|---|
| Linjer | 9 938 | **10 836** (+898) |
| Seksjoner med id | 14 | **18** |
| Stop-ladder items | 14 | **18** |
| CSS-braces | 868/868 | **960/960** |
| JS IIFE-er | 9 | **10** |
| Em-dash | 0 | **0** |
| JS-syntaks | OK | **OK** |

## Sluttbruk-flyt (for Tobias-demo)

1. **Åpne fila lokalt** → slide-mode aktiveres 0.6 sek etter load
2. **Scroll naturlig** → seksjoner snapper softt på plass (proximity-mode tillater fri scroll)
3. **Eller bruk piltaster** → smooth 600ms-scroll mellom seksjoner
4. **Press M** → oversiktsmodus med alle 18 seksjoner som tiles
5. **På Bransje-pulsen** → kommer i syne, starter auto-play, 5.5 sek senere er hele 2020-2026 fortalt
6. **På Synthesis-pilar** → 4 stat-celler reveal med stagger, rød hairline glir over toppen av hver. Closing-linje "Fire tall. Én bransje. Ett rådgivermandat."

## Filer

| Fil | Status |
|---|---|
| `bdo_demo_2026_v37.html` | Endret (+898 linjer) |
| `SYNTHESIS_OG_PULS_v37.md` | Ny (denne fila) |
| Resten urørt | |

## Hva du sannsynligvis vil ha tilbake

Du kan komme tilbake og si "fjern X" eller "endre Y". Sannsynlige justeringer:
- Synthesis-pilar font-størrelse hvis 92px føles for stort på din skjerm
- Bransje-pulsen speed (default 220ms/kvartal) hvis for tregt/raskt
- Slide-mode opt-out for seksjoner som lugger
- Tall i Synthesis hvis du har bedre/oppdaterte
- Stop-ladder romerske tall til arabiske hvis det leses lettere

Alt er reversibelt med små edits.
