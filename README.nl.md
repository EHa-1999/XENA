# Archiefwaardige opslag voor de medewerker

[English](README.md) · **Nederlands** · [Deutsch](README.de.md)

**▶ [Open de demo](https://eha-1999.github.io/XENA/#nl)** · ook in [English](https://eha-1999.github.io/XENA/#en) · [Deutsch](https://eha-1999.github.io/XENA/#de) · [Français](https://eha-1999.github.io/XENA/#fr) · [Español](https://eha-1999.github.io/XENA/#es) · [Italiano](https://eha-1999.github.io/XENA/#it) · [Polski](https://eha-1999.github.io/XENA/#pl)

Een interactieve demo van hoe soevereine, archiefwaardige bestandsopslag op **Nextcloud** en **S3-objectopslag** eruitziet voor een gewone medewerker van een gemeente. Bewaartermijnen, legal hold, metagegevens en toegangsregels worden eronder afgedwongen, terwijl medewerkers blijven werken in de vensters die ze al kennen.

![De Verkenner met het eigenschappenpaneel](docs/screenshot-explorer.png)

> **Een demo, geen product.** Alle voorbeeldgegevens zijn verzonnen: personen, dossiers en zaaknummers bestaan niet. De demo toont de stip op de horizon; de schakelaar *Tijdvak* en de weergave *Groeipad* laten zien wat wanneer beschikbaar komt.

---

## Uitproberen

Open `index.html` in een browser. Het is één zelfstandig bestand: geen installatie, geen buildstap, geen server.

Of open hem online: **[https://eha-1999.github.io/XENA/](https://eha-1999.github.io/XENA/)**. Met een taalcode erachter opent hij in die taal, bijvoorbeeld `https://eha-1999.github.io/XENA/#de`.

## Wat de demo laat zien

| Weergave | Wat je ziet |
|---|---|
| **Verkenner** | De bestandsverkenner op de pc met de schijven M:, P:, I: en W:. Elke schijf is een bucket in één Nextcloud-omgeving. |
| **Documentbibliotheek** | De bestandenlijst op een samenwerkingssite, bijvoorbeeld SharePoint, met kolommen voor classificatie en bewaring. |
| **Teamkanaal** | Het tabblad Bestanden in een teamkanaal, bijvoorbeeld Teams. Kies de kanaalbestanden of een gekoppelde schijf. |
| **Office Assistent** | Een invoegtoepassing in Word met kenmerken, suggesties, toegankelijkheid en workflow naast het document. |
| **Architectuur** | Hoe vensters, Nextcloud, register en objectopslag samenhangen, met voorbeelden van WebDAV- en S3-berichten. |
| **Techniek** | Per functie wat die van Nextcloud vraagt: standaard, uitbreidingspunt, kernwijziging of iets buiten Nextcloud. |
| **Groeipad** | In zes stappen van de netwerkschijven naar de stip op de horizon, met mijlpalen en beslismomenten. |
| **Help** | Functies, waarom de combinatie ertoe doet, veelgestelde vragen, begrippen en een instructie voor beheerders. |

De balk onderaan (*Onder de motorkap*) toont bij elke handeling welk bericht naar de opslag gaat.

## Belangrijkste functies

- **Werken met bestanden:** bestanden, mappen en dossiers aanmaken; openen, hernoemen, kopiëren, knippen en plakken; zoeken in de zoekindex van het register; filteren op kenmerken.
- **Informatiebeheer:** zakelijk of persoonlijk, metagegevens volgens MDTO, dossiers die classificatie en bewaartermijn doorgeven, bewaartermijn afgedwongen met S3 Object Lock, legal hold.
- **Vergissingen herstellen:** een herroepingstermijn na registratie; voor vergrendelde stukken het onleesbaar maken van de inhoud door de sleutel te vernietigen.
- **Versies:** eerdere versies bekijken en terugzetten; terugzetten maakt een nieuwe versie.
- **Delen en toegang:** duurzame links via register en resolver; drie rechten (lezen, bewerken, beheren) per persoon of groep; zichtbaarheid (vindbaar of verborgen) ingesteld door de beheerder van het object; toegang aanvragen.
- **Samenwerken:** vergrendeling "in gebruik door" bij bureaubladapps; samen bewerken in de browser-editor; een workflowpaneel per object.
- **Tijdvak:** wissel tussen *Vandaag*, *Eind 2027* en *Horizon* om te zien wat er wanneer is.
- **Echte WebDAV-server:** koppel een echte server in het losse bestand (zie hieronder).

## Waarom deze combinatie

Elk van de drie bestaat al. Samen in één opslag zijn ze zeldzaam, en pas samen lossen ze het probleem van overheidsorganisaties op:

1. **Archiefwaardige opslag.** De opslag dwingt bewaartermijn en legal hold zelf af, per versie. Zonder dat blijft archiefwaardigheid een belofte van een toepassing.
2. **Functies voor informatiebeheer.** Metagegevens, dossiers, versies, toegangsregels en workflow geven elk bestand de context om het terug te vinden voor een Woo-verzoek, openbaar te maken of verantwoord te vernietigen.
3. **Integratie met vertrouwde vensters.** Zonder die integratie blijven bestanden op de oude schijven en in mailboxen staan.

Op opslag onder eigen beheer met open source, en met een identificatie die los staat van het platform, blijft de organisatie baas over haar informatie bij een volgende migratie. De aanpak vult Common Ground aan: het zaaksysteem blijft leidend voor zaken, deze opslag zorgt voor alle andere documenten.

![Het groeipad](docs/screenshot-roadmap.png)

## Talen

De demo is beschikbaar in het Nederlands, Duits, Engels, Frans, Spaans, Italiaans en Pools. Alle vertalingen zitten in `index.html`.

- De taal volgt de browser; rechtsboven kies je een andere.
- Verwijs rechtstreeks naar een taal met een hekje, bijvoorbeeld `index.html#de` of `index.html#fr`.
- De keuze wordt in de browser onthouden (`localStorage`).

De vertalingen zijn gemaakt met aandacht voor vakterminologie, maar niet nagekeken door moedertaalsprekers. Verbeteringen zijn welkom.

## Een echte WebDAV-server koppelen

In het losse bestand accepteert *Netwerkschijf koppelen* ook het adres van een echte WebDAV-server, met gebruikersnaam en wachtwoord. Bladeren en openen werken, en aanmaken, hernoemen, mappen maken en verwijderen **gebeuren echt op die server**; verwijderen is definitief. De archieffuncties (metagegevens, bewaartermijnen, dossiers) en kopiëren, knippen en plakken zijn daar uitgeschakeld. Gebruik een testserver met testgegevens.

De browser staat dit alleen toe als de server het toestaat (CORS) en het certificaat wordt vertrouwd. De Help (*Voor beheerders*) beschrijft twee nette manieren:

1. Lever de pagina uit vanaf dezelfde server als de WebDAV-schijf (zelfde schema, host en poort). CORS speelt dan niet.
2. Laat de server CORS-koppen sturen, het voorafgaande `OPTIONS`-verzoek zonder aanmelding beantwoorden, en kopnamen hoofdletterongevoelig lezen.

Binnen claude.ai werkt de koppeling niet, omdat pagina's daar geen verbindingen naar buiten mogen maken.

## Architectuur en groeipad in het kort

- **Presentatielaag:** Verkenner, Office met de Office Assistent, documentbibliotheek, teamkanaal, Nextcloud Files in de browser, Nextcloud-client.
- **Nextcloud:** WebDAV-eindpunt, Files, een Governance- en Archief-app, de opslaginterface.
- **Archiefwaardige laag:** objectenregister, resolver en sleutelbeheer naast S3-objectopslag met versiebeheer, Object Lock en legal hold; één bucket per schijf.
- **Zes verzoeken aan Nextcloud:** wijzigingsmelding, gedelegeerde versiegeschiedenis, alleen-lezen metagegevens uit het register, bestuurde verwijdering, duurzame identiteit, en van bestand naar informatieobject. Alleen verzoek 3 en 4 vallen binnen de huidige opdracht.
- **Toegang:** nu rollen (RBAC); in stap 4 centrale beleidsregels die worden vertaald naar toegangsregels in Nextcloud; op de horizon een centraal beslispunt per verzoek (PBAC).

![De architectuur](docs/screenshot-architecture.png)

## Technische opmerkingen

- Eén HTML-bestand met gewone JavaScript en CSS. Geen framework, geen afhankelijkheden, geen build.
- Het enige externe verzoek is het lettertype IBM Plex van Google Fonts. Zonder dat valt de browser terug op een systeemlettertype.
- Licht en donker volgen het besturingssysteem.
- De demo houdt alles in het geheugen: wat je aanmaakt, blijft bestaan tot je de pagina herlaadt.

## Opbouw van de repository

```
index.html                  de demo
README.md                   Engelse versie
README.nl.md                dit bestand
README.de.md                Duitse versie
docs/                       schermafbeeldingen voor de README
```

## Makers

Gemaakt door **Erik Hoekstra**, programma-architect en senior consultant, afdeling i-Ontwikkeling, Gemeente Haarlem, met assistentie van Claude Opus 5.5 (Anthropic).

Ten behoeve van het gesprek met Nextcloud over archiefwaardige opslag, het Common Ground-team en het samenwerkingsverband OWC, en medewerkers, informatiebeheerders en architecten van de gemeenten Haarlem en Zandvoort.

Contact: [ehoekstra@haarlem.nl](mailto:ehoekstra@haarlem.nl) · [erik@erikhoekstra.com](mailto:erik@erikhoekstra.com)

## Licentie

© 2026 Gemeente Haarlem. Vrij te gebruiken, aan te passen en te verspreiden onder de [European Union Public Licence (EUPL) 1.2](https://interoperable-europe.ec.europa.eu/collection/eupl/eupl-text-eupl-12). Zie `LICENSE`.
