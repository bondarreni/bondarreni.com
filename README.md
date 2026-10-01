# bondarreni.com
<3

Bondár Reni beszélő mesekönyveinek oldala. Sima statikus HTML, nincs build lépés. Minden oldal a saját `<style>` blokkjában hordozza a stílusait.

## Mi hol van

| Hely                   | Mire való                                                                 |
| ---------------------- | ------------------------------------------------------------------------- |
| `index.html`           | Főoldal: beszélő mesekönyv, hogyan készül, visszajelzések, feliratkozás   |
| `konyvek.html`         | Az összes mese listája                                                     |
| `konyvek/*.html`       | Egy-egy mese oldala (ár, pillantás a könyvbe, személyre szabás), plusz `uj-mese.html` az egyedi mesékhez |
| `szovegek/*.html`      | A mesék teljes szövege                                                     |
| `rajzok.html`, `rolam.html` | Rajzgaléria és bemutatkozás                                          |
| `aszf.html`, `adatkezeles.html`, `impresszum.html` | Jogi oldalak                                  |
| `assets/`              | Képek, videók, ikonok. A könyvek képei az `assets/books/`-ban              |
| `hirlevel/utm.md`      | UTM szabályok a hírlevelek linkjeihez                                      |
| `hirlevel/<dátum>/`    | Egy-egy hírlevél: `.mjml` forrás, a belőle generált `.html` és a `kepek/` mappa |
| `design-system.md`     | **Hogyan nézzen ki:** színek, betűk, elemek, új aloldal és hírlevél készítése |
| `writing-style.md`     | **Hogyan szóljon:** hangnem, megszólítás, kifejezések, hírlevél felépítése |

## Új aloldal vagy hírlevél készítése

Mielőtt új oldalt vagy hírlevelet írsz (vagy íratsz Claude-dal), olvasd el a `design-system.md`-t és a `writing-style.md`-t. Ezek írják le a website kinézetét és hangját, hogy minden új tartalom illeszkedjen a meglévőkhöz.

Hírlevél HTML generálása a levél mappájában (pl. `hirlevel/2026-10-01/`):

```
npx mjml <nev>.mjml -o <nev>.html
```

A levél képei a Bluefox Email galériájából töltődnek be, a `hirlevel-<dátum>` mappából.

A feliratkozás és a hírlevélküldés a Bluefox Emailen keresztül megy.
