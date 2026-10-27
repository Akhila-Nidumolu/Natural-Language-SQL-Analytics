Natural Language SQL Analytics

A Java-based application that allows users to ask questions about electoral bond CSV data in natural language and receive data-driven answers using LLM-powered SQL generation.

Overview

Natural Language SQL Analytics bridges the gap between natural-language questions and structured data queries. Users can ask questions about electoral bond data without writing SQL manually. The application uses a large language model (LLM) to generate SQL queries, executes them against an in-memory H2 database, and returns the results.

CSV datasets are loaded into the database when the application starts.

Key Features

- Natural-language querying: Ask questions about electoral bond data using everyday language.
- LLM-powered SQL generation: Translate questions into SQL queries using the Groq API.
- Database integration: Execute queries against an H2 in-memory database using Spring JDBC.
- CSV data ingestion: Load CSV datasets automatically during application startup.
- REST API: Submit questions and retrieve query results through backend endpoints.
- Web interface: Interact with the application through a React-based frontend.

Technology Stack

Component| Technology
Programming Language| Java 17
Backend Framework| Spring Boot 3.3.2
Database Access| Spring JDBC
Database| H2 (in-memory)
CSV Processing| Apache Commons CSV
LLM Integration| Groq API
Default LLM| "llama-3.3-70b-versatile"
Frontend| React.js and Vite
Build Tool| Maven

Prerequisites

Ensure the following are installed:

- JDK 17
- Maven 3.8 or later
- Node.js and npm
- A Groq API key from "Groq Console" (https://console.groq.com/)

Getting Started

1. Configure Environment Variables

Set your Groq API key before starting the backend.

export GROQ_API_KEY=your_groq_api_key_here

Optionally, specify the model:

export GROQ_MODEL=llama-3.3-70b-versatile

The application uses this model by default if no alternative is configured.

Security: Never commit API keys or other credentials to version control.

2. Start the Backend

From the project root, run:

cd backend
mvn spring-boot:run

Once the application starts, check its health using:

curl http://localhost:8080/api/health

3. Start the Frontend

Open a separate terminal and run:

cd frontend
npm install
npm run dev

Open the local URL displayed in the terminal, typically:

"http://localhost:5173"

API Usage

Health Check

Property| Value
Method| "GET"
Endpoint| "/api/health"
Purpose| Checks the backend service health status

Submit a Natural-Language Question

Property| Value
Method| "POST"
Endpoint| "/api/ask"
Purpose| Submits a question for SQL generation and data retrieval

Example request:

{
  "question": "Show the total electoral bonds by donation range."
}

The backend processes the question, generates a SQL query, executes it against the database, and returns the result.

Data Loading and Persistence

The application loads CSV data into an H2 in-memory database during startup.

Because the database is in memory, its contents are not retained between application restarts. The CSV data is loaded again whenever the application starts.

Project Structure

Natural-Language-SQL-Analytics/
├── backend/     # Java and Spring Boot backend
├── frontend/    # React and Vite frontend
└── README.md    # Project documentation

Security Considerations

- Store API keys and credentials in environment variables; never commit them to the repository.
- Rotate credentials immediately if they are exposed.
- Review generated SQL before relying on it for sensitive or critical operations.
- Treat SQL validation and query restrictions as safeguards, not a complete security boundary.
- Avoid sending sensitive or personally identifiable information to external LLM services.
- Verify the provenance and licensing of datasets before distributing or using them.

License

No license has been specified for this project. Unless a license is added, reuse and redistribution are not automatically permitted.
