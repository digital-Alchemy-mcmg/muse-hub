---
name: sdna-set-twin-down
description: "Place one completed atomic-twin .txt file and its JSON completion receipt in the Amazon document repository, verify both can be read back there, and stop. In Monitor Run, present the pair for inspection and save only on explicit operator authorization."
---

# sdna-set-twin-down

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 2 and 4, plus the operator's U1–U6 resolutions of the same day. This skill is self-contained: it needs only this skill, the completed atomic-twin `.txt` file and its JSON completion receipt, and the destination and execution mode supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

## Inputs

- The completed atomic-twin `.txt` file, supplied at invocation.
- Its separate JSON completion receipt, supplied at invocation.
- The destination, supplied at invocation: the Amazon document repository (Spaces or My Files, as supplied), with two separate folders — one for original source documents, one for completed atomic twins. The twin and receipt go in the completed-twins folder.
- The original source document's location, supplied at invocation, in the originals folder.
- The execution mode, supplied at invocation: `AUTO` or `MONITOR`. The operator selects the mode when starting the agent.
- The source reference, original filename, available binding identifier, shared completion-record identifier, and atom count, as stated in the two items supplied.

If any of these is missing, incomplete, or marked failed, stop and report what is missing. Do not place a partial pair. A failed source produces nothing to place under this skill.

If no destination or no execution mode is supplied at invocation, report a hold and name what is missing. Do not invent a destination, a folder, a storage location, or a naming convention. Do not place the pair anywhere on an assumed destination.

## Procedure

1. Compare the two items supplied: source reference and filename, file and receipt versions, completion-record identifier, and atom count must match across both. A mismatch stops the run; report the mismatch and do not place the pair.
2. Confirm the pairing: the original document filename and the available binding identifier, where one exists, link the original in the originals folder to the twin in the completed-twins folder. Record that pairing in the handoff so the relationship is preserved for workbook registration. If no binding identifier exists, record it as not available; do not invent one.
3. Place the pair according to the execution mode:
   - `AUTO`: save the atomic-twin `.txt` file and its JSON receipt together in the completed-twins folder, using the twin filename as supplied.
   - `MONITOR`: present the pair for inspection first. Save them in the completed-twins folder only on explicit operator authorization supplied for this run. Without that authorization, hold and do not save.
   In either mode, do not convert either item into a spreadsheet, a sheet export, or any other format while placing it. Do not add spreadsheet structure, frozen rows, protected ranges, or validation rules.
4. Confirm both items can be reopened and read back in full at their actual destination, with the intended identities. Record the destination, names, locations, pairing, and execution mode in the handoff.
5. Stop after successful set-down. This skill's job is done when the pair is placed and verified readable at its destination. This skill assigns no permanent identity: the completion-record identifier in the pair is not a permanent document-family UID, and no permanent family or blurb UID is minted here. Permanent identity is assigned only by the workbook, after registration.

Source reading, decomposition, counting, and validation are identical in `AUTO` and `MONITOR`. Full-fidelity processing cannot be bypassed in either mode. The modes differ only in authorization to save the completed outputs, not in the underlying processing.

## Output and check

Return the placed locations and `SET_DOWN` only with observed read-back of both items at the destination; otherwise return `HOLD` and the missing action, missing destination, missing mode, missing authorization, or mismatch.

Test one item supplied without its partner: no done status is returned and no placement is made. Test with no destination supplied: the run holds and names the missing destination, and nothing is placed. Test `MONITOR` without operator authorization: the pair is presented for inspection, nothing is saved, and the run holds.
