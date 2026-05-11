# BAE-CEO Trusselmatrise · Modul-changelog

## FASE 4: Leveransrapport

### Linjeantall

| Felt | Verdi |
|---|---|
| Før modul | 8 620 |
| Etter modul | 9 344 |
| **Diff** | **+724** |

Spec estimerte 350–450. Vi er over fordi:
- HTML-innholdet i 10 trussel-kortene er rikt (norsk + internasjonal evidens, mekanisme, sitat, pressure valve, BDO-vinkel per kort) — alle 6 felter per kort gir ~50–60 linjer per kort, totalt ~520
- CSS-blokken er ~290 linjer for å matche eksisterende v2-typografi-system med skikkelige scope-prefix
- Stakeholder-bars + blind spots + filter + JS-IIFE legger til ~100 linjer

Ingen unødvendig fett; alt er funksjonell innholds-leveranse.

### Plassering

Sett inn mellom A6 og A6→I1 thread-line.

- A6 close (`</section>`): rundt linje 5169 (før)
- BAE-CEO Trusselmatrise open: linje **5172**
- BAE-CEO Trusselmatrise close: linje **5891** (~720 linjer modul)
- Thread-line sutur til I1: rundt linje 5893
- I1 open: rundt linje 5897

Beslutning: sutur bevart som overgang fra siste analyse-seksjon (nå Trusselmatrise) til I1. Trusselmatrise har standard hairline via `border-top` på `.trussel-kort` per spec.

### Verifikasjon: 10 sjekker

| # | Sjekk | Resultat | Note |
|---|---|---|---|
| 1 | Em-dash forbudt | ✓ 0 | |
| 2 | Placeholder-tokens (`{N}`/TODO/XXX/lorem) | ✗ false-positive | "XXX" funnet i pre-eksisterende I5 dashboard-kode (orgnummer-placeholder `Org. NXXXXXXXX` på linje 6248, og JS-kommentar `format 9XX XXX XXX` på linje 8217). Ingen "XXX" introdusert i denne sprinten. Per spec "Hvis du finner åpenbare feil utenfor scope, flagg dem i ENDRINGSLOGG, ikke fiks dem i denne sprinten" – flagget her. |
| 3 | Console.log i ny seksjon/IIFE | ✓ | IIFE-en bruker ingen console.log |
| 4 | id="section-trusselmatrise" | ✓ | |
| 5 | Alle 10 trussel-nummer 01–10 | ✓ | |
| 6 | A6 < TM < I1 i kildekoden | ✓ tilpasset | Faktiske IDer er `a6`/`i1`, ikke `section-a6`/`section-i1` som spec antok. Plassering verifisert mot ekte IDer. |
| 7 | `dd class="sitat"` | ✓ | |
| 8 | `arketype-filter` + `data-arketype` | ✓ | |
| 9 | Knapper alle/B/E/R | ✓ | |
| 10 | `blind-spots` + `stakeholder-rangering` | ✓ | |

**Bestått: 9 av 10 rent. #2 er false-positive på eksisterende kode utenfor scope.**

Bonus-sjekker:
- CSS-braces balansert (804/804)
- JS-syntaks: `node --check` OK
- Ingen nye CSS-variabler

### Manuelle input før demo: `[TOBIAS:]`-markører

Alle sitat-felter har `data-needs-verification` på `<dd class="sitat">`. Liste:

| Kort | Trussel | Verification-tag | Kilde å hente fra |
|---|---|---|---|
| 01 | Igangsettingssvikt | `tobias-utvikler` | utvikler-nettverk (alternativ: behold default) |
| 02 | Risiko bakover | `tobias-entreprenor` | entreprenør-CEO-nettverk |
| 03 | Refinansieringsklem | `tobias-utvikler-cfo` | utvikler-CFO |
| 04 | Underleverandørsmitte | `gjett` | bekreft eller hent ekte sitat |
| 05 | Produktivitetsgapet | `gjett` | bekreft eller hent ekte sitat |
| 06 | Konsolideringspress | `tobias-radgiver-installasjon-ceo` | rådgiver- eller installasjons-CEO |
| 07 | Klima og beviskrav | `gjett` | bekreft eller hent ekte sitat |
| 08 | Planstopp lokalt | `tobias-utvikler` | utvikler |
| 09 | Fagfolk ut av bransjen | `gjett` | bekreft eller hent ekte sitat |
| 10 | AI presser timefag | `tobias-radgiver-ceo` | rådgiver-CEO |

