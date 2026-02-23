# Vodič za postavljanje repozitorija kolegija

## Zašto Quarto + GitHub Pages

Već radite u R-u, pa je Quarto put najmanjeg otpora. Službeni je nasljednik R Markdowna, održava ga Posit, a od `.qmd` i `.md` datoteka generira profesionalnu web stranicu s navigacijom, pretragom, tamnim modom i mobilnom responzivnošću bez ikakvih frontend alata. GitHub Pages hostira stranicu besplatno. Radni tok je jednostavan: napišite sadržaj u markdownu, renderirajte lokalno s `quarto render`, commitajte i pushajte, a GitHub Actions automatski izgradi stranicu. Bez poslužitelja, bez troškova hostinga, bez problema s deploymentom.

Claude Code idealan je pratilac za ovaj setup jer može scaffoldati datoteke, napisati sadržaj iz vaših bilješki, popraviti probleme s renderiranjem, upravljati git operacijama i ažurirati stranicu tjedan po tjedan kroz upute u prirodnom jeziku.

---

## Preduvjeti

Trebate četiri stvari instalirane na svom računalu prije početka.

**1. Quarto CLI**
Ako imate noviju verziju RStudija (2022.07+) već ga imate. Inače instalirajte s https://quarto.org/docs/get-started/. Provjerite s `quarto --version` u terminalu.

**2. R i rmarkdown**
Ovo već imate. Samo provjerite da je `install.packages("rmarkdown")` izvršeno.

**3. Git**
Provjerite s `git --version`. Ako nedostaje, instalirajte s https://git-scm.com/.

**4. GitHub račun**
Trebate GitHub račun i konfigurirane HTTPS vjerodajnice ili SSH ključ. Ako nikada niste pushali na GitHub sa svog računala, najlakši put je instalirati GitHub CLI (`gh`) i pokrenuti `gh auth login`.

**5. Claude Code**
Instalirajte s `npm install -g @anthropic-ai/claude-code`. Zahtijeva Node.js 18+. Ako nemate Node, instalirajte s https://nodejs.org/.

---

## Korak 1. Stvorite GitHub repozitorij

Možete to napraviti ručno na github.com ili pustiti Claude Code da to odradi.

### Opcija A. Claude Code (preporučeno)

Otvorite terminal, navigirajte do mjesta gdje želite projekt i pokrenite Claude Code.

```bash
cd ~/Projects  # ili gdje god držite repozitorije
claude
```

Zatim mu recite:

```
Stvori novi git repozitorij nazvan "web-tech-course" s Quarto website 
strukturom koja mi treba za sveučilišni kolegij. Inicijaliziraj git, 
stvori .gitignore za Quarto projekte i postavi GitHub Pages deployment 
putem GitHub Actions.
```

Claude Code će scaffoldati sve. Kada završi, recite mu:

```
Stvori novi javni repozitorij na GitHubu nazvan web-tech-course pod mojim 
računom i pushaj inicijalni commit.
```

### Opcija B. Ručno

```bash
mkdir web-tech-course
cd web-tech-course
git init
# kopirajte starter datoteke (isporučene uz ovaj vodič)
git add .
git commit -m "Inicijalna struktura stranice kolegija"
gh repo create web-tech-course --public --source=. --push
```

---

## Korak 2. Struktura repozitorija

Starter kit (datoteke isporučene uz ovaj vodič) ima sljedeću strukturu.

