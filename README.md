# Site personal — Cuciuvan Lucas-Florian

Site static, scris de mână. Fără framework, fără build step, fără
`node_modules`. Funcționează complet cu JavaScript dezactivat.

Specificația completă e în [`PROJECT.md`](PROJECT.md).
Pașii de publicare sunt în [`DEPLOY.md`](DEPLOY.md).

---

## Cum îl vezi pe calculator

**Nu deschide `index.html` cu dublu-click.** Paginile leagă stilurile
absolut (`/assets/styles.css`), exact ca pe serverul real — prin
`file://` browserul caută în rădăcina discului și pagina apare fără CSS.

Pornește un server local din folderul proiectului:

```bash
python3 -m http.server 8000
```

Pe Windows, dacă `python3` nu merge, încearcă `py -m http.server 8000`.

Apoi deschide <http://localhost:8000>. Oprești cu `Ctrl+C`.

Nu trebuie instalat nimic — Python vine preinstalat pe macOS și pe
majoritatea distribuțiilor Linux. Dacă ai Node, merge la fel de bine
`npx serve` sau extensia *Live Server* din VS Code.

---

## Structura

```
/
├── index.html                      home
├── about/index.html
├── work/index.html                 lista de proiecte
├── work/cuttracker/index.html      case study
├── work/liceu/index.html           case study
├── work/restaurant-pizzerie/       case study
├── work/_template/index.html       șablon gol, noindex — se duplică
│                                   pentru fiecare proiect nou
├── assets/
│   ├── styles.css                  TOT CSS-ul, cu tokens
│   ├── fonts/                      woff2 self-hostate
│   ├── images/og-default.png       preview 1200×630
│   ├── og-source.html              sursa preview-ului, noindex
│   └── favicon.svg
├── _headers                        cache + securitate (Netlify)
├── robots.txt
└── sitemap.xml
```

## Cum se lucrează la el

**Culorile și mărimile** se schimbă dintr-un singur loc: blocul `:root`
din `assets/styles.css`. Nu pune hex-uri direct în reguli.

**Spațierea între secțiuni** se face doar prin clase (`.section`,
`.wrap`), niciodată prin selectori de element. Dacă adaugi
`margin`/`padding` pe `p` sau pe `section`, se vor anula reciproc cu
regulile existente.

**Header-ul și footer-ul sunt duplicate** în fiecare pagină, intenționat
— la 7 pagini e mai ieftin decât un toolchain. Când schimbi ceva în ele,
schimbă în toate.

**Un proiect nou:** copiază `work/_template/` ca `work/<slug>/`, scoate
`noindex`-ul, completează cele 8 secțiuni, apoi adaugă-l în
`work/index.html`, pe home și în `sitemap.xml`.

## Ce a mai rămas de completat

Tot ce lipsește e marcat vizibil `TODO` în pagină. Le vezi pe toate cu:

```bash
grep -rn "TODO" --include=*.html --include=*.xml --include=*.txt .
```

Pe scurt: email, headline-ul de pe home, cele trei puncte din „What I
offer", bio-ul, CV-ul, numele localului și al liceului, linkurile live,
screenshot-urile și rezultatele.

Cât timp TODO-urile sunt vizibile, nu publica site-ul fără parolă —
vezi prima secțiune din `DEPLOY.md`.

## Verificat

Lighthouse pe home: Performance 100, Accessibility 100, Best Practices
100, SEO 100. Zero layout shift. Fără overflow orizontal de la 320px în
sus. Toate perechile text/fundal trec 4.5:1.
