# AirGuard AI — Multi-Agent Daily Air Quality Action System 🛡️💨

> **Problem Statement #15**: Complete implementation of the AI-Powered Daily Air Quality Action Agent fulfilling all 6 official challenge objectives using RAG, Multi-Agent Architecture, and Langflow.

---

## 🎯 Full Objective Compliance Matrix

| # | Challenge Objective | AirGuard AI Implementation Details |
| :-: | :--- | :--- |
| **1** | **AQI Data Retrieval (RAG)** | Grounded retrieval over structured guideline corpus (`air_quality_guidelines.txt`) using Chroma Vector Store and MiniLM embeddings to prevent medical hallucination. Real-time Open-Meteo & Satellite RAG API source toggle. |
| **2** | **Personalized Health Recommendations** | Tailored to user age, sensitive health conditions (Asthma/Cardiovascular/Elderly), location, planned activity (running, sports), commute mode (motorcycle, metro), and outdoor duration. |
| **3** | **Predictive Alerts** | Calculates **Personal Exposure Score** ($\text{AQI} \times \text{Exposure Hours}$) and issues 24-hour predictive forecast alerts warning users of morning pollution spikes before they happen. |
| **4** | **Policy & Awareness Insights** | Summarizes community-level micro-actions (carpooling, no open burning) and government policy advisories (CPCB Stage II GRAP guidelines). |
| **5** | **Multi-Agent System** | Architecture featuring 4 specialized agent roles:<br>1. 📡 **AQI Data Agent** (fetches & interprets AQI data)<br>2. 🩺 **Health Advisory Agent** (personalized lifestyle suggestions)<br>3. 🔮 **Forecasting Agent** (predicts trends & risk warnings)<br>4. 📢 **Community Action Agent** (drives awareness campaigns) |
| **6** | **Visualization Dashboard** | Sleek Web UI Dashboard (`index.html`) displaying real-time metrics, risk badges, multi-agent status, health advisories, policy insights, and an interactive "What-If" simulator. |

---

## 🏗️ Multi-Agent RAG Architecture

```
                                USER CONTEXT & AQI DATA
                                           │
                                           ▼
                      ┌─────────────────────────────────────────┐
                      │    📡 Agent 1: AQI Data Agent           │
                      │    Fetches & interprets real-time data  │
                      └────────────────────┬────────────────────┘
                                           │
                                           ▼
                      ┌─────────────────────────────────────────┐
                      │    🔍 RAG Guideline Retriever           │
                      │    Retrieves Chroma DB safety rules     │
                      └────────────────────┬────────────────────┘
                                           │
                                           ▼
                      ┌─────────────────────────────────────────┐
                      │    🩺 Agent 2: Health Advisory Agent    │
                      │    Personalized age & risk advisories   │
                      └────────────────────┬────────────────────┘
                                           │
                                           ▼
                      ┌─────────────────────────────────────────┐
                      │    🔮 Agent 3: Forecasting Agent        │
                      │    Personal Exposure Score & 24h Alert  │
                      └────────────────────┬────────────────────┘
                                           │
                                           ▼
                      ┌─────────────────────────────────────────┐
                      │    📢 Agent 4: Community Action Agent   │
                      │    Policy advisories & awareness rules  │
                      └────────────────────┬────────────────────┘
                                           │
                                           ▼
                                 VISUALIZATION DASHBOARD
                       (Action Plan, Advisories, What-If Tools)
```

---

## 🛠️ Technology Stack

- **Framework**: Langflow Orchestration
- **Reasoning LLM**: IBM Granite 4.0 8B Instruct
- **RAG Vector Database**: Chroma DB
- **Embeddings**: HuggingFace (`all-MiniLM-L6-v2`)
- **Frontend Dashboard**: HTML5 / CSS3 / Vanilla JS (Glassmorphism Dark Mode)
- **Language**: Python 3.11

---

## 🧩 Langflow Components Used

1. **Chat Input**: Accepts user location, AQI, age, health conditions, activity, commute method, and exposure hours.
2. **File Loader**: Imports `knowledge/air_quality_guidelines.txt`.
3. **Text Splitter**: Chunks guidelines into searchable vector segments.
4. **Embedding**: Transforms text chunks into vector embeddings using MiniLM.
5. **Vector Store (ChromaDB)**: Stores vector indices for fast retrieval.
6. **Retriever**: Queries top-k guideline chunks based on user context.
7. **Prompt Template**: Formats prompt combining user input + retrieved context + instructions.
8. **Granite 4.0 8B Instruct**: Performs reasoning and generates structured multi-agent outputs.
9. **Chat Output**: Renders formatted recommendations to the dashboard.

---

## 🚀 Quick Start & Live Demo

1. **Web Dashboard**: Navigate to `http://localhost:8000` in your web browser.
2. **Langflow Graph**: Import `flow/airguard_flow.json` into Langflow canvas.
