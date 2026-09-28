# Design system - bondarreni.com

Ez a leírás a website jelenlegi kinézetét rögzíti, hogy az új aloldalak és hírlevelek ugyanígy nézzenek ki. Ha valami itt nincs leírva, a meglévő oldalak (`index.html`, `konyvek.html`, `konyvek/*.html`) a mérvadók.

A hangulat: **csendes, papíros, kézműves**. Sok levegő, vékony vonalak, halvány színek, és a rajzok vannak a középpontban. Nincsenek élénk színek, vastag betűk vagy árnyékos, "appos" elemek.

---

## Színek

Minden oldal `:root`-jában ugyanez az öt változó van. Új oldalon csak ezeket használd:

| Változó       | Érték     | Mire                                                         |
| ------------- | --------- | ------------------------------------------------------------ |
| `--ink`       | `#1a1a1a` | Fő szövegszín, címek, fekete gombok háttere                  |
| `--ink-light` | `#6b6b6b` | Másodlagos szöveg, leírások, navigációs linkek               |
| `--paper`     | `#fafaf8` | Oldal háttere (törtfehér), fekete gomb szövegszíne           |
| `--accent`    | `#c8a96e` | Arany kiemelés: kis címkék, elválasztó vonal, ♡, idézőjel    |
| `--border`    | `#e8e5e0` | Minden keret és elválasztó vonal                             |

Kiegészítő színek (a meglévő oldalakon előfordulnak):

| Érték     | Mire                                                                 |
| --------- | -------------------------------------------------------------------- |
| `#f0ede8` | Meleg, sötétebb papír: kiemelt szekció háttere (pl. visszajelzések). Az `uj-mese.html`-ben `--warm` néven |
| `#ffffff` | Kártyák, beviteli mezők, kiemelt dobozok háttere (`--card`)          |
| `#c0c0c0` | Lábléc jogi linkjei és copyright                                     |

> A `konyvek.html` néhol `--gold`, `--muted`, `--soft`, `--line` változókat használ, ezek nincsenek definiálva. A `konyvek/*.html` oldalakon pedig van néhány közeli, beégetett árnyalat (`#c69b55`, `#77716b`, `#fbfaf7`). Új oldalon ezek helyett a fenti öt változót használd.

---

## Tipográfia

Két betűtípus, mindkettő a Google Fontsról:

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Inter:wght@300;400;500&display=swap"
  rel="stylesheet"
/>
```

- **Cormorant Garamond** (serif) - címek, könyvcímek, idézetek, árak, a "Bondár Reni" név. Vékony (300) vagy normál (400) súllyal, soha nem félkövéren. Egy-egy szót dőlten (`<em>`) is lehet kiemelni: *"Egy kis mesés update"*, *"Őrizd meg a szeretteid hangját egy mesekönyvben."*
- **Inter** (sans-serif) - minden más: törzsszöveg, gombok, címkék, navigáció. A törzsszöveg **300-as** (light) súlyú, a gombok 500-asok.

| Szerep                        | Betű      | Méret                          | Egyéb                                                |
| ----------------------------- | --------- | ------------------------------ | ---------------------------------------------------- |
| Nagy cím (hero, oldalcím)     | Cormorant | `clamp(2.4rem, 3.5vw, 3.8rem)` | 300, `line-height: 1.1`, `letter-spacing: -0.01em`   |
| Szekciócím                    | Cormorant | `clamp(2rem, 5vw, 3rem)`       | 300-400, `line-height: 1.05`                         |
| Kártyacím, könyvcím           | Cormorant | `1.5-1.65rem`                  | 400                                                  |
| Idézet, visszajelzés          | Cormorant | `1.25rem`                      | dőlt, `line-height: 1.55`                            |
| Ár                            | Cormorant | `1.8rem`                       | 500                                                  |
| Törzsszöveg                   | Inter     | `0.9-1rem`                     | 300, `line-height: 1.7-1.9`, max `44-58ch` széles    |
| Kis címke ("eyebrow")         | Inter     | `0.68-0.72rem`                 | NAGYBETŰS, `letter-spacing: 0.25-0.3em`, `--accent`  |
| Navigációs link, lábléc link  | Inter     | `0.72-0.8rem`                  | NAGYBETŰS, `letter-spacing: 0.12-0.2em`, `--ink-light` |
| Gomb                          | Inter     | `0.78rem`                      | 500, NAGYBETŰS, `letter-spacing: 0.18em`             |

A **nagybetűs, széthúzott kis szöveg** és a **vékony serif cím** kombinációja adja az oldal karakterét. Ezt minden szekcióban érdemes megtartani.

---

## Alapelemek

### Szekció fejléce

Szinte minden szekció így kezdődik: arany kis címke, alatta serif cím, alatta szürke leírás.

```html
<p class="section-label">Hogyan készül?</p>
<h2>Így készül a beszélő mesekönyved</h2>
<p>...</p>
```

### Arany elválasztó

Egy 40px széles, 1px magas arany vonal a cím alatt: `.hero-divider` (`width: 40px; height: 1px; background: var(--accent)`). A könyvoldalakon középre igazítva `.section-line` a neve.

### Szekcióhatár

A szekciókat nem háttérszín, hanem egy vékony vonal választja el: `border-top: 1px solid var(--border)`. A tágas belső térköz (`padding: 4-8rem 2rem`) fontos része a hangulatnak.

### Gombok

Kétféle gomb van, egy oldalon belül ne keverd őket:

1. **Szögletes fekete gomb** (hero űrlap, hírlevél): `background: var(--ink); color: var(--paper)`, nincs lekerekítés, `padding: 0.9rem`, NAGYBETŰS Inter 500 `letter-spacing: 0.18em`. Hover: `#333` és 1px-es felemelkedés.
2. **Kerek (pill) fekete gomb** (lépések, `uj-mese.html`): `border-radius: 999px`, hover-re arany (`--accent`) lesz. Másodlagos változat: átlátszó háttér, `--border` keret.

