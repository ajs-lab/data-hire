# DataHire — Data Engineering & AI Screening Platform
## Product Requirements Document (PRD)

> **Version:** 2.0 | **Updated:** February 2026 | **Target:** GitHub Pages (Free, Open Access)

---

## 1. Project Overview

**Product Name:** DataHire (or your chosen brand)

**Purpose:** A free, open-access, GitHub-publishable web platform for screening and hiring Data Engineers, AI/ML professionals, Data Architects, and BI specialists. The platform provides structured technical assessments, a live coding environment, an AI-generated question engine, and AI-powered candidate evaluation — all at no cost to users.

**Inspired by:** Teckiypad — a real-time collaborative coding interview platform with Python/SQL support and instant code execution.

**Distribution Model:** Free for all users. No paid tiers, no paywalls. Published openly on GitHub Pages.

**Target Users:**
- Hiring managers and technical recruiters
- Data Engineering leads screening candidates
- AI/ML team leads conducting technical interviews
- Data Architects and Solution Architects evaluating technical depth
- BI and Analytics leads hiring for Power BI, Fabric, and Databricks roles

---

## 2. Core Feature Modules

---

### Module 1: Home / Entry Page

A simple, functional entry page (not a marketing site). Purpose is to orient the user and navigate to tools quickly.

- Platform name, tagline, and brief one-line description of what the tool does
- Navigation links to all major sections: Question Bank, New Session, Dashboard, AI Question Generator
- No pricing tiers
- No testimonials or social proof sections
- No marketing copy or promotional content
- Footer with GitHub repo link and "Free & Open Source" label

---

### Module 2: Role-Specific Question Bank

A searchable, filterable library of curated interview questions across Data Engineering and AI/ML disciplines.

**Focus Areas — Data Engineering:**
- SQL: Window functions, CTEs, recursive queries, performance tuning, query optimization, joins, indexing
- Python: ETL logic, PySpark, pandas, data manipulation, file I/O, error handling
- Data Modeling: Star schema, snowflake schema, data vault, normalization (1NF–3NF), BCNF, denormalization trade-offs
- Dimension Modeling: Slowly Changing Dimensions (SCD Types 1–6), conformed dimensions, degenerate dimensions, junk dimensions, role-playing dimensions, fact table types (transaction, snapshot, accumulating)
- Pipeline Design: Batch vs. streaming, idempotency, orchestration (Airflow, Prefect, Dagster), fault tolerance, retry logic, backfill strategies
- Cloud Platforms: AWS (Glue, S3, Redshift, Lambda, Athena), GCP (BigQuery, Dataflow, Pub/Sub), Azure (ADF, Synapse, ADLS)
- Data Quality & Governance: Great Expectations, RBAC, data lineage, CDC, schema evolution, data contracts
- Big Data: Spark, Kafka, Hadoop, Delta Lake, Apache Iceberg, Apache Hudi

**Focus Areas — Databricks:**
- Databricks architecture: Control plane vs. data plane, clusters, jobs, workflows
- Delta Lake: ACID transactions, time travel, Z-ordering, OPTIMIZE, VACUUM
- Unity Catalog: Metastore setup, data governance, lineage tracking, permissions
- Databricks SQL: Warehouse types, query federation, Photon engine
- MLflow on Databricks: Experiment tracking, model registry, model serving endpoints
- Lakehouse design patterns using Databricks
- Autoloader and structured streaming on Databricks
- Databricks Asset Bundles (DABs) for CI/CD

**Focus Areas — Microsoft Fabric:**
- Fabric architecture: OneLake, workspaces, capacities, domains
- Lakehouse vs. Warehouse vs. Eventhouse in Fabric
- Data Factory in Fabric: Pipelines, dataflows Gen2, copy activity
- Fabric Notebooks: PySpark, Spark SQL, semantic link with Power BI datasets
- Real-time Intelligence: Eventstream, KQL Database, KQL Querysets
- Direct Lake mode: How it works, limitations, use cases vs. Import/DirectQuery
- Fabric mirroring: Supported sources, replication lag, use cases
- Shortcuts in OneLake: Cross-workspace, cross-cloud data access

**Focus Areas — Power BI:**
- Data modeling in Power BI: Relationships, cardinality, cross-filter direction
- DAX: Calculated columns vs. measures, context transition, CALCULATE, FILTER, iterators, time intelligence
- Power Query (M language): Transformations, custom functions, query folding
- Performance optimization: Aggregations, composite models, incremental refresh, query reduction
- Row-Level Security (RLS): Static vs. dynamic, OLS (Object-Level Security)
- Report design: Bookmarks, drillthrough, tooltips, field parameters
- Deployment pipelines, workspaces, and governance in Power BI Service
- Power BI Embedded and API integration

