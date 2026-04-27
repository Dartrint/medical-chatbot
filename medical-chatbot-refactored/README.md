# 🩺 Medical RAG Chatbot

### AI-Powered Clinical Question Answering System (with Source Grounding)
---

## 🚀 Overview

This project is an **AI-powered medical assistant** that answers clinical questions using a **Retrieval-Augmented Generation (RAG)** pipeline.

Instead of relying purely on a language model (which may hallucinate), the system:

* 🔎 Retrieves relevant medical knowledge from curated PDFs
* 🧠 Uses an LLM to generate answers **grounded in real sources**
* 📚 Provides **traceable evidence** for every response

> 💡 Designed as a practical implementation of an **AI Agent with retrieval memory**

---

## 🎯 Problem Statement

Traditional LLM-based chatbots:

* ❌ May hallucinate medical facts
* ❌ Lack verifiability
* ❌ Are unsafe for knowledge-sensitive domains

### ✅ This system solves it by:

* Grounding responses in **trusted medical documents**
* Using **semantic search (FAISS)** for accurate retrieval
* Returning **source-backed answers**

---

## 🧠 How It Works (RAG Pipeline)

```
PDF Documents → Text Chunking → Embeddings → FAISS Vector Store
                                      │
User Query → Semantic Retrieval (Top-k) ─┘
                    │
              Prompt Injection
                    │
            LLM Generation (Groq / HF)
                    │
        Final Answer + Source Evidence
```

---

## 💬 Demo

**User Query**

```
How is hypertension managed?
```

**Generated Answer (Example)**

```
Hypertension is typically managed through lifestyle modifications such as reducing salt intake,
regular exercise, and medication including ACE inhibitors or beta-blockers...
```

**Source Evidence**

```
[Source 1] Hypertension is defined as...
[Source 2] Treatment includes ACE inhibitors...
```

> ✅ Answers are **not generated blindly** — they are grounded in retrieved knowledge

---

## ✨ Key Features

* 🔎 **FAISS Vector Search** for fast semantic retrieval
* 🧠 **RAG-based Answer Generation** (reduces hallucination)
* 📚 **Source Attribution** (traceable answers)
* 🔌 **Multi-LLM Support**

  * HuggingFace (Mistral)
  * Groq (LLaMA-based models)
* ⚡ **Lightweight Embeddings** (`all-MiniLM-L6-v2`)
* 💬 **Interactive Chat UI (Streamlit)**
* 🧩 Modular & extensible architecture

---

## 🧰 Tech Stack

| Component  | Technology                          |
| ---------- | ----------------------------------- |
| LLM        | Groq (LLaMA), HuggingFace (Mistral) |
| Retrieval  | FAISS                               |
| Embeddings | SentenceTransformers                |
| Framework  | LangChain                           |
| Frontend   | Streamlit                           |
| Language   | Python                              |

---

## 🏗 Project Structure

```
.
├── data/                         # Medical PDF documents
├── vectorstore/db_faiss         # Persisted FAISS index
├── create_memory_for_llm.py     # Build vector database
├── connect_memory_with_llm.py   # CLI-based chatbot
├── medibot.py                   # Streamlit UI chatbot
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

### 1. Create Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Setup Environment Variables

Create `.env`:

```env
HF_TOKEN=your_huggingface_token
GROQ_API_KEY=your_groq_api_key
```

---

## 🗂 Build Vector Store (One-time)

```bash
python create_memory_for_llm.py
```

This step:

* Loads medical PDFs
* Splits into chunks
* Generates embeddings
* Stores them in FAISS

---

## 💻 Run the Application

### ▶ CLI Version (HuggingFace)

```bash
python connect_memory_with_llm.py
```

---

### 🖥 Streamlit Chat UI (Recommended)

```bash
streamlit run medibot.py
```

Open:

```
http://localhost:8501
```

---

## 🔄 Embedding Mode Options

You can switch between:

### Local Embeddings

```python
get_vectorstore()
```

### API-based Embeddings

```python
get_vectorstore_hf_api(HF_TOKEN)
```

---

## 🧪 Quick Test

```bash
python - <<'PY'
from langchain_huggingface import HuggingFaceEmbeddings
from langchain_community.vectorstores import FAISS

emb = HuggingFaceEmbeddings(model_name='sentence-transformers/all-MiniLM-L6-v2')
db = FAISS.load_local('vectorstore/db_faiss', emb, allow_dangerous_deserialization=True)

print(db.similarity_search('What is diabetes?', k=2))
PY
```

---

## 📘 What I Learned

* Built an end-to-end **RAG pipeline**
* Applied **vector similarity search (FAISS)**
* Integrated **LLM APIs (Groq, HuggingFace)**
* Designed **prompt templates for grounded QA**
* Developed a **modular AI system architecture**
* Improved understanding of **AI Agents with memory**

---

## 🧱 Future Improvements

* 🔬 Add evaluation metrics (RAGAS, faithfulness score)
* 💾 Persistent chat memory
* 🌐 Deploy as web service (Docker / Cloud)
* 🧠 Fine-tuned medical LLM
* 📊 Multi-document retrieval optimization

---

## ⚖️ Disclaimer

This project is for **educational purposes only**.
It does **not provide medical advice**. Always consult a licensed healthcare professional.

---

## ✅ Quick Start

```bash
python create_memory_for_llm.py
streamlit run medibot.py
```

