# Change report addendum — U1–U6 resolutions applied — 2026-11-15

Base package: `~/workspace/sdna-atrium/producer-revision-2026-11-15/` (Four Decisions, Decisions 1–4). This folder, `producer-implementation-2026-11-15/`, applies the operator's Consolidated Conflict Resolutions U1–U6 to the same four skills. The base package is preserved as-is; this folder is the implementation version.

## Per-skill changes

### sdna-decompose-source.md
- Section map entries now carry an alphabetical label (A = first section in original order, B = second, and so on). Headings unchanged. This supersedes the base package's "no A–Z labels" restriction, which rested on neither the directive nor the spec naming them; U1 now names them.
- Phase 3 now keeps employer/entity and role/position with each atom so the twin can group by employment/job as stated.
- Phase 4 output now includes the alphabetical label per section.
- Added U4 boundary: local IDs only; no permanent family or blurb UID is minted here; no permanent family UID is assigned to a run stopping before workbook registration.
- Nothing else changed: Gate 0 full-fidelity, Phases 1–4 order, counts, isolation tests unchanged.

### sdna-write-atomic-twin.md
- Output is now a plain-text `.txt` file (U1), replacing the generic "document artifact" of the base package. Filename `LastName.FirstName.SDNA.txt` from the subject name as stated; missing name parts → hold, do not invent.
- New three-part structure: manifest front matter (candidate name, processing date/time, original filename, available binding ID or not available, executing agent `Amazon`, pairing metadata), document body (original section sequence, alphabetically labeled sections, employment/job groupings as stated, blurbs numbered from 01 by local atom ID), footer (total blurb count + SHA-256 hash of manifest + body, excluding the footer hash line).
- The 22 content elements are preserved in full, mapped to manifest (01–04, 21) and body (05–20, 22). No element dropped for the format change.
- Added U4/U6 boundaries: completion-record identifier is a completion record only, never a permanent family UID; no permanent UID minted in the file; manifest records `Amazon` only, no reasoner/model name, no invented interpreter metadata.
- Added closing line: this skill does not save the file; saving is the set-down step, controlled by execution mode (U5).

### sdna-write-decomposition-receipt.md
- Format confirmed as JSON, R01–R16, keys unchanged, schema not replaced (U3).
- R06 is now `Amazon` (U6). R07 is a version only if supplied at invocation, otherwise `null`; no model name/version substituted, no invented interpreter metadata (U6, governed deviation from the spec table's "Yes" for R07).
- R01 now explicitly a completion record only, never a permanent family UID (U4).
- Failed fidelity now explicitly produces a failure notification, not a receipt (U3).
- Nothing else changed: R14 `[]`, R15 `COMPLETE`, R16 `null` on every receipt; input validation unchanged.

### sdna-set-twin-down.md
- Destination is now the Amazon document repository (Spaces or My Files, as supplied), with two separate folders — originals and completed twins (U2). Twin `.txt` + receipt `.json` placed together in the completed-twins folder.
- Pairing step added: original filename + available binding identifier link original to twin; pairing recorded in the handoff for workbook registration (U2, U4).
- Execution mode added (U5): `AUTO` or `MONITOR` supplied at invocation. AUTO saves automatically; MONITOR presents for inspection and saves only on explicit operator authorization for that run; without it, hold and do not save.
- Added U4 boundary: assigns no permanent identity; completion-record identifier is not a family UID.
- Nothing else changed: match check, read-back verification, stop condition unchanged.

## Governed deltas vs the spec (additions to the base package's D-1–D-7)
| # | Spec point | Implementation | Authority |
|---|---|---|---|
| D-8 | M01.D.1 twin as 22-column dataframe | Plain-text `.txt`, manifest/body/footer per U1; 22 elements preserved as content | U1 + Decision 2 |
| D-9 | M01.D.2 receipt R06 interpreter ID / R07 version | R06 `Amazon`; R07 version only if supplied, else `null`, no invention | U6 |
| D-10 | M01.D.2 R01 = field 21 | R01 is a completion-record identifier only, never a permanent family UID | U4 |
| D-11 | M01.E twin as Google Sheet in `02_ATOMIC_TWINS` | Twin `.txt` + receipt `.json` in Amazon repository, separate originals / completed-twins folders | U2 |
| D-12 | (no spec execution-mode concept) | `AUTO` / `MONITOR` mode supplied at invocation; MONITOR saves only on explicit operator authorization | U5 |

## Files in this folder
- `sdna-decompose-source.md`, `sdna-write-atomic-twin.md`, `sdna-write-decomposition-receipt.md`, `sdna-set-twin-down.md` — revised with U1–U6 applied
- `ARCHITECTURE-ADDENDUM-SKILLS-AS-TASK-INSTRUCTIONS.md` — unchanged copy from the base package
- `RESOLUTIONS-U1-U6-APPLIED.md` — per-resolution register and where each is implemented
- `CHANGE-REPORT-ADDENDUM-U1-U6.md` — this file
- `VALIDATION-ADDENDUM-U1-U6.md` — per-skill validation for U1–U6
- `PACKAGE-MANIFEST.json` — hashes for this folder

The base package's `CHANGE-REPORT.md`, `VALIDATION.md`, and `UNRESOLVED-OUTPUT-REQUIREMENTS.md` are superseded by this folder for U1–U6 (the unresolved file's six items are all resolved here) and are not copied into it. The six downstream skills remain untouched.
