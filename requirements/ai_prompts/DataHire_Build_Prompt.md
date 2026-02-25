# AI Prompt: Build DataHire — Data Engineering & AI Screening Platform
## (Copy & Paste into Claude, ChatGPT-4o, or Cursor AI)

---

## MASTER PROMPT

```
You are a senior full-stack developer and UX designer. Build me a complete, fully functional, single-file (or multi-file) web application for a technical hiring platform called **DataHire** focused on **Data Engineering and AI/ML roles**. The platform is inspired by Teckiypad, which offers real-time collaborative coding interviews with a Monaco code editor, Python & SQL execution, and instant output.

The entire site must be publishable to GitHub Pages. Use HTML, CSS (with CSS variables and no external CSS frameworks unless CDN-linked), and JavaScript. Use Monaco Editor via CDN, Pyodide for in-browser Python execution, and SQL.js for in-browser SQLite.

---

## BRAND & DESIGN

- **Name:** DataHire
- **Tagline:** "Screen Smarter. Hire Better. Built for Data & AI Teams."
- **Aesthetic:** Dark, modern, technical — deep navy/slate background (#0a0d12), teal accent (#00e5b0), orange accent (#ff6b35), white text. Think: terminal meets SaaS dashboard.
- **Fonts:** Use Google Fonts — "Syne" for headings, "IBM Plex Mono" for code/labels
- **Style:** Clean cards, subtle grid lines, glow effects on interactive elements

---

## PAGES TO BUILD

### 1. Landing Page (index.html)

Sections:
- **Header/Nav:** Logo "DataHire", links: Features, Questions, Pricing, Login, "Start Free" CTA button
- **Hero:** Large headline "The Interview Platform Built for Data & AI Hiring", sub-text, two CTA buttons: "Start a Session" and "Explore Question Bank". Background: animated CSS grid with subtle dot pattern.
- **How It Works:** 3-step horizontal flow — (1) Create Session → (2) Candidate Codes Live → (3) AI Evaluates
- **Feature Cards (6 cards):**
  1. 🖥️ Monaco Code Editor — VS Code-grade in-browser editor
  2. 🐍 Python Execution — Run Python instantly with Pyodide WASM
  3. 🗄️ SQL Sandbox — Execute SQL queries against sample datasets
  4. 🤖 AI Evaluation — Instant scoring and feedback via LLM
  5. 📋 Role-Specific Questions — DE & AI question bank with difficulty levels
  6. 🔗 Shareable Sessions — Send a link; candidate joins instantly
- **Question Topic Tags:** Visual tag cloud showing: SQL, Python, PySpark, Airflow, Kafka, Spark, dbt, Snowflake, BigQuery, LLMs, MLOps, RAG, Feature Stores, Data Modeling
- **Pricing Table:** Free (3 sessions/mo), Pro ($49/mo unlimited), Enterprise (custom)
- **Footer:** Links + "Built for Data Teams" tagline

---

### 2. Question Bank Page (questions.html)

- Filter bar: Role (Data Engineering / AI-ML), Difficulty (Beginner / Intermediate / Advanced / Senior), Type (Coding / SQL / System Design / Behavioral)
- Grid of question cards, each showing:
  - Question title
  - Category tag (SQL, Python, MLOps, etc.)
  - Difficulty badge (color coded)
  - Type icon
  - "Try It" button → opens coding room with that question pre-loaded
- Include at least 20 hardcoded questions across both roles using a JavaScript array

**Sample question data to include (JavaScript array):**
```js
const questions = [
  { id: 1, title: "Window Functions: Running Total", category: "SQL", difficulty: "Intermediate", type: "Coding", role: "Data Engineering", prompt: "Write a SQL query that calculates the running total of sales per region, ordered by date." },
  { id: 2, title: "PySpark Deduplication", category: "Python", difficulty: "Advanced", type: "Coding", role: "Data Engineering", prompt: "Given a PySpark DataFrame with event logs, remove duplicate events within a 5-minute window using watermarking and deduplication." },
  { id: 3, title: "Design a Real-Time Pipeline", category: "System Design", difficulty: "Senior", type: "System Design", role: "Data Engineering", prompt: "Design a real-time data pipeline ingesting 1M events/second from IoT devices with < 5s dashboard latency." },
  { id: 4, title: "SCD Type 2 Implementation", category: "Data Modeling", difficulty: "Intermediate", type: "Coding", role: "Data Engineering", prompt: "Write SQL to implement Slowly Changing Dimension Type 2 for a customer address table." },
  { id: 5, title: "ETL Pipeline in Python", category: "Python", difficulty: "Intermediate", type: "Coding", role: "Data Engineering", prompt: "Write a Python ETL function that reads a CSV, validates schema, deduplicates, and writes to Parquet." },
  { id: 6, title: "Batch vs Streaming", category: "Concepts", difficulty: "Beginner", type: "Behavioral", role: "Data Engineering", prompt: "Explain the difference between batch and streaming processing. Give a real-world use case for each." },
  { id: 7, title: "Feature Store Design", category: "ML System Design", difficulty: "Advanced", type: "System Design", role: "AI-ML", prompt: "Design a feature store for a recommendation system. Cover ingestion, storage, serving, and consistency." },
  { id: 8, title: "RAG Pipeline Architecture", category: "LLM / GenAI", difficulty: "Advanced", type: "System Design", role: "AI-ML", prompt: "Design a Retrieval-Augmented Generation (RAG) pipeline for a company knowledge base chatbot." },
  { id: 9, title: "Model Drift Detection", category: "MLOps", difficulty: "Intermediate", type: "Coding", role: "AI-ML", prompt: "Write a Python function that detects feature drift between a training dataset and production inference data using KL divergence." },
  { id: 10, title: "SQL: Second Highest Salary", category: "SQL", difficulty: "Beginner", type: "Coding", role: "Data Engineering", prompt: "Write a SQL query to find the second highest salary from an employee table without using LIMIT/OFFSET." },
  { id: 11, title: "Kafka Consumer in Python", category: "Python", difficulty: "Intermediate", type: "Coding", role: "Data Engineering", prompt: "Write a Python Kafka consumer that reads messages, validates JSON schema, and writes valid records to a PostgreSQL table." },
  { id: 12, title: "Airflow DAG Design", category: "Pipeline Design", difficulty: "Advanced", type: "Coding", role: "Data Engineering", prompt: "Write an Apache Airflow DAG that orchestrates a daily ETL: extract from S3, transform with Spark, load into Redshift." },
  { id: 13, title: "LLM Fine-tuning Strategy", category: "LLM / GenAI", difficulty: "Senior", type: "System Design", role: "AI-ML", prompt: "A company wants to fine-tune an LLM on proprietary legal documents. Walk through your approach: data prep, training, evaluation, deployment." },
  { id: 14, title: "Explain EXPLAIN ANALYZE", category: "SQL", difficulty: "Advanced", type: "Behavioral", role: "Data Engineering", prompt: "How do you use EXPLAIN ANALYZE in PostgreSQL to diagnose a slow query? Walk through a real example." },
  { id: 15, title: "Star Schema vs Snowflake", category: "Data Modeling", difficulty: "Beginner", type: "Behavioral", role: "Data Engineering", prompt: "What is the difference between a star schema and snowflake schema? When would you choose each?" },
  { id: 16, title: "Vector Database Selection", category: "LLM / GenAI", difficulty: "Intermediate", type: "Behavioral", role: "AI-ML", prompt: "Compare Pinecone, Weaviate, and pgvector for a production RAG use case. What factors influence your choice?" },
  { id: 17, title: "Data Quality Framework", category: "Data Governance", difficulty: "Intermediate", type: "Coding", role: "Data Engineering", prompt: "Write a Python class using Great Expectations to validate a DataFrame: non-null IDs, valid email format, revenue > 0." },
  { id: 18, title: "Describe a Pipeline Failure", category: "Behavioral", difficulty: "Beginner", type: "Behavioral", role: "Data Engineering", prompt: "Tell me about a time a data pipeline you owned failed in production. How did you detect it, respond, and prevent recurrence?" },
  { id: 19, title: "CI/CD for ML Models", category: "MLOps", difficulty: "Advanced", type: "System Design", role: "AI-ML", prompt: "Design a CI/CD pipeline for an ML model: from code commit to production deployment with automated testing and rollback." },
  { id: 20, title: "CDC with Debezium", category: "Pipeline Design", difficulty: "Advanced", type: "Coding", role: "Data Engineering", prompt: "Explain how Change Data Capture works. Write a config for Debezium to track changes from a MySQL orders table to Kafka." }
];
```

---

### 3. Live Interview Room (interview.html)

Layout: Split-panel view
- **Left Panel (40%):** Question display — title, prompt, difficulty badge, hints toggle, notes textarea for interviewer
- **Right Panel (60%):** Monaco Editor + Output panel

Features:
- Language selector: Python | SQL
- "Run Code" button → executes Python via Pyodide OR SQL via SQL.js
- Output panel shows stdout, errors, table results (for SQL)
- Timer (countdown from 30 min, configurable)
- "Evaluate with AI" button → sends code + question prompt to Claude/OpenAI API, returns:
  - Score (0-100)
  - Strengths
  - Weaknesses / Gaps
  - Suggested follow-up question
- Session ID shown in URL param (?session=abc123)
- "End Session" button → shows summary modal

**SQL Sample Database (preloaded in SQL.js):**
```sql
CREATE TABLE employees (id INT, name TEXT, department TEXT, salary INT, hire_date TEXT);
INSERT INTO employees VALUES (1,'Alice','Engineering',95000,'2020-01-15');
INSERT INTO employees VALUES (2,'Bob','Data',82000,'2019-06-01');
INSERT INTO employees VALUES (3,'Carol','ML',110000,'2021-03-22');
INSERT INTO employees VALUES (4,'Dave','Data',87000,'2018-11-05');
INSERT INTO employees VALUES (5,'Eve','Engineering',105000,'2022-07-30');

