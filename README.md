#  RAG Pipeline with Automated Evaluation using Groq LLMs

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline to process PDFs and answer questions with high factual accuracy using multiple search strategies and Groq LLMs. It includes automated evaluation for **faithfulness** and **relevance** using a judge model.

> ⚗️ **Purpose**: This project is built for **experimentation with different chunking and retrieval methodologies** to assess the impact of responses in a RAG setup.

---

###  PDF Parsing
- **Text Extraction**: Uses `PyMuPDF` (`fitz`) to extract all text from PDFs.
- **Table Extraction**: Uses `pdfplumber` to extract tables accurately from each page.

###  Chunking Strategies
Four different chunking approaches are available:
- **Token-based** (via `LangChain`)
- **Recursive character-based**
- **Paragraph-based**
- **Sentence-based**

Each method includes configurable `chunk_size` and `chunk_overlap` options.

###  Retrieval Methods
You can use the following strategies to retrieve relevant chunks:
- **Semantic Search** (FAISS + HuggingFace MiniLM)
- **BM25 Search** (lexical)
- **MMR (Maximal Marginal Relevance)**
- **Hybrid Search**:
  - Semantic + BM25
  - Semantic + MMR
- All methods have summarized variants using Groq summarization

### Generation & Summarization
- **Answer Generation**: Uses Groq models such as `llama3-8b-8192`, `llama-guard-3-8b`
- **Summarization**: summarizes the retrieved chunks

###  Evaluation with Judge Model
Automatically evaluates the quality of each generated answer using a **Groq-hosted LLM as a judge**:
- **Judge Model**: `deepseek-r1-distill-llama-70b`
- **Evaluation Prompt**: Takes the **question**, **golden reference answer**, and **generated answer** as input and produces scored outputs.

Metrics:
- **Faithfulness**: Is the generated answer consistent with the golden reference?
- **Relevance**: Does it actually address the original question?


Metrics:
- **Faithfulness**: Is the generated answer consistent with the golden reference?
- **Relevance**: Does it actually answer the question?
