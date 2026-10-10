# Project Proposal: ScholarFeed

**Project Title**: ScholarFeed — Autonomous AI-Powered Literature Discovery & Literature Digest Platform  
**Author / Proponent**: Rana M. Mazhar Khan  
**Status**: Production-Ready / Implemented  
**Date**: October 2026  
**Document Version**: 2.5  

---

## 1. Project Overview & Problem Statement

### 1.1 Context & Background
The pace of global scientific discovery has expanded beyond human processing capacity. Over **5 million academic papers** and preprints are published annually across computer science, biomedicine, engineering, and physics. Researchers, scientists, and students face an overwhelming "literature firehose" every morning.

### 1.2 The Problem
1. **Information Overload & Research Fatigue**: An individual researcher cannot manually scan hundreds of new submissions published every week. Consequently, critical breakthroughs, novel baselines, and adjacent literature are routinely missed.
2. **Siloed and Fragmented Repositories**: High-impact preprints are scattered across incompatible databases:
   - Computer Science & Physics live predominantly on **arXiv**.
   - Clinical trials and biomedical studies are cataloged on **PubMed (NCBI)**.
   - Citation networks are indexed on **OpenAlex** and **Semantic Scholar**.
   - Global institutional archives are hosted on **DOAJ** and **CORE**.
   There is no unified, automated workflow that aggregates, filters, and standardizes these disparate feeds into a single cohesive workspace.
3. **High Operational Friction**: Researchers must constantly switch context between disjointed tools—reading papers on one site, uploading PDFs into a separate chatbot, manually formatting citations in BibTeX or APA for reference managers (Zotero/Mendeley), and tracking keywords by hand.

---

## 2. Proposed Solution

**ScholarFeed** is an intelligent, autonomous academic discovery and literature digestion ecosystem designed to operate as a **24/7 personal research assistant**.

### Core Value Proposition
ScholarFeed continuously monitors the global preprint ecosystem, interprets each researcher's evolving academic profile, semantically filters candidate submissions, and delivers curated, high-relevance briefs directly to their inbox and interactive dashboard.

Instead of manual search queries, ScholarFeed automates the entire discovery lifecycle:
* **Understands the Researcher**: Extracts interests and expertise weights directly from uploaded CVs/Resumes or custom keyword registries.
* **Autonomous Daily Scouting**: Crawls global academic APIs automatically every morning.
* **Semantic Filtering & Plain-English Summarization**: Leverages large language models (LLMs) to score relevance, generate 2-sentence executive briefs, and provide exact reasoning for why each paper matters to the specific researcher.
* **Interactive Exploration & Document Dropzone**: Allows researchers to converse with AI about any paper or upload custom drafts for instant sectional parsing.
* **Zero-Friction Citation & Reference Export**: Generates one-click formatted citations (APA, MLA, Chicago, BibTeX) and instant downloadable `.bib` / `.ris` files.
* **Background Adaptive Learning**: Dynamically tunes user interest weights based on paper bookmarks and dismissals without requiring manual profile reconfiguration.

---

## 3. Objectives & Expected Outcomes

### 3.1 Primary Objectives
1. **Reduce Literature Screening Time by 85%**: Enable researchers to review their daily domain-specific preprints in under 5 minutes rather than 45–60 minutes of manual browsing.
2. **Eliminate Literature Fragmentation**: Aggregate 6 major academic platforms (arXiv, PubMed, OpenAlex, Semantic Scholar, DOAJ, CORE) into a single normalized data pipeline.
3. **Dynamic Personalization**: Implement an adaptive background learning loop where user engagement automatically fine-tunes future recommendations.
4. **Accelerate Publication & Writing Workflows**: Provide one-click citation exports and conversational paper interrogation directly within the discovery feed.

### 3.2 Expected Outcomes
* **Quantifiable Productivity Boost**: Elimination of missed relevant literature, faster literature reviews for grant proposals and journal submissions.
* **Zero-Setup Barrier**: A researcher can upload a CV or type 3 keywords and immediately receive an automated daily intelligence feed.
* **Enterprise-Grade Reliability**: Fully resilient architecture with automated offline fallbacks so the platform functions seamlessly even under API rate limits or network degradation.

---

## 4. Target Users

