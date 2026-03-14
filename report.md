# HiLabs Workshop: Reliability & Evaluation Report

## 1. Quantitative Evaluation Summary
The evaluation focused on comparing automated OCR entity extraction against manual ground truth. 
- **High Performance:** `VITAL_NAME` and `TEST` values showed >95% accuracy.
- **Low Performance:** `Temporality` and `Assertion` (specifically `UNCERTAIN`) showed significant error rates (>25%).

## 2. Identified Systemic Weaknesses
1. **Temporality Drift:** The model frequently assigns `CLINICAL_HISTORY` to admission events that are clearly `CURRENT`.
2. **Context Blindness:** Specific instructions (e.g., "Hold home meds") are often extracted as standard prescriptions without capturing the "Hold" instruction status accurately.

## 3. Proposed Guardrails
- **Keyword-Based Temporal Correction:** Implement a post-processing script to check for current dates associated with "admission" or "discharge" strings.
- **Negation/Hold Logic:** Introduce a dependency parser to link verbs like "Hold" or "Stop" directly to `MEDICINE` entities.