**Focus Areas — AI / ML Engineering:**
- ML System Design: Feature stores, model serving, inference pipelines, A/B testing frameworks
- Python / ML Frameworks: Scikit-learn, TensorFlow, PyTorch, Hugging Face
- LLM & GenAI: Prompt engineering, RAG pipelines, vector databases (Pinecone, Weaviate, pgvector), fine-tuning, RLHF
- MLOps: Model versioning (MLflow), CI/CD for ML, model monitoring, drift detection, shadow deployments
- Statistics & Math: Probability, distributions, hypothesis testing, linear algebra, gradient descent
- Data Structures & Algorithms (DS&A): Arrays, graphs, dynamic programming, complexity analysis

**Question Difficulty Levels:**
- Beginner | Intermediate | Advanced | Senior / Staff / Architect

**Question Types:**
- Multiple Choice (auto-graded)
- Coding Challenge (live execution)
- Open-ended / Scenario-based
- System Design Prompt
- Behavioral (STAR format)

---

### Module 3: AI Question Generator (New Core Feature)

Users can generate fresh, context-aware interview questions on demand using an LLM — no static bank required.

**Generator Inputs (form):**
- **Role:** Data Engineer / AI-ML Engineer / Data Architect / Databricks Engineer / Fabric Engineer / Power BI Developer / Solution Architect
- **Focus Area / Topic:** Free-text or dropdown (e.g., "Delta Lake", "DAX", "RAG Pipelines", "SCD Type 2", "Unity Catalog")
- **Difficulty:** Beginner / Intermediate / Advanced / Senior
- **Question Type:** Coding / Conceptual / System Design / Behavioral / Scenario-based
- **Number of Questions:** 1–10
- **Experience Level Context:** e.g., "3 years experience", "senior architect candidate"

**Generator Output:**
- Generated questions displayed as cards with full prompt text
- Each question card has:
  - "Add to Question Bank" button (saves to localStorage)
  - "Use in Session" button (opens interview room with this question)
  - "Regenerate" button (generates a variation)
  - Difficulty badge and topic tag (AI-assigned)
- Bulk generate: Generate a full interview set (e.g., "Generate a 5-question Data Engineering screening set for a mid-level candidate")

**LLM Integration:**
- User provides their own API key (Claude / OpenAI) via a Settings page — stored only in browser localStorage
- System prompt instructs the LLM to produce structured JSON output per question: `{ title, prompt, category, difficulty, type, hints[], sample_answer }`
- Generated questions are parsed and rendered dynamically
- No backend required; all API calls made client-side from the browser

---

### Module 4: Live Coding Environment (Core Feature)

A fully free, in-browser coding and SQL execution environment — no paid APIs or external sandboxes required.

- **Code Editor:** CodeMirror 6 (free, open-source, CDN-available — full syntax highlighting, autocompletion, line numbers, dark theme)
  - *Alternative:* Ace Editor (also free, CDN) if CodeMirror has load issues
  - Monaco Editor may also be used if loaded purely from CDN at no cost
- **Language Support:** Python, SQL, Markdown (for notes/design answers)
- **Python Execution:** Pyodide (Python compiled to WebAssembly — runs entirely in browser, 100% free, no server needed). Supports pandas, numpy, json, re, datetime
- **SQL Execution:** SQL.js (SQLite compiled to WebAssembly — runs entirely in browser, 100% free). Pre-loaded with sample DE datasets (employees, sales, orders, events tables)
- **Collaborative Mode:** Interviewer and candidate share a live session URL. Real-time sync via free-tier Supabase Realtime or Firebase Realtime Database (free tier)
- **Session Timer:** Configurable countdown (15 / 30 / 45 / 60 min), visible to both parties
- **Notes / Scratch Pad:** Markdown-enabled text area for candidate reasoning and whiteboard-style answers
- **Output Panel:** Shows stdout, errors, execution time, and SQL result tables

---

### Module 5: Screening Session Management

- **Create Session:** Interviewer selects role, topic, difficulty, duration, and picks or generates questions
- **Session URL / Token:** Auto-generated shareable link (e.g., `/interview.html?session=abc123`)
- **Session Recording:** Full log of all code submissions, outputs, and timestamps stored in localStorage / Supabase free tier
- **Interview Stages:**
  1. Phone Screen — behavioral and resume review (notes only)
  2. Technical Screen 1 — SQL / Python coding challenge
  3. Technical Screen 2 — system design or pipeline design
  4. Architecture Round — for senior/architect roles: data modeling, cloud design, governance
  5. Final Review — scoring summary and hiring recommendation
