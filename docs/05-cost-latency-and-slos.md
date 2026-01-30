# AI Cost, Latency & SLOs (PM + Infra Lens)

> AI products fail in production not because they are inaccurate — but because they are **too slow, too expensive, or unreliable**.

This document outlines how Product Managers should think about **cost, latency, and service-level objectives (SLOs)** for enterprise AI systems, with a focus on **voice, contact center, and platform-scale products**.

---

## 1) Why Cost & Latency Are Product Decisions

In AI systems:
- every request has a **variable cost**
- latency directly impacts **user trust**
- reliability depends on **multiple downstream dependencies**

Key PM mindset:
> Cost, latency, and reliability are **features** — not backend implementation details.

---

## 2) Cost Model Fundamentals (AI Systems)

### 2.1 Common Cost Drivers
- Model inference (tokens in / tokens out)
- Retrieval (embedding + vector search)
- Tool/function calls
- Speech-to-text / text-to-speech (voice)
- Logging, storage, and observability
- Human review (when applicable)

PM responsibility:
Understand *which actions trigger cost* and *how often*.

---

### 2.2 Cost Per Request vs Cost Per Resolution

- **Cost per request**  
  Total cost of a single AI invocation

- **Cost per resolution**  
  Total cost to successfully solve a user issue

📌 Product insight:
A higher per-request cost may still be acceptable if it **reduces retries, escalations, or agent time**.

---

## 3) Latency Fundamentals (User Experience Impact)

### 3.1 Latency Components
End-to-end latency often includes:
- input processing (ASR for voice)
- retrieval (RAG)
- model inference
- guardrail validation
- response streaming
- escalation handoff

PMs should reason about **p50, p95, and tail latency**, not just averages.

---

### 3.2 Latency Tolerance by Interface

| Interface | User tolerance |
|---------|----------------|
| Voice | Very low |
| Chat | Moderate |
| Async (email, summaries) | High |

Guideline:
> Voice systems must optimize for **fast, safe responses**, even if they are less verbose.

---

## 4) Cost & Latency Optimization Levers

### 4.1 Model Routing
- use smaller / faster models for first pass
- escalate to larger models only when needed
- match model capability to task complexity

---

### 4.2 Token Budgeting
- strict input truncation
- concise system prompts
- limit retrieved context
- cap output length

PMs should explicitly define **token budgets** per use-case.

---

### 4.3 Caching Strategies
- embedding cache for frequent queries
- retrieval result caching
- partial response reuse

Caching is often the **highest ROI cost reducer**.

---

### 4.4 Asynchronous & Deferred Work
Not all AI tasks must block user interaction:
- summaries
- analytics
- post-call processing

Move non-critical AI work **off the critical path**.

---

## 5) SLOs for AI Systems

### 5.1 Why SLOs Matter
Without SLOs:
- teams react instead of plan
- incidents feel random
- reliability erodes silently

SLOs make tradeoffs explicit.

---

### 5.2 Example AI SLOs

#### Availability
- AI response success rate ≥ 99.5%

#### Latency
- p95 response time:
  - voice: ≤ X seconds
  - chat: ≤ Y seconds

#### Quality
- hallucination rate ≤ Z%
- grounded response rate ≥ N%

#### Escalation
- escalation success rate ≥ 99.9%

PMs must negotiate these with engineering, not assume defaults.

---

## 6) Error Budgets & Tradeoffs

Error budgets enable teams to:
- ship improvements faster
- accept calculated risk
- prioritize reliability work

Example tradeoff:
> Temporarily relax latency SLOs during peak load to maintain availability.

PM role:
Make these tradeoffs **visible and intentional**.

---

## 7) Monitoring & Alerting (PM View)

PM dashboards should include:
- cost per resolution (trend)
- p95 latency
- timeout rate
- fallback / escalation rate
- dependency health (retrieval, tools)

Alerts should focus on **user-impacting thresholds**, not raw metrics.

---

## 8) Voice-Specific Considerations

Voice AI introduces:
- tighter latency budgets
- higher abandonment risk
- stronger emotional response

Voice-specific strategies:
- aggressive timeout handling
- early escalation when uncertain
- short, confirmatory responses
- guaranteed human handoff

Rule of thumb:
> In voice, fast and safe beats slow and smart.

---

## 9) Failure Modes to Watch For

| Signal | Likely Cause |
|------|-------------|
| Rising costs | Token bloat, lack of caching |
| p95 latency spikes | Cold starts, large models |
| Increased timeouts | Downstream dependency failures |
| High retries | Low answer quality |
| Silent degradation | Missing SLO monitoring |

---

## 10) Product Rollout Strategy (Cost-Aware)

Recommended sequence:
1. Start with **assist-only** mode
2. Measure cost and latency baselines
3. Optimize before scaling traffic
4. Introduce automation gradually
5. Revisit SLOs as usage grows

Never scale:
- without cost visibility
- without SLOs
- without rollback plans

---

## Summary

Sustainable AI products require:
- clear cost models
- latency-aware design
- explicit SLOs
- monitoring tied to user impact

Product Managers who understand **cost, latency, and reliability** can scale AI products responsibly — and keep them alive in production.
