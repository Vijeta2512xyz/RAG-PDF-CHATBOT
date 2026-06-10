# PDF Chatbot using Streamlit, MySQL, Sentence Transformers, and Ollama

## Overview

This project is a Retrieval-Augmented Generation (RAG) based PDF Chatbot that enables users to upload PDF documents, extract and store their contents, generate vector embeddings, perform semantic search, and interact with the documents through a Large Language Model (LLM).

The application includes user authentication, document management, embedding generation, similarity-based retrieval, and AI-powered question answering.

---

## Features

### User Authentication
- User registration and login
- Secure password hashing using SHA-256
- Session management with Streamlit

### PDF Processing
- Upload multiple PDF files
- Extract text from PDFs using PyPDF2
- Automatic text chunking
- Store document content and metadata in MySQL

### Embedding Generation
- Uses Sentence Transformers (`paraphrase-MiniLM-L3-v2`)
- Generates vector embeddings for document chunks
- Stores embeddings in the database

### Semantic Search
- Converts user queries into  embeddings
- Computes cosine similarity scores
- Retrieves the most relevant document chunks

### AI-Powered Question Answering
- Retrieval-Augmented Generation (RAG) workflow
- Context-aware responses using retrieved document content
- Powered by Ollama and Llama 2

---

## Technology Stack

| Layer | Technology |
|---------|------------|
| Frontend | Streamlit |
| Backend | Python |
| Database | MySQL |
| PDF Parsing | PyPDF2 |
| Embedding Model | Sentence Transformers |
| Vector Search | NumPy |
| Large Language Model | Ollama (Llama 2) |
| Authentication | SHA-256 Password Hashing |

---

## System Architecture

```text
User Query
     │
     ▼
Embedding Generation
     │
     ▼
Vector Similarity Search
     │
     ▼
Top Relevant Chunks
     │
     ▼
Prompt Construction
     │
     ▼
Ollama LLM
     │
     ▼
Generated Response
```

---

## Database Schema

### USER_CREDENTIALS

| Column | Type |
|----------|----------|
| USERS | VARCHAR(255) |
| PASSWORD | VARCHAR(255) |

### DOCUMENT_FILES

| Column | Type |
|----------|----------|
| ID | INT |
| EXTRACTED_LAYOUT | LONGTEXT |
| FILE_URL | TEXT |
| PROCESSED_AT | DATETIME |
| RELATIVE_PATH | TEXT |

### DOCUMENT_CHUNKS

| Column | Type |
|----------|----------|
| ID | INT |
| CHUNK | LONGTEXT |
| CHUNK_ID | VARCHAR(255) |
| CHUNK_INDEX | INT |
| EMBEDDING | LONGTEXT |
| FILE_URL | TEXT |
| LANGUAGE | VARCHAR(10) |
| RELATIVE_PATH | TEXT |

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/yourusername/pdf-chatbot.git
cd pdf-chatbot
```

### Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment:

**Windows**

```bash
venv\Scripts\activate
```

**Linux/macOS**

```bash
source venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Install and Run Ollama

Install Ollama from:

https://ollama.com

Pull the Llama 2 model:

```bash
ollama pull llama2
```

Start the Ollama server:

```bash
ollama serve
```

### Configure MySQL

Update the database credentials in the application:

```python
HOST = "localhost"
USER = "root"
PASSWORD = "your_password"
DATABASE = "pdf_chatbot"
```

### Run the Application

```bash
streamlit run app.py
```

---

## Workflow

1. User registers and logs into the application.
2. PDF files are uploaded through the Streamlit interface.
3. Text is extracted using PyPDF2.
4. Documents are divided into chunks.
5. Sentence Transformer generates embeddings.
6. Chunks and embeddings are stored in MySQL.
7. User submits a question.
8. Query embedding is generated.
9. Most relevant chunks are retrieved using cosine similarity.
10. Retrieved context is passed to Ollama.
11. The generated answer is displayed to the user.

---

## Project Structure

```text
PDF-Chatbot/
│
├── app.py
├── requirements.txt
├── README.md
│
├── database/
│   ├── USER_CREDENTIALS
│   ├── DOCUMENT_FILES
│   └── DOCUMENT_CHUNKS
│
└── uploaded_pdfs/
```

---

## Known Issue

### Ollama Chat Error

```python
AttributeError: module 'ollama' has no attribute 'chat'
```

Possible causes:

- Outdated Ollama Python package
- Incorrect package installation
- Naming conflict with a local file named `ollama.py`

Suggested fix:

```bash
pip uninstall ollama
pip install --upgrade ollama
```

For newer versions:

```python
from ollama import Client

client = Client(host="http://localhost:11434")

response = client.chat(
    model="llama2",
    messages=[
        {
            "role": "user",
            "content": prompt
        }
    ]
)

answer = response["message"]["content"]
```

---

## Future Enhancements

- User-specific document repositories
- Chat history persistence
- Multi-document filtering
- Conversation memory
- FAISS vector database integration
- ChromaDB integration
- Multi-LLM support
- Cloud deployment
- Document preview functionality
- Role-based access control

---

## Author

Vijeta Vadehi

B.Tech in Artificial Intelligence and Machine Learning

### Project Title

**Full-Stack Retrieval-Augmented Generation (RAG) PDF Chatbot using Streamlit, MySQL, Sentence Transformers, and Ollama**
