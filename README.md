# Enterprise RAG & Conversational Agents with LangChain

A modular Retrieval-Augmented Generation (RAG) system built with LangChain, ChromaDB, and local Hugging Face embeddings, integrated with cloud-agnostic Large Language Models (LLMs) via OpenRouter and LangChain Core.

This project demonstrates the end-to-end implementation of an intelligent document retrieval and reasoning pipeline, moving from raw unstructured data ingestion to a stateful conversational assistant with memory.

---

## Architecture Overview

The system follows an industry-standard decoupled architecture designed for high privacy, cost efficiency, and modularity:

```
[ Unstructured Documents ]
           │
           ▼
[ Character / Recursive Text Splitter ]
           │
           ▼
[ Hugging Face Embeddings (Local) ]
           │
           ▼
[ Chroma Vector Database ]
           │
           ├─── Semantic Similarity Search (Top-K)
           │
           ▼
[ Prompt Engineering & Anti-Hallucination Guardrails ]
           │
           ▼
[ LLM Inference Engine (OpenRouter / Llama 3.2 / Any OpenAI-Compatible Provider) ]
           │
           ▼
[ ConversationBufferMemory (Multi-Turn Context) ]
           │
           ▼
[ Conversational Retrieval Interface ]
```

---

## Key Components Implemented

### 1. Document Ingestion and Chunking
* Text ingestion from unstructured corporate policy documents.
* Chunking strategy using `CharacterTextSplitter` with defined chunk sizes and overlap to preserve semantic context across chunk boundaries.

### 2. Local Semantic Embeddings & Vector Storage
* Generation of high-dimensional vector representations using `HuggingFaceEmbeddings` running entirely locally, eliminating embedding API costs.
* Persistent indexing and similarity retrieval powered by `ChromaDB`.

### 3. Decoupled, Provider-Agnostic LLM Layer
* Elimination of proprietary vendor lock-in by replacing single-cloud dependencies with the standardized `ChatOpenAI` interface connected to OpenRouter.
* Secure credential management using `.env` files and `python-dotenv` to safeguard API keys outside repository tracking.

### 4. Custom Prompt Engineering & Anti-Hallucination Guardrails
* Implementation of explicit system instructions preventing the model from generating fabricated facts when context is absent.
* Parameterized templates using `PromptTemplate` with strict context binding.

### 5. Multi-Turn Conversational Memory
* Implementation of `ConversationBufferMemory` to retain interaction state.
* Integration of `ConversationalRetrievalChain`, which automatically reformulates follow-up queries containing pronouns or implicit references into standalone semantic search queries.
* Interactive command-line chat loop with graceful termination handling.

---

## Tech Stack

* Language: Python 3.10+
* Framework: LangChain, LangChain Core, LangChain Community, LangChain Classic
* Vector Store: ChromaDB
* Embeddings: Hugging Face Transformers (`sentence-transformers`)
* LLM Interface: `langchain-openai` (via OpenRouter API endpoint)
* Environment Management: `python-dotenv`

---

## Setup and Installation

### 1. Clone the repository and navigate to the project folder
```bash
git clone <your-repository-url>
cd "AI - RAG, LangChain and LLMs"
```

### 2. Install dependencies
```bash
pip install -U langchain langchain-core langchain-community langchain-chroma langchain-huggingface langchain-openai chromadb sentence-transformers python-dotenv
```

### 3. Configure environment variables
Create a `.env` file in the root directory:
```env
OPENROUTER_API_KEY=your_openrouter_api_key_here
```

### 4. Run the notebook
Launch Jupyter Notebook or Jupyter Lab and execute `RAG-and-Agents.ipynb`:
```bash
jupyter notebook RAG-and-Agents.ipynb
```

---

## Enterprise Applicability: International Logistics and Supply Chain

While demonstrated on organizational policies, the underlying architecture directly addresses critical operational bottlenecks in global trade and freight forwarding:

### 1. Customs Document Cross-Auditing
* Automated cross-verification between Bill of Lading (B/L), Commercial Invoice, and Packing List.
* Detects discrepancies in gross/net weight, consignee details, and item counts before vessel arrival, avoiding customs retention and terminal storage fees.

### 2. Semantic Tariff Classification (HS Code / NCM)
* Indexing official customs regulations, general interpretation rules, and tariff notes into ChromaDB.
* Enables semantic matching of commercial cargo descriptions to official tariff positions, delivering recommended HS codes with legal justification to prevent compliance penalties.

### 3. Contract Governance, Incoterms, and Demurrage Mitigation
* Rapid extraction of contracted free-time days, demurrage, and detention penalty rates from Master Service Agreements across ocean carriers.
* Instant evaluation of liability division based on Incoterms 2020 rules during transit disruptions.

### 4. Event-Driven Autonomous Agents
* Extending RAG pipelines with LangChain Tools and external APIs (carrier tracking, port congestion feeds, and ERP systems such as SAP or CargoWise).
* Empowers models to autonomously identify shipping delays, cross-reference contractual free-time, evaluate financial risk, and trigger mitigation workflows.

---

## Author

Mateus  
AI Specialist in International Logistics and Supply Chain
