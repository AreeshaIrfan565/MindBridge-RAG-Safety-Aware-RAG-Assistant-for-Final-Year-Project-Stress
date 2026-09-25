# MindBridge-RAG - Group 16

Safety-Aware RAG Assistant for Final-Year Project Stress.

## Team

- Hassaan (049)

## Project Overview

MindBridge-RAG is a final-year project stress support chatbot that compares three AI system designs:

- **S0 Basic LLM:** baseline chatbot response without retrieval grounding.
- **S1 Basic RAG:** retrieval-augmented chatbot that uses corpus chunks before answering.
- **S2 Safety-aware RAG:** retrieval-augmented chatbot with risk classification, safety routing, and response safety checking.

S2 is the main contribution. It routes crisis, medical-boundary, and out-of-scope inputs to safer rule-based guidance instead of relying only on normal generation.

## Backend Run Commands

```powershell
cd "C:\Users\Hp\Desktop\mindbridge_rag_group16\backend"
.\.venv\Scripts\Activate.ps1
python run.py
```

Backend URL:

```text
http://127.0.0.1:8000
```

Useful endpoints:

```text
GET  /api/admin/validate
POST /api/admin/rebuild-index
POST /api/chat
GET  /api/evaluation/metrics
```

## Frontend Run Commands

```powershell
cd "C:\Users\Hp\Desktop\mindbridge_rag_group16\frontend"
npm install
npm run dev
```

Frontend URL:

```text
http://127.0.0.1:5173
```

Production build:

```powershell
npm run build
```

## Data Files

The project data is stored in `backend/data/`:

- `1_sources.csv`
- `2_corpus_chunks.csv`
- `3_benchmark_questions.csv`
- `4_ideal_answers.csv`
- `5_risk_labels.csv`
- `6_model_responses.csv`
- `7_human_evaluation.csv`
- `evaluation_summary.csv`
- `risk_evaluation_summary.csv`
- `retrieval_summary.csv`

## Evaluation Snapshot

- Corpus chunks: 100
- Benchmark questions: 100
- Ideal answers: 100
- Risk labels: 100
- Model responses: 135
- Evaluated responses: 99
- Complete S0/S1/S2 triples: 33
- S2 unsafe count: 0
- S2 safety average: 4.94
- S1 retrieval hit rate: 0.85
- S2 retrieval hit rate: 0.79

## Gemini Rate Limits and Safe Fallback

During testing, some Gemini requests returned API rate-limit errors. The backend handled those cases with a safe offline fallback response while preserving retrieval output and S2 safety routing behavior. This prevents the demo from failing when the external model API is temporarily unavailable or rate-limited.

## Safety Rules

- No diagnosis.
- No medication advice.
- No therapy plan.
- No private student stories.
- L3 crisis cases bypass normal RAG in S2.
- L4 medical cases refuse diagnosis or medication advice and suggest qualified support.
- L5 out-of-scope cases stay within the MindBridge academic-stress support scope.
