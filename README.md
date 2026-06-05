# ReefMind — Coral Reef NLP Chatbot

## A domain-specific NLP chatbot for coral reef education and conservation, built on a custom dataset of 15,945 QA pairs curated from Corals of the World and Wikipedia. The project compares two retrieval architectures.

## Two Architectures

**Model A — SBERT Semantic FAQ Matcher**
Encodes questions using `all-MiniLM-L6-v2` into 384-dimensional embeddings, stored in a FAISS index. At inference, the user query is embedded and matched via cosine similarity — the closest pre-validated answer is returned directly. Zero hallucination risk, high precision within domain.

**Model B — Semantic Retrieval + LLM Generation (Fully Offline)**
Retrieves the top-k most relevant species attributes from the raw dataset, injects them as grounded context into a structured prompt, and streams a synthesized response via a local Ollama LLM. Runs entirely offline — no API calls, no internet required after setup. Greater flexibility for complex queries at the cost of potential generation variance.

---

## Dataset

- **Size:** 15,945 QA pairs synthetically generated from structured species data
- **Species coverage:** 831 unique coral species across 12 attributes
- **Sources:** Corals of the World, Wikipedia, iNaturalist
- **Geographic scope:** Indo-Pacific (97.6%) + Caribbean/Atlantic

---

## Getting Started

**1. Clone and set up environment**

```bash
git clone https://github.com/yashpandey0031/coral-reefs-nlp
cd coral-reefs-nlp
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # Windows
pip install -r requirements.txt
```

**2. Run Model A (Semantic FAQ)**

```bash
streamlit run app.py
```

**3. Run Model B (Retrieval + LLM)**

Install Ollama from [ollama.com](https://ollama.com), pull the model, then run:

```bash
ollama pull llama3.2
streamlit run app_rag.py
```

---

## Tech Stack

- SentenceTransformers (`all-MiniLM-L6-v2`)
- FAISS — vector similarity search
- Ollama + Llama 3.2 — local LLM inference
- Streamlit — UI

---
