---
name: sdna-write-decomposition-receipt
description: "Produce the separate completion receipt for one completed atomic-twin document: what was examined, how many atoms were produced, and what remains ambiguous, conflicting, or unsupported."
---

# sdna-write-decomposition-receipt

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 2, 3 and 4, plus the operator's U1–U6 resolutions of the same day. This skill is self-contained: it needs only this skill, the completed atomic-twin `.txt` file, and the decomposition record supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

This receipt is retained as a separate completion record accompanying the atomic-twin file, in the existing 16-field JSON structure, R01–R16. Do not invent or replace that schema. It records decomposition activity only. It is not an admission of evidence and not a verification of truth.

## Inputs

- The completed atomic-twin `.txt` file supplied at invocation.
- The decomposition record supplied at invocation: source identity, regions examined, atoms produced, unresolved ambiguities, conflicting statements, unsupported extraction attempts, and unreliable regions.
- The completion-record identifier supplied at invocation, shared with the atomic-twin file. If none is supplied, do not invent one; report it as missing input and stop. The completion-record identifier is a completion record only. It is not a permanent document-family UID and must not be treated as one.

If the supplied file or record is incomplete, marked failed, or missing required elements, stop and report the missing or incomplete input. Do not produce a partial receipt. A failed source produces a failure notification, not a receipt, and this skill is not invoked for a failed source.

## Procedure

Produce one separate completion receipt, as a JSON file, for the one atomic-twin `.txt` file supplied. Count atoms from the file itself and regions from the decomposition record supplied. Use the same completion-record identifier as the file. The executing agent that generates this receipt is Amazon.

**Empty value rule:** no value = `null`; an empty list = `[]`.

The receipt must contain all of the following elements:

| # | Element | Type | Required | Rule |
|---|---|---|---|---|
| R01 | Completion-record identifier | text | Yes | Shared with the atomic-twin file; a completion record only, never a permanent family UID |
| R02 | Receipt version | text | Yes | `SDNA_DECOMP_RECEIPT_V1` |
| R03 | Document version | text | Yes | The atomic-twin file version |
| R04 | Source reference | text | Yes | As in the file |
| R05 | Source filename | text | Yes | As in the file |
| R06 | Interpreter ID | text | Yes | `Amazon` — the executing agent that performed the workflow |
| R07 | Interpreter version | text or `null` | Yes | A version only if supplied at invocation; if none is supplied, `null`. Do not substitute a model name or model version, and do not invent missing reasoner or interpreter metadata. |
| R08 | Processing timestamp | text (ISO 8601) | Yes | — |
| R09 | Source regions examined | integer ≥ 0 | Yes | Count from the decomposition record supplied |
| R10 | Atoms produced | integer ≥ 0 | Yes | Equals the atom count of the document supplied |
| R11 | Unresolved ambiguities | list of local atom IDs | Yes; may be `[]` | Every ID must exist in the document |
| R12 | Conflicting source statements | list of local atom IDs | Yes; may be `[]` | Every ID must exist in the document |
| R13 | Unsupported extraction attempts | list of `{region_ref, reason}` | Yes; may be `[]` | These have no atom and no atom ID |
| R14 | Unreliable regions | list of region references | Yes; must be `[]` | See below |
| R15 | Coverage status | text | Yes | `COMPLETE` only; see below |
| R16 | Coverage limitations | text or `null` | Yes | `null`; see below |

Derive the ambiguity and conflict IDs from the decomposition record, and recheck that each one exists in the document supplied.

**Coverage under full fidelity:** a receipt exists only for a source that passed the full-fidelity check in full. Any unreadable, missing, inaccessible, or truncated region would have stopped the run before any file or receipt was produced, and would have produced a failure notification instead. Therefore every receipt produced under this skill has R14 empty, R15 `COMPLETE`, and R16 `null`. A `PARTIAL` receipt is not produced. If the decomposition record supplied shows any unreliable region or incomplete coverage, stop and report the inconsistency; do not produce the receipt.

The receipt is a JSON file with the sixteen elements above. No replacement format is used.

## Output and check

Return the separate JSON completion receipt and confirm it against the file: identifiers R01–R05 match the file; R06 is `Amazon`; R10 equals the file's atom count; R11–R12 refer only to atom IDs present in the file; R14 is empty, R15 is `COMPLETE`, and R16 is `null`.

Test with a document whose decomposition record lists an ambiguous atom and a conflicting pair: both IDs appear in R11 and R12 and exist in the document. Test with a decomposition record showing an unreliable region: the run stops and no receipt is produced.

When the receipt is complete and verified, this skill's job is done. Stop here.
