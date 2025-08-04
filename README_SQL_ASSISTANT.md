# 🧠 SQL Assistant GPT (FastAPI + Next.js + SQL Server)

Asistent AI conversațional pentru generare, executare și explicare de interogări SQL folosind GPT-4 și schema bazei de date reale.

---

## ⚙️ Tehnologii folosite

- **Backend**: Python, FastAPI, Uvicorn, pyodbc, OpenAI GPT
- **Frontend**: Next.js (App Router), Tailwind CSS
- **Database**: Microsoft SQL Server

---

## 📁 Structură principală

```
sql-assistant-gpt/
├── backend/
│   ├── main.py
│   ├── routes/
│   ├── services/
│   ├── prompts/
│   ├── models.py
├── frontend/
│   ├── src/app/
│   │   ├── page.jsx
│   │   ├── ask/page.jsx
│   │   ├── ddl/page.jsx
│   │   ├── insert-gpt/page.jsx
│   │   ├── sql-gpt/page.jsx
```

---

## 🚀 Funcționalități implementate

### ✅ 1. Natural Language → SQL

- `/ask`: GPT generează interogări SELECT
- `/ddl`: GPT generează CREATE TABLE / ALTER
- `/insert-smart`: GPT inserează automat date în tabele existente

### ✅ 2. Comenzi GPT cu execuție automată

- `/update-smart`: GPT generează UPDATE
- `/delete-smart`: GPT generează DELETE
- `/execute-sql`: execută manual SQL periculos confirmat din frontend

### ✅ 3. Extragere dinamică a schemei bazei de date

- Serviciul `schema_service.py` interoghează `INFORMATION_SCHEMA.COLUMNS`
- Prompturile GPT se generează automat pe baza structurii reale

### ✅ 4. Frontend interactiv

- `/ddl`: creezi tabele prin GPT
- `/insert-gpt`: inserezi date random
- `/sql-gpt`: interfață completă Select / Update / Delete
- Modal UI pentru confirmare executare query periculos

---

## 🧠 Exemple întrebări în limbaj natural

```
- Afișează toate proiectele active
- Creează un tabel clients cu nume, email, telefon
- Inserează 10 utilizatori random
- Actualizează statusul proiectului 5 în „finalizat”
- Șterge proiectele cu status „test”
```

---

## 🔌 Configurare `.env` în backend

```
OPENAI_API_KEY=sk-xxxxx
SQLSERVER_CONN_STR=DRIVER={ODBC Driver 17 for SQL Server};SERVER=localhost;DATABASE=AssistantDemo;UID=sa;PWD=parola
```

---

## 🖥️ Configurare `.env.local` în frontend

```
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## ▶️ Pornire proiect

### 🔹 Backend

```bash
cd backend
venv\Scripts\activate
uvicorn main:app --reload
```

### 🔹 Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## ✅ Rute backend disponibile

| Metodă | Endpoint          | Descriere                          |
|--------|-------------------|------------------------------------|
| POST   | /ask              | GPT SELECT                         |
| POST   | /ddl              | GPT DDL (CREATE TABLE)             |
| POST   | /insert-smart     | GPT INSERT                         |
| POST   | /update-smart     | GPT UPDATE                         |
| POST   | /delete-smart     | GPT DELETE                         |
| POST   | /execute-sql      | Execută SQL periculos confirmat    |

---

## 📚 Extensii posibile

- 🧾 Istoric interogări cu salvare în DB
- 🔍 Vizualizare ERD dinamică
- 🔐 Login & roluri
- 💡 Auto-form generator pe baza tabelei (pentru frontend)

---

