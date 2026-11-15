---
name: sdna-set-twin-down
description: "Place one completed atomic-twin document and its completion receipt at the destination supplied at invocation, verify both can be read back there, and stop."
---

# sdna-set-twin-down

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 2 and 4. This skill is self-contained: it needs only this skill, the completed atomic-twin document and its completion receipt, and the destination supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

## Inputs

- The completed atomic-twin document, supplied at invocation.
- Its separate completion receipt, supplied at invocation.
- The destination for the pair, supplied at invocation, including the naming to use.
- The source reference, filename, shared completion-record identifier, and atom count, as stated in the two items supplied.

If any of these is missing, incomplete, or marked failed, stop and report what is missing. Do not place a partial pair. A failed source produces nothing to place under this skill.

If no destination is supplied at invocation, report a hold and name the missing destination. Do not invent a destination, a folder, a storage location, or a naming convention. Do not place the pair anywhere on an assumed destination.

## Procedure

1. Compare the two items supplied: source reference and filename, document and receipt versions, completion-record identifier, and atom count must match across both. A mismatch stops the run; report the mismatch and do not place the pair.
2. Place the atomic-twin document and its completion receipt together at the destination supplied at invocation, using the naming supplied at invocation. Do not convert either item into a spreadsheet, a sheet export, or any other format while placing it. Do not add spreadsheet structure, frozen rows, protected ranges, or validation rules.
3. Confirm both items can be reopened and read back in full at their actual destination, with the intended identities. Record the destination, names, and locations in the handoff.
4. Stop after successful set-down. This skill's job is done when the pair is placed and verified readable at its destination.

## Output and check

Return the placed locations and `SET_DOWN` only with observed read-back of both items at the destination; otherwise return `HOLD` and the missing action, missing destination, or mismatch.

Test one item supplied without its partner: no done status is returned and no placement is made. Test with no destination supplied: the run holds and names the missing destination, and nothing is placed.
