# UTM szabályok a hírlevelekhez

Minden hírlevélben ezek alapján kapják meg a linkek az UTM tageket. A cél az, hogy a Google Analyticsben (`G-ZJ1Q9NGRDW`) minden levél és azon belül minden link külön látszódjon, és a levelek egymással összehasonlíthatók legyenek.

## Melyik link kap UTM-et

**Kap:** minden link, ami a **bondarreni.com**-ra mutat, a lábléc jogi linkjei is.

**Nem kap:**

| Link                                   | Miért                                                                                   |
| -------------------------------------- | --------------------------------------------------------------------------------------- |
| TikTok, Instagram, más külső oldal     | Ott nincs Google Analytics, a tagek nem mérnének semmit. A kattintást a Bluefox méri.   |
| `mailto:`                              | Nem weboldal.                                                                           |
| `{{unsubscribeLink}}`                  | A Bluefox saját leiratkozó linkje, nem szabad módosítani.                               |
| Képek `src`-je, Google Fonts           | Nem kattintható linkek.                                                                 |

## A tagek

Mindig mind a négy tag szerepeljen, ebben a sorrendben:

| Tag            | Érték                       | Szabály                                                                       |
| -------------- | --------------------------- | ----------------------------------------------------------------------------- |
| `utm_source`   | `bluefox`                   | Mindig ez. A küldő szolgáltatás.                                              |
| `utm_medium`   | `email`                     | Mindig ez. A csatorna.                                                        |
| `utm_campaign` | `ÉÉÉÉ-HH-NN-rovid-tema`     | Levelenként egyedi: a kiküldés dátuma és 2-4 szavas téma. Egyezik a levél mappájának dátumával (`hirlevel/ÉÉÉÉ-HH-NN/`). |
| `utm_content`  | lásd lent                   | Linkenként: megmondja, hol van a link a levélben.                             |

**Írásmód minden értéknél:** csak kisbetű, ékezet nélkül (á → a, ő → o, ű → u …), szóköz helyett kötőjel. Pl. `2026-10-01-beszelo-mesekonyv-update`, nem `2026_10_01 Beszélő Mesekönyv`.

## `utm_content` értékek

Ugyanaz a típusú link minden levélben ugyanazt az értéket kapja, így a levelek összehasonlíthatók. Ha egy link több elemhez tartozik (pl. borító, cím és "Megnézem →" ugyanarra a könyvre), mind ugyanazt az értéket kapja.

| Érték                    | Mire                                                                      |
| ------------------------ | ------------------------------------------------------------------------- |
| `fejlec-logo`            | A "Bondár Reni" név a levél tetején                                        |
| `legujabb-mese`          | A levél elején kiemelt (legújabb) mese linkje                              |
| `konyv-<slug>`           | Egy könyv a könyvrácsban. A `<slug>` a könyvoldal fájlneve `.html` nélkül, pl. `konyv-kis-gido`, `konyv-a-cinege-cipoje` |
| `osszes-konyv`           | "Összes könyv →" gomb (`/konyvek.html`)                                   |
| `uj-mese`                | Az egyedi / új mese oldal (`/konyvek/uj-mese.html`), ha szerepel           |
| `cta-<rovid-nev>`        | Bármilyen más gomb, pl. `cta-sajat-mesekonyv`                              |
| `szoveg-<rovid-nev>`     | Szöveg közbeni link, pl. `szoveg-rolam`                                    |
| `lablec-aszf`            | Lábléc: ÁSZF                                                               |
| `lablec-adatkezeles`     | Lábléc: Adatkezelési tájékoztató                                           |
| `lablec-impresszum`      | Lábléc: Impresszum                                                         |

Ha ugyanaz az oldal két különböző helyről is linkelve van (pl. a kiemelt mese és ugyanaz a mese a rácsban), a két hely különböző értéket kapjon (`legujabb-mese` és `konyv-<slug>`), hogy látszódjon, melyik működik jobban.

Új típusú linknél előbb vedd fel ide a táblázatba, aztán használd.

## Formátum

```
https://bondarreni.com/<oldal>?utm_source=bluefox&utm_medium=email&utm_campaign=<kampany>&utm_content=<link>
```

- A főoldal `https://bondarreni.com/?utm_...` alakú (perjellel a `?` előtt).
- Az MJML-ben és a HTML-ben az `&` helyett `&amp;` áll az `href`-ben. Ez szabályos HTML, a böngésző `&`-ként olvassa.
- Ha a link már tartalmaz `?`-t, az UTM-ek `&`-tel kerülnek a végére.

Példa:

```
https://bondarreni.com/konyvek/kis-gido.html?utm_source=bluefox&utm_medium=email&utm_campaign=2026-10-01-beszelo-mesekonyv-update&utm_content=konyv-kis-gido
```

## Ellenőrzés küldés előtt

1. Nincs bondarreni.com-os link UTM nélkül:
   ```
   grep -o 'href="https://bondarreni.com[^"]*"' <nev>.mjml | grep -v utm_campaign
   ```
   Ennek üresnek kell lennie.
2. Az `utm_campaign` minden linkben ugyanaz, és a levél dátumával kezdődik.
3. Egy-két linket megnyitva az oldal rendben betölt.

## Hol látszik

- **Google Analytics:** *Jelentések → Akvizíció → Forgalomszerzés*, szűrés `Munkamenet kampánya = <utm_campaign>`. Linkenkénti bontáshoz másodlagos dimenzió: *Munkamenet kézi hirdetéstartalma* (`utm_content`). Az összes hírlevél együtt: szűrés `Munkamenet forrása = bluefox`.
- **Bluefox:** a kampány statisztikái (megnyitás, kattintás minden linkre, a külső linkeket is beleértve).

## Eddigi kampányok

| Dátum      | `utm_campaign`                          | Mappa                    |
| ---------- | --------------------------------------- | ------------------------ |
| 2026-10-01 | `2026-10-01-beszelo-mesekonyv-update`   | `hirlevel/2026-10-01/`   |
