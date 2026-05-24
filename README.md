# Self-RAG 🔍

> An optimized implementation of a Retrieval-Augmented Generation (RAG) system that evaluates retrieval quality and works in iterative loops to generate grounded, hallucination-free answers.

---

## Overview

Self-RAG is a step-by-step implementation of a self-reflective RAG pipeline. Unlike standard RAG, Self-RAG evaluates whether retrieved documents are actually relevant before using them, and loops to re-retrieve or refine answers when needed. The result is more accurate, grounded responses with significantly reduced hallucinations.

This repository walks through the full pipeline across 7 incremental notebooks, from basic document ingestion to a complete web-aware Self-RAG system.

---

## How It Works

The Self-RAG pipeline introduces a feedback loop around the standard retrieve-then-generate pattern:

1. **Retrieve** — Fetch documents relevant to the query
2. **Evaluate Retrieval** — Grade whether the retrieved documents actually support the question
3. **Generate** — Produce an answer grounded in the verified documents
4. **Evaluate Generation** — Check whether the answer is supported by the documents and actually resolves the question
5. **Loop or Return** — If grading fails, re-retrieve with a refined query and repeat

This self-correcting loop prevents the model from generating answers based on irrelevant or misleading context.

---

## Repository Structure

```
self-rag/
├── documents/               # Sample documents used as the knowledge base
├── self_rag_step1.ipynb     # Document loading and vector store setup
├── self_rag_step2.ipynb     # Basic retrieval pipeline
├── self_rag_step3.ipynb     # Retrieval grader (relevance scoring)
├── self_rag_step4.ipynb     # Answer generation with grounded context
├── self_rag_step5.ipynb     # Hallucination and answer grader
├── self_rag_step6.ipynb     # Full Self-RAG loop with conditional routing
├── self_rag_step7.ipynb     # Complete optimized Self-RAG system
└── self_rag_web.ipynb       # Web search-augmented Self-RAG variant
```

---

## Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab
- An OpenAI API key (or compatible LLM provider)

### Installation

```bash
git clone https://github.com/codeantik/self-rag.git
cd self-rag
pip install -r requirements.txt   # if provided, else install dependencies per notebook
```

### Running the Notebooks

Work through the notebooks in order to understand each component of the pipeline:

```bash
jupyter notebook self_rag_step1.ipynb
```

Or open them all at once in JupyterLab:

```bash
jupyter lab
```

### Environment Variables

Set your API key before running any notebook:

```bash
export OPENAI_API_KEY="your-api-key-here"
```

---

## Key Concepts

**Retrieval Grading** — A separate LLM call evaluates whether each retrieved document is relevant to the query, filtering out noise before generation.

**Hallucination Grading** — After generation, the answer is checked against the source documents to ensure all claims are grounded.

**Answer Grading** — A final check determines whether the generated answer actually resolves the original question, or whether re-retrieval is needed.

**Web Search Fallback** — The `self_rag_web.ipynb` variant incorporates live web search when local document retrieval is insufficient.

---

## Tech Stack

- **LangChain** — Pipeline orchestration and LLM integration
- **LangGraph** — Graph-based control flow for the retrieval/generation loop
- **ChromaDB / FAISS** — Vector store for document embeddings
- **OpenAI GPT** — Language model for generation and grading steps
- **Jupyter Notebooks** — Step-by-step interactive walkthrough

---

## Contributing

Contributions and improvements are welcome. Feel free to open an issue or submit a pull request.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## License

This project is open source. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

Inspired by the original [Self-RAG paper](https://arxiv.org/abs/2310.11511): *"Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection"* by Asai et al. (2023).