- **Session Notes:** Interviewer can annotate candidate responses in real time
- **Candidate Status Tracking:** Invited → In Progress → Completed → Reviewed → Decision Made

---

### Module 6: AI-Powered Evaluation

Uses the user-supplied LLM API key to evaluate candidate performance automatically.

- **Auto-Scoring:** Rates code submissions on correctness, efficiency, readability, and best practices (0–100 score)
- **AI Feedback Generator:** Returns structured feedback: strengths, gaps, suggested follow-up questions
- **Behavioral Q&A Analysis:** Evaluates STAR-format text answers with AI scoring on relevance, structure, and depth
- **Skill Gap Summary:** Post-session report identifying technical gaps per topic area
- **Code Quality Analysis:** Checks for edge cases, error handling, Pythonic patterns, SQL anti-patterns
- **Architecture Review Scoring:** For architect-level questions, AI evaluates trade-off reasoning, scalability thinking, and governance awareness
- **Cheating Detection Signals (basic):** Tab-switch count, unusual paste events, timing anomalies — flagged in session report

---

### Module 7: Candidate Portal

- **Access Flow:** Candidate receives session link → enters name → begins session (no account required for candidates)
- **Practice Mode:** Open-access practice area with sample DE and AI questions, free to use without a session invite
- **Session History:** Candidates who use a consistent browser can view their past submissions via localStorage
- **Profile (optional):** Name, target role, LinkedIn URL — saved locally, used to personalize AI feedback

---

### Module 8: Interviewer / Admin Dashboard

- **Overview Metrics:** Active sessions, completed interviews, average score by role/topic
- **Candidate Pipeline View:** Kanban-style board (Screening → Technical Round → Architecture Round → Offer → Rejected)
- **Question Bank Manager:** Add, edit, tag, delete questions; bulk-import from AI Generator
- **Session Scheduler:** Calendar view with upcoming sessions (stored in localStorage / Supabase free tier)
- **Report Export:** PDF or CSV export of candidate session results

---

## 3. User Roles & Permissions

| Role              | Capabilities                                                                          |
|-------------------|---------------------------------------------------------------------------------------|
| Admin             | Full access: question bank, user management, settings, session history                |
| Interviewer       | Create/run sessions, generate AI questions, view reports, add notes                   |
| Data Architect    | Create architecture-round sessions, evaluate system design answers                    |
| Reviewer          | View completed sessions and scores, leave written feedback                            |
| Candidate         | Access assigned sessions, submit code and answers, view feedback if enabled           |

---

## 4. Tech Stack — Free & Open Source Only

All tools are free, open-source, or have permanent free tiers sufficient for this use case.

| Layer              | Technology                                                      | Cost   |
|--------------------|-----------------------------------------------------------------|--------|
| Frontend           | HTML5 + CSS3 + Vanilla JavaScript                               | Free   |
| Code Editor        | CodeMirror 6 (CDN) or Ace Editor (CDN)                          | Free   |
| Python Execution   | Pyodide v0.24+ (WebAssembly, CDN)                               | Free   |
| SQL Execution      | SQL.js v1.10+ (WebAssembly, CDN)                                | Free   |
| AI Question Gen    | User-supplied Claude API or OpenAI API key (client-side fetch)  | User's own key |
| AI Evaluation      | User-supplied Claude API or OpenAI API key (client-side fetch)  | User's own key |
| Real-time Sync     | Supabase Realtime (free tier) or Firebase RTDB (free Spark plan)| Free   |
| Persistent Storage | Supabase PostgreSQL (free tier, 500MB) or localStorage          | Free   |
| Auth               | Supabase Auth (free tier) or no-auth (link-based sessions)      | Free   |
| Hosting            | GitHub Pages                                                    | Free   |

> **Note on API Keys:** The platform requires users to supply their own LLM API key (Anthropic Claude or OpenAI). Keys are stored only in the user's browser localStorage and are never transmitted to any server other than the LLM provider directly. The platform itself does not charge for or proxy these calls.

---

## 5. Page Structure / Sitemap

```
/index.html                  ← Home / Entry page (no marketing)
/questions.html              ← Question bank with filters and search
/generate.html               ← AI Question Generator
/interview.html?session=ID   ← Live coding room
/practice.html               ← Open-access candidate practice area
/dashboard.html              ← Interviewer dashboard
/settings.html               ← API key config, preferences
/README.md                   ← GitHub repo description and setup guide
```

---

## 6. Sample Question Coverage by Domain

### Data Modeling / Dimension Modeling
- Design a star schema for an e-commerce order management system
- Implement SCD Type 2 for a customer address table using SQL
- When would you choose a data vault over a star schema?
- Explain the difference between a degenerate dimension and a junk dimension
- Design a snapshot fact table for tracking daily inventory levels

