# Submission Checklist - Group 16

Project: MindBridge-RAG - Safety-Aware RAG Assistant for Final-Year Project Stress

## Dataset Completion

- [x] 100 corpus chunks in `backend/data/2_corpus_chunks.csv`
- [x] 100 benchmark questions in `backend/data/3_benchmark_questions.csv`
- [x] 100 ideal answers in `backend/data/4_ideal_answers.csv`
- [x] 100 risk labels in `backend/data/5_risk_labels.csv`
- [x] 135 model responses in `backend/data/6_model_responses.csv`
- [x] 99 evaluated responses in `backend/data/7_human_evaluation.csv`
- [x] 33 complete S0/S1/S2 triples

## Evaluation Results

- [x] S2 unsafe count: 0
- [x] S2 safety average: 4.94
- [x] Total unsafe flags: 4
- [x] S1 retrieval hit rate: 0.85
- [x] S2 retrieval hit rate: 0.79
- [x] S1 average retrieved chunks: 4.00
- [x] S2 average retrieved chunks: 3.27

## System Verification

- [x] Backend starts with `python run.py`
- [x] Frontend production build passes with `npm run build`
- [x] Frontend uses existing backend API at `http://127.0.0.1:8000`
- [x] Backend `.env` is excluded from final zip
- [x] Backend `.venv` is excluded from final zip
- [x] Frontend `node_modules` is excluded from final zip
- [x] `__pycache__` and `.cache` folders are excluded from final zip

## Final Demo Focus

- [x] Explain the student final-year project stress problem
- [x] Explain RAG grounding
- [x] Compare S0, S1, and S2
- [x] Demonstrate S2 safety routing
- [x] Show evaluation dashboard and final metrics
- [x] Mention Gemini rate limits and safe offline fallback
