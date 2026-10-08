# influenza-surveillance-rag
```markdown
# Influenza Surveillance RAG (Retrieval-Augmented Generation) Pipeline

This repository contains an end-to-end Python pipeline designed to ingest, clean, and analyze influenza genomic metadata, then index the structured records into a FAISS vector store to power an intelligent, epidemiologically-aware QA bot using Anthropic's Claude (`claude-haiku-4-5-20251001`).

## 📌 Project Overview
Traditional search or LLM querying on raw spreadsheet data lacks synthesized contextual knowledge. This project bridges that gap by combining a **Pattern Summary** (aggregated stats from the entire dataset) with a **Similarity Search Retriever** (highly relevant individual records) in a single unified prompt template.

### Key Features
* **Automated Processing:** Concatenates multiple genomic spreadsheets, cleans locations, standardizes subtypes, parses collection dates, and derives seasons.
* **Fast Vector Search:** Leverages `sentence-transformers/all-mpnet-base-v2` and FAISS for sub-millisecond retrieval of historical metadata records.
* **Dual-Context Prompting:** Feeds both global analytical patterns (e.g., top locations, seasonal counts) and localized record retrievals to the LLM.
* **Modern LCEL Implementation:** Leverages LangChain Expression Language (LCEL) for robust, reproducible prompt chaining.

## 🛠️ Tech Stack
* **Data Wrangling:** `pandas`, `openpyxl`
* **Orchestration:** `langchain`, `langchain-community`, `langchain-anthropic`
* **Vector Search:** `faiss-cpu`
* **Embedding Models:** `sentence-transformers/all-mpnet-base-v2` (Hugging Face)
* **Generative Model:** Anthropic Claude 3.5 / 4.5

## 📂 Repository Structure
```
├── data/
│   └── USA/                 # Raw spreadsheet files (.xls / .xlsx)
├── src/
│   └── pipeline.py          # Main processing, indexing, and QA chain execution
├── README.md                # Project documentation
└── requirements.txt         # Package dependencies
```

## 🚀 Quick Start & Setup

### 1. Clone the repository
```bash
git clone https://github.com/your-username/influenza-surveillance-rag.git
cd influenza-surveillance-rag
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```
*Make sure to include:* `langchain`, `langchain-community`, `langchain-anthropic`, `faiss-cpu`, `sentence-transformers`, `pandas`, and `openpyxl`.

### 3. Set your API Key
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

### 4. Run the Pipeline
Prepare your spreadsheet files inside the designated directory and run the pipeline script:
```python
from src.pipeline import ask

# Example Query
ask("What is the most common influenza subtype?")
```

## 📊 Example Queries Supported
* *"Are there any seasonal patterns in the data?"*
* *"Which states/locations have the most cases?"*
* *"Has any subtype been increasing or decreasing over time?"*
```
