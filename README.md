# jonathanfribert.github.io — portfolio-forside

Forsiden på https://jonathanfribert.github.io/ i "Morgenavisen"-identiteten:
avisforside med nameplate, udgavelinje, dobbeltstreg og projektcases som
historier. Én selvstændig HTML-fil, ingen build-trin.

Projektcasen om nyhedsmonitoren bor i sit EGET repo
(`JonathanFribert/nyhedsmonitor-case`, serveres på `/nyhedsmonitor-case/`).
Denne forside linker derover; design-tokens (palet, skrifter, dobbeltstreg,
stempel) er kopieret derfra og skal holdes i familie ved ændringer.

## Engelsk udgave (en.html)

`en.html` er et 1:1-spejl af `index.html` på engelsk (samme CSS/JS, kun tekst,
lang-attributter, canonical/og-metas og linkmål er oversat). VED ENHVER ÆNDRING
i index.html skal en.html have samme ændring — samme regel som på casen.
Sprogskiftet er `.language-switch`-linket i topbarens `head-actions` (EN på
dansk side, DA på engelsk). Den engelske side linker til casens `en.html` som
primær knap og har eget delekort `og-image-en.png` (regenerér fra
`og-template-en.html` med headless Chrome, når indholdet ændrer sig).
Terminologi følger casens engelske udgave ("the Danish Prime Minister's
Office", "real operational data"). hreflang-blokken (da/en/x-default) er ens i
begge filer, og sitemap.xml fører begge URL'er med alternates.

## Case 03: Blaze It Up Radio Africa-appen (blazeitupradio-case/)

Casen om musikplatformen for Blaze It Up Radio Africa / 9thwunder ligger som
undermappe i DETTE repo (`blazeitupradio-case/index.html` + `en.html` + egen
`sitemap.xml`) og serveres på `/blazeitupradio-case/`, altså samme URL-mønster som
de to andre cases, der bor i egne repos. Den kan flyttes til et eget repo
(`JonathanFribert/blazeitupradio-case`) uden at links ændrer sig; husk så at
root-`robots.txt` stadig skal pege på dens sitemap.

Tal i casen er fra 14. september 2026 (seneste commit `fbb90fc` i det private
repo `JonathanFribert/blaze-9thwunder`): 428 commits på 30 unikke dage
(`git log --format=%ad --date=short | sort -u`), 67.970 linjer TS/TSX i 498
filer under `src/`, 105 filer i `supabase/migrations/`, 1.587 unit tests
(Vitest, CI-kørsel 146 og lokal kørsel) og 1.126 pgTAP-assertions i 67 filer
(CI's database-job). Appen er i lukket pilot: ingen bruger-, afstemnings- eller
omsætningstal. Skærmbillederne (`skaerm-*.png`) er taget fra produktionssitet
https://www.blazeitupradioafrica.com den 5. oktober 2026 med Playwright
(desktop 1440 px, mobil 390 px i 2x) og viser kun den offentlige del; admin
beskrives i tekst, fordi skærmbilleder derfra viser pilotens kontotal og
testbetalinger.

Figurerne i casen er ren HTML/CSS (ingen billeder): billetrejsen (ADR-230/235),
søjler over de 67 pgTAP-filer grupperet efter filnavn, CI-banerne med
trin-varigheder fra GitHub Actions' tidsstempler i kørsel 146, og commits pr.
kalenderdag fra `git log`. Regenerér tallene med samme kommandoer, hvis casen
opdateres efter et nyt commit i app-repoet.

## Tilføj et nyt projekt

1. Kopiér `<article class="story">`-blokken (IKKE `.lead`) og udfyld kicker,
   rubrik (med link), dek, nøgletal og knapper. Læg den nederst i `.stories`.
2. Historie nummer to og frem bruger klassen `story` alene; kun den øverste
   har `lead`. Placeholder-kortet (og dets CSS) blev fjernet ved case 03;
   nye historier lægges nederst i `.stories`.
3. Nøgletal: `stat-value` skal starte med et heltal, hvis tallet skal tælle op.
4. Regenerér `og-image.png` fra `og-template.html`, hvis forsidens indhold
   ændrer sig væsentligt (headless Chrome, se casens README). Udgavelinjens
   måned (`.edition-line` og og-skabelonerne) opdateres til udgivelsesmåneden.
5. Sandfærdighed som på casen: kun tal fra rigtige kørsler/logs.
6. Spejl ændringen i `en.html` (se afsnittet om den engelske udgave).

## Når monitoren pensioneres (ugens afslutning)

1. Opdatér nøgletallene i BEGGE sprog (kørsler/fejl efterprøves mod
   `gh run list -R JonathanFribert/nyhedsmonitor` — pas på arbejdsmappen:
   uden `-R` tælles det forkerte repos kørsler).
2. Skift kicker fra "Sat i drift juli 2026" / "In production since July 2026"
   til afsluttet form, og fjern `live-dot`-prikken (den signalerer aktiv drift).
3. Casens efterskrift og case-brief opdateres samtidig — se casens README.

## Effekter (alle gated bag prefers-reduced-motion; fuld visning uden JS)

Indgangssekvens (ren CSS: udgavelinje → nameplate → dobbeltstregen tegnes →
tophistorien rejser sig), nøgletal der tæller op (JS, 0,55 s efter lead),
levende grøn drift-prik (pinger tre gange, aldrig uendeligt), iris-temaskift
fra knappen, cross-document view transitions til/fra casen (forside↔case
crossfader i Chromium), papirkorn i baggrundslaget, rubrik-underlinje og
pil-glid på hover.

## Publicering

```
git add -A && git commit -m "beskrivelse" && git push origin main
```

Pages serverer main/rod automatisk. OBS: robots.txt her i roden gælder HELE
domænet jonathanfribert.github.io, også /nyhedsmonitor-case/ — derfor peger
den på begge sitemaps. Casens egen robots.txt er uden virkning (ikke i roden)
og ignoreres.

Kendte Pages-fejl og kure: se casens README (konfiguration kan forsvinde →
POST /pages; auto-build kan udeblive → POST /pages/builds).
