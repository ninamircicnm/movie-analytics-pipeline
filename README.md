# movie-analytics-pipeline
**Movie popularity analysis integrating Kaggle IMDB dataset with OMDb API — data pipeline, SQLite database, REST API &amp; visualizations.**

---

## O projektu

Projekt provodi sustavnu analizu popularnosti filmova integracijom podataka iz dva heterogena izvora:
- **Kaggle dataset** — IMDB Top 1000 Movies and TV Shows
- **OMDb API** — Open Movie Database REST API

Obuhvaćen je cijeli data pipeline: prikupljanje, čišćenje, integracija, pohrana u bazu podataka, izlaganje podataka putem REST API-ja te vizualizacija i analiza.

---

## Tehnologije

| Kategorija | Alati |
|---|---|
| Jezik | Python 3 |
| Analiza podataka | pandas, numpy |
| Vizualizacija | matplotlib, seaborn |
| Baza podataka | SQLite, SQLAlchemy |
| API | Flask, pyngrok |
| Vanjski podaci | OMDb API, Kaggle |
| Okolina | Google Colab |

---

## Struktura projekta

```
movie-analytics-pipeline
 ┣ movie_analytics_pipeline.ipynb   # Glavna Colab bilježnica
 ┣ README.md                             # Ovaj dokument
 ┗.env.example                          # Primjer potrebnih varijabli okoline
```

---

## Pokretanje projekta

### Google Colab (preporučeno)

1. Otvori bilježnicu u Google Colabu
2. U lijevom izborniku klikni ikonu **Secrets**
3. Dodaj sljedeće tajne:

| Naziv | Opis |
|---|---|
| `OMDB_API_KEY` | API ključ s [omdbapi.com](http://www.omdbapi.com/) — besplatna registracija |
| `NGROK_TOKEN` | Auth token s [ngrok.com](https://ngrok.com/) — besplatna registracija |

4. Pokreni sve ćelije redom (**Runtime → Run all**)

### Lokalno pokretanje

```bash
# Kloniraj repozitorij
git clone https://github.com/ninamircicnm/movie-analytics-pipeline.git
cd movie-analytics-pipeline

# Instaliraj ovisnosti
pip install pandas numpy matplotlib seaborn requests sqlalchemy flask pyngrok kagglehub python-dotenv

# Postavi varijable okoline
cp .env.example .env
# Uredi .env datoteku i upiši svoje ključeve

# Pokreni bilježnicu u Jupyteru
jupyter notebook Projekt_movie.ipynb
```

---

## Što projekt radi

### 1. Prikupljanje podataka
- Automatsko preuzimanje Kaggle dataseta putem `kagglehub` biblioteke
- Dohvat dodatnih informacija za 200 filmova putem OMDb REST API-ja

### 2. Predprocesiranje i integracija
- Čišćenje podataka (konverzija tipova, uklanjanje jedinica, parsiranje)
- Integracija dvaju skupova prema naslovu filma
- Popunjavanje nedostajućih vrijednosti

### 3. Pohrana u bazu podataka
- SQLite baza s dvije tablice: `movies` i `movie_genres`
- Normalizacija podataka o žanrovima (jedan film → više žanrova)
- Testiranje baze s SQL upitima

### 4. REST API
- Flask server s ngrok tunelom
- Dostupni endpointovi:

| Endpoint | Opis |
|---|---|
| `GET /movies/{n}` | Prvih n filmova |
| `GET /stats` | Statistika baze |
| `GET /movie/{naslov}` | Pretraga po naslovu |
| `GET /top-rated/{n}` | Najbolje ocijenjeni filmovi |
| `GET /movies/year/{godina}` | Filmovi po godini |
| `GET /movies/genre/{žanr}` | Filmovi po žanru |
| `GET /movies/director/{ime}` | Filmovi po redatelju |
| `GET /movies/rating/{min}/{max}` | Filmovi u rasponu ocjena |

### 5. Analiza i vizualizacija
- Distribucija IMDb ocjena (histogram + box plot)
- Top 10 filmova prema ocjeni
- Trendovi filmske industrije po godinama
- Analiza popularnosti žanrova
- Korelacija Box Office zarade i IMDb ocjene
- Usporedba ocjena publike (IMDb) i kritičara (Metascore)
- Heatmap korelacije numeričkih varijabli

---

## Ključni zaključci

- Prosječna IMDb ocjena filmova u skupu iznosi **~8.4**
- Najzastupljeniji žanr po broju filmova je **Drama** (149/202 filmova)
- Najpopularniji žanr prema ocjenama publike je **Znanstvena fantastika**
- Filmska industrija bilježi **snažan rast od početka 21. stoljeća**
- **Visoka zarada ne jamči visoku ocjenu** — korelacija je slaba
- Publika i kritičari se često **ne slažu** — Metascore varira i za iste IMDb ocjene

---

## Literatura

1. H. Shankhdhar, *IMDB Dataset of Top 1000 Movies and TV Shows*, Kaggle, 2023. [Dataset](https://www.kaggle.com/datasets/harshitshankhdhar/imdb-dataset-of-top-1000-movies-and-tv-shows)
2. *The Open Movie Database*, OMDb API. [omdbapi.com](http://www.omdbapi.com/)

---

## Autorica

**Nina Mirčić** · [@ninamircicnm](https://github.com/ninamircicnm)

Projekt izrađen u sklopu kolegija *Programiranje za analizu podataka*, FOI, Varaždin.
