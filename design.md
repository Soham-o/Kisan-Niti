# 🌾 Kisan-Niti: AI-Powered Agricultural Scheme Assistant

> **Mission:** Bridging the gap between complex government policy and the Indian farmer using Generative AI.

---

## 1. 🚩 Problem Statement
Indian farmers struggle to access critical government schemes (subsidies, insurance, loans) because the information is locked in complex, lengthy PDF documents often available only in English or formal Hindi. 

* **The Pain Point:** "Information Asymmetry" leads to millions of rupees in unclaimed benefits.
* **The Gap:** Farmers rely on middlemen or word-of-mouth, which is often inaccurate.

## 2. 💡 Proposed Solution
**Kisan-Niti** is a Generative AI-powered chatbot that acts as a 24/7 personal assistant for farmers. It uses **Retrieval-Augmented Generation (RAG)** to read official government scheme documents and answer farmer queries in simple, actionable language.

---

## 3. 🛠️ Functional Requirements

### **User Interface (Frontend)**
* **Chat Interface:** A clean, WhatsApp-style chat window where users can type queries (e.g., *"How do I apply for PM-KISAN?"*).
* **Language Support:** The system must process queries in **English** and **Hindi** (MVP phase).
* **Voice Input (Optional):** A microphone button to accept voice queries for accessibility.

### **Core AI Features (Backend)**
* **Document Ingestion:** The system must ingest and index PDF documents of government schemes (e.g., *Pradhan Mantri Fasal Bima Yojana*).
* **Contextual Search:** The system must retrieve the most relevant sections of the schemes based on the user's query.
* **Fact-Based Generation:** The system must generate summaries based *only* on the provided documents to prevent "hallucinations."
* **Source Citation:** The AI should cite which scheme document the information came from.

---

## 4. ⚙️ Non-Functional Requirements
* **Accuracy:** The model must prioritize factual accuracy over creativity.
* **Latency:** Responses should be generated within **5-7 seconds**.
* **Scalability:** The architecture must handle multiple concurrent users using serverless components.
* **Data Privacy:** User queries should not be stored permanently for training purposes without consent.

---

## 5. ☁️ AWS Service Requirements
| Service | Purpose |
| :--- | :--- |
| **Amazon Bedrock** | Access to Foundation Models (Claude 3 Sonnet) & Knowledge Bases. |
| **Amazon S3** | Storage for source PDF documents. |
| **AWS Lambda** | Serverless compute to handle backend logic and API requests. |
| **Amazon Titan Embeddings** | To convert text into vector embeddings for search. |