Szöveges link-gomb, pl. a könyvkártyákon: `Megnézem →` NAGYBETŰS, `letter-spacing: 0.09em`, arany vagy fekete szín, a nyíl a szöveg része.

### Kártyák

- **Könyvkártya:** négyzetes borítókép `--border` kerettel, alatta serif cím, szürke alcím (pl. "Klasszikus népmese"), és egy `Megnézem →` link.
- **Lépés-, választó- és visszajelzés-kártya:** fehér vagy papír háttér, `1px solid var(--border)`, nagy lekerekítés (`22-30px`), nagyon halvány meleg árnyék: `box-shadow: 0 12px 35px rgba(70, 45, 35, 0.035)`.
- **"Új vagy egyedi mese" doboz:** ugyanilyen keretes doboz, felül arany ♡ jellel.

### Felsorolás

Pont helyett arany ♡ jel: `♡ Már elkészült mesék`. Szürke (`--ink-light`) szöveg, sok sorköz.

### Számozott lépések

Kör alakú szám: 35-42px, fekete háttér, fehér szám. Egyszerűbb változat: arany keretes kör arany számmal (`.mini-step`).

### Idézet / visszajelzés

Nagy arany `“` jel (Cormorant, `4rem`), alatta dőlt serif szöveg, a végén a név NAGYBETŰS kis Inter betűkkel vagy `- Név` formában.

### Megjegyzés doboz

Balra egy arany vonal: `border-left: 1px solid var(--accent)`, félig átlátszó fehér háttér, szürke szöveg. Pl. szerzői jogi tudnivalókhoz.

---

## Képek

- A **kézzel rajzolt illusztrációk** a főszereplők. A borítók négyzetesek (`assets/books/*_borito.png`, `assets/books/<mese>/borito.png`).
- A **kész könyvről készült fotók** (kézben tartva, szabadban, természetes fényben) mutatják a könyvet a valóságban: `assets/books/<mese>/IMG_*.jpg`.
- A képek mindig kapnak `--border` keretet vagy lekerekítést, de nincs rajtuk szűrő vagy felirat.
- Az `alt` szöveg magyar, és leírja, mi látszik: `"A kis gidó mesekönyv borítója"`.

---

## Elrendezés

- Tartalom max. szélessége: `1200px`, középre igazítva. Folyó szöveg max. `58ch`.
- Töréspontok: `950px` (tablet: a kétoszlopos kártyák egy oszlopba kerülnek), `768px` (navigáció hamburger menüre vált, a hero egy oszlopos lesz), `650px` (mobil: kisebb padding és lekerekítés, a könyvrács 2 oszlopos).
- A navigáció fix, áttetsző papír háttérrel (`rgba(250, 250, 248, 0.92)` + `backdrop-filter: blur(8px)`), alul `--border` vonallal. Az aktív link arany (`.activeNavLink`).

---

## Új aloldal készítése

Nincs közös CSS fájl, **minden oldal a saját `<style>` blokkjában hordozza a stílusait**. Új oldalnál:

