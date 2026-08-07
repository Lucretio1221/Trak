# PROJECT.md — Personal portfolio site

Salvează acest fișier ca `PROJECT.md` în rădăcina folderului de proiect, apoi
pornește Claude Code în acel folder. Primul prompt: "Citește PROJECT.md și
execută Faza 1."

## 1. Ce construim

Un site personal static, cu două audiențe simultan:

1. Proprietari de restaurante / afaceri locale — trebuie să vadă în 10
   secunde că fac site-uri bune și că se poate lucra cu mine.
2. Recrutori / oameni tehnici — trebuie să vadă că scriu cod real, nu doar
   landing pages.

Aceste două audiențe nu intră în conflict dacă site-ul e construit pe
dovezi, nu pe descrieri de mine însumi. Un studiu de caz cu screenshot,
link live și rezultat concret convinge ambele tabere. Un paragraf despre
„pasiunea mea pentru tehnologie" nu convinge pe nimeni.

Regula centrală: fiecare secțiune trebuie să răspundă la „de unde știu că
e adevărat?". Dacă o afirmație nu are dovadă atașată, se taie.

### Limbă

Engleză, cu o singură excepție: pagina de servicii/contact are și o
variantă scurtă în română (secțiune separată în josul paginii, nu un
language toggle — nu merită complexitatea la v1).

Motiv: engleza deservește partea de job fără compromis, iar pentru un
client local site-ul în engleză citește ca fiind mai profesionist, nu mai
puțin. Ce contează pentru client sunt oricum screenshot-urile și
link-urile live.

### Ce NU intră pe site

Astea nu sunt preferințe, sunt reguli. Claude Code nu le încalcă nici dacă
pare că ar umple frumos spațiul:

- Reflecții anuale, jurnal, „my year so far", note personale
- Hobby-uri, sport, Strava, muzică — orice nu susține una din cele două
  audiențe
- Auto-ironie sau auto-depreciere („a failed project", „got rejected")
- Proiecte neterminate sau nelansate
- Tagline-uri abstracte („Ideas in motion", „Building the future")
- Secțiuni „Skills" cu bare de progres sau grid-uri de logo-uri de
  tehnologii
- Testimoniale inventate, cifre inventate, mockup-uri în loc de
  screenshot-uri reale

## 2. Structura

Patru tipuri de pagină. Nimic mai mult.

```
/                     index.html   — hero, 3 proiecte, servicii, contact
/work/                index.html   — lista completă de proiecte
/work/<slug>/         index.html   — case study, unul per proiect
/about/               index.html   — scurt, factual, cu CV descărcabil
```

### Home

```
┌────────────────────────────────────────────────┐
│  nume                          work  about     │
├────────────────────────────────────────────────┤
│                                                  │
│  O propoziție: ce fac, pentru cine,             │
│  cu ce rezultat.                                │
│  O a doua linie: unde sunt, ce e disponibil.    │
│                                                  │
├────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│  │screenshot│  │screenshot│  │screenshot│       │
│  │ proiect  │  │ proiect  │  │ proiect  │       │
│  └──────────┘  └──────────┘  └──────────┘       │
│   nume + o linie despre rezultat                │
├────────────────────────────────────────────────┤
│  Ce ofer  (3 puncte scurte, pentru clienți)     │
├────────────────────────────────────────────────┤
│  Contact: email vizibil ca text, nu ca formular │
└────────────────────────────────────────────────┘
```

Headline-ul e cea mai importantă propoziție de pe site. Trebuie să fie
specific și verificabil.

Șablon: `<ce fac> for <cine> in <unde>. <constrângere concretă>.` Nu
abstract, nu superlativ.

### Case study — șablonul obligatoriu

Fiecare pagină de proiect are exact aceste secțiuni, în această ordine:

1. Nume + o propoziție — ce e și pentru cine
2. Link live + link repo dacă e public — sus, vizibile, nu în subsol
3. Screenshot mare, real — capturat din site-ul live, nu mockup într-un
   laptop
