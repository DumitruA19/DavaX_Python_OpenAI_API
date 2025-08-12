# 🧠 SQL Assistant GPT (FastAPI + Next.js + SQL Server)

**SQL Assistant GPT** is an advanced AI-powered assistant that transforms natural language into SQL queries using GPT-4, with full execution capabilities, secure access control, and intelligent data export. Built for developers, analysts, and power users, it enables seamless interaction with SQL Server databases—beyond simple SELECTs—supporting full DDL, DML, aggregation, validation, history tracking, and CSV export.

---

## ⚙️ Tech Stack

- **Backend**: Python, FastAPI, Uvicorn, pyodbc, OpenAI GPT API
- **Frontend**: Next.js (App Router), Tailwind CSS
- **Database**: Microsoft SQL Server
- **Authentication**: JWT-based auth & role system

---

## 📁 Project Structure

```
sql-assistant-gpt/
├── backend/
│   ├── main.py
│   ├── models.py
│   ├── routes/
│   ├── services/
│   ├── prompts/
├── frontend/
│   ├── src/app/
│   │   ├── page.jsx
│   │   ├── ask/page.jsx
│   │   ├── ddl/page.jsx
│   │   ├── insert-gpt/page.jsx
│   │   ├── sql-gpt/page.jsx
│   │   ├── login, register, dashboard (auth-enabled)
```

---

## 🚀 Features

### ✅ 1. Natural Language → Complex SQL

- Supports advanced analytical queries with **GROUP BY**, **HAVING**, **JOIN**, **ORDER**, **filters**, and **aggregation**
- Converts natural questions into optimized SQL using schema-aware prompt templates
- Query history viewer (UI)
### ✅ 2. Execute SQL with Safety & Confirmation

- Detects unsafe queries (`UPDATE`/`DELETE` without `WHERE`) and requires explicit confirmation
- Supports both automatic and manual query execution via `/execute-sql`

### ✅ 3. Full CRUD Support

- `/ask` → SELECT
- `/ddl` → CREATE, ALTER, DROP
- `/insert-smart` → INSERT with GPT-generated values
- `/update-smart` → UPDATE with validation
- `/delete-smart` → DELETE with filtering logic

### ✅ 4. CSV Export

- Execute a SQL query and download results as `.csv`
- Ideal for reporting, Power BI, or spreadsheet workflows

### ✅ 5. Schema Awareness

- Auto-scans schema (`INFORMATION_SCHEMA.COLUMNS`) and adapts GPT prompts accordingly
- Keeps assistant always in sync with real DB structure

### ✅ 6. Interactive Frontend UI

- Auth-protected interface for sending requests and browsing responses
- Role-based access for query execution, history view, and export tools
- Modal UI for confirmation before executing sensitive queries

### ✅ 7. Authentication & Authorization

- JWT-based login/register system
- Role support (e.g., Admin, Analyst, Viewer)
- Session persistence & secure endpoints

### ✅ 8. Logging & History

- Every interaction is logged into `query_history` table:
  - Natural input
  - Generated SQL
  - Type, status, timestamps
  - Result preview

---

## 💬 Example Prompts

```
- List total hours worked by each employee this month
- Create a table called clients with name, email, and phone
- Insert 50 random test users into the employees table
- Delete inactive users who haven’t logged in since 2024
- Export project budgets grouped by department into CSV
```

---

## 🔐 Backend `.env` Configuration

```env
OPENAI_API_KEY=sk-xxxxx
SQLSERVER_CONN_STR=DRIVER={ODBC Driver 17 for SQL Server};SERVER=localhost;DATABASE=AssistantDemo;UID=sa;PWD=your_password
JWT_SECRET_KEY=your_secret_key
```

---

## 🌐 Frontend `.env.local` Configuration

```env
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## ▶️ Run Locally

### 🔹 Backend

```bash
cd backend
python -m venv venv
venv\Scripts\activate           # or source venv/bin/activate on Linux/Mac
pip install -r requirements.txt
uvicorn main:app --reload
```

### 🔹 Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## 📡 Available API Routes

| Method | Endpoint         | Description                            |
|--------|------------------|----------------------------------------|
| POST   | `/ask`           | GPT SELECT + execution                 |
| POST   | `/ddl`           | GPT CREATE/ALTER TABLE                 |
| POST   | `/insert-smart`  | GPT INSERT generator                   |
| POST   | `/update-smart`  | GPT UPDATE with condition check        |
| POST   | `/delete-smart`  | GPT DELETE with filters                |
| POST   | `/execute-sql`   | Execute any SQL (with validation)      |
| POST   | `/export-csv`    | Run SQL and return `.csv` file         |
| POST   | `/auth/login`    | JWT login                              |

---

## 🧩 Roadmap Ideas

- 🔐 Role-based frontend with permissions
- 📊 Visual schema & ERD viewer
- 🧠 Smart GPT prompt refinement per user context
- 💡 Auto-form generator from schema
- 🧪 Query testing with sample data

---
