# RAG Practice Project

A Retrieval-Augmented Generation (RAG) application that demonstrates document processing, vectorization, and semantic search using modern LLM frameworks.

## Overview

This project implements a complete RAG pipeline with:
- **Document Processing**: Extract text from PDFs and documents
- **Document Chunking**: Split documents into overlapping chunks for optimal processing
- **Vector Embeddings**: Convert documents into semantic embeddings using Sentence Transformers
- **Vector Storage**: Store and retrieve embeddings using ChromaDB and FAISS
- **Semantic Search**: Search documents using Typesense
- **LLM Integration**: Query documents with Groq LLM through LangChain

## Project Structure

```
rag-prac/
├── main.py              # Main entry point
├── pyproject.toml       # Project configuration and dependencies
├── requirement.txt      # Additional requirements
├── books.jsonl          # Sample data file
├── Notebook/
│   ├── Document.ipynb   # Document processing and embedding notebook
│   └── TypeSense.ipynb  # Typesense search integration notebook
└── data/
    ├── text_files/      # Extracted text documents
    │   ├── machine_learning.txt
    │   └── python_intro.txt
    └── vector_store/    # ChromaDB vector storage
```

## Dependencies

### Core LLM & RAG Framework
- **langchain** (>=1.1.3) - LLM orchestration and RAG pipeline
- **langchain-community** (>=0.4.1) - Community integrations
- **langchain-groq** (>=1.1.0) - Groq LLM integration
- **langchain-core** (>=1.1.3) - Core abstractions

### Vector Storage & Search
- **chromadb** (>=1.3.6) - Vector database for embeddings
- **faiss-cpu** (>=1.13.1) - Similarity search library
- **sentence-transformers** (>=5.1.2) - Semantic embeddings
- **typesense** (>=1.3.0) - Full-text and semantic search

### Document Processing
- **pypdf** (>=6.4.1) - PDF text extraction
- **pymupdf** (>=1.26.6) - Alternative PDF processing
- **beautifulsoup4** (>=4.14.3) - HTML/XML parsing

### Data & Utilities
- **pandas** (>=2.3.3) - Data manipulation
- **python-dotenv** (>=1.2.1) - Environment variable management
- **ipykernel** (>=7.1.0) - Jupyter kernel support

## Prerequisites

- Python 3.13 or higher
- Groq API key (set in `.env` file)
- pip or uv package manager

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd rag-prac
   ```

2. **Set up environment variables**
   ```bash
   # Create a .env file and add your API keys
   echo "GROQ_API_KEY=your_groq_api_key_here" > .env
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirement.txt
   ```
   
   Or using uv:
   ```bash
   uv sync
   ```

## Usage

### Running the Main Script
```bash
python main.py
```

### Using Jupyter Notebooks

#### Document Processing
```bash
jupyter notebook Notebook/Document.ipynb
```
This notebook covers:
- Loading and processing PDF/text documents
- Chunking documents into smaller segments for optimal embedding
- Creating semantic embeddings
- Storing vectors in ChromaDB
- Querying the vector database

#### Typesense Integration
```bash
jupyter notebook Notebook/TypeSense.ipynb
```
This notebook demonstrates:
- Indexing documents in Typesense
- Performing full-text and semantic search
- Ranking and filtering results

## Features

✅ **Document Ingestion**: Support for PDF, JSONL, and text files  
✅ **Document Chunking**: Split large documents into manageable chunks with configurable overlap  
✅ **Semantic Embeddings**: Using pre-trained transformer models  
✅ **Vector Search**: Fast similarity search with FAISS and ChromaDB  
✅ **Full-Text Search**: Integrated Typesense search engine  
✅ **LLM Integration**: Query documents using Groq  
✅ **Interactive Notebooks**: Learn and experiment with RAG workflows  

## Document Chunking

Document chunking is a critical component of the RAG pipeline that breaks large documents into smaller, semantically meaningful segments:

- **Why Chunking?**: Large documents exceed token limits of embedding models. Chunking ensures each segment captures coherent information while remaining within embedding constraints.
- **Chunk Size**: Configurable chunk size (typically 512-1024 tokens) balances context preservation with model limitations.
- **Overlap**: Overlapping chunks (typically 20-50 tokens) preserve context at chunk boundaries, improving retrieval quality.
- **Smart Splitting**: Uses recursive character-based splitting to maintain sentence and paragraph boundaries.
- **Metadata Preservation**: Each chunk retains metadata (source, page number, position) for traceability.

### Chunking Workflow
1. Load document content
2. Configure chunk size and overlap parameters
3. Split document recursively
4. Assign metadata to each chunk
5. Generate embeddings for chunks
6. Store in vector database  

## API Configuration

### Groq API Setup
1. Sign up at [console.groq.com](https://console.groq.com)
2. Create an API key
3. Add to `.env` file:
   ```
   GROQ_API_KEY=your_key_here
   ```

## Data Files

- **books.jsonl**: Sample dataset with book information
- **data/text_files/**: Extracted text documents for processing
- **data/vector_store/**: ChromaDB storage for embeddings

## Development

To add new features or modify the RAG pipeline:

1. Update dependencies in `pyproject.toml`
2. Add implementation code in appropriate modules
3. Test with Jupyter notebooks before committing
4. Update this README with new features

## License

This is a practice/educational project.

## Notes

- Groq API key is required for LLM functionality
- ChromaDB vector store is persisted in `data/vector_store/`
- Notebooks are configured for interactive exploration
- Sensitive credentials should be added to `.env` and included in `.gitignore`
