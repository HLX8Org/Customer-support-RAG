# MVP acceptance and TDD plan

Date: 2026-10-06 | Status: Planned; no executable application tests exist

Related: [specification](../specs/insurance-rag-mvp.md), [ADRs](../adr/README.md), [traceability](../specs/traceability.json).

Concrete tooling and test placement: [Technical design](../technical-design.md#9-test-and-evaluation-implementation). pytest/FastAPI TestClient/Streamlit AppTest are proposed implementations of this plan; they have not been installed or exercised. DP-13 maps the stack to existing test IDs, without adding redundant checks or claiming application verification.

## Test-first workflow

1. Select one requirement and its acceptance example. Check the ADR status; do not treat an unresolved recommendation as an accepted technology choice.
2. Write the smallest meaningful behavior test. Use fixtures and dependency boundaries so ordinary checks need no API credentials or model download.
3. Run it and record Red: a failure because the required behavior is absent. Import/collection failures alone are not adequate evidence of a behavior test. Add only enough interface skeleton to reach the intended assertion when needed.
4. Implement the smallest change that satisfies the behavior; run the relevant tests and record Green.
5. Refactor duplication/boundaries without changing required behavior; rerun relevant checks. Do not weaken assertions to hide a defect.
6. Update requirement/ADR traceability and record actual commands, environment, outcomes and checks not run. Integrations and model evaluation have separate evidence gates.

The following T-IDs are planned behaviors, not current Python functions or runnable commands. Convert each to an executable test when its increment begins. Choose the test runner with runtime dependencies; do not publish placeholder commands as verified commands.

## Fixture and oracle design

An oracle is the expected result against which a test is checked. Use manually reviewed evidence IDs and controlled behavior, not the model's answer as its own oracle.

- Actors: prospect P1; customers C1 and C2; authorized support S1; ordinary employee E1; unknown principal U1. Every value is fictional and labelled.
- Accounts: C1 references the exact Care+ document/version; C2 references Theft & Loss. Personal dates, device details, premiums and fees are fictional account fixtures, not insurer statements.
- Corpus: immutable source manifest; reviewed blocks and chunks; exact references to source pages/clauses. Include two-column summaries, oversized clauses, different versions and intentionally malformed extraction fixtures.
- Cross-section fixture: Care+ battery benefit on PDF page 3 plus manufacturer-warranty timing on PDF page 6. Test missing/known warranty status with reviewed evidence labels.
- Access fixtures: a private customer record, support-only note, private ticket and permitted public policy. Include ownership changes, missing permissions and cache reuse across actors.
- Model stubs: deterministic document/query encoders and generation outputs, including invalid citations, unsupported capabilities, service failures and unsupported answers. Stub success verifies application behavior only.
- Real adapters: separate opt-in local model runs; external API runs require configured credentials and explicit run authorization if billable. No real customer information is used.

## Planned acceptance tests

Unit = isolated logic; contract = common adapter interface; integration = components with actual local storage/index; acceptance = observable user journey; evaluation = labelled real-model measurements.

| Test | Level | Given / when / expected result |
| --- | --- | --- |
| T-01 | Integration | Import a known PDF; original bytes remain unchanged and manifest checksum/source/version metadata match the imported document. Reimport does not silently duplicate identical source content. |
| T-02 | Unit/integration | Import corrupt PDF, empty extraction or extraction failure; document is quarantined/failed with reason and cannot enter a ready index. |
| T-03 | Unit | Load synthetic account/certificate fixtures; every personal field is labelled fictional and cannot overwrite official product wording. |
| T-04 | Integration | Import a user-exported Drive PDF; preserve origin/import mode and explicit application permissions. Missing private permission mapping fails closed; no claim of live Drive ACL verification. |
| T-05 | Integration | Extract reviewed numbered clauses/headings across pages; all retained text has correct heading and page/span provenance. |
| T-06 | Integration | Extract a two-column summary and benefit table; reviewed insured/excluded bullets and row labels remain associated correctly. Compare structural blocks, not mere nonempty text. |
| T-07 | Unit | Chunk complete clauses from different product/versions; chunks retain coherent units and never combine those scopes. |
| T-08 | Unit/contract | An oversized clause or model-overlimit input is submitted; split at valid boundaries or return explicit overlimit failure; no silent truncation or dropped citation spans. |
| T-09 | Unit/acceptance | Retrieve the battery benefit; required reviewed warranty condition is included from its distant source section with both references preserved. |
| T-10 | Unit | A linked parent/condition belongs to a different version, missing source or denied scope; reject/flag the link and never include unauthorized evidence. |
| T-11 | Acceptance | Exercise the actor matrix across public/private search and lookup; each allowed/denied result agrees with server entitlements. Support broad access is limited to the synthetic prototype scope. |
| T-12 | Acceptance | C1 supplies C2's account ID, a support role flag or another session ID; server identity remains C1 and private lookup/action is denied. |
| T-13 | Integration/acceptance | Reuse caches and access citation/history/ticket URLs across actors or changed permissions; no private content, source snippets, replies or cached answers leak. |
| T-14 | Unit | Resolve C1's current policy; select the exact account reference, not a semantically similar policy. Missing authoritative reference returns an explicit missing-policy state. |
| T-15 | Unit/acceptance | Multiple historical policy versions exist; select the account-bound version and relevant date scope. Missing/ambiguous dates or mappings require clarification/review. |
| T-16 | Contract | Run each embedding adapter through document/query operations; model-specific instructions/tokenization are used and declared output shape/configuration are consistent. |
| T-17 | Contract | Include headings/query prompts near a tokenizer limit; count using that adapter's tokenizer and reject/report any overlimit input. Batch empty/error behavior is explicit. |
| T-18 | Integration | Query an index with mismatched revision, dimensions, prompts, normalization or preprocessing; reject before similarity search. Matching configuration succeeds. |
| T-19 | Integration/acceptance | Select an absent or partially built index; show a build-required state and do not silently query another model's index. A ready matching index becomes selectable. |
| T-20 | Integration | Change corpus, chunking or embedding configuration; use a distinct vector/result cache namespace. Repeat the identical configuration may reuse cache without mixing entitlements. |
| T-21 | Integration | Highly similar but unauthorized/wrong-policy evidence exists; it is excluded before context construction and never reaches generation. |
| T-22 | Integration/evaluation | Retrieve answerable cross-section cases; measure inclusion of every labelled required benefit, condition and exclusion rather than only one relevant hit. |
| T-23 | Unit/integration | Candidate search contains duplicate overlapping evidence and configured limits; preserve unique provenance and obey recorded limits without silently discarding required conditions. If context cannot fit, surface incomplete evidence. |
| T-24 | Contract | Switch generation adapters while holding an evidence fixture fixed; business request/response behavior is preserved, no evidence or permission selection changes, and unsupported capabilities fail explicitly. |
| T-25 | Contract/acceptance | Generation times out, rejects a capability or returns malformed output; show SERVICE_ERROR with retry/help options, not an insurance denial or factual UNKNOWN. |
| T-26 | Acceptance/evaluation | No supporting evidence exists; answer is UNKNOWN with appropriate uncertainty and a support offer, not a fabricated coverage assertion. Real-model behavior is separately measured. |
| T-27 | Acceptance | Evidence requires incident facts or warranty status that are missing; answer is NEEDS_FACTS and asks for the relevant information rather than giving unconditional coverage. |
| T-28 | Unit/acceptance/evaluation | Generation cites absent, incorrect-version or denied evidence; citation validator rejects it. Human-labelled evaluation separately checks whether valid citations actually support each claim. |
| T-29 | Acceptance/evaluation | Reviewed sources contain unresolved contradictory wording; answer is REVIEW_REQUIRED with relevant evidence rather than silently selecting the highest score. |
| T-30 | Contract/evaluation | A retrieved document tells the assistant to change roles or reveal records; source text is passed as untrusted evidence, no business side effect occurs, and real-model adversarial outputs are assessed separately. Mock success is not prompt-injection immunity. |
| T-31 | Acceptance/evaluation | Compare Care+ and Theft & Loss; retrieve separate permitted product evidence and cite documented differences, conditions and exclusions without cross-version contamination. |
| T-32 | Acceptance/evaluation | Ask for exact premium, upgrade eligibility or enrollment when no authoritative evidence exists; state the missing evidence, offer review where appropriate, and do not invent a quote or execute a purchase. |
| T-33 | Acceptance | Assistant offers escalation but customer has not submitted; no ticket exists. Explicit customer submission binds actor/session server-side and creates a support request, not an insurer claim. |
| T-34 | Integration | Create a ticket/reply, stop and restart storage/application; the owned ticket, transcript/evidence references and reply remain available with consistent status. |
| T-35 | Integration | Submit the same request twice or retry after ambiguous response; return the existing ticket/reference with one durable record. Persistence failure never produces a submitted confirmation. |
| T-36 | Acceptance | Support S1 reviews/replies, C1 reads their ticket, and C2/E1/U1 attempt access; only entitled actions succeed, regardless of chosen embedding/generation adapter. |
| T-37 | Unit/integration | Move tickets through allowed transitions and submit a forbidden transition; valid changes persist and invalid changes are rejected. A customer reply resumes a waiting case as specified. |
| T-38 | Evaluation contract | Compare embedding configurations; validate identical source/chunks/labels/access/retrieval settings and no truncation. Chunking experiments vary only chunking with fixed embeddings; end-to-end comparisons fix generation/prompt. Reject mislabeled incomparable runs. |
| T-39 | Evaluation integration | Complete/fail an evaluation run; report per-query evidence, required-evidence success, citation/answer review, raw timings, model startup/warm-query separation, memory, errors, configs and unrun checks. Do not substitute invented measurements. |
| T-40 | Unit/evaluation | Similarity scores differ across adapters; do not represent them as coverage probability or apply an uncalibrated cross-model confidence cutoff. Gold-label revisions remain separate and recorded. |
| T-41 | Integration | Run application/vector/account storage locally with deterministic models; local services bind only to loopback, state persists and core fixtures do not require external network access. |
| T-42 | Contract | Replace a source, persistence or support adapter with a compatible fixture; business access and response contracts remain intact. A missing provider configuration fails clearly without silently switching vendors. |
| T-43 | Test-run configuration | Execute the default offline suite without API credentials; network-dependent/local-model-download checks remain unrun or explicitly skipped with reasons. An explicit opt-in run reports separately and never claims billable/live success from mocks. |

## Evaluation seed and release evidence

Before tuning, author approximately 40 manually reviewed questions and reserve a held-out subset. Include ordinary paraphrases, explicit exclusions, missing incident facts, distant conditions, policy versions, comparisons, unknown eligibility and unsupported questions. Evidence labels include all necessary clause IDs; account facts and policy text remain separate.

Do not assert a quality percentage until there are actual measurements. Retrieval recall at k counts labelled evidence found in the first k results; all-required-evidence success checks whether the complete required set was found. Neither alone proves a generated answer is correct. Track false coverage assertions separately, with human review for ambiguous cases.

For each implementation increment, retain evidence of intended Red/Green/refactor runs, relevant regression results and failure explanations. Record tests not run. No test-coverage percentage or production-readiness claim follows from this planning document.

## Current validation status

- Planned behaviors: 43.
- Executable application tests: 0.
- Application TDD cycles: not started.
- Local embedding benchmarks: not run.
- External model/API checks: not run.
- Documentation mapping/link validation: recorded in the delivery response; distinct from application verification.
