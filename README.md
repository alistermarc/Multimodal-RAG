# Multimodal RAG Pipeline for Document Analysis

This project outlines a complete, end-to-end pipeline for processing PDF documents to build a multimodal Retrieval-Augmented Generation (RAG) system. The pipeline extracts text and figures from a document, generates AI-powered summaries for the figures, and builds a hybrid search retriever that can answer questions using both text and image context.

A crucial part of this pipeline is the dynamic retrieval stage, which brings the multimodal capabilities to life. In this process, the extracted figures are first summarized by an AI. It is these text-based summaries that are stored and embedded in the vector database, while the original image files are kept in a local folder. When a user's query retrieves a chunk containing a figure's summary, the system is designed to fetch the corresponding original image from the folder. This image—not its summary—is then sent to the multimodal language model as direct visual context, allowing the AI to generate a comprehensive answer based on both the textual and visual information.

The workflow is broken down into major steps, which should be run in order within Jupyter Notebook.

---

## 🛠️ Prerequisites

Before you begin, ensure you have the following:

### 1. Python Environment
A working Python environment (e.g., using Anaconda or `venv`) with **Jupyter Notebook** installed.

### 2. Required Libraries
Install all necessary libraries by running the following command in a notebook cell:

```bash
pip install boto3 python-dotenv pandas PyMuPDF langchain-openai langchain langchain-community chromadb rank_bm25
```

### 3. AWS Credentials
An AWS account with an S3 bucket already created.

### 4. .env File
Create a file named .env in the root of your project directory with the following content, replacing the placeholders with your actual credentials:

```env
AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY
AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_KEY
AWS_DEFAULT_REGION=your-aws-region
AWS_BUCKET_NAME=your-s3-bucket-name
OPENAI_API_KEY=your-openai-api-key
```

---