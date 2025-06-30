# Llama2 Medical Chatbot

## Introduction

The **Llama2 Medical Chatbot** is an AI-powered assistant designed to answer medical queries using advanced language models and document retrieval. It leverages the Llama-2 large language model and a vector database built from medical literature (PDFs) to provide accurate, context-aware responses. This project is ideal for prototyping medical Q&A bots, research assistants, or educational tools.

## Features
- **Conversational Medical Q&A:** Ask medical questions and get context-based answers.
- **Document Retrieval:** Uses a FAISS vectorstore built from medical PDFs for grounded responses.
- **Source Attribution:** Returns source documents for transparency.
- **Chainlit UI:** Modern, interactive web interface for chat.
- **Custom Prompting:** Easily modify the prompt template for different use cases.

## Tech Stack
- **Python 3.6+**
- **LangChain** (retrieval-augmented generation, chains)
- **Chainlit** (chatbot UI)
- **Sentence Transformers** (embeddings)
- **FAISS** (vector database)
- **CTransformers** (Llama-2 model inference)
- **PyPDF** (PDF parsing)

## Project Structure
```
Llama2-Medical-Chatbot/
├── chainlit.md                # Chainlit UI welcome/config markdown
├── ingest.py                  # Script to build the FAISS vectorstore from PDFs
├── model.py                   # Main app: model loading, QA chain, Chainlit handlers
├── requirements.txt           # Python dependencies
├── README.md                  # Project documentation
├── data/                      # Folder for medical PDF documents
│   └── 71763-gale-encyclopedia-of-medicine.-vol.-1.-2nd-ed.pdf
├── vectorstore/               # Vectorstore directory
│   └── db_faiss/
│       ├── index.faiss
│       └── index.pkl
├── TheBloke/                  # Folder for Llama-2 model file (not tracked by git)
│   └── llama-2-7b-chat.ggmlv3.q8_0.bin
├── venv/ or .venv/            # Python virtual environment (not tracked by git)
└── .gitignore                 # Git ignore file
```

## Setup Instructions

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd Llama2-Medical-Chatbot
```

### 2. Create and Activate a Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Download the Llama-2 Model
- Download the GGML version of Llama-2-7B-Chat (e.g., `llama-2-7b-chat.ggmlv3.q8_0.bin`) from HuggingFace or TheBloke's repo.
- Place it in the `TheBloke/` directory.
- **Do not add this file to git.**

### 5. Prepare the Vectorstore
- Place your medical PDF(s) in the `data/` folder.
- Run the ingestion script to build the FAISS vectorstore:
  ```bash
  python ingest.py
  ```
- This will create the `vectorstore/db_faiss/` directory with `index.faiss` and `index.pkl`.

### 6. Run the Chatbot
```bash
chainlit run model.py
```
- Open [http://localhost:8000](http://localhost:8000) in your Windows browser.

## Notes
- The `.gitignore` file excludes large files and virtual environments (`TheBloke/`, `venv/`, `.venv/`).
- The app runs in WSL; always use your Windows browser to access the UI.
- If you update your PDFs, re-run `ingest.py` to refresh the vectorstore.
- For best results, use the same model and embedding settings as in `model.py`.


