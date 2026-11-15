# Change report — Four producer skills — Operator Decisions 1–4 — 2026-11-15 01:01 EST

## Package
Location: `~/workspace/sdna-atrium/producer-revision-2026-11-15/`
Authority: Operator Directive — Four Approved Decisions (Amazon Quick Skills — Producer Skill Revision), 2026-11-15.
Spec baseline: `SDNA_Evidence_Foundry___Authoritative_Construction_Specification.md`, SHA-256 `cc83d331f93b503c28a013b7265c96388b1be671db9739b6bbdf07a7b9b6b042`.
Original package baseline: `~/workspace/sdna-atrium/skills-zip/payloads/`, manifest `PAYLOAD-MANIFEST.json`. Originals untouched — see hashes in `PACKAGE-MANIFEST.json`.

## Scope
Revised, 4 skills only:
1. `sdna-decompose-source`
2. `sdna-write-atomic-twin`
3. `sdna-write-decomposition-receipt`
4. `sdna-set-twin-down`

Unchanged, 6 skills — not rewritten, not reworded:
`sdna-validate-twin`, `sdna-register-family`, `sdna-place-and-score`, `sdna-flag-conflict`, `sdna-record-in-workbook`, `sdna-reasoner-scratch-copy`.
No skill was merged or split. No structural change to the four task boundaries.

This revision supersedes the 2026-11-14 23:43 single-skill revision of `sdna-decompose-source` (`~/workspace/sdna-atrium/revised-skills/`). That file is preserved as-is for the record. What supersedes it: the PARTIAL-output behavior is now removed entirely (Decision 3), and downstream skill names / workbook references are now removed from the skill text (Decision 4). The scan-first / group-first order from that revision is carried forward unchanged.

## What was checked before editing
- All four original payloads, read in full.
- Spec M01.C.1–C.15, M01.D.1–D.3, M01.E, M01.G, M01.H.
- Downstream handoff expectations in the originals (twin 22-column table, receipt R01–R16, set-down export to Sheets / `02_ATOMIC_TWINS`).
- Searched the workspace for an established Amazon document format or destination for the atomic-twin document. None was found. The Quick↔Sheets research confirms Sheets editing only; Decision 2 states that does not govern the twin document. No format or destination was invented — see `UNRESOLVED-OUTPUT-REQUIREMENTS.md`.

## Decision 1 — Scan-first / group-first (`sdna-decompose-source` only)
Added as the execution order, Phases 1–4, before any atom is extracted:
- Phase 1 Full document scan: subject name, contact information present in the source, number of sections, original headings verbatim, original order, overall structure/regions. Missing = unknown, never invented.
- Phase 2 Section organization: section groupings, original headings preserved, stable source-location references, unheaded regions identifiable by location reference + start/end locators with no invented heading. Section map: sequence number, heading exactly as written (or unheaded), start locator, end locator, stable region reference. No invented section labels; no A–Z labels or glyphs (neither the directive nor the spec names them).
- Phase 3 Decomposition and counting: one atom per independently meaningful assertion, compound assertions split, source-local IDs in document order, every atom associated with its section and precise location, per-section counts + overall count with a sum check that stops the run on mismatch.
- Phase 4 Organized output: the nine determinability items from the directive, mapped to concrete output elements (source identity, subject, section count, headings, start/end locators, per-section counts, atoms grouped by section, location + quotation per atom, review list).
- The original C.1–C.15 substance is preserved inside the phases; the phase annotations replace the original's C.2/C.3 wording, not its requirements.

## Decision 2 — Amazon-specific output (all four skills)
Removed wherever it conflicted with the Amazon workflow:
- "NotebookLM source reference" → source reference supplied at invocation / as stated in the source. No NotebookLM notebook, reference document, or export setting is required or assumed in any revised skill.
- Google Sheets dataframe requirements removed: no "write one text row per atom", no "exact headers in numeric order", no spreadsheet staging surface, no header-order read-back, no sheet export, no `02_ATOMIC_TWINS`, no frozen rows / protected ranges / validation rules.
- `sdna-write-atomic-twin`: produces an atomic-twin *document* via the document-generation workflow supplied at invocation. The 22 data elements are preserved as *content elements* per atom (same items, same rules, numbered 01–22 for reference), not as spreadsheet columns. Presentation order/layout is the workflow's, not the skill's. No information discarded for format change: quotation, proposition, semantic ceiling, classification, dates, duplicate/conflict references, taxonomy status all retained.
- `sdna-write-decomposition-receipt`: retained as a separate completion record, because the package's first-cut success evidence is a paired twin + receipt export. Its 16 content elements (R01–R16) are preserved with their rules, reworded without dataframe references (R10 = atom count of the document, not row count). Its physical format is NOT decided here — see unresolved U3.
- `sdna-set-twin-down`: no Sheets export, no manual export, no assumed destination. Places the pair at the destination supplied at invocation, verifies read-back there, and holds (placing nothing) when no destination is supplied.
- No replacement format or destination invented in any skill.

