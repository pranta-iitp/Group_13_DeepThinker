# Group_13_DeepThinker

# Mini RAG-Powered Assistant

## Overview

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

## Architecture

```
        <img width="1037" height="601" alt="image" src="https://github.com/user-attachments/assets/afa21b85-2e0a-4e08-82f2-d7c9fe901fda" />

```

---

## 1. Corpus Preparation

* Purpose: Build a high-quality, domain-specific knowledge base.
* Collected 3–5 English documents containing Indian folktales
* Sources include public datasets, story collections, and curated articles
* Preprocessing steps:

* Text normalization
* Removal of noise and metadata
* Logical paragraph segmentation
* Text is chunked into 300–500 token blocks
* Chunk overlap is applied to preserve story continuity

---

## 2.Embedding Layer

* Model Used: sentence-transformers/all-MiniLM-L6-v2
* Why embeddings are required:
  * Converts text into dense semantic vectors
  * Enables meaning-based retrieval instead of keyword matching
  * Improves recall for paraphrased user queries
  * Process:
    * Each text chunk → embedding vector
    * Each user query → embedding vector

## 3. Embeddings & Vector Store

### Embedding Model Used: 

* **google/flan-t5-base**

### Vector Database

* **FAISS** (local, lightweight, fast)

---

## 4. Query Handling Flow

### Steps

1. Convert user query → embedding
2. Perform **similarity search** in FAISS
3. Retrieve top-K relevant chunks
4. Pass context + user prompt → LLM
5. LLM generates final grounded answer

## 5.Tech Stack


### **FLAN-T5 (LLM)**

### Why Used

* Instruction-tuned encoder–decoder model
* Performs well when provided with external context
* Lower computational cost compared to large decoder-only LLMs
* Suitable for question answering and text generation tasks

### Role in the System

* Generates final answers using retrieved folktale context
* Ensures responses remain grounded and relevant



### **Sentence Transformers**

### Model: `all-MiniLM-L6-v2`

### Why Used

* Produces high-quality semantic embeddings
* Captures meaning beyond keyword matching
* Fast and efficient on CPU
* Widely adopted for semantic search applications

### Role in the System

* Converts folktale text chunks and user queries into vector embeddings
* Enables semantic similarity search



## **FAISS (Vector Database)**

### Why Used

* Optimized for fast similarity search over dense vectors
* Lightweight and open-source
* Works efficiently without cloud dependency
* Scales well for medium-sized document collections

### Role in the System

* Stores document embeddings
* Retrieves top-K relevant folktale chunks for a given query

---
