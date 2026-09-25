# The Angelos Engine

**An Analytic Network Engine for Government Evaluation of Legislation and Opinion Sources**

> From the Greek word *Angelos*, meaning messenger, they cut through public noise to deliver unvarnished truth to leadership.

## The Problem

Government analysts must assess proposed laws and regulations while understanding how citizens, communities, businesses, and the news media will respond. That information is scattered across policy documents, public comments, news coverage, citizen correspondence, call-center transcripts, surveys, and social platforms. Reviewing it manually can take weeks — and a simple sentiment score ("72% negative") hides the *why*: misunderstanding, genuine harm, media misreporting, or something else entirely.

The Angelos Engine is an AI-powered application that connects authoritative policy text with the news coverage, public comments, and citizen feedback surrounding it, and produces a single evidence-grounded briefing an analyst can trust enough to act on.

## Core Idea

Think **VirusTotal, but for public policy**: instead of running a file through dozens of antivirus engines and showing exactly which engine flagged what, Angelos runs a policy document through multiple analysis modules and shows exactly which source backs each claim in the final briefing.

The non-negotiable design rule: **never blend policy fact, news reporting, public opinion, and AI interpretation into one undifferentiated blob.** Every output is traceable back to what kind of source it came from.

## System Architecture

| Mythological Anchor | Module | Function |
|---|---|---|
| **Angelos** (The Messenger) | Angelos Briefing Engine | Core dashboard that compiles the final evidence-grounded briefing, separating policy fact from public rumor |
| **Socrates** (The Gadfly) | Socratic Cross-Examiner | RAG-powered QA module that interrogates policy text against public comments to surface contradictions and misunderstandings |
| **The Chorus** | Chorus Aggregator | Ingestion pipeline that pulls in social posts, call logs, and surveys and clusters them into unified public-sentiment waves |
| **Hermes** (Messenger of the Gods) | Hermes Translator | NLP layer that breaks dense, jargon-heavy legal text into plain-language summaries |
| **Pheme** (Goddess of Rumor) | Pheme Bias & Rumor Filter | Data-provenance module that flags source bias, echo chambers, and misinformation |

```
[ Policy Document Input ]
          │
          ▼
  Hermes Translator  ──────► plain-language policy summary
          │
          ▼
  Chorus Aggregator  ──────► ingests news / comments / social, tagged by source type
          │
          ▼
  Socratic Cross-Examiner ─► RAG QA: cites policy text + public sources, flags contradictions
          │
          ▼
  Pheme Bias Filter  ──────► scores source reliability / representativeness
          │
          ▼
  Angelos Briefing Engine ─► final briefing, color/tab-coded by source type, with confidence scores
```

## What It Does

- **Summarizes** the policy document in plain language
- **Cross-references** policy text against public comments/news via retrieval-augmented generation, citing every claim
- **Separates** every sentence in the output into one of four categories: Policy Text / Factual Reporting / Public Opinion / AI Interpretation
- **Flags bias** — surfaces when feedback is dominated by a narrow or unrepresentative slice of sources
- **Communicates uncertainty** — attaches a confidence score to interpretive claims instead of presenting them as fact
- **Preserves minority viewpoints** rather than averaging them into a single sentiment number
- **Keeps a human analyst in the loop** — Angelos assembles evidence and drafts a briefing; it does not issue a final recommendation

## Hackathon Scope (MVP)

Built over ~3 days with restricted network access on school infrastructure, which limited which hosted APIs and package sources we could reach. The MVP focuses on proving the core loop rather than the full production pipeline:

- [ ] Ingest one sample policy document
- [ ] Ingest one small public-comment / news dataset
- [ ] Socratic Cross-Examiner: RAG QA over both, with inline source citations
- [ ] Truth-Sieve UI: basic tabbed/color-coded view splitting Policy Text / News / Opinion / AI Interpretation
- [ ] Minimal confidence-scoring on AI-generated claims

**Explicitly out of scope for this build** (future work): multi-draft revision diffing, PII-scrubbing pipeline, full unsupervised dissent-clustering, production-grade dashboard.

## Tech Stack

- **LLM Orchestration:** LangChain / LlamaIndex (RAG pipeline)
- **Vector Store:** Pinecone or Milvus
- **PII Anonymization (planned):** Microsoft Presidio
- **Frontend:** Streamlit or Gradio (rapid prototype)

## Constraints We Designed Around

- Distinguish policy language, factual reporting, public opinion, and AI-generated interpretation at all times
- Protect personally identifiable information in citizen correspondence and transcripts
- Account for source bias and representativeness rather than treating all input as equally reliable
- Preserve conflicting and minority viewpoints instead of collapsing them into an average
- Cite supporting evidence for every claim in the briefing
- Communicate uncertainty rather than presenting guesses as fact
- Keep human analysts responsible for the final call — Angelos assists, it doesn't decide

## Team Notes

Development was constrained by school network restrictions that blocked access to some planned tools/APIs partway through the 3-day build; the architecture above reflects the intended full system, while the working prototype covers the MVP checklist.