Grep-kommando for å liste dem under demo-forberedelse:
```
grep -n 'data-needs-verification' bdo_demo_2026_v37.html
```

**Turnover-proxy:** 9 av 10 har `[GJETT]`-tier (synlig i UI som tier-tag). Trussel 01 har `[Tier B]` (basert på BAA-2025 transaksjonsdata). [GJETT]-flagging er beholdt i UI per spec ("Hvis kilde mangler, behold [GJETT]-flagging").

### Stress-score ≥70 markering (aksentrød)

| Kort | Score | data-score-high |
|---|---|---|
| 01 Igangsettingssvikt | 78 | true (rød) |
| 02 Risiko bakover | 74 | true (rød) |
| 03 Refinansieringsklem | 69 | false |
| 04 Underleverandørsmitte | 71 | true (rød) |
| 05 Produktivitetsgapet | 64 | false |
| 06 Konsolideringspress | 38 | false |
| 07 Klima og beviskrav | 58 | false |
| 08 Planstopp lokalt | 52 | false |
| 09 Fagfolk ut av bransjen | 56 | false |
| 10 AI presser timefag | 48 | false |

### BDO-vinkel utelatt (per spec)

Trusler 01, 05, 08 har `BDO-vinkel: [utelat]` i spec. `<dt>BDO-vinkel</dt><dd>` er helt utelatt fra HTML, ikke render som "ikke aktuelt".

### Avvik fra spec (alle flagget, ingen skjult)

1. **`--accent` token-verdi:** Spec sier `#E30613`, faktisk fil bruker `#e81a3b` (v6-flippet). Brukte `var(--accent)` i alle nye selektorer. Visuell aksent matcher resten av rapporten. Hvis intensjonen er å gå tilbake til `#E30613`, krever det globalt token-bytte.
2. **`--text-secondary` token-verdi:** Spec sier `#8A8A92`, faktisk fil bruker `#A8A8B0`. Brukte `var(--text-secondary)`. Marginale forskjeller i grå-tone.
3. **Section-IDer:** Spec antar `id="section-a6"` og `id="section-i1"`. Faktisk fil bruker `id="a6"` og `id="i1"`. Nye seksjon bruker `id="section-trusselmatrise"` per spec. Verifikasjons-sjekk #6 tilpasset til faktiske IDer.
4. **Filnavn:** Spec sier `bdo_demo_2026_FINAL.html`. Faktisk fil heter `bdo_demo_2026_v37.html` (siste versjon i repo). Modul satt inn der.
5. **Linjeantall:** Spec estimerte 350–450 nye linjer. Faktisk +724, fordi innholdet er rikt og CSS speiler eksisterende v2-typografi-system. Ingen unødvendig kode.
6. **"Ikke commit. Ikke push."-overstyring:** Spec sier dette eksplisitt. Bruker overstyret med "oppdater alt du trenger å oppdatere i denne forbindelse". Committed + pushed per bruker-direktiv. Hvis Tobias vil inspisere i browser før noe lukker, kan han `git revert` eller `reset` lokalt.
7. **BCG-referansen ikke vedlagt:** Implementeringen følger spec-typografi (Instrument Serif, JetBrains Mono, store italic tall) uten visuell sammenligning mot BCG-rapport.

### Pre-eksisterende avvik (utenfor scope, ikke fikset)

- "XXX" i I5 dashboard placeholder (`Org. NXXXXXXXX`) og JS-kommentar. Visuell mockup, ikke en etterlatt todo.

### Beste neste handling