4. Context — 2-3 propoziții: care era situația înainte, ce lipsea
5. Ce am construit — 3-5 bullet-uri, funcționalități concrete
6. Stack — listă simplă de tehnologii, fără logo-uri
7. Rezultat — cifre dacă există, altfel un fapt verificabil
8. Rolul meu — dacă am lucrat cu cineva, se spune explicit cine ce a făcut

Dacă un proiect nu poate umple secțiunile 4-7 cu conținut real, nu e gata
pentru site.

## 3. Conținutul — proiectele

Ordinea pe home page contează. Primul proiect e cel care decide dacă omul
mai derulează.

### CutTracker — proiectul tehnic principal

Aplicație web pentru monitorizarea unei perioade de cut în bodybuilding,
cu două moduri: Solo (tracking personal + coach AI) și Coach→Atlet (un
antrenor gestionează mai mulți sportivi, definește șabloane de check-in,
dă feedback).

- Stack: React + Vite, Supabase (auth, bază de date, storage), Anthropic
  Claude API, deploy pe Netlify
- Funcționalități de evidențiat: editare inline tip spreadsheet, calcule
  săptămânale de macro, rapoarte generate de AI, analiză video a pozelor
  de fizic, roluri și permisiuni coach/atlet
- Aici merge un link către repo dacă e public — pentru audiența tehnică e
  cel mai valoros lucru de pe site

Ăsta e proiectul care demonstrează că nu ești doar „omul cu landing
page-uri". Merită cel mai lung case study.

### Site-uri pentru restaurante / pizzerie

Cel mai valoros pentru clienți. Dacă localul avea ceva înainte,
before/after side by side e cea mai convingătoare imagine de pe tot
site-ul.

- De completat: numele localului (cu acordul lui), ce s-a schimbat
  concret, cât a durat
- Bun de menționat dacă e adevărat: viteza de încărcare, faptul că meniul
  se poate actualiza singur, că merge bine pe telefon
- Spune explicit că a fost lucrat în doi, și cine ce a făcut

### Site-ul liceului

Redesign cu utilizatori reali și constrângeri reale (conținut existent,
structură moștenită, public non-tehnic). Arată că poți lucra cu ceva ce
nu ai pornit de la zero.

### Nu se pune pe site (încă)

- travelai — neterminat. Se adaugă când e lansat, nu înainte.
- Automatizarea de conținut / clipping — nu susține niciuna dintre cele
  două audiențe în forma actuală.

### Ce trebuie să pregătesc eu înainte de Faza 3

- Screenshot-uri reale, la rezoluție mare, din fiecare site live (desktop
  + mobil)
- Adresa de email pentru contact
- Link-urile live pentru fiecare proiect
- CV în PDF, dacă vreau butonul de download pe /about
- Confirmare de la clienți că le pot folosi numele și screenshot-urile

## 4. Direcție vizuală

Site-ul e el însuși o probă de lucru. Un site lent sau generic anulează
tot ce scrie pe el.

### Ce să eviți — important

Design-ul generat de AI se adună în acest moment în trei clișee. Nu
folosi niciunul dintre ele fără un motiv anume:

