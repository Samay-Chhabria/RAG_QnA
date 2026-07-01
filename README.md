# RAG QA System

A lightweight retrieval-augmented generation (RAG) question-answering application built in Python. It combines dense retrieval, sparse retrieval, and a Hugging Face text-generation model to answer questions using a knowledge base.

This repository is ready to be uploaded to GitHub and shared with other developers.

## Features

- Hybrid retrieval using FAISS and BM25
- Reciprocal rank fusion for combining retrieval signals
- Flask-based web interface with a simple frontend
- CLI support for single queries and interactive use
- Data preprocessing and knowledge-base construction utilities
- Easy setup for local experimentation and demonstration

## Tech Stack

- Frontend: HTML, CSS, and JavaScript served by Flask
- Backend: Python, Flask
- Retrieval: FAISS, BM25, Sentence Transformers
- Generation: Hugging Face Transformers
- Data processing: pandas, NumPy, tqdm

## Project Structure

```text
RAG_Qna/
├── app/
│   ├── app.py
│   └── static/
│       └── index.html
├── data/
│   ├── processed/
│   └── raw/
├── src/
│   ├── data/
│   │   ├── embeddings/
│   │   ├── build_knowledge_base.py
│   │   ├── loader.py
│   │   └── preprocessor.py
│   ├── generation/
│   │   └── prompt.py
│   └── retrieval/
│       └── rag_pipeline.py
├── .env.example
├── .gitignore
├── pipeline.MD
├── requirements.txt
└── README.md
```

## Prerequisites

- Python 3.10 or newer
- Internet access for downloading model weights on first run
- Optional: GPU for faster inference

## Installation

1. Clone the repository

```bash
git clone <your-repository-url>
cd RAG_Qna
```

2. Create and activate a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
# On Windows PowerShell:
# .\.venv\Scripts\Activate.ps1
```

3. Install dependencies

```bash
pip install -r requirements.txt
```

4. Create your environment file

```bash
copy .env.example .env
# or: cp .env.example .env
```

5. Build the local knowledge-base assets

The app expects processed retrieval files under the data folder. If they are not present, generate them locally:

```bash
python src/data/build_knowledge_base.py --nq-only --max-nq 100
python src/data/embeddings/build_fiass.py
python src/data/embeddings/build_bm25.py
```

## Environment Variables

Create a .env file using the template in [.env.example](.env.example):

```env
FLASK_ENV=development
HOST=0.0.0.0
PORT=5000
MODEL_NAME=google/flan-t5-base
```

## Running the Project

### Start the web app

```bash
python app/app.py --serve --host 0.0.0.0 --port 5000
```

Then open http://localhost:5000 in your browser.

### Run a single query from the CLI

```bash
python app/app.py --query "What is machine learning?"
```

### Run the interactive REPL

```bash
python app/app.py
```

## API Endpoints

The Flask app exposes the following routes:

- GET /api/health
- POST /api/query
- GET /api/suggestions


## Future Improvements

- Add automated tests
- Add Docker support
- Improve indexing and caching for larger corpora
- Add a better configuration interface for retrieval settings

## Contributing

Contributions are welcome. Please open an issue or submit a pull request with a clear description of the change.

## License

This project is intended for educational and research purposes.

## Author

Prepared as a research-oriented RAG application sample.
