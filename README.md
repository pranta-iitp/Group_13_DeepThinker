# Group_13_DeepThinker

# 🧠 Mini RAG-Powered Assistant

## 📌 Overview

This project implements a **Mini RAG (Retrieval-Augmented Generation) Assistant** capable of answering user queries based on a **custom knowledge base of Indian folktales**.
The assistant uses **embeddings**, a **vector database**, and an **LLM** to retrieve relevant context and generate accurate, grounded responses. This approach significantly reduces hallucination and improves factual and contextual accuracy.

Objective

* Design and implement an end-to-end RAG pipeline
* Use Sentence Transformers for semantic embeddings
* Use FAISS as a vector database for similarity search
* Use FLAN-T5 for grounded answer generation
* Demonstrate understanding of GenAI system architecture
* Cloud Deployment

---

## 🚀 Architecture

```
          ┌──────────────────────┐
          │   Document Corpus     │
          │  (PDFs / Articles)    │
          └─────────┬────────────┘
                    │
            Preprocessing & Chunking
                    │
          ┌─────────▼──────────┐
          │   Embedding Model  │
          │ (OpenAI / HF etc.) │
          └─────────┬──────────┘
                    │
          ┌─────────▼──────────┐
          │ Vector Store        │
          │ (FAISS / Pinecone)  │
          └─────────┬──────────┘
                    │ Similarity Search
          ┌─────────▼──────────┐
          │ Node.js Query Layer │
          │ (API / Web UI / CLI)│
          └─────────┬──────────┘
                    │ Context Passing
          ┌─────────▼──────────┐
          │     LLM (Gen AI)   │
          │ ChatGPT / OpenSource│
          └─────────┬──────────┘
                    │
           ┌────────▼────────┐
           │ Final Answer     │
           └──────────────────┘
```

---

## 🗂️ 1. Corpus Preparation

* Selected **3–5 documents** (PDFs, technical articles, sample internal docs).
* Performed:

  * Cleaning (removing headers, footers, symbols)
  * Chunking (using sliding window or fixed chunk size)
  * Converting text to JSON/Markdown chunks

---

## 🔍 2. Embeddings & Vector Store

### Embedding Model Used: 

* **google/flan-t5-base**

### Vector Database

* **FAISS** (local, lightweight, fast)

---

## ❓ 3. Query Handling Flow

### User Query (Node.js frontend)

* Simple UI or CLI where user types a question.

### Steps

1. Convert user query → embedding
2. Perform **similarity search** in FAISS
3. Retrieve top-K relevant chunks
4. Pass context + user prompt → LLM
5. LLM generates final grounded answer

### Tech Stack

* FLAN-T5 (LLM)

Why used:

Instruction-tuned encoder–decoder model

Performs well when provided with external context

Lower computational cost compared to large decoder-only LLMs

Suitable for question answering and text generation tasks

Role in the system:

Generates final answers using retrieved folktale context

Ensures responses remain grounded and relevant
* Sentence Transformers

Model: all-MiniLM-L6-v2

Why used:

Produces high-quality semantic embeddings

Captures meaning beyond keyword matching

Fast and efficient on CPU

Widely adopted for semantic search applications

Role in the system:

Converts folktale text chunks and user queries into vector embeddings

Enables semantic similarity search
* FAISS (Vector Database)

Why used:

Optimized for fast similarity search over dense vectors

Lightweight and open-source

Works efficiently without cloud dependency

Scales well for medium-sized document collections

Role in the system:

Stores document embeddings

Retrieves top-K relevant folktale chunks for a given query

---

## ☁️ 4. Cloud Deployment

* Deploy backend on **Azure App Service / Azure Container Apps**
* Store vector DB locally or on cloud storage
* Use **GitHub** for version control
* Optionally integrate **GitHub Copilot** for faster development

---

## 🛠️ Setup Instructions

### 1️⃣ Clone Repository

```bash
git clone https://github.com/pranta-iitp/Group_13_DeepThinker.git
cd mini-rag-assistant
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Environment Variables

Create a `.env` file:

```
OPENAI_API_KEY=your_key_here
PORT=3000
```

### 4️⃣ Build Embeddings

```bash
node scripts/embed.js
```

### 5️⃣ Run the App

```bash
node server.js
```

### 6️⃣ Access UI

```
http://localhost:3000
```

---

## 📦 Folder Structure

```
📁 mini-rag-assistant
│── 📁 data/               # Raw documents
│── 📁 chunks/             # Preprocessed & chunked data
│── 📁 vectorstore/        # FAISS or Pinecone index
│── 📁 scripts/            # ETL scripts (chunking, embedding)
│── server.js              # Node.js backend
│── index.html             # Basic UI (optional)
│── README.md
│── .env
```

---

## 📘 Learnings

### ✔ Understanding of RAG Pipeline

Learned how documents → chunks → embeddings → vector search → LLM response are connected.

### ✔ Working with Vector Databases

FAISS/Chroma helped understand:

* similarity search
* vector indexing
* retrieval performance

### ✔ Cloud Deployment Experience

Deployed on Azure to practice:

* environment variables
* scalability
* CI/CD using GitHub

### ✔ Node.js Integration

Learned building a minimal API to handle:

* queries
* LLM calls
* retrieval logic

---

## ⚠️ Challenges & Solutions

### **1. Chunking Strategy Issues**

**Problem:** Poor chunking → irrelevant search results
**Fix:** Used overlapping window technique for better context retention.
