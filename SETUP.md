# Uputstvo za Inicijalizaciju Django Projekta

## 📋 Pregled Projekta

Ovaj Django projekat koristi:
- **Django 5.0.3**
- **PostgreSQL** za produkciju (psycopg2-binary)
- **SQLite** za lokalni development
- **Gunicorn** za produkciju
- Podeljene settings konfiguracije (local/production)

## 🚀 Koraci za Inicijalizaciju

### 1. Kreiranje Virtualnog Okruženja (ako već ne postoji)

```bash
python -m venv venv
```

### 2. Aktivacija Virtualnog Okruženja

**Na Windows (Git Bash):**
```bash
source venv/Scripts/activate
```

**Na Windows (PowerShell):**
```powershell
venv\Scripts\Activate.ps1
```

**Na Windows (CMD):**
```cmd
venv\Scripts\activate.bat
```

**Na Linux/Mac:**
```bash
source venv/bin/activate
```

### 3. Instalacija Zavisnosti

```bash
pip install -r requirements.txt
```

**Zavisnosti u projektu:**
- `asgiref==3.7.2`
- `Django==5.0.3`
- `gunicorn==21.2.0`
- `packaging==24.0`
- `psycopg2-binary==2.9.9`
- `sqlparse==0.4.4`

### 4. Provera Django Instalacije

```bash
python manage.py --version
```

Očekivani output: `5.0.3`

### 5. Primena Migracija

Migracije kreiraju tabele u bazi podataka za Django admin, autentifikaciju, sesije, itd.

```bash
python manage.py migrate
```

**Šta se dešava:**
- Kreira se `db.sqlite3` fajl (ako ne postoji)
- Primene se migracije za: `admin`, `auth`, `contenttypes`, `sessions`

### 6. Kreiranje Superuser-a (Opciono)

Superuser je potreban za pristup Django admin panelu.

```bash
python manage.py createsuperuser
```

**Unesi:**
- Username
- Email (opciono)
- Password (2 puta)

### 7. Pokretanje Development Servera

```bash
python manage.py runserver
```

**Server će biti dostupan na:**
- http://127.0.0.1:8000/
- http://localhost:8000/

**Zaustavljanje servera:**
- Pritisni `CTRL+C` ili `CTRL+BREAK` u terminalu

### 8. Dodatne Opcije za Pokretanje Servera

**Pokretanje na specifičnom portu:**
```bash
python manage.py runserver 8080
```

**Pokretanje na svim IP adresama (dostupno iz mreže):**
```bash
python manage.py runserver 0.0.0.0:8000
```

## ⚙️ Settings Konfiguracija

### Development (Local)

Projekat automatski koristi `settings/local.py` za development:
- **Database:** SQLite (`db.sqlite3`)
- **DEBUG:** `True`
- **ALLOWED_HOSTS:** `[]`

### Production

Za produkciju, postavi environment varijablu:
```bash
export PIPELINE=production
```

Ili na Windows:
```bash
set PIPELINE=production
```

**Potrebne environment varijable za produkciju:**
- `SECRET_KEY` - Django secret key
- `HOST` - Allowed host
- `DB_NAME` - PostgreSQL database name
- `DB_USER_NM` - PostgreSQL username
- `DB_USER_PW` - PostgreSQL password
- `DB_IP` - PostgreSQL host
- `DB_PORT` - PostgreSQL port

## 📁 Struktura Projekta

```
django_prod_template/
├── manage.py                 # Django management script
├── requirements.txt          # Python zavisnosti
├── db.sqlite3               # SQLite baza (development)
├── venv/                    # Virtualno okruženje
├── django_prod_template/    # Glavni projekat folder
│   ├── __init__.py
│   ├── urls.py              # URL konfiguracija
│   ├── wsgi.py              # WSGI konfiguracija
│   ├── asgi.py              # ASGI konfiguracija
│   └── settings/            # Settings folder
│       ├── __init__.py      # Određuje koji settings koristiti
│       ├── local.py         # Development settings
│       └── production.py    # Production settings
└── Dockerfile               # Docker konfiguracija
```

## 🔍 Korisne Django Komande

### Provera Statusa Migracija
```bash
python manage.py showmigrations
```

### Kreiranje Migracija (za custom apps)
```bash
python manage.py makemigrations
```

### Django Shell
```bash
python manage.py shell
```

### Collect Static Files (za produkciju)
```bash
python manage.py collectstatic
```

### Provera Projekta
```bash
python manage.py check
```

## 🐛 Rešavanje Problema

### Problem: "No module named 'django'"
**Rešenje:** Aktiviraj virtualno okruženje i instaliraj zavisnosti:
```bash
source venv/Scripts/activate
pip install -r requirements.txt
```

### Problem: "You have unapplied migrations"
**Rešenje:** Primeni migracije:
```bash
python manage.py migrate
```

### Problem: "Port already in use"
**Rešenje:** Koristi drugi port:
```bash
python manage.py runserver 8080
```

### Problem: "Database is locked" (SQLite)
**Rešenje:** Zatvori sve druge konekcije ka bazi ili restartuj server.

## ✅ Checklist za Novi Projekat

- [ ] Virtualno okruženje kreirano i aktivirano
- [ ] Sve zavisnosti instalirane (`pip install -r requirements.txt`)
- [ ] Migracije primenjene (`python manage.py migrate`)
- [ ] Superuser kreiran (`python manage.py createsuperuser`)
- [ ] Server pokrenut (`python manage.py runserver`)
- [ ] Aplikacija dostupna na http://127.0.0.1:8000/
- [ ] Admin panel dostupan na http://127.0.0.1:8000/admin/

## 📝 Napomene

- **SQLite** se koristi za development - nije potrebna dodatna konfiguracija
- **PostgreSQL** se koristi za produkciju - potrebno je postaviti environment varijable
- Settings se automatski prebacuju između local/production na osnovu `PIPELINE` varijable
- `db.sqlite3` fajl se automatski kreira pri prvom pokretanju migracija

