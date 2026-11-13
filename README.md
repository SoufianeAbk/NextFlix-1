# NextFlix

NextFlix is een statische front-end prototype van een filmstreamingplatform in de stijl van Netflix. Het project bestaat uit pure HTML, CSS en een beetje JavaScript, zonder framework, buildstap of backend. Alle teksten zijn in het Nederlands (`lang="nl"`).

> **Status:** prototype / werk in uitvoering. De pagina's zijn visueel uitgewerkt, maar de interactie (filteren, navigeren naar details, afspelen) is grotendeels nog niet geïmplementeerd. Zie [Bekende beperkingen](#bekende-beperkingen) en [Roadmap](#roadmap).

---

## Inhoud

1. [Overzicht](#overzicht)
2. [Projectstructuur](#projectstructuur)
3. [Starten](#starten)
4. [Pagina's](#paginas)
5. [Ontwerpsysteem](#ontwerpsysteem)
6. [JavaScript-functies](#javascript-functies)
7. [Externe afhankelijkheden](#externe-afhankelijkheden)
8. [Responsive gedrag](#responsive-gedrag)
9. [Bekende beperkingen](#bekende-beperkingen)
10. [Roadmap](#roadmap)

---

## Overzicht

| Onderdeel        | Keuze                                           |
| ---------------- | ----------------------------------------------- |
| Type             | Statische website (front-end prototype)         |
| Talen            | HTML5, CSS3, vanilla JavaScript                 |
| Build/dependencies | Geen                                          |
| Lettertypen      | Bebas Neue (titels), Inter (tekst) via Google Fonts |
| Afbeeldingen     | Placeholders via `via.placeholder.com`          |
| Taal van de UI   | Nederlands                                      |

## Projectstructuur

```
NextFlix-1-main/
├── index.html   # Startpagina: hero, categoriefilters, filmgrids, footer
├── home.html    # Detailpagina van één film (voorbeeld: Inception)
└── README.md
```

Elk HTML-bestand is volledig zelfstandig: de CSS staat in een `<style>`-blok in de `<head>` en de JavaScript in een `<script>`-blok onderaan de `<body>`. Er zijn dus geen losse `.css`- of `.js`-bestanden.

## Starten

Er is geen installatie nodig.

**Optie 1: direct openen**
Open `index.html` in een browser (dubbelklikken volstaat).

**Optie 2: lokale server (aanbevolen)**
```bash
# Python
python -m http.server 8000

# of Node.js
npx serve .
```
Ga daarna naar <http://localhost:8000>.

Een internetverbinding is nodig voor de Google Fonts en de placeholder-afbeeldingen.

## Pagina's

### `index.html` — Startpagina

Titel: *NextFlix - Jouw Filmplatform*

Secties:

- **Header/navigatie** (vast bovenaan, `position: fixed`, met blur-effect): logo en links naar Home, Films, Series, Nieuw en Mijn Lijst.
- **Hero**: welkomsttekst *"Welkom bij NextFlix"* met paarse gradiënt.
- **Populaire Films** (`#films`): categoriebuttons (Alle, Actie, Drama, Komedie, Thriller, Sci-Fi) en een grid met 8 filmkaarten: Inception, Interstellar, The Dark Knight, Parasite, Dune, Oppenheimer, Barbie en Avatar: The Way of Water.
- **Nieuw op NextFlix** (`#nieuw`): grid met 4 kaarten: The Creator, Killers of the Flower Moon, Napoleon en Aquaman and the Lost Kingdom.
- **Footer**: vier kolommen (NextFlix, Ondersteuning, Juridisch, Volg ons) en een copyrightregel.

Een filmkaart (`.film-card`) bestaat uit een poster, een ratingbadge rechtsboven (`.film-rating`), de titel en het jaar. Een klik op een kaart roept `goToFilmDetail(id)` aan.

### `home.html` — Filmdetailpagina

Titel: *Inception - NextFlix*

Deze pagina is een uitgewerkt voorbeeld van een detailpagina voor **Inception** (hardcoded). Secties:

- **Hero-banner** met titel, rating (8.8/10), jaar, duur (148 min), leeftijdsclassificatie (PG-13) en actieknoppen: *Afspelen*, *Mijn Lijst*, *Beoordelen*.
- **Verhaal**: plotbeschrijving en genretags (Actie, Sci-Fi, Thriller, Mystery).
- **Cast**: grid met zes acteurs en hun rol.
- **Recensies**: drie reviewkaarten met naam, sterrenbeoordeling en tekst.
- **Zijbalk**: filminformatie (regisseur, schrijver, studio, budget, box office), talen en ondertitels, en awards.
- **Gerelateerde Films**: horizontaal scrollbare rij (Interstellar, Tenet, The Prestige, Memento, Shutter Island, The Matrix). Een klik roept `goToFilm(id)` aan.
- **Footer**: identiek aan de startpagina.

## Ontwerpsysteem

Beide pagina's gebruiken dezelfde CSS-variabelen in `:root`:

| Variabele           | Waarde    | Gebruik                                  |
| ------------------- | --------- | ---------------------------------------- |
| `--primary-color`   | `#e50914` | Accentkleur: logo, badges, knoppen, hover |
| `--dark-bg`         | `#141414` | Pagina-achtergrond                       |
| `--dark-secondary`  | `#1a1a1a` | Kaarten, footer, informatieblokken       |
| `--text-primary`    | `#ffffff` | Hoofdtekst                               |
| `--text-secondary`  | `#b3b3b3` | Secundaire tekst (jaar, labels, plot)    |
| `--hover-bg`        | `#2a2a2a` | Hover-achtergrond, tags, reviewkaarten   |
| `--success-color`   | `#46d369` | Alleen gedefinieerd in `home.html`, nog ongebruikt |

**Typografie:** `h1`–`h3` gebruiken *Bebas Neue* met `letter-spacing: 1px`; de rest van de tekst gebruikt *Inter* (gewichten 300–700).

**Layout:** de inhoud heeft een maximale breedte van 1400px en staat gecentreerd. Filmgrids gebruiken `repeat(auto-fill, minmax(200px, 1fr))`; de detailpagina gebruikt een tweekoloms layout (`2fr 1fr`).

**Animaties:** kaarten schuiven 5px omhoog met een rode gloed bij hover; het logo en gerelateerde kaarten schalen licht op.

## JavaScript-functies

| Functie | Bestand | Beschrijving |
| ------- | ------- | ------------ |
| `filterFilms(category)` | `index.html` | Zet de actieve categoriebutton om en logt de gekozen categorie in de console. De kaarten worden **nog niet echt gefilterd**. |
| `goToFilmDetail(filmId)` | `index.html` | Navigeert naar `film-detail.html?id=<filmId>`. |
| `goToFilm(filmId)` | `home.html` | Navigeert naar `film-detail.html?id=<filmId>`. |

Categoriewaarden: `all`, `action`, `drama`, `comedy`, `thriller`, `scifi`.

## Externe afhankelijkheden

- **Google Fonts** — Bebas Neue en Inter.
- **via.placeholder.com** — placeholderposters, castfoto's en bannerafbeelding.

## Responsive gedrag

- Onder **968px** (`home.html`): de tweekoloms layout wordt één kolom en de titel en castgrid worden kleiner.
- Onder **768px**: de navigatielinks worden verborgen (er is nog geen hamburgermenu), de herotitel wordt kleiner, het filmgrid gebruikt kleinere kaarten (`minmax(150px, 1fr)`) en de actieknoppen staan onder elkaar op volle breedte.

## Bekende beperkingen

- **Ontbrekende detailpagina:** alle navigatie verwijst naar `film-detail.html`, dat niet bestaat. De bestaande detailpagina heet `home.html`. Dit geeft een 404 bij elke klik op een filmkaart.
- **Naamgeving:** `home.html` is in werkelijkheid de detailpagina van Inception, geen homepage. Hernoemen naar `film-detail.html` lost bovenstaand probleem deels op.
- **Hardcoded inhoud:** de detailpagina toont altijd Inception, ongeacht de `id`-parameter.
- **Filter werkt niet:** `filterFilms` wijzigt enkel de actieve knop. Daarnaast gebruikt het `event.target` via de globale `event`, wat beter als parameter kan worden doorgegeven.
- **Dode navigatielinks:** *Series*, *Mijn Lijst* en alle footerlinks (`#`) verwijzen nergens naartoe; de knoppen *Afspelen*, *Mijn Lijst* en *Beoordelen* hebben geen functionaliteit.
- **Dubbele code:** CSS (header, footer, variabelen) is in beide bestanden gekopieerd.
- **Placeholderdienst:** `via.placeholder.com` is onbetrouwbaar en kan wegvallen; afbeeldingen laden dan niet.
- **Toegankelijkheid:** klikbare kaarten zijn `<article onclick>` zonder toetsenbordondersteuning (`tabindex`, `role="link"` of een echte `<a>`).
- **Kleine inconsistenties:** het jaartal in de footer is statisch (2024); in de castlijst wordt in de `alt`-tekst "Ellen Page" gebruikt terwijl de zichtbare naam "Elliot Page" is; de H3 in de zijbalk gebruikt de klasse `section-title`.

## Roadmap

Voorgestelde vervolgstappen, in volgorde van prioriteit:

1. `home.html` hernoemen naar `film-detail.html` en de links herstellen.
2. De filmdata verplaatsen naar een `films.json` (of een API) en de detailpagina dynamisch vullen op basis van `?id=`.
3. `filterFilms` echt laten filteren via `data-category`-attributen op de kaarten.
4. CSS verplaatsen naar een gedeeld `styles.css` en JavaScript naar `app.js`.
5. Zoekfunctie, hamburgermenu voor mobiel en een werkende *Mijn Lijst* (bijvoorbeeld met `localStorage`).
6. Een videospeler voor *Afspelen* en lokale of echte posterafbeeldingen.
7. Toegankelijkheid verbeteren (semantische links, focusstijlen, alt-teksten).
8. Eventueel een backend (bijvoorbeeld ASP.NET Core Web API of Spring Boot) met database, gebruikersaccounts en een koppeling met een filmdatabase zoals TMDB.
