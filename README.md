# AI_Resume_Analyser_Pipeline
An event-driven AI automation pipeline that ingests resumes via forms, parses PDF layouts using PDF.co, and executes structured ATS evaluations via the Google Gemini API. Built on a serverless architecture, it instantly distributes responsive HTML feedback via Gmail and logs metrics to Google Sheets. Perfect for scalable HR-tech screening.

# AI-Powered ATS Resume Analyzer (Automated Production Pipeline)

An end-to-end automated system that ingests user resumes via forms, parses PDF text layouts dynamically, utilizes Large Language Models (LLMs) to perform structured ATS capability evaluations, and instantly distributes analytics to users and internal tracking sheets.

Built during my work as a Web Development Intern at Cubicle Buddies to optimize student recruitment workflows.

## 🛠️ System Architecture & Data Flow

The entire application runs as a serverless, event-driven architecture orchestrated via automated JSON routing blueprints:

1. **Ingestion (Tally Forms):** Webhook triggers immediately upon user form submission, capturing metadata (Name, Email, Phone) and the secure binary storage URL of the uploaded document.
2. **File Processing (HTTP Buffer & PDF.co):** The pipeline programmatically downloads the document object array and processes it through a simple layout-agnostic OCR text engine (`toTextSimple`) to extract raw string sequences safely.
3. **Inference (Google Gemini API):** Formulates a system prompt using the parsed layout array and posts a `POST` request to the `gemini-2.5-flash` endpoint, handling payload conversions as structured text streams.
4. **Distribution & Storage (Gmail & Google Sheets API):** Concurrently dispatches a formatted HTML responsive mail to the applicant's input string while executing a row appending operation (`addRow`) to populate analytics tables.

---

## 💻 Tech Stack & API Endpoints Used

* **Orchestration:** Make.com Logic Engine (Rotational Serverless Pipelines)
* **LLM Engine:** Google Gemini API (`gemini-2.5-flash:generateContent`)
* **Document Parser:** PDF.co Document Processing API (`PDFToAnything`)
* **Data Stores:** Google Sheets Engine API, Tally Webhook Integrations
* **Frontend Intake:** Tally Forms UI Framework

---

## 🤖 Prompt Engineering Implementation

The core reasoning logic is handled via the following engineered system prompt passed directly into the Gemini context window matrix:

```text
You are an expert ATS recruiter and career coach.

Analyze this resume and provide:

1. Overall Resume Score (0-100)
2. ATS Compatibility Score (0-100)
3. Top 3 Strengths
4. Top 3 Weaknesses
5. Specific Improvement Suggestions
6. Final Career Readiness Verdict

Resume: {{Parsed_Resume_Text_From_PDF_Co}}
