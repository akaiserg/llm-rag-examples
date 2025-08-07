# LLM RAG Examples

A collection of Retrieval-Augmented Generation (RAG) examples demonstrating advanced query expansion techniques for document question-answering systems.

## Overview

This project showcases four powerful RAG enhancement techniques:

1. **Query Expansion with Multiple Queries** (`expansion_queries.py`) - Generates multiple related questions to improve retrieval coverage
2. **Query Expansion with Hypothetical Answers** (`expansion_answer.py`) - Creates hypothetical answers to improve semantic similarity matching
3. **Cross-Encoder Reranking** (`reranking.py`) - Uses cross-encoder models to rerank retrieved documents for better relevance
4. **DPR with Cross-Encoder** (`dpr_technique.py`) - Combines Dense Passage Retrieval with cross-encoder reranking for optimal results

All techniques use the Microsoft Annual Report as sample data, with some including UMAP visualizations of embedding spaces.

## Features

- 📄 PDF document processing and text extraction
- 🔧 Advanced text splitting strategies (character-based and token-based)
- 🔍 ChromaDB vector database for semantic search
- 🤖 OpenAI GPT integration for query expansion and final answer generation
- 🔄 Cross-encoder reranking for improved document relevance scoring
- 📊 UMAP visualization of embedding spaces
- 📈 Interactive matplotlib plots for result analysis

## Installation

### Prerequisites

- Python 3.11+
- OpenAI API key

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd llm-rag-examples
```

2. Install dependencies using `uv` (recommended):
```bash
uv sync
```

Or using pip:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file in the project root:
```env
OPENAI_API_KEY=your_openai_api_key_here
```

4. Place your PDF document in the `data/` directory (currently uses `microsoft-annual-report.pdf`)

## Usage

### Query Expansion with Multiple Queries

Generates multiple related questions to cast a wider retrieval net:

```bash
python expansion_queries.py
```

This technique:
- Takes an original query about revenue growth factors
- Generates 5 related questions using GPT-3.5
- Searches with all queries simultaneously
- Deduplicates and visualizes results

### Query Expansion with Hypothetical Answers

Creates hypothetical answers to improve semantic matching:

```bash
python expansion_answer.py
```

This technique:
- Takes an original query about profit and year-over-year comparison
- Generates a hypothetical answer using GPT-3.5
- Combines original query with hypothetical answer
- Searches using the enriched query

### Cross-Encoder Reranking

Improves retrieval quality by reranking documents using cross-encoder models:

```bash
python reranking.py
```

This technique:
- Retrieves initial documents using standard vector similarity
- Uses a cross-encoder model to score query-document pairs
- Reranks documents based on cross-encoder relevance scores
- Demonstrates improved relevance ordering

### DPR with Cross-Encoder Pipeline

Combines multiple techniques for optimal retrieval performance:

```bash
python dpr_technique.py
```

This technique:
- Implements multi-query expansion for broader retrieval
- Uses cross-encoder reranking for relevance scoring
- Deduplicates retrieved documents across multiple queries
- Generates final answers using top-ranked context

### Helper Functions

The `helper_utils.py` module provides:
- `word_wrap()` - Text formatting for display
- `project_embeddings()` - UMAP projection for visualization
- `extract_text_from_pdf()` - PDF text extraction
- `load_chroma()` - ChromaDB collection loading

## Project Structure

```
llm-rag-examples/
├── data/
│   └── microsoft-annual-report.pdf    # Sample document
├── expansion_queries.py               # Multi-query expansion
├── expansion_answer.py               # Hypothetical answer expansion
├── reranking.py                      # Cross-encoder reranking
├── dpr_technique.py                  # DPR with cross-encoder pipeline
├── helper_utils.py                   # Utility functions
├── main.py                          # Basic entry point
├── pyproject.toml                   # Project dependencies
└── README.md                        # This file
```

## Dependencies

- **chromadb** - Vector database for embeddings
- **langchain** & **langchain-community** - Text splitting and document processing
- **openai** - GPT models for query expansion and answer generation
- **pypdf** - PDF text extraction
- **sentence-transformers** - Embedding generation and cross-encoder reranking
- **umap-learn** - Dimensionality reduction for visualization
- **matplotlib** - Plotting and visualization
- **pandas** - Data manipulation and analysis

## Techniques Explained

### 1. Multi-Query Expansion

**Problem**: Single queries may miss relevant documents due to vocabulary mismatch.

**Solution**: Generate multiple related questions that cover different aspects of the topic.

**Benefits**:
- Broader retrieval coverage
- Captures different phrasings and perspectives
- Reduces vocabulary mismatch issues

### 2. Hypothetical Answer Expansion

**Problem**: Queries and documents may have different semantic structures.

**Solution**: Generate a hypothetical answer and use it to augment the original query.

**Benefits**:
- Better semantic alignment with document content
- Improves retrieval of answer-like passages
- Leverages LLM knowledge for query enrichment

### 3. Cross-Encoder Reranking

**Problem**: Vector similarity doesn't always correlate with semantic relevance.

**Solution**: Use a cross-encoder model to score query-document pairs for better ranking.

**Benefits**:
- More accurate relevance scoring than bi-encoder similarity
- Considers interaction between query and document
- Significantly improves retrieval precision

### 4. Multi-Technique Pipeline

**Problem**: Single techniques may not capture all aspects of effective retrieval.

**Solution**: Combine query expansion, retrieval, reranking, and generation in a pipeline.

**Benefits**:
- Leverages strengths of multiple approaches
- Broader retrieval coverage with precise reranking
- End-to-end answer generation with context

## Visualization

Query expansion examples include UMAP visualizations showing:
- 🔘 Gray dots: All document embeddings
- ❌ Red X: Original query
- ❌ Orange X: Expanded queries/hypothetical answers
- 🟢 Green circles: Retrieved documents

Cross-encoder examples focus on relevance scoring and ranking improvements.

## Customization

To use with your own documents:

1. Replace the PDF file in `data/`
2. Update the file path in the scripts
3. Modify the query expansion prompts for your domain
4. Adjust chunk sizes and overlap parameters as needed

## Troubleshooting

### Missing sentence-transformers

If you get an import error for `sentence_transformers`:

```bash
uv add sentence-transformers
```

### API Key Issues

Ensure your `.env` file contains a valid OpenAI API key:
```env
OPENAI_API_KEY=sk-...
```

## Contributing

Feel free to submit issues and enhancement requests!

## License

[Add your license here]