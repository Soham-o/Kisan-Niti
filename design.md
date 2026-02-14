# 🏗️ System Design: Kisan-Niti

## 1. 📐 High-Level Architecture
The system follows a **Serverless RAG (Retrieval-Augmented Generation)** architecture entirely hosted on AWS. It decouples the frontend from the heavy AI processing to ensure scalability and cost-efficiency.

**Logic Flow:**
`User Query` ➡️ `Frontend` ➡️ `AWS API Gateway` ➡️ `Lambda` ➡️ `Amazon Bedrock` ➡️ `Response`

---

## 2. 🧩 Component Architecture

### **A. Data Layer (The Knowledge Base)**
* **Storage:** **Amazon S3** stores the raw PDF files (Government Schemes).
* **Vector Database:** **Amazon OpenSearch Serverless** (managed via Bedrock) stores the vector embeddings of the text.
* **Ingestion Pipeline:** **Amazon Bedrock Knowledge Base** automatically syncs data from S3, chunks the text, and converts it to vectors using **Amazon Titan Embeddings v2**.

### **B. Intelligence Layer (The Brain)**
* **Model:** **Anthropic Claude 3 Sonnet** (via Amazon Bedrock).
* **Reasoning:** The model receives the user query + relevant chunks from the vector store and generates a simplified answer.

### **C. Application Layer (The Logic)**
* **Backend:** **AWS Lambda** functions (Python) act as the middleware. They take the user input from the frontend, call the `RetrieveAndGenerate` API of Amazon Bedrock, and return the response.
* **API Management:** **Amazon API Gateway** exposes the Lambda function as a REST API endpoint.

### **D. Presentation Layer (The UI)**
* **Frontend:** A lightweight web application (built with Streamlit or React) hosted on **AWS Amplify**.

---

## 3. 🔄 Data Flow Diagram
1.  **Upload:** Admin uploads `PM-KISAN.pdf` to the S3 Bucket.
2.  **Sync:** Bedrock Knowledge Base syncs the file ➡️ creates embeddings ➡️ stores in OpenSearch.
3.  **Query:** Farmer asks *"What is the subsidy for tractors?"*
4.  **Retrieve:** Bedrock searches the vector store for *"tractor subsidy"* context.
5.  **Generate:** Claude 3 receives the search results and drafts a simplified response in the requested language.
6.  **Deliver:** The response is sent back to the user app via API Gateway.

---

## 4. 💻 Tech Stack Summary

| Component | Technology |
| :--- | :--- |
| **Cloud Provider** | AWS (Amazon Web Services) |
| **LLM (Model)** | Claude 3 Sonnet (via Bedrock) |
| **Embeddings** | Titan Embeddings G1 - Text |
| **Storage** | Amazon S3 |
| **Compute** | AWS Lambda (Serverless) |
| **Frontend** | Streamlit (Python) |
