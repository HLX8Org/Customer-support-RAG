# Candidate mobile-protection corpus

Application requirements and decisions are maintained in the [MVP specification](../../../docs/specs/insurance-rag-mvp.md), [ADR log](../../../docs/adr/README.md), and [TDD plan](../../../docs/testing/mvp-test-plan.md). This file documents source evidence and earlier discovery notes; the specification is the entry point for implementation.

Downloaded on 2026-10-06 from the public links on [Samsung UK's Care+ page](https://www.samsung.com/uk/offer/samsung-care-plus/).

These are authentic public policy documents, not a benchmark dataset or customer records. Public availability does not establish an open redistribution license; no open dataset license was verified. Preserve originals and provenance. The user accepted UK/English for the learning prototype.

| Product | Document | Pages |
| --- | --- | ---: |
| Samsung Care+ | [Full terms](SCPlus_Terms_Conditions_UK_1.pdf) | 10 |
| Samsung Care+ | [Product summary](SCPlus_IPID_UK_1.pdf) | 2 |
| Samsung Care+ with Theft & Loss | [Full terms](SCPlus_Theft_and_Loss_Terms_Conditions_UK_1.pdf) | 11 |
| Samsung Care+ with Theft & Loss | [Product summary](SCPlus_Theft_and_Loss_IPID_UK_1.pdf) | 2 |

The full terms contain a printed version label of 5.12.2025 and policy symbols UK_SC_01 and UK_SCTL_01. Being linked from the provider's current page does not establish that these terms apply to every existing customer. Keep document version, product, and jurisdiction explicit.

## Validation completed

- Confirmed four files are PDFs and parsed successfully with pypdf.
- Confirmed nonempty text extraction on every page: 25 pages total.
- Visually inspected the first Care+ summary page and the third Theft & Loss terms page using rendered local PDFs.
- Recorded source URLs, retrieval date, byte lengths, page counts, extracted character counts, printed version labels, and SHA-256 checksums in [source-manifest.json](source-manifest.json).

No index, embeddings, customer records, or application have been created. Extraction checks do not establish reading-order correctness for all tables or end-to-end answer accuracy.

## Confirmed application requirements

- Begin with non-life mobile-device protection as a local learning prototype; expand toward production later.
- Provide customer chat for policy explanations, product comparisons, and possible upgrade exploration.
- Start with local PDFs and Google Drive as sources; add connectors later.
- Use synthetic customer data rather than real customer records.
- Prospects can use public product information; existing customers can access their own private policy information.
- Authorized customer-support employees initially have access across customers; later limit access to the escalated customer and current session. Other employees must not access the support workspace or private customer data.
- If retrieved evidence is insufficient, say so and escalate uncertain cases.

## Proposed design choices, pending interview completion

- Use an authoritative account-to-policy mapping for exact policy identification. Use vector retrieval to find clauses within the entitled product/version, not to decide which customer owns a policy.
- Keep public product wording separate from private customer/account data and support-only material. Apply access checks on all retrieval and record-lookup paths.
- Ask for missing incident facts where relevant. If no supporting evidence is found, state that the answer is unknown; do not infer a coverage exclusion merely from missing search results.
- Cite document, page, and relevant clause for coverage explanations; retrieve conditions and exclusions as well as benefits.
- Compare products without claiming an existing customer's upgrade eligibility unless an authoritative source supports it. These PDFs alone have not established a general upgrade entitlement.
- Use a local support queue for prototype escalation; a real support-service integration is a later decision.
- Test unsupported questions, insufficient incident facts, mismatched policy versions, and attempts to access another customer's records.

## Confirmed implementation direction

- UK/English is suitable for the learning corpus.
- Python-first development with incremental feature additions.
- Host the vector database locally.
- Keep answer-generation providers and model types replaceable. Also support configurable embedding models for MVP testing and evaluation. Pin each embedding configuration within its own index; never mix incompatible document and query vectors. No specific model provider or vector database has been selected.
- Changing an incompatible embedding model requires regenerating document vectors and migrating the index; changing the answer-generation model requires compatibility and quality checks.

## Embedding evaluation requirements

- Use one embedding interface with separate document and query encoding methods. Each adapter owns its model-specific query/document prompts, tokenizer, normalization, and output dimensions.
- Initial recommended candidates: Qwen/Qwen3-Embedding-0.6B and BAAI/bge-small-en-v1.5. This is a proposed benchmark pair; neither has been run on the corpus.
- Persist canonical extracted blocks and chunk texts with stable source references and IDs. Build a separate index for each corpus snapshot, chunking configuration, and embedding configuration.
- Record model ID/revision, adapter/preprocessing version, tokenizer, query/document prompts, dimensions, normalization, similarity metric, corpus checksum, and chunking version in an index manifest. Validate the selected query encoder against that manifest before searching.
- Selecting a model with an already built compatible index switches retrieval to that index. Selecting an unbuilt configuration requires indexing before it can answer questions.
- Hold the corpus, chunk texts, access filters, retrieval settings, and labelled questions constant for embedding-only comparisons. Use chunks that fit every candidate's tokenizer/input limit, including prompts and headings; reject or report overlength inputs rather than silently truncating them.
- Evaluate chunking strategies in separate experiments. Hold the generation model and prompt fixed when comparing end-to-end answers.
- Report required-clause retrieval, completeness of benefit/condition/exclusion evidence, citation correctness, indexing time, warm query latency, startup time, and memory use. Include unsupported questions and unauthorized-access cases. Similarity scores are not coverage probabilities or directly calibrated across models.
- Cache vectors and results by the complete experiment configuration. Keep customer permissions and support escalation behavior consistent across all model adapters.

Separate indexes trade extra storage for simple isolation and reproducible comparisons. For this small candidate corpus, this is the recommended MVP approach. Shared records with multiple named vector fields are a possible later optimization if the selected database supports them.

## Escalation recommendation and verified reference process

Recommended MVP: a persistent local support queue, customer-triggered request, evidence and transcript references, support-only review screen, and a response visible in the customer's app. This is a proposed design, not a Samsung integration.

Samsung UK public sources checked on 2026-10-06:

- [Repair routing](https://www.samsung.com/uk/support/repair/) separates policies purchased before 19 January 2026 (Assurant) from policies on or after that date (bolttech route).
- [Current Care+ portal](https://uk.careplus.co/) offers policy lookup, cancellation, and claim initiation; lists contact.uk@careplus.co and +44 204 623 8217, available 24 hours except public holidays.
- The full policy wording above publishes complaints_uk@bolttech.eu and a complaint process: contact within three working days, aim to answer within four weeks, and eligible Financial Ombudsman Service escalation after an unsatisfactory final response or no response within eight weeks. Refer to the full terms for conditions, including the referral deadline.

These sources do not establish Samsung's internal ticketing platform, model vendor, AI escalation thresholds, or automatic chat-transcript transfer. Do not represent the prototype support queue as an insurer claim submission or approval.
