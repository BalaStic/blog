# Blog

Egy statikus, build nélküli weboldal, amely betölti a `posts/` mappában lévő összes Markdown bejegyzést, és egyetlen görgethető oldalon, bal oldali tartalomjegyzékkel jeleníti meg őket.

## Működés

- Az `index.html` betölti a `posts.json` manifestet, amely a bejegyzés-fájlnevek listáját tartalmazza.
- A fájlneveket **névszerint csökkenő sorrendbe** rendezi, majd a [`marked`](https://github.com/markedjs/marked) könyvtárral HTML-lé alakítja mindegyiket, és egymás után fűzi őket.
- Minden bejegyzés egy saját horgonyt (`id`) kap a fájlnév alapján: `#post-<fájlnév kiterjesztés nélkül>`.
- A bal oldali oldalsávban minden bejegyzéshez egy kattintható link jelenik meg, amely a megfelelő horgonyra görget.
- A `.nojekyll` fájl letiltja a Jekyll-feldolgozást a GitHub Pagesen, így a `.md` fájlok nyers szövegként töltődnek le.

## Új bejegyzés hozzáadása

1. Dobd be az új Markdown fájlt a `posts/` mappába (pl. `posts/2026-09-01.md`).
2. Add hozzá a fájl nevét a gyökér `posts.json` listájához:

   ```json
   [
     "2026-07-10.md",
     "2026-08-11.md",
     "2026-09-01.md"
   ]
   ```

A sorrend automatikus (név szerint csökkenő), nem kell kézzel rendezni a listát.

## Helyi kipróbálás

A fájl megnyitása után a böngésző `fetch` hívása blokkolva lehet a `file://` korlátozás miatt. Ajánlott egy lokális szerver indítása:

```
python -m http.server 8000
```

Majd nyisd meg: http://localhost:8000

## GitHub Pages közzététel

1. Hozz létre egy új GitHub repositoryt, és töltsd fel ezt a mappát:

   ```
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<felhasznalonev>/<repo>.git
   git push -u origin main
   ```

2. A repositoryban: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` → `/ (root)` → Save**.

3. Az oldal elérhető lesz itt: `https://<felhasznalonev>.github.io/<repo>/`

> Megjegyzés: a `fetch('posts.json')` és a `fetch('posts/<fájlnév>')` relatív útvonalakat használ, ami projektoldalon (`/<repo>/` alatt) helyesen működik.