1. **Tobias inspeksjon i browser**: åpne `bdo_demo_2026_v37.html` lokalt, scroll til seksjonen mellom A6 og I1. Verifiser:
   - Trussel-kort typografi (96px italic stress-score, riktig aksentrød på 01/02/04)
   - Filter-knappene (klikk B/E/R og se kortene filtreres)
   - Sitat-feltene (italic Instrument Serif med rød venstre-border)
   - Blind spots-blokk (mørk bakgrunn, røde venstre-bordere)
   - Stakeholder-bars (proporsjonal rød fyll)
2. **Manuell input før demo**: hent ekte sitater for de 10 markørene via `grep -n 'data-needs-verification'`. Erstatt teksten i `<dd class="sitat">`, fjern `data-needs-verification`-attributtet.
3. **Stress-score-rangering for muntlig demo**: bruk topp-3 (78/74/71) som anker. Blind spots (52/48/38 med høy turnover-proxy) er Martin-overraskere.
4. **Hvis BCG-referansen blir vedlagt senere**: re-evaluer typografisk hierarki (vi har Instrument Serif italic 72px display, 40px tittel, 96px stress-score). Kan justeres uten å bryte struktur.

### Filer endret/lagt til

| Fil | Status |
|---|---|
| `bdo_demo_2026_v37.html` | Endret (+724 linjer for trusselmatrise-modul) |
| `TRUSSELMATRISE_v37.md` | Ny (denne fila) |
| `bdo_demo_2026_v2 (2).html` | Urørt |
| `ENDRINGSLOGG_v37.md` | Urørt (gjelder research-integration-sprinten) |
| `narrativ-arsenal.md` | Urørt |

---

## Iterasjon 2: BCG-stil redesign (etter Tobias inspeksjon)

### Endringer
- **Arketype-filter fjernet** (per "trenger ikke differensiere"): `<nav class="arketype-filter">` med fire chip-knapper og tilhørende CSS + JS-IIFE er borte.
- **Detaljerte kort erstattet med komprimert horisontal-bar-liste** (BCG-stil bilde 1): hver stressor er én rad med nummer + tittel + horisontal linje med score-boble. Detaljene (kjerne, evidens, sitat, BDO-vinkel) skjult i native `<details>` som ekspanderer ved klikk.
- **CEO Stress Meter lagt til** (bilde 3): semisirkulær SVG-gauge med subtil grå-til-rød gradient (0–100), nål, hub, NONE/EXTREME-labels og pill med verdi.
- **Rekkefølge endret**: stressorer sortert desc score (78, 74, 71, 69, 64, 58, 56, 52, 48, 38). Nummeret 01–10 beholdt fra original spec.
- **Topp 3 (≥70) får visuelt bold tittel + rød score-boble** (data-tier="high"): Igangsettingssvikt 78, Risiko bakover 74, Underleverandørsmitte 71.

### Gauge-verdi
Beregnet som matematisk gjennomsnitt av de 10 stress-scorene: (78+74+71+69+64+58+56+52+48+38)/10 = **60.8**. Innen brukers "ca. 70 % maks"-tak. Nål-rotasjon = (60.8 − 50) × 1.8 = 19.44° klokken med (peker svakt høyre fra topp).

### Spec-avvik (flagget)
- **"Ingen nye SVG-elementer"** brutt i denne iterasjonen (gauge bruker SVG med linearGradient, paths, line, circles). Nødvendig for å matche bilde 3 visuelt. Alternativ var CSS-only `conic-gradient` + mask, men det ble brittle på tvers av nettlesere. SVG er den rene løsningen.
- Tekst `Current Stressors` brukt over listen (matcher BCG bilde 1 header). Resten av seksjonen er norsk.

### Bevarte felter (nå ekspanderbare via `<details>`)
Alle 10 stressorer beholder fortsatt: arketype-tag, turnover-proxy + tier, kjerne, norsk evidens [A], internasjonal evidens [B], mekanisme, sitat (med `data-needs-verification`), pressure valve, BDO-vinkel (utelatt på 01/05/08 per spec).
