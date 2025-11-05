# Django Production Template

Produkcijski Django template projekat sa konfiguracijom za development i production okruženje.

## 📋 Opis

Ovaj template projekat je pripremljen za brzi start novih Django projekata sa prekonfigurisanim:
- ✅ Podeljenim settings fajlovima (local/production)
- ✅ PostgreSQL podrškom za produkciju
- ✅ SQLite za lokalni development
- ✅ Gunicorn konfiguracijom za produkciju
- ✅ Docker konfiguracijom
- ✅ Environment varijablama za sigurnost

## 🚀 Brzi Start

Za detaljna uputstva o inicijalizaciji projekta, pogledaj **[SETUP.md](SETUP.md)**.

### Minimalni koraci:

1. **Kloniraj ili kopiraj template:**
   ```bash
   git clone <repository-url>
   cd django_prod_template
   ```

2. **Kreiraj virtualno okruženje:**
   ```bash
   python -m venv venv
   source venv/Scripts/activate  # Windows Git Bash
   # ili
   source venv/bin/activate      # Linux/Mac
   ```

3. **Instaliraj zavisnosti:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Primeni migracije:**
   ```bash
   python manage.py migrate
   ```

5. **Pokreni server:**
   ```bash
   python manage.py runserver
   ```

Aplikacija će biti dostupna na **http://127.0.0.1:8000/**

## 🛠️ Tehnologije

- **Django 5.0.3** - Web framework
- **PostgreSQL** (psycopg2-binary) - Produkcijska baza podataka
- **SQLite** - Development baza podataka
- **Gunicorn** - WSGI HTTP Server za produkciju
- **Docker** - Containerizacija

## 📦 Zavisnosti

```
asgiref==3.7.2
Django==5.0.3
gunicorn==21.2.0
packaging==24.0
psycopg2-binary==2.9.9
sqlparse==0.4.4
```

## 📁 Struktura Projekta

```
django_prod_template/
├── manage.py                    # Django management script
├── requirements.txt             # Python zavisnosti
├── Dockerfile                   # Docker konfiguracija
├── SETUP.md                     # Detaljna uputstva za inicijalizaciju
├── django_prod_template/        # Glavni projekat folder
│   ├── urls.py                  # URL konfiguracija
│   ├── wsgi.py                  # WSGI konfiguracija
│   ├── asgi.py                  # ASGI konfiguracija
│   └── settings/                 # Settings folder
│       ├── __init__.py           # Određuje koji settings koristiti
│       ├── local.py              # Development settings (SQLite)
│       └── production.py        # Production settings (PostgreSQL)
└── venv/                        # Virtualno okruženje (kreira se)
```

## ⚙️ Settings Konfiguracija

### Development (Default)
- Automatski koristi `settings/local.py`
- **Database:** SQLite
- **DEBUG:** True
- Nije potrebna dodatna konfiguracija

### Production
- Postavi environment varijablu: `PIPELINE=production`
- Koristi `settings/production.py`
- **Database:** PostgreSQL
- Zahteva environment varijable:
  - `SECRET_KEY`
  - `HOST`
  - `DB_NAME`, `DB_USER_NM`, `DB_USER_PW`, `DB_IP`, `DB_PORT`

## 📚 Dokumentacija

- **[SETUP.md](SETUP.md)** - Kompletna uputstva za inicijalizaciju projekta
  - Koraci za pokretanje
  - Settings konfiguracija
  - Korisne Django komande
  - Rešavanje problema
  - Checklist za novi projekat

## 🐳 Docker

Projekat uključuje Dockerfile za containerizaciju:

```bash
docker build -t django-prod-template .
docker run -p 8080:8080 -e PIPELINE=production django-prod-template
```

## 🔐 Bezbednost

- Secret key se čuva u environment varijablama (produkcija)
- Podeljeni settings fajlovi za različita okruženja
- PostgreSQL za produkciju (ne SQLite)
- Gunicorn za produkciju (ne development server)

## 📝 Napomene

- Ovaj template je pripremljen za produkciju i development
- Settings se automatski prebacuju između local/production
- SQLite se koristi samo za development
- Sve environment varijable moraju biti postavljene za produkciju

## 🤝 Korišćenje Template-a

1. Kloniraj ili preuzmi ovaj template
2. Preimenuj projekat (ako je potrebno)
3. Primeni prilagođavanja po potrebi
4. Zaprati uputstva u **[SETUP.md](SETUP.md)** za inicijalizaciju

## 📄 Licenca

Prilagodljivo za ličnu i komercijalnu upotrebu.

---

**Za detaljna uputstva, pogledaj [SETUP.md](SETUP.md)**
