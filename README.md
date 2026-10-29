# C21-borden & bereikbaarheid — Amsterdam

Twee kaarten die vrachtverkeer met een **ontheffing voor de 7,5-tonszone** helpen zien **welke gewichtsborden voor hén gelden** en **waar hun voertuig kan komen**.

> **Over welke ontheffing gaat dit?** Amsterdam heeft in het centrum een **7,5-tonszone**: een aaneengesloten gebied waar voertuigen zwaarder dan 7,5 ton in principe niet in mogen. Met een **RVV-ontheffing voor díé zone** ben je vrijgesteld van de *zone*borden (begin, herhaling en einde), maar **niet** van losse gewichtsborden (C21) die elders in de stad staan, en ook niet van andere beperkingen zoals hoogte, breedte, afslagverboden of de milieuzone. Precies dat onderscheid maken deze kaarten zichtbaar. Heb je een ánder type ontheffing, dan gaan deze aannames niet op — controleer altijd je eigen voorwaarden.

**Live:**
- Bordenkaart → https://jes-gearbox.github.io/c21-amsterdam/index.html
- Bereikbaarheidskaart → https://jes-gearbox.github.io/c21-amsterdam/bereikbaarheid.html

## De twee kaarten

**Bordenkaart** (`index.html`) — alle C21-gewichtsborden in Amsterdam, met onderscheid tussen de **7,5t-zone** (waar je ontheffing geldt) en de **losse C21-borden** die wél voor je gelden. Filter op gewicht, zonetype en status.

**Bereikbaarheidskaart** (`bereikbaarheid.html`) — welke wegvakken wel/niet bereikbaar zijn voor een specifiek vrachtwagenprofiel, met de 7,5t-zone er zichtbaar overheen. Klik op de kaart voor een puntcheck op de dichtstbijzijnde weg. Dagelijks automatisch bijgewerkt.

## Waarom

Met een ontheffing voor de 7,5-tonszone ben je vrijgesteld van de zoneborden rond het centrum, maar niet van de overige C21-borden in de stad. Bestaande kaarten maken dat onderscheid niet zichtbaar — deze wel. En de bereikbaarheidskaart laat zien waar een zwaar voertuig überhaupt kan komen, zodat je die twee dingen kunt combineren.

## Databronnen

- **Verkeersborden:** NDW open data (gewichtsborden C21, gemeente Amsterdam)
- **Bereikbaarheid:** NDW bereikbaarheids-API (accessibility-map)
- **Wegennet & luchtfoto:** PDOK — NWB Wegen en Luchtfoto
- **Basiskaart:** Esri Light Gray Canvas (met OpenStreetMap-data)
- **Bordpictogrammen:** officiële RVV-borden (publiek domein, via Wikimedia Commons), in de bereikbaarheidskaart zelf-gehost in de pagina

## Hoe het bijgewerkt wordt

De bordenkaart haalt de borden live bij NDW op. De bereikbaarheidskaart draait op een dagelijkse GitHub Action (`.github/workflows/update-accessibility.yml`): die berekent de bereikbaarheid server-side voor het profiel in `vehicle-request.json` en werkt het resultaat (`accessibility.geojson`) bij. Wijzig je een bord in NDW, dan loopt de kaart binnen een dag mee.

De live-aanroepen naar de NDW-bereikbaarheids-API lopen via een kleine Cloudflare Worker-proxy (NDW staat cross-origin verzoeken vanuit de browser niet toe).

## Voertuigprofiel

Het profiel van de bereikbaarheidskaart staat in **`vehicle-request.json`** (nu: vrachtwagen, 22,5 t, aslast 10,5 t, 4 m hoog, 2,35 m breed, 8,25 m lang, diesel Euro 6). Aanpassen = dat bestand wijzigen; de volgende Action-run rekent het opnieuw. In de kaart zelf kun je het profiel ook tijdelijk aanpassen en live laten herberekenen.

## Status & volgende stappen

Dit is een MVP die in gebruik is. Recent toegevoegd: klik-puntcheck met snapping naar de dichtstbijzijnde weg, "bekijk op straat"-link, officiële bordpictogrammen en een key-loze basiskaart.

Op de rol:
- Zelf instelbaar voertuigprofiel in de kaart (bijv. leeg/vol, brandstof/emissieklasse) zonder `vehicle-request.json` te hoeven wijzigen
- Officiële bordpictogrammen ook in de bordenkaart, zodat beide kaarten er hetzelfde uitzien
- Panoramax-link bij een bord (straatbeeld) zodra bruikbaar

## Let op

Borden **met een onderbord** (venstertijden, uitzonderingen) worden door de bereikbaarheids-API genegeerd en tellen als bereikbaar; afslagverboden tellen niet mee. De kaarten zijn een hulpmiddel, geen juridisch oordeel — controleer altijd je eigen ontheffingsvoorwaarden.

## Colofon

Een persoonlijk project, gebouwd om collega's te helpen. Kaart- en borddata © NDW, PDOK / Rijkswaterstaat, OpenStreetMap-bijdragers en Esri. Bordpictogrammen: publiek domein (Wikimedia Commons).
