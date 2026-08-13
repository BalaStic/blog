# Blog

Egy statikus, build nélküli weboldal, amely betölti és formázva megjeleníti a `posts/2026-07-10.md` bejegyzést.

## Működés

- Az `index.html` betölti a Markdown fájlt (`fetch`), majd a [`marked`](https://github.com/markedjs/marked) könyvtárral HTML-lé alakítja és megjeleníti.
- A `.nojekyll` fájl letiltja a Jekyll-feldolgozást a GitHub Pagesen, így a `.md` fájl nyers szövegként töltődik le.

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

> Megjegyzés: a `fetch('posts/2026-07-10.md')` relatív útvonalat használ, ami projektoldalon (`/<repo>/` alatt) helyesen működik.