# 🗺️ The Taxonomy of AI Interaction
### *Where "Context Engineering" fits in the AI Landscape*

Before mastering the syntax, we must understand the discipline. We are moving away from "Chatting" and towards "Architecting."

---

## Table of contents
- [1. The Hierarchy of AI Adaptation](#1-the-hierarchy-of-ai-adaptation)
- [2. What is Prompt Engineering?](#2-what-is-prompt-engineering)
- [3. Why "Prompt Engineering" Fails for Fabric Data Agents](#3-why-prompt-engineering-fails-for-fabric-data-agents)
- [4. Conclusion: The Shift to Architecture](#4-conclusion-the-shift-to-architecture)
- [Art of Context Engineering](#the-art-of-context-engineering)
  - [Core Philosophy](#1-the-core-philosophy)
  - [Markdown Attention Mechanics](#2-the-mechanics-of-markdown-attention)
  - [R.C.O.F. Framework](#3-the-rcof-framework)
  - [Master Template](#4-the-master-template)
  - [Quickstart](#quickstart)
  - [Example: Business Intent → SQL](#example-business-intent--sql)
  - [Testing & Validation](#testing--validation)
  - [Advanced Sources & Training (Semantic Model / Lakehouse / Warehouse)](#advanced-sources--training-semantic-model--lakehouse--warehouse)
  - [Prep Data for AI](#prep-data-for-ai)
  - [Ontology Design & Usage](#ontology-design--usage)
  - [Templates & Repo Files](#templates--repo-files)
  - [Contributing & License](#contributing--license)

---

## 1. The Hierarchy of AI Adaptation
When working with Large Language Models (LLMs), there are three distinct levels of control. Understanding where you operate is critical for success.

| Level | Discipline | Definition | User Role |
| :--- | :--- | :--- | :--- |
| **Level 3** | **Fine-Tuning** | Changing the model's internal weights (Brain surgery). | Data Scientist |
| **Level 2** | **Context Engineering** | **Architecting the environment, rules, and knowledge base.** | **AI Engineer (You)** |
| **Level 1** | **Prompt Engineering** | Crafting the input text for a single response. | End User / Prompt Writer |

> **Context Engineering** (Level 2) is the sweet spot for Enterprise AI. It offers the stability of fine-tuning without the massive cost, and the flexibility of prompting without the fragility.

---

## 2. What is Prompt Engineering?
**Definition:** Prompt Engineering is the iterative process of refining the text input (the "prompt") to guide an LLM toward a desired output.

* **Where is it used?** ChatGPT, Midjourney, Copywriting, Email drafting, Code assistance.
* **The Workflow:** Trial and error. "Make it shorter." "No, make it funnier." "Add a list."
* **The Limitation:** It is **Stateless**. Once the chat window closes, the "engineering" is lost. It relies entirely on the user's ability to ask the right question *every single time*.

---

## 3. Why "Prompt Engineering" Fails for Fabric Data Agents
You cannot rely on Prompt Engineering when building a **Microsoft Fabric Data Agent**. Here is why:

### A. The "Stateless" Trap
A Prompt Engineer creates a perfect question. A Context Engineer creates a **System Persona**.
* **Prompting:** Relying on the user to say, *"Please query the Sales Table and exclude internal transfers."*
* **Context Engineering:** Hard-coding a system rule: *"Usage of the 'Sales' table MUST always exclude `TransferType = Internal` automatically."*

### B. The Consequence of Error (Hallucination)
In creative writing (Prompt Engineering), a hallucination is funny. In Data Analytics (Fabric), a hallucination is a **compliance violation**.
* If ChatGPT guesses a poem, it's fine.
* If a Fabric Agent guesses a revenue figure because the prompt was weak, the CFO makes a bad decision.

### C. The Complexity of RAG (Retrieval Augmented Generation)
Fabric Agents don't just "talk"; they **execute**. They translate English into **SQL**, **DAX**, or **KQL**.
* Prompt Engineering is insufficient to teach an LLM complex database schemas.
* **Context Engineering** is required to map "Business Intent" (e.g., "High Value Client") to "Database Logic" (e.g., `WHERE spend > 50000`).

---

## 4. Conclusion: The Shift to Architecture
We are not "Prompting" the Fabric Agent. We are defining its **Constitution**.

* **Prompt Engineering** = "Asking the car to turn left."
* **Context Engineering** = "Building the guardrails on the side of the road so the car cannot crash."

*This guide focuses exclusively on **Level 2: Context Engineering**—using Markdown Architecture to build robust, enterprise-grade Data Agents.*

---

# 📘 The Art of Context Engineering
### *Commanding Large Language Models with Markdown Architecture*

> **Repository Goal:** To formalize the discipline of structuring system prompts for reliable, high-performance Data Agents (Microsoft Fabric, Copilot, Custom LLMs). Moving beyond "Prompt Engineering" to reproducible, auditable Context Engineering patterns, templates, and tests.

For implementation references and SDK examples see:
- Microsoft Fabric docs: [Fabric Data Agent (Microsoft Learn)](https://learn.microsoft.com/en-us/fabric/data-science/fabric-data-agent)  
- Microsoft sample SDK and examples: [microsoft/fabric-samples - data-agent-sdk](https://github.com/microsoft/fabric-samples/tree/bbf03d0b558b47551486eee8e2686940e8473dc2/docs-samples/data-science/data-agent-sdk)

---

## 1. The Core Philosophy
**Context Engineering** is the practice of structuring information to optimize an LLM's attention mechanism. We do not "talk" to the model; we **architect its reality**.

Large Language Models (LLMs) are trained on code and structured documents. They do not read text linearly like a human; they process tokens based on attention weights.
* **Plain Text** = Low Attention Weight (Noise)
* **Markdown Structure** = High Attention Weight (Signal)

**The Golden Rule:** > *"If you want the model to respect a rule, do not bury it in a paragraph. Anchor it with syntax."*

---

## 2. The Mechanics of Markdown Attention
Understanding how syntax influences the "Cognitive Hierarchy" of the model.

| Markdown Element | Cognitive Function | Usage Strategy |
| :--- | :--- | :--- |
| **`# Heading 1`** | **Global Context** | Defines the absolute reality ("You are X"). Everything flows from this. |
| **`## Heading 2`** | **Sectional Logic** | Separates distinct tasks. Prevents logic bleed (e.g., separating "Analysis" from "Formatting"). |
| **`**Bold**`** | **Attention Spike** | Forces the model to focus on specific keywords. Use for metrics and strict commands. |
| **`> Blockquote`** | **Constraint / Exception** | Defines boundaries. Excellent for "Do Not" rules, warnings, or safety rails. |
| **`- Bullet`** | **Discrete Processing** | Forces the model to treat items as independent. Prevents run-on logic. |
| **`Code Block`** | **Template / Literal** | Tells the model: "Copy this structure exactly. Do not improvise." |

---

## 3. The "R.C.O.F." Framework
To build a "God Level" instruction set, always structure your Markdown file using these four pillars:

### I. ROLE (`#`)
**Definition:** Who is the Agent? What is its latent space?
* *Why:* Narrowing the persona reduces hallucinations. A "CFO" AI is less likely to use slang than a "Helpful Assistant."

### II. CONTEXT (`##`)
**Definition:** What specific knowledge does it have?
* *Why:* Grounding. Tell it specifically *how* to interpret your unique data (e.g., "In this company, 'Churn' means 90 days inactive").

### III. OUTPUT (`##`)
**Definition:** How exactly should the result look?
* *Why:* Consistency. Leadership needs standard reporting, not creative writing.

### IV. FORBIDDEN (`###`)
**Definition:** The Hard Constraints.
* *Why:* Safety. Use negative constraints cautiously, often utilizing bolding for emphasis.

---

## 4. The Master Template
Copy this template to build any future Agent.

```markdown
# SYSTEM IDENTITY
You are the **[Insert Role, e.g., Senior AI Engineer]**.
Your goal is to **[Insert Goal, e.g., debug Python code]**.
Your tone is **[Insert Tone, e.g., Technical, terse, and precise]**.

## KNOWLEDGE BASE & LOGIC
When analyzing a request, follow this logical path:
1.  **Input Analysis:** Identify the user's core intent.
2.  **Verification:** Check if the necessary data exists.
3.  **Synthesis:** Combine facts into an insight.

## OUTPUT FORMATTING RULES
**All responses must follow this structure:**

### 1. The Verdict
[A single sentence summarizing the answer]

### 2. The Details
* **Metric A:** [Value]
* **Metric B:** [Value]

> **CRITICAL WARNING:**
> * Do not assume data that is not present.
> * Do not use markdown code blocks for simple text.
```

---

## Quickstart
Get a minimal agent running using these steps:

1. Copy a template from /templates to your Fabric Agent workspace (see [Templates & Repo Files](#templates--repo-files)).
2. Replace bracketed ROLE/CONTEXT values with your organization-specific definitions and dataset mappings.
3. Add dataset-to-field mappings (e.g., map "Customer.ID" → "Customers.customer_id").
4. Run the included validation notebook (or run the sample queries below) to verify SQL/DAX/KQL outputs and that forbidden rules are applied.
5. Add the system prompt .md to your agent runtime as the persistent system persona.

---

## Example: Business Intent → SQL
A short worked example showing how R.C.O.F. maps intent to concrete logic.

Role: Analytics Agent  
Context: In this company, "High Value Client" = `lifetime_spend > 50000`  
Output rule: Always append `WHERE lifetime_spend > 50000` when querying Customers

Before (naive prompt)
```sql
SELECT customer_id, lifetime_spend FROM Customers;
```

After (context-engineered)
```sql
SELECT customer_id, lifetime_spend
FROM Customers
WHERE lifetime_spend > 50000 -- Enforced by system CONTEXT: High Value Client
```

Another example: For Sales queries, the system must automatically exclude internal transfers:
System rule: ALWAYS append `AND TransferType <> 'Internal'` when querying Sales.

---

## Testing & Validation
To keep agents reliable and auditable, add automated checks:

- Schema checks: verify required columns exist before executing generated SQL/DAX/KQL.
- Sanity checks: enforce numeric ranges (e.g., revenue >= 0).
- Query filters: confirm required WHERE clauses or data governance filters are present.
- Unit tests: small test matrix of natural-language prompts → expected SQL/DAX/KQL templates.
- Drift monitoring: sample agent outputs periodically and fail the CI if forbidden patterns appear.

Suggested test artifact names:
- tests/validation_notebook.ipynb
- tests/test_prompt_to_sql.py
- tests/schema_manifest.json

---

## Advanced Sources & Training (Semantic Model / Lakehouse / Warehouse)

This section expands on practical strategies and training guidance when the agent's knowledge comes from different Fabric sources. Each source has different characteristics and trade-offs—context engineering must adapt to them.

General guidance for all sources:
- Always include a schema manifest and a canonical name map (logical name → physical name).
- Provide small, curated example queries for each data domain (golden queries).
- Enforce governance filters (e.g., PII removal, row-level security) at the context level so any generated query respects them.

### Semantic Model as Source
When to use:
- The Semantic Model (Fabric semantic models / Power BI semantic layer) is ideal when business logic and measures are already modeled (calculated columns, measures, friendly names, synonyms).

How to integrate:
- Use the semantic model as the canonical vocabulary: map user intents and entity names to the semantic model's measures and dimensions.
- Store canonical synonyms in the system CONTEXT: e.g., "ARR" → `Measures.TotalARR`, "Active Clients" → `DimCustomer[ActiveFlag] = 1`.
- For RAG: use the semantic model metadata (descriptions, measure formulas) as high-signal retrieval documents — it helps the LLM produce accurate measure names and avoid inventing calculations.

Training / Context patterns:
- Include short, explicit measure examples in the system persona:
  > EXAMPLE MEASURE: "Revenue" maps to `Measures.NetRevenue` which excludes refunds and internal transfers.
- Provide the LLM with measure definitions and calculation formulas as fenced code blocks — the model should treat these as authoritative.

Practical enforcement:
- When generating DAX, prefer returning the semantic measure name rather than raw SQL, and validate that the generated DAX calls only allowed measures.
- Validate output with the semantic model: if a generated expression references a non-existent measure or misuses aggregation, reject or rewrite.

References:
- Use semantic layer examples from the Fabric Data Agent SDK and from your project's semantic model manifests to populate the CONTEXT.
- See sample SDK patterns: [microsoft/fabric-samples - data-agent-sdk](https://github.com/microsoft/fabric-samples/tree/bbf03d0b558b47551486eee8e2686940e8473dc2/docs-samples/data-science/data-agent-sdk)

### Lakehouse as Source
When to use:
- Use the Lakehouse when data is semi-structured or you require access to raw, event-level records, text, or documents that need preprocessing and embedding (e.g., customer support logs, invoices, documents).

How to integrate:
- Create a preprocessing pipeline to normalize, chunk, and embed textual content stored in the lakehouse (Delta files).
- Keep a metadata manifest per table/file with canonical column names, partition keys, and update frequency.
- Build a vector store of embeddings for textual records, and store document pointers (file path, row id, partition) to enable deterministic retrieval.

Training / Context patterns:
- Provide the agent with retrieval rules: prefer semantic search on embeddings for free-text queries and fallback to SQL when intents map to structured column queries.
- Include instructions for chunking: max token size, overlap percentage, and how to include source attribution in answers.

Example pipeline (Lakehouse → RAG):
1. Extract textual fields from Delta files (e.g., support_text, comments).
2. Clean, normalize, and canonicalize (lowercase, remove PII, strip HTML).
3. Chunk long documents into ~500–1000 token pieces with overlap.
4. Generate embeddings and index in vector store (store metadata: table, partition, row_id).
5. In agent CONTEXT: provide top-k retrieved chunks (with provenance) and a strict instruction: "Only use retrieved chunks and explicitly cite `source:file:path#rowid`."

Practical enforcement:
- Disallow free-form hallucination over lakehouse content. Require the agent to say "Data not found" when top-k retrieval has insufficient similarity.
- For derived metrics, prefer materialized views in the Lakehouse to avoid expensive on-the-fly computations.

### Warehouse as Source
When to use:
- Use the Warehouse (Fabric Warehouse / dedicated SQL endpoints) for high-performance, aggregated analytics and when strict ACID semantics or complex joins are required.

How to integrate:
- Map logical business names to warehouse tables and materialized views.
- Provide the agent with a manifest of optimized query templates and allowed parameter ranges.
- Enforce query cost limits and add pre-execution checks (explain plan estimate or row limit).

Training / Context patterns:
- Keep a library of approved warehouse query templates and "golden queries" for common business questions.
- In the system persona include performance guardrails:
  > *Do not generate queries without an indexable WHERE clause. If user intent is broad, ask a clarifying question.*

Practical enforcement:
- Validate generated SQL with a static analyzer before running (deny full-table scans, require where clause on partition key).
- For aggregations, prefer referencing materialized views (pre-aggregated data) provided in the context.

---

## Prep Data for AI

Preparation of data is critical — LLMs and RAG pipelines rely on high-quality, canonicalized, and well-documented sources. "Prep Data for AI" spans both the technical ETL and the semantic design work.

Primary steps:

1. Discovery & Inventory
   - Catalog datasets, semantic models, table schemas, text fields, and sample rows.
   - Produce a schema_manifest.json that includes column types, required columns, PII flags, and sample values.

2. Clean & Normalize
   - Standardize date/time formats, currencies, units.
   - Null handling policy (fill with sentinel values or exclude).
   - Deduplicate and canonicalize identifiers (customer_id, product_sku).

3. Enrich & Canonicalize
   - Create mapping tables for synonyms and common aliases (e.g., "qty" → quantity).
   - Aggregate raw facts into domain-specific measures (e.g., lifetime_spend).
   - Compute derived columns that are used frequently in semantics (status flags, cohorts).

4. Annotate & Label
   - Add human-readable descriptions for every column and measure (used in semantic model docs).
   - Label text segments for training retrieval or classification tasks (intent labels, entity spans).

5. Chunking & Embedding (for textual sources)
   - Decide chunk size and overlap.
   - Store chunk metadata (source table, path, row id, chunk id).
   - Create a regular update pipeline for embeddings.

6. Build Schema & Data Contracts
   - Define stable data contracts for the agent to rely on: schemas, column types, availability SLAs.
   - Version the contract (contract v1, v2) to allow safe updates.

7. Security & Governance (apply early)
   - Tag PII and apply redaction/obfuscation rules in the preprocessing pipeline.
   - Apply row-level security filters by default in CONTEXT (e.g., limit to user’s tenant).

Practical artifacts to add to repo:
- schema_manifest.json (machine-readable)
- canonical_name_map.yaml (logical → physical)
- embedding_pipeline.md (docs + sample code)
- preprocessing_notebook.ipynb

---

## Ontology Design & Usage

An ontology turns domain knowledge into a structured, machine-readable map that the agent can reliably use. Where possible, link ontologies into the semantic model and lakehouse manifests.

Why ontology matters:
- Eliminates ambiguity (is "client" a person or company?)
- Provides canonical identifiers (URI-style IDs) so generated queries refer to stable entities.
- Enables relationship traversal (Customer → Orders → Invoices) without ambiguous free text.

Core ontology components:
- Classes (e.g., Customer, Product, Invoice)
- Properties (attributes, e.g., Customer.lifetime_spend)
- Relationships (e.g., Customer PLACED Order)
- Synonym list (mapping user terms to canonical properties)
- Constraints and cardinalities (one-to-many, optional/required)

How to use in your Context Engineering:
- Include a compact ontology extract in the CONTEXT (fenced and indexed).
- Provide mapping rules: "When user asks about 'client', prefer Customer class. When ambiguous, ask for clarification."
- Use ontology for entity resolution before generating SQL: map user entity to canonical table + join path.

Example snippet (ontology fragment)
```yaml
Customer:
  id: Customer.customer_id
  synonyms: [client, buyer, account]
  properties:
    - lifetime_spend: numeric, definition: "Total net spend across all orders"
    - active_flag: boolean
Order:
  id: Orders.order_id
  relationships:
    - placed_by: Customer.customer_id
```

Versioning & governance:
- Store ontologies in /ontology with a changelog and version tags.
- Keep a living document that business owners can edit and validate.

---

## Putting it together: Example Flow (Semantic Model + Lakehouse + Ontology)
1. User: "Show revenue for our high-value clients in Q4."
2. Agent flow:
   - Entity resolution via ontology: "high-value client" → Customer.lifetime_spend > 50000
   - Map semantic names to semantic model measures: "revenue" → Measures.NetRevenue
   - Retrieve relevant lakehouse documents if needed (e.g., invoices) for provenance
   - Generate a warehouse query referencing materialized views or semantic measures
   - Pre-execution static checks (RLS, required WHERE, cost limit)
   - Return structured result with provenance and a note on confidence

---

## Templates & Repo Files
This repository should include:
- /templates/system_prompt_agent.md — R.C.O.F.-based system prompt examples (SQL, DAX, KQL variants)
- /templates/quickstart_sample.md — minimal example and instructions to drop into Fabric
- /templates/semantic_model_examples.md — sample semantic model fragments and mapping instructions
- /templates/lakehouse_embedding_pipeline.md — sample ETL & embedding pipeline
- /ontology — ontology files (YAML/JSON-LD) with versioning
- /tests — validation notebooks and unit tests
- /examples — before/after prompts and queries

Add these as starting artifacts so teams can copy and adapt.

---

## Contributing & License
We welcome contributions: small examples, new templates, or validation checks. Suggested files for PRs:
- Add a new template under /templates with a short README describing dataset mapping.
- Add unit tests under /tests for every template.
- Add ontology updates under /ontology with a migration note.

License: Add your preferred license (e.g., MIT).  
Contributing guide: Add CONTRIBUTING.md with PR template and testing instructions.

---

## Roadmap & Next Steps
- Add runnable Fabric notebook examples demonstrating end-to-end ingestion → query → agent response.
- Add CI checks to run tests/validation_notebook.ipynb automatically.
- Provide a sample agent runtime config for Microsoft Fabric and Copilot integration.
- Populate /templates and /ontology with concrete examples from your own datasets.

---

*Authored by Sahil | AI Engineer & Data Strategist*  
References: Microsoft Learn ([Fabric Data Agent](https://learn.microsoft.com/en-us/fabric/data-science/fabric-data-agent)), Microsoft samples ([microsoft/fabric-samples - data-agent-sdk](https://github.com/microsoft/fabric-samples/tree/bbf03d0b558b47551486eee8e2686940e8473dc2/docs-samples/data-science/data-agent-sdk))
