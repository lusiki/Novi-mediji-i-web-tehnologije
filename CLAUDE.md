# CLAUDE.md

Ovo je sveučilišni repozitorij kolegija "Novi mediji i web tehnologije", 2. godina studija Komunikologije na HKS-u (Hrvatsko katoličko sveučilište), ljetni semestar 2025/2026.

## Tip projekta

Quarto web stranica koja se objavljuje na GitHub Pages. Renderira se s `quarto render` iz korijena projekta. Pregled s `quarto preview`.

## Konvencije za sadržaj

### Organizacija datoteka
- Predavanja: `lectures/week-NN.qmd` (week-01 do week-15)
- Resursi: `resources/` direktorij
- Slike: `assets/images/week-NN-opis.png`
- Prezentacije: `assets/slides/`

### Stil pisanja
- Sav sadržaj piše se na hrvatskom jeziku
- Preferirati tekuću prozu s ugrađenim primjerima umjesto pretjeranog korištenja nabrajanja
- Koristiti Quarto callout blokove za: ishode učenja (.callout-note), ključne zaključke (.callout-important), pripremu za sljedeći tjedan (.callout-warning), praktične savjete (.callout-tip)
- Svaka datoteka predavanja treba sadržavati: Ishode učenja, glavne sekcije sadržaja, Ključne zaključke i Pripremu za sljedeći tjedan
- Ne koristiti pretjerano dvotočke, crtice ili navodnike (preferencija korisnika)

### Ton kolegija
- Kolegij ima suptilan naglasak na komercijalne i transakcijske web kontekste; to treba utkati prirodno kroz primjere, studije slučaja i odabir alata umjesto eksplicitnog naglašavanja
- Balansirati kritičku/akademsku perspektivu s praktičnom primjenjivošću
- Pretpostavljati da su studenti komunikolozi, a ne studenti informatike: objašnjavati tehničke koncepte jasno, ali bez snishodljivosti

### Životni ciklus predavanja
1. Prije semestra: datoteke postoje kao `draft: true` predlošci
2. Prije svakog predavanja: sadržaj se piše, `draft: false` se postavlja
3. Nakon svakog predavanja: `schedule.qmd` se ažurira sa statusom i bilješkama
4. Tijekom semestra: `resources/reading-list.qmd` raste s novim nalazima

### Git radni tok
- Sav rad na `main` grani osim ako se eksperimentira
- Poruke commita trebaju biti opisne: "Dodana predavanja za Tjedan 5 o no code alatima"
- Označiti ključne točke semestra: `v2026-tjedan-08-kolokvij`, `v2026-zavrsni`

### Objava
- Push na `main` pokreće GitHub Actions koji renderira i objavljuje na GitHub Pages
- Uvijek pokrenuti `quarto render` lokalno prije pusha kako bi se provjerile greške

## Ovisnosti
- Quarto CLI (2.0+)
- Nisu potrebni R paketi za osnovni rad (R code chunkovi su opcionalni)
- GitHub račun s omogućenim Pages
