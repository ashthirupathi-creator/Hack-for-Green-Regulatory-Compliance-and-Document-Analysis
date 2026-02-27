# Real-Time Compliance RAG 🛡️⚖️
### *Streaming Regulatory Intelligence with Pathway & Groq*

![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![Pathway](https://img.shields.io/badge/Framework-Pathway-green)
![LLM](https://img.shields.io/badge/LLM-Llama--3.3--70B-orange)
![Accelerator](https://img.shields.io/badge/Inference-Groq-red)

An industrial-grade, streaming **Retrieval-Augmented Generation (RAG)** pipeline designed for financial institutions. It automates the analysis of regulatory documents and audit reports by eliminating the "Indexing Latency" found in traditional vector databases.

---

## 🚀 The Core Problem: Indexing Latency
In high-stakes compliance, a policy updated 10 minutes ago is already the "law of the land." 
* **Traditional RAG:** Requires manual triggers to re-index data, causing a "knowledge gap" where the AI provides outdated legal advice.
* **Our Solution:** Uses **Pathway's Unified Engine** to create a live sync between Google Drive and the LLM. If a file changes, the vector space updates in milliseconds.

---

## 🏗️ Technical Architecture & Pathway Integration

The system bypasses traditional batch processing in favor of a **Unified Streaming Pipeline**:



1.  **Streaming Ingestion:** We utilized `pathway.io.gdrive` to create a live listener. This detects "File Create," "File Update," or "File Delete" events in the source Google Drive folder instantly.
2.  **Adaptive Parsing:** Employs **Docling** to handle complex financial layouts (multi-column PDFs, nested tables) that standard parsers often break.
3.  **Local Vectorization:** Vectors are computed locally using `SentenceTransformer` on **CUDA**, ensuring document embeddings never leave your secure environment.
4.  **Instantaneous Indexing:** We utilized Pathway’s unified **VectorStoreServer**. This keeps the vector index in-memory and synchronized with the data source, providing sub-second retrieval times.
5.  **LLM Reasoning:** Queries are processed by **Groq’s Llama-3.3-70B**, providing a "Senior Compliance Officer" persona for precise, formal responses.

---

## 📂 Project Structure

```bash
green_hackathon/
├── src/
│   ├── main.py             # Entry point: Starts the Pathway streaming server
│   ├── answerer.py         # Client script: Handles user queries and Groq API calls
│   └── utils/
│       ├── parser.py       # Custom Docling configuration for financial PDFs
│       └── embeddings.py   # Local embedding logic (CUDA optimized)
├── .gitignore              # Prevents leaking credentials.json and __pycache__
├── credentials.json        # Google Cloud Service Account / OAuth keys
├── README.md               # Detailed documentation
└── requirements.txt        # Exact versions for reproducibility
