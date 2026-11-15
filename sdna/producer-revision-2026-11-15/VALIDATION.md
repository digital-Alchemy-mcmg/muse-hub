# Validation — Four producer skills — Operator Decisions 1–4 — 2026-11-15

Method: each revised skill was checked against the directive's 10 validation checks by reading the revised text. No skill was loaded into Quick, executed, or tested against a live document in this revision; live execution tests are listed as remaining work in each skill's own test section and are not claimed here.

Directive checks:
1. Full-fidelity acceptance occurs before decomposition.
2. Scan-first/group-first is implemented in the correct order.
3. Section-level and total blurb counts are produced.
4. Source-local IDs and provenance remain intact.
5. Incomplete sources cause a complete stop.
6. No partial atomic twin or receipt can be produced following source failure.
7. Amazon output is document-oriented, not inherited NotebookLM dataframe production.
8. Each skill can perform its own task without requiring knowledge of the broader architecture.
9. Workflow invocation does not require the operator to re-enter the skill's prompt instructions.
10. No unrelated skills or architectural responsibilities have been changed.

## sdna-decompose-source
| Check | Result | Evidence in the revised skill |
|---|---|---|
| 1 | PASS | Gate 0, before Phases 1–4: whole-document faithful-read check. |
| 2 | PASS | Phase 1 scan → Phase 2 section map → Phase 3 decomposition/counting → Phase 4 organized output; later phases barred until earlier complete. |
| 3 | PASS | Phase 3 per-section counts + overall count, sum check stops on mismatch; Phase 4 returns both. |
| 4 | PASS | Source-local IDs `001`+, document order, text-preserved; every atom carries section, heading as written, most precise location, quotation, proposition. |
| 5 | PASS | Gate 0 failure list (unreadable/missing/inaccessible/truncated); only output is failure notification with affected location + explanation. |
| 6 | PASS | Gate 0: no partial atoms, no partial output; twin/receipt are not produced by this skill and its failure output gives the next step nothing to build on. |
| 7 | PASS | No NotebookLM, no Sheets, no dataframe in the skill. Output is organized decomposition material, not a spreadsheet. |
| 8 | PASS | No other skill named; no workbook, routing, registration, admission, or pipeline knowledge; no spec citations. Inputs/procedure/output/failure are its own. |
| 9 | PASS | Skill contains the full procedure; invocation supplies only the one original (+ optional reference/subject/classification list). |
| 10 | PASS | Only this skill's text changed; six downstream skills untouched. |
| Required tests | STATED IN SKILL, NOT RUN | Two-in-one STOP; two-separate PROCEED independently; unreadable page STOP; missing content STOP; compound assertions in readable document PROCEED. Live run required before use. |

## sdna-write-atomic-twin
| Check | Result | Evidence |
|---|---|---|
| 1 | PASS (by input) | Incomplete/failed supplied material → stop, no partial document. Fidelity itself is established by the decomposition skill; this skill does not re-admit a failed source. |
| 2 | N/A | Scan-first/group-first is the decomposition skill's order; this skill preserves it by producing atoms grouped by section in document order from the supplied section map. |
| 3 | PASS (by preservation) | Atom count returned and checked equal to the supplied overall count; per-section grouping preserved. |
| 4 | PASS | All 22 content elements preserved per atom; local IDs, section, location, quotation, proposition unchanged from supplied material. |
| 5 | PASS (by input) | Failed/incomplete material → stop, report, no document. |
| 6 | PASS | Same input validation; mismatch between supplied count and produced count stops the run; no partial document is returned. |
| 7 | PASS | Document artifact via the supplied document-generation workflow; 22 elements are content, not spreadsheet columns; explicit ban on converting to spreadsheet/sheet export. No NotebookLM reference. |
| 8 | PASS | No other skill named; no workbook, Sheet 01, registration, admission, or pipeline knowledge. Completion-record identifier is an input value, not downstream knowledge. |
| 9 | PASS | Full procedure in the skill; invocation supplies the decomposition material (+ identifier). |
| 10 | PASS | Only this skill's text changed. |
| Required tests | STATED IN SKILL, NOT RUN | Blank quotation → REVIEW_REQUIRED; missing date → UNSPECIFIED; later-atom reference intact; incomplete material → stop, no partial document. Live run required. |

## sdna-write-decomposition-receipt
| Check | Result | Evidence |
|---|---|---|
| 1 | PASS (by input) | Incomplete/failed document or record → stop, no receipt. |
| 2 | N/A | Ordering belongs to decomposition; receipt preserves counts derived from the supplied record and document. |
| 3 | PASS (by preservation) | R09 regions examined from supplied record; R10 = document atom count, checked equal. |
| 4 | PASS | R04/R05 match the document; R11/R12 IDs rechecked to exist in the document; R13 attempts carry region + reason, no ID. |
| 5 | PASS (by input + coverage rule) | A record showing an unreliable region or incomplete coverage → stop, no receipt. |
| 6 | PASS | Same stop; R14 `[]`, R15 `COMPLETE`, R16 `null` on every receipt produced; PARTIAL receipt is not produced. |
| 7 | PASS | No NotebookLM, no Sheets, no dataframe. Receipt is a separate completion record; its physical format is flagged missing rather than invented (see unresolved U3). |
| 8 | PASS | No other skill named; no workbook, registration, admission, or pipeline knowledge. |
| 9 | PASS | Full procedure in the skill; invocation supplies the document, the record, and the identifier. |
| 10 | PASS | Only this skill's text changed. |
| Required tests | STATED IN SKILL, NOT RUN | Ambiguous/conflicting IDs appear in R11/R12 and exist; unreliable-region record → stop, no receipt. Live run required. |

## sdna-set-twin-down
| Check | Result | Evidence |
|---|---|---|
| 1 | PASS (by input) | Missing/incomplete/failed items → stop, report, place nothing. |
| 2 | N/A | Ordering belongs to decomposition; this skill preserves the pair as supplied. |
| 3 | PASS (by preservation) | Atom count compared across the pair before placement; mismatch stops the run. |
| 4 | PASS | Source reference, filename, identifier, and atom count compared across both items; read-back verified at destination. |
| 5 | PASS (by input) | Failed source produces nothing to place; incomplete pair is not placed. |
| 6 | PASS | No partial pair placed; one item without its partner → no done status, no placement. |
| 7 | PASS | No Sheets export, no manual export, no `02_ATOMIC_TWINS`, no spreadsheet conversion. Destination is supplied at invocation; none invented. |
| 8 | PASS | No other skill named; no Sheet 01, registration, routing, Apps Script, reconciliation, or pipeline knowledge. |
| 9 | PASS | Full procedure in the skill; invocation supplies the pair, the destination, and the naming. |
| 10 | PASS | Only this skill's text changed. |
| Required tests | STATED IN SKILL, NOT RUN | Single item without partner → no done status; no destination supplied → hold naming the missing destination, nothing placed. Live run required. |

## Cross-skill checks
- Check 6 across the sequence: a fidelity failure in decomposition yields only a failure notification, which contains no atoms, no counts, and no document — so the twin skill's input validation has nothing complete to accept, the receipt skill has no document to receipt, and set-down has no pair to place. No partial twin or receipt can be produced following source failure, provided the workflow does not invoke the later skills on a failed run (workflow orchestration; each skill enforces the same stop at its own input boundary).
- Check 10 across the package: six downstream skills untouched; no architecture module, dependency, or responsibility added. See manifest hashes.
- Not validated here: live Quick invocation, document-generation binding, and the unresolved output requirements (U1–U6). Those need operator decisions and a live test run; they are not claimed as passing.
