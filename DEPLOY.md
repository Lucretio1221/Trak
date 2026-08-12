# Deploy — Netlify

Site static, fără build step. Netlify nu trebuie să ruleze nimic: doar
servește folderul așa cum e.

---

## Înainte de primul deploy public

Site-ul are momentan blocuri `TODO` **vizibile pe pagină** — asta e
intenționat pentru fazele de lucru, dar nu e ceva ce vrei să vadă un
client sau un recrutor.

Ai două variante:

- **Deploy privat pentru preview** (recomandat acum): în Netlify, la
  *Site configuration → Access & security → Visitor access*, pune o
  parolă. Poți vedea site-ul live, dar nu-l găsește nimeni.
- **Așteaptă** până dispar TODO-urile. Le găsești pe toate cu:

  ```
  grep -rn "TODO" --include=*.html --include=*.xml --include=*.txt .
  ```

---

## 1. Înlocuiește domeniul placeholder

Peste tot în proiect apare `TODO-domain.netlify.app`. După ce știi
subdomeniul real (sau domeniul tău), un singur find & replace:

```
grep -rl "TODO-domain.netlify.app" . | xargs sed -i 's|TODO-domain\.netlify\.app|NUMELE-TAU.netlify.app|g'
```

Atinge: `canonical`, `og:url`, `og:image`, `robots.txt`, `sitemap.xml`.

Verifică după, să nu fi rămas nimic:

```
grep -rn "TODO-domain" . || echo "curat"
```

---

## 2. Deploy prin drag & drop (prima dată)

1. Intră pe <https://app.netlify.com/drop>.
2. Trage **folderul proiectului** (cel care conține `index.html`) în
   pagină. Nu-l arhiva, nu trage doar conținutul.
3. Netlify îți dă imediat o adresă de forma
   `random-name-123456.netlify.app`.
4. *Site configuration → Change site name* — pune ceva de dat mai
   departe, ex. `cuciuvan-lucas-florian`.
5. Întoarce-te la **pasul 1** cu numele real și re-fă deploy-ul.

Ce urcă: tot, inclusiv `_headers`, `robots.txt`, `sitemap.xml`,
`assets/`. Netlify le tratează automat — `_headers` nu e un fișier
public, e citit ca configurație.

---

## 3. Conectează la Git (după ce merge)

Ca fiecare `git push` să publice singur:

1. *Add new site → Import an existing project → GitHub*.
2. Alege repo-ul `Lucretio1221/Trak`.
3. Setări:
   - **Branch to deploy**: `main` (nu branch-ul de lucru)
   - **Build command**: *gol*
   - **Publish directory**: `.` (rădăcina)
4. Deploy.

Nu pune `npm install` sau vreun build command. Nu există `package.json`
și nu trebuie să existe.

---

## 4. După deploy — de verificat pe adresa reală

- [ ] `https://.../robots.txt` se încarcă și arată domeniul corect
- [ ] `https://.../sitemap.xml` la fel
- [ ] Antetele merg: `curl -sI https://.../assets/fonts/familjen-grotesk-500-latin.woff2 | grep -i cache-control`
      → `public, max-age=31536000, immutable`
- [ ] Compresia merge: `curl -sI -H "Accept-Encoding: br" https://.../assets/styles.css | grep -i content-encoding`
      → `br`
- [ ] Preview-ul social: lipește adresa în
      <https://www.opengraph.xyz/> — trebuie să apară imaginea 1200×630
- [ ] JSON-LD: <https://search.google.com/test/rich-results> pe home →
      trebuie să găsească un `Person`
- [ ] Activează CSP-ul comentat din `_headers` și re-testează rich
      results (vezi nota din fișier)

---

## 5. Trimite sitemap-ul la Google

1. <https://search.google.com/search-console> → *Add property* →
   URL prefix → adresa site-ului.
2. Verifică proprietatea (Netlify: cel mai simplu prin DNS TXT dacă ai
   domeniu propriu, altfel prin fișier HTML încărcat în rădăcină).
3. *Sitemaps* → trimite `sitemap.xml`.

---

## Note

**Minificare CSS.** Lighthouse semnalează ~6 KB de economie pe
`styles.css`. Netlify trimite fișierul cu Brotli, ceea ce acoperă
aproape toată diferența, iar CSS-ul e scris de mână și comentat ca să
poată fi citit — nu-l minifica manual. Dacă totuși vrei economia,
activează *Asset optimization* din Netlify, nu edita sursa.

**Cache pe `styles.css`.** E setat la o oră, nu la un an, pentru că
numele fișierului nu conține hash. Dacă vreodată apare un build step
care adaugă hash, atunci se poate trece pe `immutable`.

**Fonturi.** Sunt servite local din `assets/fonts/`. Nu reintroduce
link-ul către Google Fonts: adăuga două handshake-uri către alt domeniu
și un stylesheet care bloca randarea.
