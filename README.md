# Birds API 🐦

A simple Flask REST API for managing and viewing birds, built with Flask, Flask-RESTful, SQLAlchemy, and Flask-Migrate. This project demonstrates basic CRUD-style read endpoints, database modeling, migrations, and seeding.

---

## 📁 Project Structure

```
.
├── .venv/            
└── migrations/         
│   ├── versions/
│   │   └── 5fe56f731e65_create_table_birds.py
│   ├── alembic.ini
│   ├── env.py
│   ├── README
│   └── script.py.mako
├── app.py              
├── models.py          
├── Pipfile
├── Pipfile.lock
├── requirements.txt
└── seed.py              

```

---

## 🧰 Tech Stack

* **Python 3**
* **Flask**
* **Flask-RESTful**
* **Flask-SQLAlchemy**
* **Flask-Migrate / Alembic**
* **PostgreSQL** (production database on Render; SQLite may be used locally)

---

## ⚙️ Local Setup (Optional)

### 1. Clone the repository

```bash
git clone git@github.com:P-RF/python-p4-deploying-a-flask-api-to-render.git
cd python-p4-deploying-a-flask-api-to-render
```

### 2. Install dependencies

Using Pipenv:

```bash
pipenv install
pipenv shell
```

Or using pip:

```bash
pip install -r requirements.txt
```

---

## 🗄️ Database Configuration (Local Development)

### 1. Set your database URI

Export a `DATABASE_URI` environment variable:

```bash
export DATABASE_URI=postgresql://<username>:<password>@<host>:<port>/<database_name>
```

For quick local testing, you may also use SQLite:

```bash
export DATABASE_URI=sqlite:///app.db
```

(PostgreSQL is used in production on Render.)

### 2. Run migrations

```bash
flask db upgrade
```

---

## 🌱 Seeding Sample Data (Optional)

Populate the database with sample bird data:

```bash
python seed.py
```

This will create the following birds:

* Black-Capped Chickadee
* Grackle
* Common Starling
* Mourning Dove

---

## 🚀 Running the Server

This project is deployed on **Render** for production, but you can run it locally in multiple ways depending on what you’re doing.

### 1️⃣ The Development Way (Recommended)

If you’re actively making changes, use Flask’s built-in development server. It includes the debugger and automatically reloads when you save files.

```bash
pipenv shell
export FLASK_APP=app.py
export FLASK_RUN_PORT=5555  # Optional, choose any port you like
flask run
```

The API will be available at:

```
http://localhost:5555
```

---

### 2️⃣ The Gunicorn Way (To Mimic Render)

To run the app locally the same way Render runs it (production-style server), use Gunicorn:

```bash
pipenv run gunicorn app:app
```

This is useful for catching deployment-related issues before pushing changes.

**Note:** If you did not add a SQLite fallback in your configuration, you may need to set the database URI manually:

```bash
export DATABASE_URI=sqlite:///app.db
```

---

### 3️⃣ The “Everything Is Broken” Way

If you open VS Code and nothing seems to work (commands not found, Flask won’t run, imports failing), these commands usually fix it:

```bash
pipenv install   # Rebuilds the virtual environment if it’s missing
pipenv shell     # Activates the environment so Flask & SQLAlchemy work
```

Once things are running again, use one of the methods above to start the server.

---

## 📡 API Endpoints

### Get all birds

```
GET /birds
```

**Response:**

```json
[
{
"id": 1,
"name": "Black-Capped Chickadee",
"species": "Poecile Atricapillus"
},
{
"id": 2,
"name": "Grackle",
"species": "Quiscalus Quiscula"
},
{
"id": 3,
"name": "Common Starling",
"species": "Sturnus Vulgaris"
},
{
"id": 4,
"name": "Mourning Dove",
"species": "Zenaida Macroura"
}
]
```

---

### Get a bird by ID

```
GET /birds/1
```

**Response:**

```json
{
  "id": 1,
  "name": "Black-Capped Chickadee",
  "species": "Poecile Atricapillus"
}
```

---

## 🧠 Notes

* This app is deployed on **Render** using Gunicorn as the production server.
* You can bookmark your **Render Dashboard** to:
  * View production logs
  * Trigger a **Manual Deploy** if GitHub doesn’t auto-sync
* Models use `SerializerMixin` for easy JSON serialization.
* Only `GET` endpoints are implemented (read-only API).
* Error handling for missing IDs can be added as an improvement.
* Models use `SerializerMixin` for easy JSON serialization.
* Only `GET` endpoints are implemented (read-only API).
* Error handling for missing IDs can be added as an improvement.

---

## ✨ Possible Extensions

* Add POST, PATCH, and DELETE endpoints
* Add validations and error handling
* Add testing with pytest
* Dockerize the application

---

## 🪶 Author

Built with Flask and birds in mind 🐤

Happy coding!