```
web-tech-course/
├── _quarto.yml              # Konfiguracija stranice (naslov, navigacija, tema, jezik)
├── index.qmd                # Početna stranica / pregled kolegija
├── syllabus.qmd             # Cjelokupni silabus
├── schedule.qmd             # Tjedni raspored s praćenjem statusa
├── lectures/
│   ├── _metadata.yml         # Zajedničke postavke za sve stranice predavanja
│   ├── week-01.qmd          # Bilješke za Tjedan 1
│   ├── week-02.qmd          # Tjedan 2 (predložak)
│   └── ...                   # Jedna datoteka po tjednu
├── resources/
│   ├── reading-list.qmd     # Organiziran popis literature s poveznicama
│   ├── tools.qmd            # Preporuke alata i tutorijali
│   └── datasets/            # Primjeri skupova podataka za vježbe analitike
├── projects/
│   └── practical-project.qmd # Upute za projekt i rubrika
├── assets/
│   ├── images/              # Slike za predavanja, dijagrami
│   └── slides/              # PDF ili reveal.js prezentacije
├── .github/
│   └── workflows/
│       └── publish.yml       # GitHub Actions deployment
├── .gitignore
├── styles.css                # Prilagođeni CSS
├── CLAUDE.md                 # Upute za Claude Code o konvencijama projekta
└── README.md
```

Ključne dizajnerske odluke.

**Jedna `.qmd` datoteka po predavanju.** To čini ažuriranja atomskima. Kada pripremate Tjedan 5, dirate samo `lectures/week-05.qmd`. Ništa drugo se ne mijenja.

**Datoteke `_metadata.yml`** postavljaju zadane vrijednosti (autor, format datuma, sadržaj) tako da individualne datoteke predavanja ostaju čiste.

**Datoteka `schedule.qmd`** djeluje kao živa nadzorna ploča. Svaki tjedan ažurirate jednostavnu tablicu kako biste označili što je obrađeno, povezali materijale i zabilježili promjene.

**Mapa `resources/`** raste tijekom semestra kako pronalazite dobre članke, alate i skupove podataka.

---

## Korak 3. Konfigurirajte GitHub Pages

GitHub Actions workflow (`.github/workflows/publish.yml`, isporučen u starter kitu) automatski to rješava. Nakon pusha, idite na svoj repozitorij na GitHubu, zatim Settings > Pages, i postavite izvor na "GitHub Actions". Stranica će biti aktivna na `https://vasekorisnickoime.github.io/web-tech-course/` unutar nekoliko minuta od svakog pusha.

---

## Korak 4. Tjedni radni tok s Claude Code

Ovdje se setup isplati. Svaki tjedan vaš radni tok izgleda ovako.

### Prije predavanja

Otvorite Claude Code u direktoriju repozitorija.

```bash
cd ~/Projects/web-tech-course
claude
```

Zatim mu dajte upute poput ovih.

```
Napiši bilješke za predavanje Tjedna 5 (No code i low code alati za 
komunikologe). Obradi Webflow, Notion, Airtable, Zapier, Make i Stripe 
integracije. Uključi praktične primjere relevantne za komunikacijske 
stručnjake koji grade odredišne stranice i automatizirane radne tokove. 
Dodaj placeholder mjesta za slike gdje bih trebao naknadno umetnuti 
screenshotove. Prati format uspostavljen u week-01.qmd.
```

Claude Code će stvoriti ili ažurirati `lectures/week-05.qmd` prateći postojeći obrazac.

### Nakon predavanja

```
Ažuriraj schedule.qmd kako bi Tjedan 5 bio označen kao završen. Dodaj 
bilješku da smo potrošili dodatno vrijeme na Zapier demonstracije i da 
ćemo nastaviti s Makeom sljedeći tjedan.
```

### Dodavanje resursa koje ste pronašli

```
Dodaj ova tri članka na popis literature pod sekciju "No code alati":
- [naslov i URL]
- [naslov i URL]
- [naslov i URL]
Također dodaj kratku anotaciju za svaki koja objašnjava zašto bi ga 
studenti trebali pročitati.
```

### Objava ažuriranja

```
Commitaj sve promjene s porukom "Dodane bilješke za Tjedan 5 i ažuriran 
raspored" i pushaj na GitHub.
```

GitHub Action pokreće se automatski i stranica se izgradi za otprilike 60 sekundi.

---

## Korak 5. Korištenje Coworka kao alternative

Ako preferirate ne koristiti terminal, Anthropicov Cowork desktop alat može obaviti iste zadatke. Cowork radi na vašim lokalnim datotekama, pa biste:

