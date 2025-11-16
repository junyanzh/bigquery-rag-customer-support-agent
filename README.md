# BigQuery RAG Customer Support Agent

A production-ready multilingual customer support AI agent that leverages **BigQuery as a vector database** for Retrieval-Augmented Generation (RAG). The system performs semantic search over translated FAQ datasets and provides intelligent responses using Google's Gemini models.

## 🎯 Features

- **Semantic Search with BigQuery**: Utilizes `VECTOR_SEARCH` and `gemini-embedding-001` for efficient FAQ retrieval
- **Multilingual Support**: Handles Chinese and English queries with automatic translation pipeline
- **Hybrid Response Strategy**: Direct FAQ matching for high-confidence queries, LLM-refined answers for complex cases
- **Production-Ready Architecture**: Deployed on Vertex AI Workbench or Cloud Run with RESTful API

## 🏗️ Architecture

The system consists of three main components:

1. **Data Pipeline** (`MakTek-Customer-Support-FAQs-Translate.ipynb`): 
   - Loads MakTek FAQ dataset from Hugging Face
   - Translates Q&A pairs to Traditional Chinese using Gemini 2.5 Flash
   - Generates embeddings and loads to BigQuery

2. **RAG Agent** (`Customer-Chatbot-Agent-zh-tw.ipynb`):
   - Accepts user queries via HTTP endpoint
   - Performs vector similarity search in BigQuery
   - Returns direct answers or LLM-refined responses based on confidence scores

3. **Vector Database**: BigQuery table with semantic search capabilities

## 🚀 Getting Started

### Prerequisites

- Google Cloud Platform account with billing enabled
- Vertex AI API and BigQuery enabled
- Python 3.9+ environment
- Required GCP permissions for BigQuery and Vertex AI

### Setup

1. Clone this repository
2. Open `MakTek-Customer-Support-FAQs-Translate.ipynb` in Vertex AI Workbench
3. Configure your GCP project ID and dataset location
4. Run the data pipeline to populate BigQuery
5. Open `Customer-Chatbot-Agent-zh-tw.ipynb` to deploy the agent

## 🗃️ Data Source

This project uses the **MakTek Customer Support FAQs** dataset from Hugging Face, containing common customer service Q&A pairs in English, translated to Traditional Chinese (zh-TW) for bilingual support.

## 🛠️ Technology Stack

- **Cloud Platform**: Google Cloud Platform (Vertex AI, BigQuery)
- **LLM Models**: Gemini 2.5 Pro, Gemini 2.5 Flash
- **Embedding Model**: gemini-embedding-001
- **Vector Database**: BigQuery with `VECTOR_SEARCH` function
- **Languages**: Python, SQL

## 📊 How It Works

1. User submits a Chinese question via HTTP
2. Agent generates query embedding using Gemini
3. BigQuery performs semantic search over FAQ embeddings
4. System evaluates confidence score:
   - **High confidence**: Returns matched FAQ directly
   - **Low confidence**: Uses Gemini Pro for RAG-based answer generation
5. Response returned to user in Chinese

## 🔧 Configuration

Key parameters can be adjusted in the notebooks:

- `TOP_K`: Number of similar FAQs to retrieve (default: 5)
- `CONFIDENCE_THRESHOLD`: Distance threshold for direct answers
- `EMBEDDING_MODEL`: gemini-embedding-001 for multilingual support
- `LLM_MODEL`: Gemini variant for answer generation (gemini-2.5-pro)
- `TEMPERATURE`: Generation temperature (default: 0.3 for stable responses)
