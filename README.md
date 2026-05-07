# RAG Document Q&A System

A complete Retrieval-Augmented Generation (RAG) implementation enabling intelligent question-answering over PDF documents using LangChain, ChromaDB, and LLMs (Mistral AI / OpenAI).

## ✨ Features

- **PDF Processing**: Load and parse PDF documents with intelligent chunking
- **Web Content Extraction**: Retrieve and index content from web pages
- **Advanced Retrieval Techniques**:
  - Similarity Search
  - MMR (Maximal Marginal Relevance) - diversity-optimized retrieval
  - Multi-Query Retrieval - LLM-generated query variations
- **Vector Database**: ChromaDB for semantic search and persistent storage
- **Multiple LLM Support**: Mistral AI & OpenAI integration
- **Dual Interfaces**:
  - 🎨 Streamlit Web UI - Interactive document upload and Q&A
  - 💻 CLI Interface - Command-line query system

## 🛠️ Tech Stack

- **Python 3.13+**
- **LangChain** - LLM orchestration
- **ChromaDB** - Vector database
- **OpenAI & Mistral AI** - LLM providers
- **Streamlit** - Web UI
- **HuggingFace & OpenAI Embeddings** - Text embeddings
- **PyPDF** - PDF parsing

## 📁 Project Structure

```
GenAI-basic-1st-proj/
├── app.py                      # Streamlit web interface
├── main.py                     # CLI interface
├── create_database.py          # Database initialization
├── requirements.txt            # Dependencies
├── .gitignore                  # Git configuration
├── document_loaders/           # Document ingestion
│   ├── pdf.py                 # PDF loading & chunking
│   └── page.py                # Web content loading
├── retrievers/                 # Retrieval strategies
│   ├── mmr.py                 # MMR retrieval demo
│   └── multiquery.py          # Multi-query retrieval demo
└── vector_store/               # Vector DB management
    └── DB.py                  # Chroma operations
```

## 🚀 Quick Start

### Prerequisites
- Python 3.13+
- API Keys:
  - OpenAI API Key
  - Mistral AI API Key

### Installation

```bash
# Clone the repository
git clone https://github.com/yashbhatewara/GenAi-basic-1st-proj.git
cd GenAi-basic-1st-proj

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Environment Setup

Create a `.env` file in the project root:

```
OPENAI_API_KEY=your_openai_key_here
MISTRAL_API_KEY=your_mistral_key_here
```

### Usage

#### 🎨 Streamlit Web Interface (Recommended)
```bash
streamlit run app.py
```
- Upload a PDF
- Click "Create Vector Database"
- Ask questions about the document

#### 💻 CLI Interface
```bash
python main.py
```
- Enter your queries interactively
- Type "0" to exit

#### 🗄️ Create Vector Database
```bash
python create_database.py
```
- Processes a PDF and creates persistent Chroma database

## 📚 Core Concepts

### RAG Pipeline
```
Document → Chunking → Embeddings → Vector Store → Retrieval → LLM → Response
```

### Document Loading
- **PDF**: Extract text with metadata preservation
- **Web**: Fetch and parse web page content

### Text Chunking
- Recursive character splitting
- Configurable chunk size: 1000 chars
- Overlap: 200 chars (for semantic continuity)

### Retrieval Strategies

**1. Similarity Search**
- Direct vector similarity matching
- Fast, simple baseline

**2. MMR (Maximal Marginal Relevance)**
- Balances relevance and diversity
- Reduces redundant results
- Parameters: k=4, fetch_k=10, lambda_mult=0.5

**3. Multi-Query Retrieval**
- LLM generates query variations
- Improves coverage and accuracy
- Great for complex questions

### LLM Integration
```python
# Using Mistral AI
llm = ChatMistralAI(model="mistral-small-2506")

# Using OpenAI
llm = ChatOpenAI(model="gpt-4")
```

## ⚙️ Configuration

### Adjust Retrieval Parameters
Edit `main.py` or `app.py`:
```python
retriever = vectorstore.as_retriever(
    search_type="mmr",
    search_kwargs={
        "k": 4,              # Number of results to return
        "fetch_k": 10,       # Candidates to fetch initially
        "lambda_mult": 0.5   # Diversity weight (0-1)
    }
)
```

### Change Embedding Model
```python
# OpenAI (best quality, requires API key)
embeddings = OpenAIEmbeddings()

# HuggingFace (free, local)
from langchain_huggingface import HuggingFaceEmbeddings
embeddings = HuggingFaceEmbeddings()
```

## 📊 Example Workflow

```
User: "What is gradient descent?"
↓
[Query Expansion] → Generates variations
↓
[Retrieval] → Finds relevant chunks (MMR)
↓
[Context Building] → Combines top chunks
↓
[LLM Processing] → Mistral AI generates answer
↓
Output: "Gradient descent is an optimization algorithm that..."
```

## 🎓 Learning Outcomes

From this project, you'll learn:
- ✅ End-to-end RAG system implementation
- ✅ Vector database management (ChromaDB)
- ✅ Advanced retrieval techniques
- ✅ LangChain framework expertise
- ✅ LLM integration and prompt engineering
- ✅ Full-stack application development
- ✅ Document processing pipelines

## 🤝 Contributing

Contributions are welcome! Consider:
- Adding support for more document types (DOCX, TXT, etc.)
- Implementing additional retrieval strategies
- Optimizing embedding models
- Enhancing UI/UX
- Adding conversation memory/chat history

## 📝 License

MIT License - Free to use for personal or commercial projects

## 🔗 Resources

- [LangChain Docs](https://python.langchain.com/)
- [ChromaDB Docs](https://docs.trychroma.com/)
- [Mistral AI API](https://docs.mistral.ai/)
- [OpenAI API](https://platform.openai.com/docs/)
- [Streamlit Docs](https://docs.streamlit.io/)

---

**Author**: Yash Bhatewara  
**Last Updated**: May 2026

