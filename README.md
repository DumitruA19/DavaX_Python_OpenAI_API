# 🧠 SQL Assistant GPT (FastAPI + Next.js + SQL Server)

**SQL Assistant GPT** is a full-stack AI-powered conversational assistant that translates natural language into SQL queries using OpenAI's GPT-4. It executes safe queries automatically, protects against dangerous commands (e.g., `UPDATE` without `WHERE`), and logs the full interaction history.

---

## ⚙️ Tech Stack

- **Backend**: Python, FastAPI, Uvicorn, pyodbc, OpenAI GPT API
- **Frontend**: Next.js (App Router), Tailwind CSS
- **Database**: Microsoft SQL Server

---

## 📁 Project Structure

```
sql-assistant-gpt/
├── backend/
│   ├── main.py                      # Entry point for FastAPI
│   ├── models.py                    # SQLAlchemy or Pydantic models
│   ├── routes/                      # API route handlers
│   │   ├── orchestrator_router.py  # Main NLP endpoint
│   │   ├── execute_router.py       # Query execution handler
│   ├── services/                    # Core business logic
│   │   ├── schema_service.py       # DB schema extraction
│   │   ├── prompt_builder.py       # GPT prompt generation
│   │   ├── query_orchestrator.py   # Intent classification
│   │   ├── sql_executor.py         # SQL safety and execution
│   │   ├── query_logger.py         # Logs to DB
│   ├── prompts/                    # Custom prompt templates
├── frontend/
│   ├── src/app/                    # Next.js frontend routes
│   │   ├── page.jsx                # Main homepage
│   │   ├── ask/page.jsx            # Natural language to SELECT
│   │   ├── ddl/page.jsx            # CREATE TABLE / ALTER
│   │   ├── insert-gpt/page.jsx     # Insert random data
│   │   ├── sql-gpt/page.jsx        # Full SQL interface
```

---

## 🚀 Key Features

### ✅ 1. Natural Language → SQL Conversion

- `/ask`: Generate **SELECT** queries using GPT-4
- `/ddl`: Generate **DDL** statements (CREATE TABLE, ALTER)
- `/insert-smart`: Insert synthetic/random data into real tables
- `/update-smart`: Update operations via GPT (with confirmation)
- `/delete-smart`: Generate DELETE queries safely

### ✅ 2. Safe SQL Execution with Validation

- `/execute-sql`: Executes any SQL only after safety checks
  - Example: Detects `UPDATE` or `DELETE` without `WHERE`
  - Requires manual confirmation (`force=true`) for execution

### ✅ 3. Dynamic Schema Extraction

- Queries SQL Server's `INFORMATION_SCHEMA.COLUMNS`
- Automatically builds prompt context based on real table structures

### ✅ 4. Interactive Frontend UI

- `/ddl`: Create tables via GPT-generated SQL
- `/insert-gpt`: Generate fake/random INSERTs
- `/sql-gpt`: Unified SQL interface for Select / Update / Delete
- Modal prompts for query confirmation before execution

### ✅ 5. Query Logging

- Logs are stored in a SQL table `query_history`, including:
  - Natural language question
  - Generated SQL
  - Query type (SELECT, INSERT, etc.)
  - Execution result
  - Status and timestamps

---

## 💬 Example Prompts

```
- Show all active projects
- Create a table called `clients` with name, email, and phone
- Insert 10 random users
- Update the status of project 5 to "completed"
- Delete all projects where status = "test"
```

---

## 🔐 Backend `.env` Configuration

Create a `.env` file inside the `backend/` directory:

```env
OPENAI_API_KEY=sk-xxxxx
SQLSERVER_CONN_STR=DRIVER={ODBC Driver 17 for SQL Server};SERVER=localhost;DATABASE=AssistantDemo;UID=sa;PWD=your_password
BASE_API_URL=http://localhost:8000
```

---

## 🌐 Frontend `.env.local` Configuration

Create a `.env.local` file inside the `frontend/` directory:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## ▶️ Running the Project Locally

### 🔹 Start Backend (FastAPI)

```bash
cd backend
python -m venv venv
venv\Scripts\activate           # or source venv/bin/activate on Linux/Mac
pip install -r requirements.txt
uvicorn main:app --reload
```

### 🔹 Start Frontend (Next.js)

```bash
cd frontend
npm install
npm run dev
```

---

## 📡 Backend API Routes Summary

| Method | Endpoint        | Description                          |
|--------|------------------|--------------------------------------|
| POST   | `/ask`           | Generate SELECT via GPT              |
| POST   | `/ddl`           | Generate CREATE TABLE via GPT        |
| POST   | `/insert-smart`  | Insert random data via GPT           |
| POST   | `/update-smart`  | Generate UPDATE statements           |
| POST   | `/delete-smart`  | Generate DELETE statements           |
| POST   | `/execute-sql`   | Executes dangerous SQL (with confirm)|

---

## 🧩 Future Enhancements

- 🧾 Full query history viewer
- 🔐 Authentication & role-based access
- 📊 Dynamic ERD generation from schema
- 💡 Auto-form generator based on table structure
- 🧠 GPT-powered data analysis + aggregation
- 📤 Export to CSV or Excel

---

## 📜 License

This project is open-source under the MIT License.
