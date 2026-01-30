# RAG vs Fine-tuning (Decision Guide for AI PMs)

> Most enterprise AI products should start with **RAG + guardrails + evaluation** before considering fine-tuning.

This guide helps Product Managers decide between:
- Prompting / system instructions
- RAG (Retrieval-Augmented Generation)
- Fine-tuning (or adapters/LoRA)
- Tool / function calling
- Hybrid approaches

It is written for enterprise use cases like **contact centers, knowledge bases, voice, and platform workflows**.

---

## 1) Quick Definitions

### Prompting (instructions)
You shape model behavior using system prompts, examples, and constraints.

### RAG (retrieval + generation)
You fetch relevant, approved content (docs/tickets/KB) and provide it as context for generation.

### Fine-tuning
You update model behavior using curated datasets to improve performance on specific tasks/styles.

### Tool / Function Calling
Model selects from approved tools (search, ticketing, APIs) to perform actions or fetch real-time truth.

---

## 2) The Default Enterprise Recommendation

**Default starting stack:**
1) Prompting + constraints  
2) RAG (permission-aware)  
3) Guardrails + confidence gating  
4) Evaluation loop (offline + online)  
5) Only then: selective fine-tuning (if needed)

Why:
- Most enterprise failures come from **freshness, governance, and trust**, not raw “intelligence.”

---

## 3) When RAG Is the Best Choice

Use RAG when you need:
- **Freshness** (content changes frequently)
- **Auditability** (show sources, citations, doc IDs)
- **Governance** (approved knowledge only)
- **Enterprise permissions** (RBAC/ABAC, tenant isolation)
- **Lower time-to-launch** (no training pipeline required)

Common examples:
- knowledge base Q&A
- agent assist referencing internal docs
- policy and procedure guidance
- troubleshooting playbooks

**RAG strength:** grounded answers with controllable knowledge.

**RAG failure modes:**
- bad retrieval (wrong docs)
- outdated sources
- permission leakage
- too much context (token bloat)

Mitigate with:
- source ownership + freshness SLAs
- retrieval evaluation
- access filters
- context limits

---

## 4) When Fine-tuning Is the Best Choice

Fine-tuning is best when you need:
- **Consistent style and formatting**
- **Specialized behavior** that prompting can’t reliably enforce
- **High-volume repeated tasks** with stable labels
- **Structured extraction** and classification improvements
- **Domain-specific jargon normalization** (where legal/security permits)

Common examples:
- classification (intent, category, compliance labels)
- extraction (entities from text/calls)
- standardized output formats
- tone and brand consistency (with strict controls)

**Fine-tuning strength:** consistent task performance at scale.

**Fine-tuning risks:**
- requires curated data + labeling
- increases operational complexity (training pipeline)
- can drift if domain changes
- does not automatically solve freshness (it “bakes in” knowledge)

---

## 5) When Tool Use Beats Both

Use tool/function calling when:
- the answer requires **real-time truth**
- you must perform actions (create ticket, update CRM, route call)
- you need deterministic outputs from systems of record

Examples:
- “What’s my ticket status?” → query ticketing system
- “Reset password” → identity + workflow automation
- “Route to billing” → deterministic routing rules

Tool use is often the best way to reduce hallucinations:
> Don’t ask the LLM to *remember* truth — let it *look it up*.

---

## 6) Decision Matrix (PM-Friendly)

| Need / Constraint | Prompting | RAG | Fine-tuning | Tools |
|---|---:|---:|---:|---:|
| Fresh content | ⚠️ | ✅ | ❌ | ✅ |
| Auditability / citations | ⚠️ | ✅ | ❌ | ✅ (via logs) |
| Enterprise permissions | ⚠️ | ✅ | ⚠️ | ✅ |
| Consistent tone/format | ⚠️ | ⚠️ | ✅ | ✅ |
| Real-time truth | ❌ | ⚠️ | ❌ | ✅ |
| Lowest operational overhead | ✅ | ✅ | ❌ | ⚠️ |
| Lowest hallucination risk | ⚠️ | ✅ | ⚠️ | ✅ |

Legend: ✅ strong fit, ⚠️ depends, ❌ poor fit

---

## 7) Typical Enterprise Patterns That Work

### Pattern A: Knowledge Assistant (Recommended)
- RAG + grounding requirement + refusal when no sources
- confidence-gated escalation

### Pattern B: Agent Assist → Automation
- start with suggestions
- measure + improve
- automate only high-confidence intents

### Pattern C: Hybrid (RAG + Fine-tuning)
- RAG for knowledge freshness
- fine-tuning for formatting, classification, or tone consistency

---

## 8) How to Decide (Practical Questions)

Ask:
1. **Does the answer require up-to-date content?**  
   If yes → RAG or tools

2. **Do we need citations and auditability?**  
   If yes → RAG

3. **Is the task repetitive with stable labels?**  
   If yes → consider fine-tuning

4. **Does the task require system-of-record truth?**  
   If yes → tools

5. **Do we have clean data + labeling capacity?**  
   If no → delay fine-tuning

---

## 9) Rollout Approach (PM Playbook)

1) Launch MVP using prompting + RAG  
2) Instrument metrics: groundedness, hallucinations, latency, cost  
3) Improve retrieval before touching fine-tuning  
4) Add tools for real-time truth and deterministic actions  
5) Fine-tune selectively after you have:
   - clear failure patterns
   - stable datasets
   - strong evaluation harness

---

## Summary

- **RAG** is best for enterprise knowledge, freshness, auditability, and governance.
- **Fine-tuning** is best for consistency and high-volume, stable tasks.
- **Tools** are best for real-time truth and deterministic workflows.
- The winning enterprise strategy is often **RAG + tools + guardrails + evaluation**, with selective fine-tuning later.
