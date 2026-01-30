# AI Product Requirements Document (PRD) Template

> This PRD template is designed for **enterprise AI products** where trust, safety, cost, and reliability are as important as functionality.

---

## 1) Problem Statement

**User problem:**  
Describe the customer or user problem clearly. Focus on outcomes, not technology.

**Who is impacted:**  
- Primary users:
- Secondary users:
- Internal stakeholders:

**Why now:**  
Explain urgency (customer pain, scale, cost, competition, reliability, compliance).

---

## 2) Goals & Non-Goals

### Goals
- What success looks like for users
- What success looks like for the business

### Non-Goals
Explicitly state what this feature will **not** do (critical for AI scope control).

---

## 3) User Experience Overview

### Primary user journey
High-level flow (chat / voice / app / agent console).

### Entry criteria
When should the AI engage?

### Exit criteria
When should the AI stop, refuse, or escalate?

---

## 4) Why AI (and Why Now)

Explain:
- Why a traditional rules-based approach is insufficient
- What AI enables that wasn’t possible before
- Where AI should **not** be used

Avoid generic statements like “AI improves efficiency.”

---

## 5) AI Approach & Architecture (PM Level)

### Chosen approach
- Prompting
- RAG
- Fine-tuning
- Tool / function calling
- Hybrid

Explain **why** this approach was selected.

### High-level flow


---

## 6) Data Sources & Governance

### Data inputs
- Knowledge sources (docs, tickets, transcripts)
- Systems of record (if any)

### Governance
- Data freshness ownership
- Access control (RBAC / ABAC)
- Tenant isolation
- Retention and logging policies

---

## 7) Risk Assessment & Guardrails

### Key risks
- Hallucinations
- Data leakage
- Over-automation
- Security abuse
- Compliance concerns

### Guardrail strategy
- Input validation
- Retrieval constraints
- Confidence thresholds
- Refusal logic
- Human-in-the-loop design

---

## 8) Metrics & Evaluation

### Adoption metrics
- Feature usage rate
- Repeat usage
- Fallback rate

### Quality & safety metrics
- Hallucination rate
- Grounded response rate
- Refusal accuracy
- Escalation success rate

### Business metrics
- Deflection (confidence-gated)
- CSAT / NPS delta
- Handle time reduction
- Cost per resolution

---

## 9) Cost, Latency & SLOs

### Latency targets
- p95 response time (by interface: voice/chat)

### Cost targets
- Cost per request
- Cost per resolution

### Reliability targets
- Availability
- Escalation success rate

---

## 10) Rollout Plan

### Phase 1: Internal / Assist-Only
- Agent assist or shadow mode
- Manual review loop

### Phase 2: Limited GA
- Conservative guardrails
- Confidence-gated automation

### Phase 3: Scale
- Expanded coverage
- Cost and latency optimization

---

## 11) Open Questions & Dependencies

- Legal/compliance approvals
- Security reviews
- Data readiness
- Tooling or infra dependencies

---

## 12) Out of Scope / Future Enhancements

- Features explicitly deferred
- V2/V3 ideas

---

## Summary

This PRD ensures AI features are:
- useful
- safe
- measurable
- scalable
- enterprise-ready
