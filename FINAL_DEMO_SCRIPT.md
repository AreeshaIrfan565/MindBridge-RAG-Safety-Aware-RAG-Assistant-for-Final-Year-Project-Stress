# Final Demo Script - 5 Minutes

Project: MindBridge-RAG - Group 16

## 0:00-0:40 - Problem

Introduce the problem: final-year project students often face deadline pressure, group conflict, supervisor anxiety, demo fear, and emotional stress. A normal chatbot may answer fluently but may not be grounded in the project knowledge base and may miss safety-sensitive situations.

Key line:

> MindBridge-RAG is designed to support final-year project stress while comparing basic generation, retrieval grounding, and safety-aware routing.

## 0:40-1:20 - RAG Concept

Explain Retrieval-Augmented Generation:

- The user asks a question.
- The system retrieves relevant corpus chunks.
- The response is generated using the retrieved context.
- This improves faithfulness compared with a basic chatbot.

Show the retrieval panel in the UI and point out chunk IDs, titles, source IDs, scores, and expandable chunk text.

## 1:20-2:10 - S0, S1, and S2

Explain the three systems:

- **S0 Basic LLM:** baseline response without retrieval.
- **S1 Basic RAG:** response grounded in retrieved chunks.
- **S2 Safety-aware RAG:** retrieval plus risk classification, safety routing, and response checking.

Key line:

> S2 is our main contribution because it does not treat every question as a normal generation task.

## 2:10-3:00 - Safety Routing

Explain risk labels:

- L0_NORMAL
- L1_STRESS
- L2_DISTRESS
- L3_CRISIS
- L4_MEDICAL
- L5_OUT_OF_SCOPE

Show that S2 routes crisis, medical-boundary, and out-of-scope cases differently. For example, medical questions should not receive diagnosis or medication advice, and crisis cases should bypass normal RAG generation.

Suggested demo question:

```text
I am not feeling safe because my project is failing.
```

Expected focus:

- Risk label appears in the safety panel.
- S2 uses safety-aware routing.
- Unsafe flag remains safe for S2.

## 3:00-4:00 - Live UI Demo

Open the frontend:

```powershell
cd "C:\Users\Hp\Desktop\mindbridge_rag_group16\frontend"
npm run dev
```

Open:

```text
http://127.0.0.1:5173
```

Run one normal stress question:

```text
My FYP deadline is close and I feel overwhelmed. What should I do first?
```

Point out:

- selected mode card
- response bubble
- response metadata
- risk confidence
- safety checker result
- retrieved chunks for RAG modes

## 4:00-4:40 - Evaluation Results

Show the evaluation dashboard:

- Model responses: 135
- Evaluated responses: 99
- Complete S0/S1/S2 triples: 33
- S2 unsafe count: 0
- S2 safety average: 4.94
- S1 retrieval hit rate: 0.85
- S2 retrieval hit rate: 0.79

Explain that S0 and S1 had unsafe flags on crisis-related benchmark rows, while S2 handled those rows more safely through routing.

## 4:40-5:00 - Limitations and Future Work

Mention limitations:

- Gemini can hit API rate limits.
- The backend uses safe offline fallback when rate-limited.
- The dataset is project-specific and should be expanded for broader deployment.
- Human evaluation can be expanded with more reviewers.

Closing line:

> MindBridge-RAG demonstrates that retrieval improves grounding, while safety-aware routing is necessary for responsible student-support chatbots.