CREATE TABLE sales (id INT, region TEXT, amount DECIMAL, sale_date TEXT);
INSERT INTO sales VALUES (1,'North',1500.00,'2024-01-01');
INSERT INTO sales VALUES (2,'South',2300.00,'2024-01-01');
INSERT INTO sales VALUES (3,'North',1800.00,'2024-01-02');
INSERT INTO sales VALUES (4,'East',3100.00,'2024-01-02');
INSERT INTO sales VALUES (5,'South',2700.00,'2024-01-03');
```

---

### 4. Dashboard (dashboard.html)

- Stats cards: Active Sessions | Questions in Bank | Candidates Screened | Avg Score
- Recent Sessions table: Candidate name, role, date, score, status, actions
- Quick Actions: "New Session", "Browse Questions", "View Reports"
- Sidebar nav: Dashboard | Sessions | Question Bank | Candidates | Settings
- Use localStorage to persist sessions array

---

## TECHNICAL IMPLEMENTATION NOTES

1. **Monaco Editor:** Load from `https://cdnjs.cloudflare.com/ajax/libs/monaco-editor/0.44.0/min/vs/loader.min.js`

2. **Pyodide (Python in browser):**
```html
<script src="https://cdn.jsdelivr.net/pyodide/v0.24.1/full/pyodide.js"></script>
```
Load Pyodide async on page load. On "Run Code", call `pyodide.runPythonAsync(code)` and capture stdout.

