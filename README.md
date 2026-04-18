# Generative AI Part 2 - RAG Project

This repository is a hands-on Retrieval-Augmented Generation (RAG) project built with LangChain, ChromaDB, Hugging Face embeddings, and Mistral.

It includes:
- A Streamlit app for uploading a PDF and asking questions
- A CLI RAG chat script over an existing vector database
- A script to build the vector database from a PDF
- Practice scripts for document loaders, retrievers, and vector store basics

## Project Structure

```text
Generative AI Part 2 RAG project/
├── app.py
├── create_database.py
├── main.py
├── requirements.txt
├── README.md
├── .env                      # create this locally
├── GenAIpart2.pdf
├── part 2.docx
├── chroma_db/                # persistent Chroma database (auto-created)
│   ├── chroma.sqlite3
│   └── <collection-id>/
├── document loaders/
│   ├── deeplearning.pdf
│   ├── GRU.pdf
│   ├── notes.txt
│   ├── page.py
│   ├── pdf.py
│   └── test.py
├── retrievers/
│   ├── arixv.py
│   ├── mmr.py
│   └── multiquery.py
└── vector store/
    └── DB.py
```

## What Each File Does

### Core RAG flow
- `create_database.py`: Loads `document loaders/deeplearning.pdf`, splits it into chunks, creates embeddings, and stores vectors in `chroma_db`.
- `main.py`: Loads existing vectors from `chroma_db` and starts a terminal chat loop for Q&A.
- `app.py`: Streamlit UI to upload a PDF, build vectors, and ask questions interactively.

### Document loader examples
- `document loaders/page.py`: Loads web page content using `WebBaseLoader`.
- `document loaders/pdf.py`: Loads and chunks a PDF.
- `document loaders/test.py`: Loads and chunks plain text file content.

### Retriever examples
- `retrievers/mmr.py`: Compares similarity retriever vs MMR retriever.
- `retrievers/arixv.py`: Retrieves paper metadata/content from ArXiv.
- `retrievers/multiquery.py`: Uses `MultiQueryRetriever` with Mistral LLM.

### Vector store example
- `vector store/DB.py`: Demonstrates Chroma vector store creation, similarity search, and retrieval.

## Prerequisites

- Python 3.10+
- pip
- Internet connection (for model downloads/API calls)

## Setup

### 1) Create and activate virtual environment (Windows PowerShell)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 2) Install dependencies

```powershell
pip install -r requirements.txt
```

### 3) Create `.env` file in project root

```env
MISTRAL_API_KEY=your_mistral_api_key
# Optional if you switch to OpenAI embeddings in code:
# OPENAI_API_KEY=your_openai_api_key
```

## How To Run

### Option A: Build database first, then use CLI chat

```powershell
python create_database.py
python main.py
```

In `main.py`, enter questions at the prompt. Enter `0` to exit.

### Option B: Use Streamlit app

```powershell
streamlit run app.py
```

Then:
- Upload a PDF
- Click **Create Vector Database**
- Ask questions in the input box

## Notes

- `chroma_db` is a persisted local vector database folder.
- Some scripts are educational examples and use hardcoded sample data.
- Folder names like `document loaders` and `vector store` contain spaces; keep quotes around paths if needed in shell commands.
- `retrievers/arixv.py` filename appears to be a typo of "arxiv" but works as-is.

## Suggested Improvements

- Add one consistent source PDF path configuration (instead of hardcoded paths in multiple scripts).
- Standardize `chroma_db` naming (`chroma_db` vs `chroma-db` in `vector store/DB.py`).
- Add a single entrypoint script and basic error handling for missing API keys.
