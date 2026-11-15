# Validation addendum — U1–U6 — 2026-11-15

Method: each revised skill was checked against the U1–U6 resolutions by reading the revised text. No skill was loaded into Quick, executed, or tested against a live document in this revision; live execution tests are listed as remaining work in each skill's own test section and are not claimed here. Base-package validation (Decisions 1–4, 10 checks) still stands except where a resolution supersedes it — noted below.

## sdna-decompose-source
| Resolution | Result | Evidence |
|---|---|---|
| U1 alphabetical labels | PASS | Section map entries carry A, B, C in original order; headings unchanged. Supersedes base "no A–Z labels" restriction. |
| U1 employment/job groupings | PASS | Phase 3 keeps employer/entity + role with each atom for grouping as stated; no grouping invented. |
| U4 no permanent identity | PASS | Local IDs only; no family/blurb UID minted; no permanent family UID for a run stopping before registration. |
| U2/U3/U5/U6 | N/A | Storage, receipt format, execution mode, and execution identity are not this skill's outputs. |

## sdna-write-atomic-twin
| Resolution | Result | Evidence |
|---|---|---|
| U1 `.txt` + filename | PASS | Plain-text `.txt`; `LastName.FirstName.SDNA.txt` from name as stated; missing name parts → hold, do not invent. |
| U1 manifest | PASS | Candidate name, processing date/time, original filename, binding ID or not available, executing agent `Amazon`, pairing metadata. |
| U1 body | PASS | Original section sequence, alphabetical labels from section map, employment/job groupings as stated, blurbs numbered from 01 by local atom ID, source wording/quotations/locations preserved. |
| U1 footer | PASS | Total blurb count + SHA-256 of manifest + body excluding the footer hash line. |
| U1 22 elements preserved | PASS | All 22 content elements present, mapped to manifest (01–04, 21) and body (05–20, 22). |
| U4 R01 not family UID | PASS | Completion-record identifier stated as completion record only; no permanent UID minted in the file. |
| U6 Amazon identity | PASS | Manifest records `Amazon`; no reasoner/model name; no invented interpreter metadata. |
| U5 saving | PASS | Skill states it does not save; saving is the set-down step controlled by mode. |

## sdna-write-decomposition-receipt
| Resolution | Result | Evidence |
|---|---|---|
| U3 JSON R01–R16 | PASS | JSON file, 16 elements, keys unchanged, schema not replaced. |
| U3 failed fidelity | PASS | Failure notification, not a receipt; skill not invoked for a failed source. |
| U3 Amazon generates | PASS | Executing agent Amazon generates the receipt. |
| U4 R01 not family UID | PASS | R01 stated as completion record only, never a permanent family UID. |
| U6 R06/R07 | PASS | R06 `Amazon`; R07 version only if supplied, else `null`; no model name/version substituted, no invention. |
| U1/U2/U5 | N/A | Twin format, storage, and execution mode are not this skill's outputs. |

## sdna-set-twin-down
| Resolution | Result | Evidence |
|---|---|---|
| U2 repository + folders | PASS | Amazon repository (Spaces/My Files as supplied), separate originals and completed-twins folders; twin + receipt together in completed-twins folder. |
| U2 pairing | PASS | Original filename + binding ID link original to twin; pairing recorded in handoff for workbook registration. |
| U4 no permanent identity | PASS | Assigns none; completion-record identifier is not a family UID. |
| U5 AUTO | PASS | Mode supplied at invocation; AUTO saves automatically after validation. |
| U5 MONITOR | PASS | Presents pair for inspection; saves only on explicit operator authorization for that run; without it, hold and do not save. |
| U5 shared requirements | PASS | Identical processing in both modes; full-fidelity cannot be bypassed; neither mode assigns permanent identifiers; modes differ only in save authorization. |
| U1/U3/U6 | N/A | Twin format, receipt schema, and execution identity are produced by the earlier skills; this skill preserves the pair as supplied. |

## Cross-skill checks
- U4 across the sequence: no skill mints a permanent UID; local IDs flow from decompose → twin (blurb numbers = local IDs) → receipt (R11/R12 reference local IDs) → set-down (pairing recorded, no UID assigned). Permanent identity can only come from workbook registration after set-down, which no skill in this package performs.
- U6 across the sequence: `Amazon` is the only executing-agent identity in the twin manifest and the receipt (R06); no skill records a model name or version, and R07 is `null` unless a version is supplied at invocation.
- U5 across the sequence: twin and receipt skills produce outputs without saving; set-down is the only skill that saves, and only under the supplied mode.
- Not validated here: live Quick invocation, the exact Spaces/My Files folder names (supplied at invocation), the first original document, and the operator's mode selection for the first run.
