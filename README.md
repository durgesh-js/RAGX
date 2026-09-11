# RAGX — Retrieval-Augmented Intelligence Engine

RAGX is a modular Retrieval-Augmented Generation (RAG) system that retrieves relevant knowledge from Wikipedia, performs semantic search using transformer embeddings and FAISS, and generates grounded responses through Gemini.

The project demonstrates an end-to-end RAG pipeline while keeping retrieval, vector search, and generation as separate components.

## Overview

For each user query, RAGX:

1. Searches Wikipedia for relevant articles.
2. Retrieves and cleans the article content.
3. Splits the content into overlapping chunks.
4. Generates semantic embeddings using Sentence Transformers.
5. Performs similarity search using FAISS.
6. Passes the most relevant context to Gemini.
7. Generates an answer with Wikipedia source references.

## Architecture

```text
User Query
    ↓
Wikipedia Search
    ↓
Article Retrieval
    ↓
Cleaning & Chunking
    ↓
Sentence Transformer Embeddings
    ↓
FAISS Semantic Search
    ↓
Relevant Context
    ↓
Gemini
    ↓
Grounded Answer + Sources
```

The retrieval and generation stages are decoupled, allowing individual components to be replaced without redesigning the complete pipeline.

## Core Features

* Wikipedia-based knowledge retrieval
* Transformer-based semantic embeddings
* FAISS vector similarity search
* Configurable top-K retrieval
* Similarity threshold filtering
* Context-grounded generation
* Wikipedia source attribution
* Interactive query console
* Secure API-key configuration

## Technology Stack

| Component        | Technology            |
| ---------------- | --------------------- |
| Language         | Python                |
| Knowledge Source | Wikipedia             |
| Embeddings       | Sentence Transformers |
| Vector Search    | FAISS                 |
| Generation       | Gemini API            |
| Runtime          | Google Colab          |

## Running the Project

RAGX is implemented as a Google Colab notebook.

1. Open `RAGX.ipynb` in Google Colab.
2. Configure the Gemini API key through Colab Secrets.
3. Run the notebook cells.
4. Enter a question in the final RAGX query console.

Example:

```text
What is machine learning?
```

The system retrieves relevant Wikipedia content, performs semantic retrieval, generates a grounded response, and displays the corresponding sources.

## Configuration

The Gemini API key is loaded through Google Colab Secrets:

```python
from google.colab import userdata

GEMINI_API_KEY = userdata.get("GEMINI_API_KEY")
```

API credentials should never be hard-coded or committed to the repository.

## Architecture Scalability

The current implementation uses freely accessible/open-source components for retrieval and embeddings and an API-accessible Gemini model for generation. These choices provide a practical and reproducible proof-of-concept.

The underlying architecture is modular and is not tied to these specific technologies. Individual components can be replaced with enterprise-grade proprietary models, managed vector databases, reranking systems, hybrid retrieval, or advanced multi-agent and agentic RAG architectures.

Such extensions can substantially improve retrieval precision, contextual reasoning, computational latency, scalability, and output quality for production workloads.

## Limitations

The current implementation is intentionally compact:

* Wikipedia is the primary knowledge source.
* FAISS indexing is created during the workflow rather than persisted.
* Retrieval uses semantic similarity rather than hybrid search.
* No dedicated reranking model is included.
* Production monitoring and deployment infrastructure are outside the current scope.

## Project Structure

```text
RAGX/
├── RAGX.ipynb
├── README.md
├── .gitignore
└── LICENSE
```

## Project Status

**Status:** Functional proof-of-concept

RAGX demonstrates the complete workflow from external knowledge retrieval to semantic search and grounded response generation.

## Google Colab

[Open RAGX in Google Colab](https://colab.research.google.com/github/durgesh-js/RAGX/blob/main/RAGX.ipynb)
