# AI Evaluation & Metrics Framework (PM Lens)

> Measuring AI success requires balancing **usefulness, safety, cost, and trust** — not just accuracy.

This document outlines a practical evaluation and metrics framework for **enterprise AI products**, with a focus on **contact centers, voice systems, and support workflows**.

---

## 1) Why AI Metrics Are Different

Traditional software metrics assume deterministic behavior.  
LLM-based systems are **probabilistic**, which means:

- The same input may produce different outputs
- Errors may sound confident
- Success is contextual, not binary

As a result, AI PMs must define success as **safe usefulness**, not raw correctness.

---

## 2) Metric Layers (How to Think About Measurement)

AI products should be measured across **four layers**:

1. **Adoption & Usage**
2. **Quality & Safety**
3. **Business Impact**
4. **Cost, Latency & Reliability**

Each layer answers a different product question.

---

## 3) Adoption & Usage Metrics

These metrics tell you whether the AI feature is being used and accepted.

### Core metrics
- **AI Feature Adoption Rate**  
  % of eligible sessions where AI is invoked

- **Assist vs Automation Mix**  
  Ratio of AI suggestions (assist) vs autonomous actions

- **Repeat Usage Rate**  
  % of users who use the AI feature more than once

- **Fallback Rate**  
  % of sessions where users abandon AI and go manual

📌 Interpretation:
- High adoption + high fallback = usefulness gap
- Low adoption = trust or UX issue

---

## 4) Quality & Safety Metrics

These metrics measure **output quality and risk**.

### Key quality metrics
- **Groundedness**  
  % of responses supported by approved sources (for RAG systems)

- **Hallucination Rate**  
  % of responses containing confident, incorrect information

- **Answer Completeness**  
  Does the response fully address the user’s intent?

- **Refusal Accuracy**  
  Does the system correctly refuse when it should?

### Safety metrics
- **Policy Violation Rate**
- **PII/PHI Exposure Incidents**
- **Unsafe Action Attempts Blocked**

📌 Recommendation:
Track hallucinations and refusals **separately** — over-refusal is also a failure.

---

## 5) Voice-Specific Metrics (Critical for CCaaS)

Voice systems introduce additional constraints.

### Voice AI metrics
- **Time-to-First-Correct-Response (TTFCR)**  
  How quickly the user gets a useful answer

- **Latency (p50 / p95)**  
  Total end-to-end response time

- **Turn Success Rate**  
  % of conversational turns that move the user forward

- **Escalation Success Rate**  
  When AI escalates, does the handoff work?

📌 Guideline:
Voice users tolerate **far less latency** than chat users. Graceful fallback matters more than perfect answers.

---

## 6) Business Impact Metrics

These metrics justify investment and guide roadmap decisions.

### Common business metrics
- **Deflection Rate (Confidence-Gated)**  
  % of issues resolved without human involvement *above a confidence threshold*

- **Agent Handle Time Reduction**
- **First Contact Resolution (FCR)**
- **CSAT / NPS Delta**
- **Cost per Resolution**

📌 Important:
Never report deflection without **confidence thresholds** — unsafe automation erodes trust.

---

## 7) Offline vs Online Evaluation

### Offline evaluation (pre-release)
- Curated test sets
- Labeled examples
- Prompt & retrieval iteration
- Regression detection

Used to answer:
> “Is this safe enough to ship?”

### Online evaluation (post-release)
- Live traffic monitoring
- Shadow mode testing
- A/B experiments
- Human review loops

Used to answer:
> “Is this delivering value in the real world?”

Strong AI teams run **both continuously**.

---

## 8) Confidence Scoring & Gating

Confidence scoring enables:
- Assist vs automate decisions
- Safe deflection
- Trust-preserving refusals

Common signals:
- Retrieval relevance score
- Model self-consistency
- Tool-call success
- Rule-based risk checks

PM responsibility:
Define **confidence thresholds** and escalation behavior.

---

## 9) Cost, Latency & Reliability Metrics

### Cost metrics
- Cost per request
- Cost per resolution
- Token usage per interaction

### Reliability metrics
- Success rate
- Timeout rate
- Escalation availability
- Dependency health (retrieval, tools, queues)

📌 Rule of thumb:
If you don’t track cost and latency, your AI feature will eventually fail — even if quality is high.

---

## 10) Sample Metrics Dashboard (PM View)

A minimal PM dashboard should include:
- Adoption trend
- Hallucination rate
- Escalation rate
- Deflection (confidence-gated)
- p95 latency
- Cost per resolution
- CSAT delta

This allows PMs to make **tradeoffs consciously**, not reactively.

---

## 11) Common Failure Patterns & Signals

| Signal | Likely Issue |
|------|-------------|
| High hallucination rate | Weak grounding or prompts |
| High refusal rate | Overly conservative policies |
| High fallback rate | UX or trust problem |
| Rising costs | Model choice or token bloat |
| Low adoption | Positioning or discoverability |

---

## Summary

Effective AI product measurement requires:
- Multiple metric layers
- Clear definitions of “safe success”
- Continuous evaluation loops
- Willingness to trade off automation for trust

AI PMs who own metrics **own the product outcome**.