## Decision 3 — Full fidelity or nothing (`sdna-decompose-source` gate; enforced in the other three as input validation)
- New Gate 0 in `sdna-decompose-source`, before scanning, organizing, or decomposition: establish that the complete original can be read faithfully. Failure causes: unreadable pages, missing pages, inaccessible sections, truncated content, unreadable regions, any condition preventing a complete faithful read.
- On failure: stop the entire run; do not extract readable portions; do not produce partial atoms, a partial twin, or a partial receipt; flag, notify the operator, identify the affected page/section/region where possible, explain what prevented processing. The only output is the failure notification.
- Removed from the Amazon producer workflow: the former unreadable-region-to-PARTIAL-output behavior (spec M01.D.3: unreadable → R14, R15 `PARTIAL`, R16 names it; and the original C.14 "visual regions recorded as unprocessed and continue"). Under this revision a visual-only evidence region that cannot be read as text fails the fidelity gate; it is not carried forward as an unprocessed region with the rest of the document.
- Preserved distinctions: a compound assertion in a fully readable document is NOT a failure and is decomposed normally; a claim with no identifiable supporting passage in a fully readable document is an unsupported extraction attempt (recorded, no atom) — that is a lack of support, not a lack of readability, and does not trigger the gate.
- Consequential change in the receipt skill: every receipt that exists has R14 `[]`, R15 `COMPLETE`, R16 `null`. A `PARTIAL` receipt is not produced. If a supplied decomposition record shows an unreliable region or incomplete coverage, the receipt skill stops and produces nothing.
- Twin, receipt, and set-down skills each carry input validation: incomplete, failed, or missing material → stop, report, produce no partial document/receipt/placement. The receipt and output skills are not invoked for a failed source (workflow orchestration; the skills enforce it at their own input boundary).
- Required tests are written into `sdna-decompose-source`: two originals in one invocation STOP; two in separate invocations process independently; unreadable page STOP; missing content STOP; fully readable with compound assertions PROCEED. The isolation test and the incomplete-source test are stated as separate tests.

## Decision 4 — Skills are self-contained task instructions (all four skills)
Removed from every revised skill:
- Names of other skills, downstream handoffs ("hand off to receipt writer / set-down"), and pipeline sequence knowledge.
- Workbook knowledge: workbook subject binding, Sheet 01, registration, admission, placement planes, routing, validation, family/full UIDs.
- Architecture citations: M01/M02 section numbers, NLM §, TERM §, FN- numbers. Traceability to the spec lives in this change report, not in the skill text.
- The phrase "producer chain / producer stage" as an architectural dependency; each skill now states its own inputs, procedure, output, and failure conditions only.
Kept in each skill, as part of its own assignment: its required inputs, its procedure, its output, its acceptance checks, its failure/stop conditions. Where an input comes from the workflow (e.g. a completion-record identifier, a destination, a document format), the skill states "supplied at invocation" and stops if it is missing — it does not name the supplier.
- `sdna-decompose-source` no longer cites twin/receipt field numbers (08/16/18/19/20/22, R13–R16). Its own output carries the same substance in its own terms (quotation blank → review + note; unsupported attempt → region + reason, no ID).
- `sdna-write-atomic-twin` and `sdna-write-decomposition-receipt` keep the shared completion-record identifier as an input value, not as knowledge of each other: each carries it unchanged if supplied, stops if it is missing, and never names the other skill.

## Governed deltas vs the spec (operator decisions govern for the Amazon deployment)
| # | Spec point | Amazon revision | Authority |
|---|---|---|---|
| D-1 | M01.D.3 unreadable → R14 / PARTIAL / R16 | Removed; full-fidelity gate stops the run, no receipt | Decision 3 |
| D-2 | M01.C.14 visual regions recorded as unprocessed, continue | Removed; unreadable visual evidence fails the gate | Decision 3 |
| D-3 | M01.D.1 atomic twin as 22-column dataframe / Google Sheet | Document artifact; 22 elements preserved as content, not columns | Decision 2 |
| D-4 | M01.D.2 receipt R15 `COMPLETE`/`PARTIAL`, R14/R16 conditional | R14 `[]`, R15 `COMPLETE`, R16 `null` on every receipt produced | Decision 3 |
| D-5 | M01.E twin as Google Sheet in `02_ATOMIC_TWINS`, receipt alongside | Destination supplied at invocation; none invented | Decision 2 |
| D-6 | M01.A/H NotebookLM notebook, reference, export settings, stable NotebookLM source reference | Not carried into any revised skill | Decision 2 |
| D-7 | M01.C.2–C.3 inventory/structure as steps | Executed as Phases 1–2 (scan-first / group-first) before decomposition | Decision 1 |

No other spec rule was changed. Evidence content, source fidelity, local IDs, section organization, and provenance are preserved in full.

## What was NOT changed
- The six downstream skills: untouched, original hashes retained in the manifest.
- No skill merged or split; individual task boundaries preserved.
- No deployment, no external production change, no Quick loading, no workbook write. These are revised files only.
- No new architecture module, system dependency, or agent responsibility introduced. See the separate architecture addendum.

## Files in this package
- `sdna-decompose-source.md` — revised
- `sdna-write-atomic-twin.md` — revised
- `sdna-write-decomposition-receipt.md` — revised
- `sdna-set-twin-down.md` — revised
- `CHANGE-REPORT.md` — this file
- `VALIDATION.md` — per-skill validation against the directive's 10 checks
- `UNRESOLVED-OUTPUT-REQUIREMENTS.md` — genuinely missing output requirements, for operator review
- `PACKAGE-MANIFEST.json` — revised + unchanged hashes
- `ARCHITECTURE-ADDENDUM-SKILLS-AS-TASK-INSTRUCTIONS.md` — separate memo implementing Decision 4
