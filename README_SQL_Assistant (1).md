# 🧠 SQL Assistant GPT (FastAPI + Next.js + SQL Server)

Asistent AI conversațional care convertește limbaj natural în interogări SQL folosind GPT-4, le poate executa automat, cu protecție împotriva comenzilor periculoase, și salvează tot istoricul.

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
│   │   ├── orchestrator_router.py   # NLP → GPT Orchestrator
│   │   ├── execute_router.py        # Executare SQL cu validare
│   ├── services/
│   │   ├── query_orchestrator.py    # NLP routing logic
│   │   ├── prompt_builder.py        # Prompturi GPT pe baza schemei
│   │   ├── schema_service.py        # Extrage schema SQL Server
│   │   ├── sql_executor.py          # Execuție + protecție SQL
│   │   ├── query_logger.py          # Salvare istoric interogări
├── frontend/
│   ├── src/app/
│   │   ├── page.jsx
```

---

## 🚀 Funcționalități implementate

### ✅ Natural Language → SQL complet automatizat

- `/nlp`: Endpoint principal care:
  - Primește întrebarea în limbaj natural
  - Clasifică intenția (SELECT, INSERT, etc.)
  - Generează prompt pe baza schemei bazei de date
  - Apelează GPT-4 și returnează SQL-ul
  - Execută automat doar interogările SELECT

### ✅ Executare SQL cu protecție

- `/execute-sql`: endpoint dedicat care:
  - Validează dacă un query este sigur (ex. UPDATE fără WHERE = periculos)
  - Execută doar cu confirmare (`force=true`)

### ✅ Salvare automată a istoricului

- Tabel SQL `query_history` salvează:
  - Întrebarea în limbaj natural
  - SQL-ul generat
  - Tipul comenzii (SELECT, etc.)
  - Rezultatul execuției
  - Status și timestamp

---

## 🖥️ Exemple întrebări NLP

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
BASE_API_URL=http://localhost:8000
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
