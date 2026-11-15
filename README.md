# The Digital Registrar: Voice-First ITSM & Workflow Automation

> **An AI-driven operational workflow designed to intercept and resolve routine administrative queries, reducing manual helpdesk dependency and SLA resolution times.**

---

## The Business Problem
Administrative helpdesks face significant operational bottlenecks due to the high volume of routine queries (e.g., fee balances, attendance records, compliance metrics). This manual ticketing process consumes valuable human capital and inflates Service Level Agreement (SLA) response times. The objective was to engineer an automated, voice-first support workflow capable of resolving these Level-1 support queries instantly in localized languages, freeing human agents for complex escalations.

## The Data & Architecture
* **Structured Data:** Integrated a live MySQL database mapping complex relational entities (User Profiles, Financials, Attendance, Departmental hierarchies) to act as the primary source of truth.
* **Unstructured Data (RAG):** Deployed a local vector database (ChromaDB) to embed and retrieve general institutional policies, creating a dual-pipeline system (SQL for quantitative metrics, RAG for qualitative policy).
* **Multilingual Localization:** Engineered the system to process and respond to queries in English, Tamil, and Tanglish, directly addressing the demographic realities of the localized user base.

## The Tech Stack
* **Core Engine:** Python, Flask (Web API bridging)
* **AI & Language Processing:** Google Gemini 2.5 Flash, all-MiniLM-L6-v2 (Embeddings), Faster-Whisper (GPU-accelerated Local STT)
* **Data Storage:** MySQL (Structured), ChromaDB (Vector)
* **Voice Synthesis:** gTTS (Primary online), pyttsx3 (Offline fallback)

---

## Key Strategic & Engineering Decisions

| Concern | Strategic Solution |
|---|---|
| **Data Privacy & Hallucination Guard** | LLM is strictly fed context via dynamic SQL queries and semantic RAG retrieval. The model is mathematically prevented from inventing financial or academic records. |
| **System Resilience (Fallback)** | Engineered a dual-layer TTS system. If network latency impacts the primary cloud TTS, the system falls back to a local offline engine to maintain seamless user experience. |
| **Accessibility & Frictionless UX** | Implemented a pure voice-to-voice interface. Users authenticate and query entirely through speech, removing the UI friction of typing complex queries. |

---

## The Business Impact
* **Operational Efficiency:** Successfully proved the viability of deploying an automated intercept layer for Level-1 support tickets. 
* **SLA Reduction:** Drops average routine query resolution time from hours (manual ticketing) to under 10 seconds (automated voice response).
* **Enterprise Scalability:** The underlying architecture (SQL + Vector RAG + Multilingual Voice Interface) serves as a direct blueprint for automating corporate HR workflows, internal IT helpdesks, or client-facing customer service portals.

---

## 🚀 Deployment Instructions (Local Environment)

### Prerequisites
- Python 3.11+
- CUDA Toolkit (Optional, for GPU-accelerated Whisper inference)
- MySQL Server running locally with the target database.
- A `GEMINI_API_KEY` set as an environment variable.

### Launch Protocol
```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. To run the CLI/Local Voice Engine
python theapp.py

# 3. To run the Web-based Interface
python web_ivr.py