1. Másold le egy hasonló oldal vázát (`rolam.html` a legegyszerűbb, `konyvek/kis-gido.html` egy könyvoldalhoz).
2. Tartsd meg: `<html lang="hu">`, meta description és `og:` tagek, favicon linkek, Google Fonts, gtag (`G-ZJ1Q9NGRDW`), a `:root` változók, a nav + hamburger menü (és a `showHamburger()` script), valamint a footer.
3. Az aktív oldal linkje a navban `activeNavLink` osztályt kap.
4. A `konyvek/` és `szovegek/` mappában lévő oldalak `../` előtaggal hivatkoznak az assetekre és a gyökér oldalaira.
5. Új könyvnél add hozzá a kártyát a `konyvek.html`-hez és az `index.html` "Válassz egy mesét" rácsához is. Készíts neki `szovegek/<mese>.html` oldalt a mese szövegével.

A footer minden oldalon ugyanaz: email, TikTok, majd ÁSZF, Adatkezelési tájékoztató, Impresszum, és `© 2026 Bondár Reni`.

---

## Hírlevél (MJML)

Minden hírlevél a saját, **kiküldési dátummal elnevezett mappájába** kerül, benne minden, ami hozzá tartozik:

```
hirlevel/
  2026-09-29/
    elso-hirlevel.mjml          <- forrás, ezt szerkesztjük
    elso-hirlevel.html          <- ebből generálva, ezt küldjük ki
    kepek/                      <- a levél képei emailhez méretezve (a Bluefoxba feltöltött képek helyi példánya)
```

Generálás (a levél mappájában):

```
cd hirlevel/2026-09-29
npx mjml elso-hirlevel.mjml -o elso-hirlevel.html
```

A `hirlevel/2026-09-29/elso-hirlevel.mjml` a minta, az `<mj-attributes>` blokkja tartalmazza a fenti színeket és betűket MJML formában (`mj-class`: `eyebrow`, `serif`, `muted`). Új levélnél másold le a mappát új dátummal, és módosítsd.

Emailben néhány dolog máshogy működik, mint a weben:

- **600px széles**, egy oszlopos törzs. Kétoszlopos rács (pl. könyvborítók) mobilon magától egymás alá kerül.
- **Csak szögletes gomb** (`border-radius="0"`), mert a pill forma nem minden levelezőben néz ki jól.
- **Árnyék és `clamp()` nincs**, fix `px` méretek vannak: cím 40px, szekciócím 28-32px, könyvcím 22px, törzsszöveg 15px, címke 11px.
- **Betűtípus tartalék:** a Gmail nem tölti be a Google Fontsot. Ezért mindig legyen tartalék: `'Cormorant Garamond', Georgia, 'Times New Roman', serif` és `Inter, Helvetica, Arial, sans-serif`.
- **Minden link és kép abszolút URL.** A képeket a **Bluefox Email galériájába** töltjük fel, egy `hirlevel-<dátum>` mappába (pl. `hirlevel-2026-09-29`), és a levél a Bluefox CDN címét használja (`https://cdn.bluefox.email/...`). A websiteról ne hivatkozz képet a levélben. A `kepek/` mappában a feltöltött képek helyi példánya marad meg.
- **Képméret:** az `assets/` képeit ne használd közvetlenül, mert a borító PNG-k 1-4,5 MB-osak. Minden képből készíts egy kisebb JPG másolatot a `kepek/` mappába, a megjelenített méret kétszeresére (retina): kétoszlopos borító 540×540 px, kiemelt kép 720 px széles. Egy kép 150 KB alatt legyen, az egész levél lehetőleg 500 KB alatt. **WebP képet ne használj**, mert az Outlook nem jeleníti meg.
- **TikTok videó:** a borítókép URL-je (oEmbed `thumbnail_url`) pár nap alatt lejár. Töltsd le, tegyél rá lejátszás gombot, és mentsd a `kepek/` mappába, majd töltsd fel a Bluefox galériába. A kép a videóra linkeljen.
- **Lábléc:** ugyanazok a linkek, mint a weben, plusz "Azért kaptad ezt a levelet, mert feliratkoztál a bondarreni.com oldalon." és a **leiratkozó link**. A leiratkozó link a Bluefox változója: `<a href="{{unsubscribeLink}}">Leiratkozás</a>`. Ezt a Bluefox küldéskor minden címzettnek a saját leiratkozó linkjére cseréli.
- Legyen `<mj-preview>` (a tárgy mellett megjelenő előnézeti szöveg) és `<mj-title>`.