1. Fundal crem (~#F4F1EA) + serif cu contrast mare + accent teracotă
   (~#D97757)
2. Fundal aproape negru + un singur accent verde acid sau vermilion
3. Layout de ziar, linii subțiri, zero border-radius, coloane dense

Notă specifică: paleta din CutTracker (crem #f7f7f5 + roșu #e8492f) cade
fix în categoria 1. E potrivită acolo, dar nu o refolosi aici — ar face
site-ul să pară o temă, nu o decizie.

### Cum alegem direcția

Înainte de a scrie CSS, Claude Code propune trei direcții, fiecare cu:

- 4-6 culori numite, cu hex
- două fonturi: unul de display cu caracter, folosit cu reținere, și unul
  de body
- o descriere de o propoziție a layout-ului
- un element de semnătură — singurul lucru pentru care site-ul e ținut
  minte

Direcțiile trebuie să pornească din subiect: cineva care livrează repede
lucruri care funcționează, pentru afaceri mici, dintr-un oraș anume. Nu
din „portofoliu de developer".

Eu aleg una, apoi se construiește exact pe ea.

**Aleasă: Direcția A — „Menu".** Tipografie de meniu tipărit și firmă de
local.

### Pragul de calitate — nenegociabil

- Responsive până la 360px lățime, testat, nu presupus
- Focus vizibil la tastatură pe fiecare element interactiv
- `prefers-reduced-motion` respectat
- Imaginile au `width` / `height` setate — zero layout shift
- Contrast text minim 4.5:1
- Lighthouse peste 95 la Performance și Accessibility
- Fără font-uri încărcate care blochează randarea; `font-display: swap`
- Animație: cel mult un moment orchestrat la încărcarea paginii și
  micro-interacțiuni la hover. Mai mult decât atât începe să pară
  generat.

## 5. Tehnic

HTML + CSS scrise de mână. Fără framework, fără build step, fără
node_modules. La 6-8 pagini statice, duplicarea header-ului e mai ieftină
decât un toolchain.

JavaScript doar dacă o interacțiune chiar îl cere. Site-ul trebuie să
funcționeze complet cu JS dezactivat.

Un singur `styles.css`, cu custom properties pentru culori și scara
tipografică. Atenție la specificitatea selectorilor — nu combina
selectori de tip cu selectori de element pentru padding/margin între
secțiuni, se anulează reciproc.

Imagini: WebP, `loading="lazy"` sub fold, dimensiuni multiple prin
`srcset`.

Deploy pe Netlify prin drag-and-drop la început, conectat la Git după.

Domeniu: se adaugă mai târziu. Până atunci, link-ul `.netlify.app` e
suficient.

### Structura de fișiere

```
/
├── index.html
├── about/index.html
├── work/index.html
├── work/<slug>/index.html
├── assets/
│   ├── styles.css
│   ├── images/
│   └── cv.pdf
├── robots.txt
└── sitemap.xml
```

### SEO — minimul care contează

Fiecare pagină: `<title>` unic, `meta description`, Open Graph complet
(titlu, descriere, imagine 1200×630), `canonical`. O imagine de preview
reală, generată din design-ul site-ului. Pe home, JSON-LD de tip
`Person`.

## 6. Fazele de execuție

Claude Code execută o singură fază per rundă și se oprește pentru
feedback.

- **Faza 1 — Direcție.** Trei direcții vizuale conform secțiunii 4,
  fiecare cu tokens și element de semnătură. Fără cod. Stop, aștept
  alegerea.
- **Faza 2 — Schelet.** Structura de fișiere, `styles.css` cu
  tokens-urile din direcția aleasă, header/footer, home page cu conținut
  placeholder marcat vizibil ca `TODO`. Stop.
- **Faza 3 — Conținut.** Case studies complete pentru cele trei proiecte,
  cu screenshot-urile și textele reale pe care le furnizez eu. Nu inventa
  cifre, nume de clienți sau testimoniale — dacă lipsește ceva, lasă
  `TODO: <ce lipsește>` și spune-mi. Stop.
- **Faza 4 — Verificare.** Rulează pragul de calitate din secțiunea 4
  punct cu punct și raportează ce trece și ce nu. Corectează ce nu trece.
  Apoi SEO, sitemap, robots.txt, imagine de preview.
- **Faza 5 — Deploy.** Instrucțiuni pas cu pas pentru Netlify.

## 7. Reguli pentru Claude Code

- Nu inventa conținut. Fără nume de clienți, cifre, testimoniale sau
  rezultate care nu mi-au fost date explicit. `TODO` e răspunsul corect
  când lipsește ceva.
- Nu adăuga secțiuni care nu sunt în specul ăsta fără să întrebi.
- Nu instala dependințe.
- Copy-ul se scrie ca material de design, nu ca decor: propoziții
  scurte, verbe active, specific în loc de inteligent. Un buton spune
  exact ce se întâmplă când e apăsat.
- La final de fiecare fază: ce ai făcut, ce ai decis și de ce, ce
  lipsește. Scurt.
