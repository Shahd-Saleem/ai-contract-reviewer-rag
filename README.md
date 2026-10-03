# AI Contract Summary & Risk Analyzer

An AI-powered contract analysis tool built with **Python, Streamlit, LangChain, Google Gemini, and ChromaDB**.

The application uses **Retrieval-Augmented Generation (RAG)** to analyze contracts, generate summaries, identify risky clauses, and answer contract-specific questions.

## Features

- Upload PDF, TXT, or Markdown contract files
- Paste contract text directly
- Generate plain-language contract summaries
- Detect high-risk clauses
- Identify financial penalties, auto-renewals, short notice periods, and liability limits
- Ask follow-up questions about the uploaded contract
- Retrieve relevant contract sections using vector search
- Filter retrieved content by document source
- Handle Gemini API rate limits

## How It Works

```text
Contract
   ↓
Document Loading
   ↓
Text Chunking
   ↓
Gemini Embeddings
   ↓
ChromaDB Vector Store
   ↓
Relevant Chunk Retrieval
   ↓
Gemini LLM
   ↓
Summary / Risk Analysis / Q&A
```

The contract is split into smaller chunks and converted into embeddings using Google's Gemini embedding model.

The embeddings are stored in **ChromaDB**. When a user asks a question, the system retrieves the most relevant contract sections and sends that context to Gemini to generate a grounded answer.

## Tech Stack

- Python
- Streamlit
- LangChain
- Gemini API
- Vector Database (ChromaDB)

## Project Structure

```text
AI-Contract-Analyzer/
│
├── app.py
├── main.py
├── docs/
├── chroma_db/
├── .env
├── requirements.txt
├── README.md
└── requirements.txt
```

### `app.py`

Handles the Streamlit interface, including document upload and text input, contract analysis, summary generation, risk display, session state, follow-up chat, and API error handling.

### `main.py`

Handles the core RAG pipeline, including document loading, text chunking, Gemini embeddings, ChromaDB vector storage, relevant chunk retrieval, source filtering, and Gemini answer generation.

## Installation

Clone the repository:

```bash
git clone https://github.com/Shahd-Saleem/ai-contract-reviewer-rag.git
cd ai-contract-reviewer-rag
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the project directory:

```env
GEMINI_API_KEY=your_api_key_here
```

Make sure `.env` is included in your `.gitignore`:

```text
.env
venv/
__pycache__/
chroma_db/
```

## Run the App

Run the Streamlit application:

```bash
streamlit run app.py
```

Then open the local Streamlit URL shown in your terminal.

## Outputs

After uploading or pasting a contract, the application can generate three main outputs:

## 1. Contract Summary
The system provides a plain-language summary of the contract, including the main agreement, key obligations, and important terms.


## 2. Risky Clause Alerts

The application automatically searches for potentially risky clauses and returns structured results such as:

```json
{
  "title": "Risk Title",
  "risk_level": "HIGH",
  "description": "Explanation of the identified risk"
}
```

Possible risk levels include:

- MEDIUM
- HIGH
- CRITICAL

## 3. Follow-Up Q&A
Users can ask follow-up questions about the uploaded contract, such as:
- What happens if I terminate the contract early?
- What are the payment terms?
- How much notice is required before cancellation?

If the answer cannot be found in the retrieved contract content, the system responds:

```text
Not found in the provided documents.
```

## Author

**Shahd Saleem**