| User Persona | Key Needs & Pain Points | How ScholarFeed Solves It |
| :--- | :--- | :--- |
| **Principal Investigators (PIs) & Professors** | Managing multiple grant projects; little time to scan daily preprints across sub-fields. | Delivers concise morning email digests with 2-sentence summaries and relevance justifications. |
| **PhD Students & Postdocs** | Writing literature reviews, finding prior art, tracking citations and writing references. | Instant multi-platform search, interactive PDF chat, and 1-click BibTeX/RIS reference exports. |
| **Industry R&D & Machine Learning Engineers** | Keeping up with state-of-the-art architectures (Transformers, LLMs, Bio-computation) on arXiv. | Automated category crawling (`cs.AI`, `cs.LG`, `cs.CL`, `cs.SE`) with match percentage scoring. |
| **Medical & Life Sciences Researchers** | Tracking clinical trial outcomes, drug mechanisms, and peer-reviewed journals. | Direct integration with PubMed NCBI Entrez E-Utilities and OpenAlex biomedical graphs. |

---

## 5. Key Features / Deliverables

### Deliverable 1: Unified OmniSearch Engine
* Live, concurrent multi-source academic search querying **arXiv**, **PubMed**, **OpenAlex**, **Semantic Scholar**, **DOAJ**, and **CORE**.
* Real-time client-side scoring algorithm calculating match percentages based on the user's active keyword weights.
* Results display with visual relevance indicators (High ≥ 80% vs Medium 50%–79%).

### Deliverable 2: Adaptive Interests Auto-Tuner (Smart Profiler)
* Observes user interactions (bookmarking/upvoting vs. dismissing/downvoting).
* **Online Mode**: Prompts OpenRouter (`google/gemini-2.5-flash`) to assess semantic alignment, discover adjacent keywords, and scale weights ($1$ to $5$).
* **Offline Fallback Engine**: Rule-based regex extractor that increments matching terms on upvote, extracts high-signal title nouns, and prunes low-performing terms on downvote.
* Instant reactive state synchronization without page reload.

### Deliverable 3: Interactive Paper AI Chat & Custom PDF Dropzone
* Drag-and-drop document dropzone accepting user research papers (`.pdf`, `.docx`, `.txt`).
* Text extraction powered by layout-aware `pdfplumber` with fallback to `PyPDF2`.
* Multi-turn chat assistant with 10-message dialogue history sliding window memory.
* Strict credit guardrails (`max_tokens=1000`) preventing API billing overruns.

### Deliverable 4: Inline Citation & Export Suite
* Inline relative popover hovering directly over the paper card's "Citation" action button.
* Formatted clipboard generation: **APA (7th)**, **MLA (9th)**, **Chicago (17th)**, and **BibTeX**.
* Zero-roundtrip browser Blob file generation for **.bib** (LaTeX) and **.ris** (Zotero, Mendeley, EndNote) files.

### Deliverable 5: Automated Daily Research Digest Agent
* Automated scheduled pipeline via GitHub Actions cron (`daily_digest.yml`) executing `python manage.py run_daily_digest` daily at 13:00 UTC.
* Automated database migration step guaranteeing database integrity on fresh runners.
* Responsive, branded HTML email digest dispatched via SMTP (Gmail / Mailgun).

### Deliverable 6: Resume & CV Profile Extraction Engine
* Allows one-click onboarding by parsing researcher CVs to automatically populate research areas, skills, and interest weights.

---

## 6. Implementation Plan & Timeline

```
+---------------------------------------------------------------------------------------------------+
| PHASE 1: Architecture & Data Modeling (Completed)                                                |
| - Django 5.x project scaffolding, SQLite/PostgreSQL configuration.                                 |
| - Relational schema design: User, Profile, ResearchArea, Paper, Match, PaperChat.                 |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 2: Multi-Platform API Aggregator (Completed)                                                |
| - Implement arXiv client, PubMed Entrez queries, OpenAlex, Semantic Scholar, DOAJ, & CORE.        |
| - Build data normalization layer and date sanitizer (`clean_date_string`).                        |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 3: AI Cognition & Adaptive Learning (Completed)                                             |
| - Integrate OpenRouter LLM (`google/gemini-2.5-flash`) with token budget safety caps.            |
| - Implement Adaptive Auto-Tuner (`core/tuner.py`) with offline fallback algorithms.               |
| - Build interactive paper chat and `pdfplumber` PDF text extractor.                               |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 4: UI/UX Engineering & Citation Center (Completed)                                          |
| - Build responsive glassmorphic dark UI using CSS Design Tokens (Outfits/Plus Jakarta Sans).       |
| - Implement inline citation popovers and zero-roundtrip Blob downloaders (.bib / .ris).            |
| - Bind instantaneous event listeners to prevent asynchronous boot UI locks.                       |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 5: Testing, CI/CD & Operations (Completed & Maintained)                                     |
| - Build automated unit test suites (`tests_tuner.py`, `tests_chat.py`).                           |
| - Configure GitHub Actions workflow with automated migrations and runner secret fallbacks.        |
| - Compile complete technical documentation and downloadable PDF artifacts.                        |
+---------------------------------------------------------------------------------------------------+
```

