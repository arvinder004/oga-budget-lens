### OGA-budget-lens: Technical Overview

This repository contains the foundations of **Budget Lens**, an auditable, human-verifiable system for extracting structured budget data from unstructured government budget documents (PDFs), with a strong focus on African public finance contexts.

The project is designed to prioritize:
- Traceability and provenance over raw automation
- Human verification as a first-class workflow
- Interoperability with open fiscal data ecosystems
- Long-term maintainability beyond any single funding program

This is an early-stage repository. Contributors should expect to **design and build core infrastructure**, not extend an existing production system.

---

### Problem Statement

Government budget documents are often:
- Published as scanned or poorly formatted PDFs
- In multiple languages (English, French, Portuguese, and others)
- Structurally inconsistent across years and countries
- Difficult to compare, audit, or reuse as data

Existing tools either:
- Optimize for speed over trust
- Hide extraction uncertainty
- Lose provenance during transformation
- Or rely on opaque AI inference

Budget Lens takes a different approach: every extracted number must be explainable, reviewable, and traceable back to its source.

---

### Core Design Principles

- **Provenance-first**: Every extracted value links back to a source page and method
- **No silent inference**: AI may clean or classify text, but must never invent fiscal data
- **Human-in-the-loop by default**: Review and correction are expected, not exceptional
- **Fail loudly**: Ambiguity and extraction failures must be flagged, not hidden
- **Cross-country by design**: No assumptions tied to a single national format

---

### High-Level Architecture (Conceptual)

1. **Document Ingestion**
   - PDF type detection (digital vs scanned)
   - Language detection
   - Source metadata capture

2. **Text & Layout Extraction**
   - OCR for scanned documents
   - Layout detection (tables, headers, footers, narrative)
   - Preservation of bounding boxes and page numbers

3. **Table & Structure Processing**
   - Table extraction into intermediate data frames
   - Hierarchy reconstruction with explicit parent–child links
   - Ambiguity detection and flagging

4. **LLM-Assisted Normalization**
   - Text cleaning and normalization only
   - Functional classification (e.g. COFOG)
   - Full prompt and model provenance

5. **Validation & QA**
   - Arithmetic checks
   - Structural integrity checks
   - Semantic anomaly detection

6. **Human Review**
   - Side-by-side PDF, extracted data, and editable fields
   - Audit trail of edits and decisions

7. **Export & Interoperability**
   - Validated JSON, CSV, Excel outputs
   - Compatibility with OpenSpending-style datasets

---

### Technology Direction (Non-Binding)

Specific libraries and tools may evolve, but likely components include:
- Python-based parsing and orchestration
- OCR engines such as Tesseract or PaddleOCR
- Layout analysis via LayoutParser or similar
- Table extraction via Camelot or Tabula
- Lightweight web UI for review workflows

All major technical trade-offs must be documented as the system evolves.

---

### Project Maturity

This repository currently represents:
- A clearly defined problem space
- A detailed target architecture
- Explicit non-goals and safety constraints

It does **not yet** include:
- A finalized data model
- A production-ready pipeline
- A stable contributor environment

Early contributors will help define these foundations.