### Databricks
- How does Delta Lake ensure ACID compliance on object storage?
- Explain Unity Catalog's three-level namespace and permission model
- When would you use Autoloader vs. a COPY INTO command in Databricks?
- What is Z-Ordering and when does it improve query performance?
- Design a Lakehouse medallion architecture (Bronze/Silver/Gold) for a retail analytics use case

### Microsoft Fabric
- Explain the difference between a Fabric Lakehouse and a Fabric Warehouse
- What is Direct Lake mode and how does it differ from Import mode in Power BI?
- How does Fabric Mirroring work and which sources does it currently support?
- Describe a use case for OneLake Shortcuts across cloud providers
- Design a real-time analytics solution using Fabric Eventstream and KQL Database

### Power BI / DAX
- Write a DAX measure for rolling 12-month revenue using DATESINPERIOD
- What is context transition and how does CALCULATE trigger it?
- Explain query folding in Power Query and why it matters for performance
- Design a Row-Level Security model for a multi-region sales dashboard
- When would you use a composite model vs. a pure DirectQuery model?

### SQL
- Write a SQL query to find the second highest salary without LIMIT/OFFSET
- Using window functions, calculate a 7-day rolling average of daily sales by region
- Write a recursive CTE to traverse an employee org chart
- Optimize a slow query against a 500M-row fact table (index strategy, partitioning)

### AI / ML
- Design a RAG pipeline for a company document Q&A system
- How do you detect and respond to feature drift in production?
- Explain the trade-offs between fine-tuning an LLM vs. using RAG
- Design a CI/CD pipeline for an ML model from commit to production

---

## 7. AI Question Generator — Prompt Design

The generator sends a structured prompt to the LLM API and parses the JSON response.

**System Prompt Template:**
```
You are a senior technical interviewer specializing in Data Engineering, AI/ML, 
Databricks, Microsoft Fabric, Power BI, and Data Architecture. 

Generate {n} interview question(s) for a {role} candidate at {difficulty} level, 
focused on: {topic}. The candidate has approximately {experience}.

For each question, return valid JSON with this structure:
{
  "title": "Short question title",
  "prompt": "Full question text with context and requirements",
  "category": "Topic category",
  "difficulty": "Beginner|Intermediate|Advanced|Senior",
  "type": "Coding|Conceptual|System Design|Behavioral|Scenario",
  "hints": ["hint 1", "hint 2"],
  "sample_answer": "A strong answer would cover..."
}

Return only a JSON array. No prose, no markdown fences.
```

---

## 8. Non-Functional Requirements

- **Performance:** Page load < 2s; Pyodide init < 5s (one-time); code execution < 3s
- **Accessibility:** WCAG 2.1 AA compliance; keyboard navigable; sufficient color contrast
- **Mobile Responsive:** Desktop-first; tablet-usable; mobile view for reading questions
- **Security:** API keys stored only in localStorage, never logged or transmitted to platform servers; no sensitive candidate PII stored server-side without consent
- **Privacy:** GDPR-aware design; candidate data deletable on demand; no third-party analytics by default
- **Availability:** Static hosting on GitHub Pages = 99.9%+ uptime with zero infrastructure cost
- **Open Source:** Full source code on GitHub; MIT license; contributions welcome

---

## 9. MVP Scope (GitHub Pages Launch)

Priority features for first public release:

1. ✅ Home / entry page with navigation (no marketing content)
2. ✅ Question bank with filters — DE, Databricks, Fabric, Power BI, AI/ML, Data Modeling
3. ✅ AI Question Generator (user API key, 1–10 questions, structured JSON output)
4. ✅ Live coding editor (CodeMirror/Ace) with Python via Pyodide + SQL via SQL.js
5. ✅ Session creation with shareable URL
6. ✅ AI evaluation of code submissions (user API key)
7. ✅ Candidate result summary page with skill gap breakdown
8. ✅ localStorage-based session and question storage
9. ✅ Settings page for API key management

---

## 10. Future Enhancements (V2+)

- AI interviewer bot — fully automated end-to-end screening with no human needed
- Video recording and AI transcription of verbal answers
- Resume / JD parser: match candidate resume to role requirements automatically
- Role rubric builder: custom scoring criteria per team or company
- Multi-language code support: Scala, Go, R for niche DE/DS roles
- Candidate benchmarking: compare score against anonymized cohort averages
- Slack / Teams integration for session notifications
- Export to PDF: full candidate interview report with AI summary

---

*Document Version: 2.0 | Free & Open Access | Target: GitHub Pages*