---

## 7. Resources & Requirements

### 7.1 Technical Stack & Dependencies
* **Core Language & Backend**: Python 3.12, Django 5.x, Django REST Framework.
* **Frontend**: Semantic HTML5, Vanilla JavaScript (ES6+), Vanilla CSS3 Design Tokens (zero heavy JS framework overhead).
* **Document Parsing**: `pdfplumber`, `PyPDF2`.
* **Report & PDF Generation**: `reportlab`.
* **Configuration & Security**: `python-decouple`, `whitenoise`.

### 7.2 External APIs & Authentication
* **arXiv API**: Free open Atom XML protocol.
* **PubMed (NCBI)**: Entrez E-Utilities JSON API.
* **OpenAlex API**: Open Scholarly Graph API (Polite Pool User-Agent).
* **Semantic Scholar API**: S2AG REST API.
* **DOAJ API**: v2 Open Access Journal API.
* **CORE API**: Open Access Repository Aggregator.
* **OpenRouter / Gemini**: `google/gemini-2.5-flash` via OpenAI Python SDK.
* **Email Gateway**: SMTP via Gmail App Passwords / Mailgun.

### 7.3 Infrastructure & Hosting
* **Production Web Server**: Any Linux host, Heroku, Railway, Render, or VPS with Gunicorn/Uvicorn.
* **Static Assets**: WhiteNoise compressed manifest storage.
* **Background Scheduling**: GitHub Actions Runners (Ubuntu latest) with cron triggers.

---

## 8. Potential Challenges, Risks & Mitigation Strategies

| Potential Challenge / Risk | Severity | Mitigation Strategy Implemented |
| :--- | :--- | :--- |
| **External API Rate Limits & Timeouts** | Medium | Requests implement strict 5-second timeouts, retry wrappers, user-agent headers, and multi-source fallback so if one API fails, remaining APIs fulfill the feed. |
| **LLM Hallucinations in Summaries** | High | Prompts strictly inject paper abstracts and extracted texts as ground truth; LLM is instructed to synthesize only verifiable objectives, baselines, and findings. |
| **OpenRouter / LLM Credit Depletion** | High | Strict `max_tokens=1000` hard-capping prevents HTTP 402 payment errors; fully functional rule-based offline algorithms handle matching and tuning when credentials expire. |
| **CI/CD Missing Database & Secret Errors** | Medium | Automated `python manage.py migrate` is built into the GitHub Actions workflow; `settings.py` incorporates inline fallback defaults (`SECRET_KEY = config(...) or "dev-key"`). |
| **Irregular External Date Formats** | Low | Custom regex sanitizer (`clean_date_string`) parses diverse YYYY-MM-DD, 4-digit years, and timestamps into compliant Django DateFields. |

---

## 9. Additional Details (Project Highlights & Innovation)

### 9.1 Zero-Roundtrip Export Performance
Unlike traditional academic portals that make server requests to generate citations, ScholarFeed computes APA, MLA, Chicago, BibTeX, and RIS formats entirely within the client browser using HTML5 Blob objects. This guarantees instant downloads with zero server load.

### 9.2 Privacy & Data Ownership
Uploaded user papers and drafts are isolated by user accounts and can be permanently deleted with a single click, which purges both the database record and the physical storage file from disk.

### 9.3 Extensibility & Future Roadmap
* **Collaborative Research Labs**: Shared team feeds where lab members can collaborate on literature reviews.
* **Citation Graph Visualizer**: Interactive network graphs visualizing how papers in the digest cite one another.
* **Direct Zotero / Mendeley OAuth Sync**: One-click cloud syncing directly into researchers' desktop reference manager libraries.
