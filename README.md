# Karpin Chat

Natural Language SQL Analytics

A Java implementation that answers natural-language questions about electoral bond CSV data using LLM-based SQL generation.

> **Note:** This is an independent Java implementation and is not the original Summer School submission. Source files have not yet been uploaded to this repository.

---

## Overview

Karpin Chat lets you ask **natural-language questions** about a dataset of electoral bonds and receive SQL queries powered by a large language model. The application loads CSV data into an in-memory H2 database on startup and uses Spring JDBC to execute the generated queries.

### Tech Stack

| Component | Technology |
|---|---|
| Language | Java 17 |
| Framework | Spring Boot 3.3.2 |
| Database Access | Spring JDBC |
| Database | H2 (in-memory) |
| CSV Parsing | Apache Commons CSV |
| LLM API | Groq API |
| Default LLM | llama-3.3-70b-versatile |
| Frontend | React / Vite |

---

## Prerequisites

- **JDK 17**
- **Maven 3.8+**
- **Node.js & npm** (for the React frontend)
- **Groq API key** — sign up at [console.groq.com](https://console.groq.com)

---

## Quick Start

### 1. Backend

```bash
# Set the Groq API key (required) and optionally the model name
export GROQ_API_KEY=your_groq_api_key_here
export GROQ_MODEL=llama-3.3-70b-versatile   # optional; this is the default

cd backend
mvn spring-boot:run
```

Once the backend is running, verify with the health endpoint:

```bash
curl http://localhost:8080/api/health
```

### 2. Frontend

Open a **second terminal** window:

```bash
cd frontend
npm install
npm run dev
```

Then open the Vite localhost URL shown in the terminal output (typically `http://localhost:5173`).

---

## API Usage

### Health Check

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/health` | Returns the service health status |

### Ask a Question

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/ask` | Submit a natural-language question |

**Request Body (example):**

```json
{
  "question": "Show the total electoral bonds by donation range."
}
```

**Response:** The backend generates and executes the corresponding SQL query against the in-memory H2 database and returns the result.

---

## Data Loading

On startup the application loads CSV files into the H2 in-memory database. The database is **not persistent** — every restart reloads the CSVs from scratch.

---

## Security Notes

Please observe the following security guidelines:

- **Never commit secrets** such as API keys or credentials to the repository.
- If a key is ever exposed, **rotate it immediately**.
- The SQL guard provided by the LLM is **not a complete security boundary**.
- **Do not send sensitive or personally identifiable data** to any LLM.
- **Review the provenance** and licensing of the dataset before use.
- **No license** is added to this project.

---

## Project Structure

```
Natural-Language-SQL-Analytics/
├── backend/          # Spring Boot Java backend
├── frontend/         # React/Vite frontend
```

> Source files are not yet present in this repository.