3. **SQL.js (SQLite in browser):**
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/sql.js/1.10.2/sql-wasm.js"></script>
```
Initialize DB with sample tables. On "Run SQL", execute and render results as an HTML table.

4. **AI Evaluation:** 
- Add an "API Key" input in settings (stored in localStorage)
- Call `https://api.anthropic.com/v1/messages` with Claude claude-sonnet-4-6
- System prompt: "You are a senior technical interviewer evaluating a Data Engineering or AI/ML candidate. Given the question and their code, provide: score (0-100), 3 strengths, 3 gaps, 1 follow-up question. Respond in JSON."
- Display parsed JSON response in a styled results panel

5. **Session Management:** 
- Generate random 6-char session IDs
- Store sessions in localStorage as JSON array
- Session link format: `/interview.html?session=abc123&question=5`

6. **Navigation:** All pages share the same header/nav component (inline HTML)

---

## FILE STRUCTURE

```
/index.html        ← Landing page
/questions.html    ← Question bank with filters
/interview.html    ← Live coding room
/dashboard.html    ← Interviewer dashboard
/README.md         ← GitHub repo description
```

All CSS is inline `<style>` in each file. All JS is inline `<script>`. No build step required. Must work by just opening HTML files or serving via GitHub Pages.

---

## QUALITY STANDARDS

- Every page must look production-quality, not like a student project
- Dark theme throughout, consistent color variables
- Smooth CSS transitions on hover/click
- Loading spinners during code execution and AI evaluation
- Error states handled gracefully (show error in output panel)
- Responsive layout (desktop-first but readable on tablet)
- Accessible: proper ARIA labels, sufficient color contrast

---

Build all four HTML files completely. Do not truncate or summarize — output full working code.
```

---

## HOW TO USE THIS PROMPT

1. **Copy the prompt block above** (between the triple backticks)
2. **Paste it into Claude** (claude.ai) or **Cursor AI** or **ChatGPT-4o**
3. Ask for one file at a time if the output is too long:
   - "Build index.html from the prompt above"
   - "Now build questions.html"
   - "Now build interview.html"
   - "Now build dashboard.html"
4. Save each file into a folder, e.g. `/datahire/`
5. Push to GitHub and enable **GitHub Pages** from Settings → Pages → Deploy from `main` branch root

---

## QUICK GITHUB SETUP

```bash
mkdir datahire && cd datahire
git init
git add .
git commit -m "Initial DataHire platform"
gh repo create datahire --public --source=. --push
# Then go to GitHub repo → Settings → Pages → Branch: main → /root → Save
# Your site will be live at: https://yourusername.github.io/datahire/
```

---

*Prompt Version: 1.0 | Target: GitHub Pages Static Site*
