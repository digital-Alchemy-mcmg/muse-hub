# Resolutions U1–U6 — Applied — 2026-11-15

Source: SDNA Evidence Foundry — Consolidated Conflict Resolutions (U1–U6), operator-approved, 2026-11-15. All six were listed as unresolved in `UNRESOLVED-OUTPUT-REQUIREMENTS.md` in the 2026-11-15 producer revision; all six are now resolved and applied to the four producer skills in this folder. No resolution was invented or altered here.

## U1 — Atomic twin format — RESOLVED, applied in `sdna-write-atomic-twin.md` (with `sdna-decompose-source.md`)
- Completed atomic twin is a plain-text `.txt` file.
- Filename: `LastName.FirstName.SDNA.txt`, from the subject's name as stated in the source. If last or first name is not available as stated, the twin skill holds and reports the missing naming input; it does not invent a filename.
- Manifest front matter: candidate name, processing date and time, original document filename, available document/binding identifier (or not available), Amazon execution identity, pairing metadata (source reference + completion-record identifier).
- Body: original section sequence, alphabetically labeled sections (A, B, C in original order), employment/job groupings as stated in the source, individually numbered atomic blurbs starting at 01 — blurb number equals local atom ID numeric value (blurb 01 = `001`). Source wording, quotations, and source-location references preserved.
- Footer: total atomic blurb count + SHA-256 integrity hash of manifest + body as written, excluding the footer hash line.
- Supersession noted: the earlier "no A–Z labels" restriction is superseded. U1 names alphabetical labels, so the decompose skill's section map now carries them (assigned in original order, headings unchanged).

## U2 — Storage and pairing — RESOLVED, applied in `sdna-set-twin-down.md`
- Files live in Amazon's available document repository, such as Spaces or My Files, as supplied at invocation.
- Separate folders: one for original source documents, one for completed atomic twins. Both folders are supplied at invocation; no folder names were invented.
- Pairing: original document filename + available binding identifier link original to twin. Set-down records the pairing in its handoff so the relationship is preserved for workbook registration.
- Twin `.txt` + receipt `.json` are placed together in the completed-twins folder.

## U3 — Receipt format — RESOLVED, applied in `sdna-write-decomposition-receipt.md`
- Existing 16-field JSON receipt structure R01–R16 retained, keys unchanged, schema not replaced.
- Executing agent/workflow (Amazon) generates the receipt.
- Failed full-fidelity processing produces a failure notification, not a successful receipt (already the rule; now explicit in the receipt skill).
- Amazon recorded as executing agent (see U6 for R06/R07).

## U4 — Permanent identity allocation — RESOLVED, applied in all four skills
- Workbook is the sole authority for permanent SDNA identity assignment.
- Sequence as resolved: Amazon receives/processes → creates twin → blurbs get sequential local IDs → source + twin submitted to workbook → workbook checks existing registrations/duplicates → upon registration assigns permanent family UID → permanent blurb UIDs derive from family UID + local IDs.
- Amazon does not mint permanent document-family or blurb UIDs. Stated explicitly in decompose (local IDs only), twin (no permanent UID in the file), receipt (R01 is not a family UID), and set-down (assigns none).
- A run stopping before workbook registration receives no permanent family UID.
- R01 / completion-record identifier must not automatically be treated as the permanent workbook family UID. Stated in twin, receipt, and set-down.

## U5 — Auto Run and Monitor Run — RESOLVED, applied in `sdna-set-twin-down.md`
- Operator selects the mode when starting the Amazon agent; the mode (`AUTO` or `MONITOR`) is supplied at invocation.
- AUTO RUN: execute complete workflow, validate twin, save `.txt` + JSON receipt to the designated repository automatically.
- MONITOR RUN: execute and validate the same workflow, present outputs for inspection; saving requires explicit operator authorization for that run.
- Shared: identical source reading, decomposition, counting, validation; full-fidelity cannot be bypassed; neither mode assigns permanent identifiers; difference is authorization to save, not processing.
- Twin and receipt skills do not save on their own; saving is set-down's step, controlled by the mode.

## U6 — Amazon execution identity — RESOLVED, applied in `sdna-write-atomic-twin.md` and `sdna-write-decomposition-receipt.md`
- Record `Amazon` in the twin manifest front matter and in the JSON receipt (R06).
- Execution identity identifies who performed the workflow, not the underlying reasoner or interpreter.
- Do not substitute a GPT model name, interpreter identity, or model version. Do not invent missing reasoner/interpreter metadata.
- Receipt R07 (interpreter version): a version only if supplied at invocation; if none is supplied, `null`. This is a governed deviation from the spec table's "Yes" for R07, per U6's do-not-invent rule.

## Resolution register

| ID | Conflict area | Operator-approved resolution | Status |
| -- | ------------- | ---------------------------- | ------ |
| U1 | Atomic twin format | Plain text `.txt`, `LastName.FirstName.SDNA.txt`, manifest, alphabetically labeled sections, employment/job groupings, numbered blurbs, footer count + SHA-256 | Resolved, applied |
| U2 | Storage and pairing | Separate Amazon repository folders (originals / completed twins), linked by source identifiers | Resolved, applied |
| U3 | Receipt format | Existing JSON R01–R16 | Resolved, applied |
| U4 | Permanent identity | Workbook assigns UIDs after duplicate verification; Amazon mints none; R01 is not a family UID | Resolved, applied |
| U5 | Workflow execution | Auto Run or Monitor Run selected at startup | Resolved, applied |
| U6 | Execution provenance | Identify Amazon, not its underlying reasoner | Resolved, applied |

## What remains open for implementation
- None of U1–U6. The remaining implementation inputs are per-run, not decisions: the first original document to process, and the execution mode (`AUTO` or `MONITOR`) the operator selects when starting the agent. The exact folder names/paths inside Spaces or My Files are supplied at invocation by the workflow; the skills require them but do not invent them.
- The dry run in Quick stays paused until the operator says resume. These skill files are not a live run.