1. Usmjerili Cowork na vašu `web-tech-course` mapu.
2. Dali mu iste upute u prirodnom jeziku (napiši bilješke za predavanje, ažuriraj raspored, dodaj resurse).
3. Pregledali promjene koje predlaže.
4. Odobrili ih, zatim koristili preferirani Git klijent (RStudio Git okno, GitHub Desktop ili terminal) za commit i push.

Cowork je prikladniji ako želite vizualni korak pregleda prije nego promjene postanu javne. Claude Code je brži ako ste udobni s terminalskim radnim tokom.

---

## Korak 6. Savjeti za održavanje kvalitete tijekom semestra

**Koristite CLAUDE.md datoteku u korijenu repozitorija.** Ovo je markdown datoteka koja Claude Codeu govori o konvencijama projekta, tonu i strukturi. Već je uključena u starter kit. Claude Code automatski čita ovu datoteku i slijedit će ove konvencije u svakoj interakciji.

**Pregledajte lokalno prije pusha.** Pokrenite `quarto preview` u terminalu. Ovo otvara lokalni poslužitelj s automatskim osvježavanjem tako da možete pregledati izgled prije objave.

**Koristite grane za eksperimentalni sadržaj.** Ako želite izraditi nacrt nečega bez utjecaja na javnu stranicu, recite Claude Codeu da stvori granu, radi na njoj, pa spoji (merge) kada bude spremno.

**Označite ključne točke semestra.** Na kolokviju i kraju semestra stvorite git oznaku (`git tag v2026-kolokvij`) kako biste se uvijek mogli vratiti na točno stanje kolegija u ključnim momentima.

---

## Korak 7. Napredna poboljšanja (opcionalno, kasnije u semestru)

Ovo su stvari koje možete dodati kako se budete uhodavali s postavom.

**Reveal.js prezentacije izravno iz Quarta.** Umjesto izrade zasebnih PowerPoint datoteka, možete pisati slajdove u istom `.qmd` formatu i Quarto ih renderira kao interaktivne HTML prezentacije. Dodajte `format: revealjs` u YAML zaglavlje bilo koje datoteke.

**Ugrađeni R kod za demonstracije analitike.** Kada predajete tjedan o analitici, možete uključiti R code chunkove u bilješke s predavanja koje studenti mogu reproducirati. Quarto će ih izvršiti tijekom renderiranja i ugraditi rezultate.

**Funkcionalnost pretraživanja.** Quarto web stranice imaju ugrađenu pretragu. Omogućena je prema zadanim postavkama u starter konfiguraciji.

**Studentske predaje putem GitHuba.** Ako želite da studenti predaju rad putem GitHuba (dobra praksa za digitalnu pismenost), možete postaviti zasebni repozitorij gdje oni rade fork i šalju pull requestove.

**Prilagođena domena.** Ako sveučilište pruža poddomenu, možete je usmjeriti na GitHub Pages stranicu dodavanjem CNAME datoteke.

---

## Brzi pregled naredbi

| Zadatak | Claude Code uputa |
|---------|-------------------|
| Napiši novo predavanje | "Napiši bilješke za predavanje Tjedna N o [tema]. Prati postojeći format." |
| Ažuriraj raspored | "Označi Tjedan N kao završen u schedule.qmd." |
| Dodaj literaturu | "Dodaj [naslov, URL] na popis literature pod [sekcija]." |
| Popravi renderiranje | "Stranica se ne renderira ispravno. Provjeri _quarto.yml i popravi probleme." |
| Dodaj prezentaciju | "Stvori reveal.js prezentaciju za Tjedan N na temelju bilješki s predavanja." |
| Objavi | "Commitaj sve promjene s porukom '[opis]' i pushaj na main." |
| Pregled | "Pokreni quarto preview i reci mi ima li grešaka u renderiranju." |
| Semestralna snimka | "Označi trenutno stanje kao v2026-tjedan-N i pushaj oznaku." |
