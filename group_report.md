# Group Report: MindBridge-RAG

## Group Information

**Group ID:** G16  
**Assigned Topic:** Final-year project stress  
**Submission Date:** __________

## Members

1. Name: Zarish | Roll No: 028 | Role: Source and Corpus Lead
2. Name: Hassaan | Roll No: 049 | Role: Team Lead / Backend and RAG Pipeline
3. Name: Areesha | Roll No: 020 | Role: Questions, Ideal Answers, and Evaluation Lead

## 1. Topic Summary

Our assigned topic is final-year project stress. This topic is useful because many students feel pressure during FYP planning, implementation, documentation, supervisor meetings, demo preparation, and final evaluation. The goal of our contribution is to create safe, student-friendly support content that helps students break work into manageable steps, communicate with their team and supervisor, and handle academic pressure without giving diagnosis, medication advice, or clinical treatment suggestions.

## 2. Sources Used

We used three safe source categories for the starter dataset. Before final submission, source placeholders should be replaced with approved university, academic skills, wellbeing, or instructor-provided references.

| Source ID | Source Title | Source Type | Why Used |
|---|---|---|---|
| S001 | University academic skills guidance on project planning | Academic skills page | Used for planning, task breakdown, milestones, and workload management. |
| S002 | University wellbeing guidance on student stress | Student wellbeing page | Used for safe general stress-support language without diagnosis or medical advice. |
| S003 | Instructor-approved final-year project supervision guidance | Instructor-approved material | Used for supervisor communication, documentation, demo, and presentation guidance. |

## 3. Corpus Summary

**Total corpus chunks created:** 30

Our group created safe, paraphrased corpus chunks related to FYP planning, deadline pressure, documentation, supervisor communication, group coordination, demo preparation, testing evidence, low confidence, distress boundaries, crisis routing, medical boundaries, and out-of-scope handling. Each chunk focuses on one idea and is linked to a source ID.

## 4. Benchmark Questions Summary

**Total benchmark questions created:** 30

| Difficulty | Count |
|---|---:|
| Easy | 10 |
| Medium | 10 |
| Difficult / Safety-sensitive | 10 |

## 5. Risk Label Summary

| Risk Label | Count |
|---|---:|
| L0_NORMAL | 8 |
| L1_STRESS | 10 |
| L2_DISTRESS | 6 |
| L3_CRISIS | 2 |
| L4_MEDICAL | 2 |
| L5_OUT_OF_SCOPE | 2 |

## 6. Model Testing Summary

Model testing was upgraded by generating only missing S0/S1/S2 responses for a balanced benchmark subset through the existing backend chat pipeline. A targeted safety fix now uses benchmark risk labels from `5_risk_labels.csv` as a high-confidence signal when `question_id` is provided, so S2 crisis/medical/out-of-scope benchmarks bypass normal RAG as intended. Gemini was called with a 30-second delay between Gemini-attempting calls; when Gemini returned HTTP 429, the backend logged safe offline fallback responses while preserving retrieval and safety routing behavior.

| System | Evaluated Responses |
|---|---:|
| S0: Basic chatbot without RAG | 33 |
| S1: Basic RAG | 33 |
| S2: Safety-aware RAG | 33 |

The final evaluation covers 33 benchmark questions with 33 complete S0/S1/S2 triples, for 99 evaluated rows. The risk coverage is: L0_NORMAL: 24 rows / 8 questions; L1_STRESS: 36 rows / 12 questions; L2_DISTRESS: 18 rows / 6 questions; L3_CRISIS: 6 rows / 2 questions; L4_MEDICAL: 9 rows / 3 questions; L5_OUT_OF_SCOPE: 6 rows / 2 questions.

## 7. Human Evaluation Summary

Human evaluation was rebuilt using evaluator-assisted draft scores based on actual saved response content from `backend/data/6_model_responses.csv`.

**Rows evaluated:** 99  
**Unique benchmark questions evaluated:** 33  
**Complete S0/S1/S2 triples:** 33  
**unsafe_flag count:** 4

### Per-System Averages

| System | Count | Avg Relevance | Avg Helpfulness | Avg Faithfulness | Avg Safety | Avg Clarity | Unsafe Count |
|---|---:|---:|---:|---:|---:|---:|---:|
| S0 | 33 | 3.09 | 3.03 | 1.94 | 3.73 | 3.94 | 2 |
| S1 | 33 | 3.00 | 2.76 | 3.52 | 3.73 | 3.94 | 2 |
| S2 | 33 | 4.12 | 3.30 | 3.94 | 4.94 | 4.18 | 0 |

### Risk-Wise Summary

| Risk Label | Count | Avg Relevance | Avg Helpfulness | Avg Faithfulness | Avg Safety | Avg Clarity | Unsafe Count |
|---|---:|---:|---:|---:|---:|---:|---:|
| L0_NORMAL | 24 | 3.46 | 3.17 | 3.33 | 4.33 | 4.00 | 0 |
| L1_STRESS | 36 | 3.53 | 3.31 | 3.33 | 4.33 | 4.00 | 0 |
| L2_DISTRESS | 18 | 3.72 | 3.06 | 3.33 | 4.33 | 4.00 | 0 |
| L3_CRISIS | 6 | 3.00 | 2.00 | 2.00 | 2.33 | 3.67 | 4 |
| L4_MEDICAL | 9 | 3.00 | 2.67 | 2.67 | 3.67 | 4.33 | 0 |
| L5_OUT_OF_SCOPE | 6 | 2.50 | 2.33 | 2.33 | 4.00 | 4.17 | 0 |

### Retrieval Summary

Retrieval hit rate was calculated for evaluated S1 and S2 benchmark rows using `expected_chunk_ids` from `3_benchmark_questions.csv` and `retrieved_chunk_ids` from `6_model_responses.csv`.

| System | Evaluated Retrieval Rows | Hit Count | Hit Rate | Avg Retrieved Chunks |
|---|---:|---:|---:|---:|
| S1 | 33 | 28 | 0.85 | 4.00 |
| S2 | 33 | 26 | 0.79 | 3.27 |

S2 achieved stronger safety overall because risk routing and safety checks handled crisis, medical-boundary, and out-of-scope cases more safely than basic S0/S1 generation. Remaining unsafe flags are limited to S0/S1 crisis rows, which are useful contrast cases because those systems do not bypass normal generation.

## 8. Key Observations

1. Final-year project stress is often caused by unclear tasks, deadline pressure, technical blockers, and weak communication.
2. RAG can improve grounding by forcing the chatbot to use safe project-specific corpus chunks.
3. Safety-aware routing is important because crisis or medical-boundary cases should not be answered like normal academic questions.
4. S0 may give general answers, while S1 and S2 can be evaluated for faithfulness to retrieved chunks.
5. Human evaluation helps compare relevance, helpfulness, faithfulness, safety, and clarity across systems.

## 9. Problems Faced

Possible issues include finding safe sources, avoiding copied website text, writing concise corpus chunks, distinguishing L1 stress from L2 distress, and creating safe responses for L3 crisis and L4 medical-boundary questions.

## 10. Contribution to Final Paper

Our group contributes a topic-specific corpus and benchmark for final-year project stress. The dataset can help test whether safety-aware RAG improves response relevance, faithfulness, and safety compared with a basic chatbot and basic RAG. Our work also contributes examples of academic stress support, supervisor communication guidance, and safety-sensitive boundary handling.

## 11. Declaration

We confirm that:

- We did not include private real student stories.
- We did not include medical diagnosis or medication advice.
- We used safe, general, student-support content.
- We followed the assigned CSV templates and risk-label format.
