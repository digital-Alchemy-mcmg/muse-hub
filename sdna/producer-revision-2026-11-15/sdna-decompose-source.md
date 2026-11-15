---
name: sdna-decompose-source
description: "Turn one original document into organized, section-grouped evidence atoms with source provenance and counts. Scan the whole document first, organize it by section, then decompose it. Stops completely if the document cannot be read in full."
---

# sdna-decompose-source

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 1, 3 and 4. This skill is self-contained: it needs only this skill and the one original document supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

## Inputs

- One original document, supplied at invocation. This is the only source for this run.
- If a source reference, filename, or subject identifier is supplied at invocation, use it unchanged. If none is supplied, use what the source itself states.
- If a classification list (taxonomy) is supplied at invocation, use it. If none is supplied, use a provisional label per atom and mark it provisional.

A material ambiguity in these inputs stops the run before decomposition. Ask for the missing input; do not guess it.

## Gate 0 — Full-fidelity acceptance

Before any scanning, organizing, or decomposition, establish that the complete original document can be read faithfully.

Read the whole document end to end for this check. The check fails if any part cannot be read faithfully, including:

- Unreadable pages.
- Missing pages.
- Inaccessible sections.
- Truncated content.
- Unreadable source regions.
- Any other condition preventing a complete, faithful read.

When the check fails:

1. Stop the entire run.
2. Do not extract readable portions.
3. Do not produce partial atoms.
4. Do not produce a partial output of any kind.
5. Flag the failure.
6. Notify the operator.
7. Identify the affected page, section, or region, where possible.
8. Explain what prevented full-fidelity processing.

The only output of a failed run is that failure notification. A failed source produces a failure notification, not a partial deliverable. The operator must correct or replace the original document and submit it again. Do not interpret, reconstruct, compensate for, or accept incomplete source material.

A compound assertion in a fully readable document is not a source failure. It is decomposed normally in Phase 3.

## Procedure — in this order

Do not skip a phase, reorder the phases, or begin a later phase before the earlier one is complete.

### PHASE 1 — Full document scan

Before extracting or counting individual atoms, scan the original document to establish its identity and structure.

Capture, as stated in the source:

- The subject's name.
- Contact information present in the source.
- The number of sections.
- Original section headings, preserving their wording.
- Original document order.
- The document's overall structure and identifiable regions.

Record missing information as unknown. Never invent missing metadata.

Do not extract, count, or assign atoms in this phase.

### PHASE 2 — Section organization

Establish the document's organizational structure before decomposition begins.

- Establish section groupings.
- Preserve original headings.
- Establish stable source-location references for each section and region.
- Keep unidentified or unheaded regions identifiable without inventing headings: an unheaded region is listed by its stable location reference and its start/end locators only, with no invented heading.

Record a section map, one entry per section, in original order. Each entry records: sequence number, heading exactly as written (or no heading, marked as unheaded), start locator, end locator, and stable region reference. No invented section labels are used.

Do not begin assigning atoms to groups before this structural pass is complete.

### PHASE 3 — Decomposition and counting

Once the section structure is established:

- Extract independently meaningful, evidence-supported assertions, one atom per assertion.
- Split compound assertions without losing their meaning. Keep qualifiers, quantities, units, and negation.
- Keep names, dates, employers, titles, quantities, and technologies as stated. A responsibility never becomes an accomplishment.
- Record the strongest directly supported claim, and no more. Participation is not leadership; familiarity is not expertise.
- Keep stated dates. Use `UNSPECIFIED` when none is stated. Do not infer continuity.
- Assign source-local atom IDs in original document order. IDs are unique within this run, start at `001`, and continue in document order (`001`–`999`, then `1000`+). Use IDs as text so leading zeros survive.
- Associate every atom with its proper section and its most precise source location.
- Count the atoms within each section.
- Calculate the overall atom count. Per-section counts must sum to the total; a mismatch stops the run until it is reconciled.
- Preserve repetitions, contradictions, ambiguities, and source limitations. Keep both sides of a contradiction and reference each other; do not reconcile them. Keep duplicates and reference each other; do not delete them.
- Classify each atom using the supplied classification list where available; otherwise use a provisional label and mark it provisional.

The section structure determines where the atoms belong. The decomposition determines what the atoms contain. Do not allow extraction to destroy the original document's organizational context. Every atom keeps its section, its heading as written, and its most precise location.

Keep four things separate for every atom: the original wording, the supporting quotation, the atomic proposition, and any interpretation. Never merge them.

If a passage can be located but provides no quotable text, keep the atom, leave the quotation blank, mark the atom as needing review, and note the limitation. If a proposed claim has no identifiable supporting passage, do not create an atom for it; record it as an unsupported extraction attempt, with its region reference and reason, and no atom ID.

### PHASE 4 — Organized output

Return structured decomposition material with clear section boundaries, individual atoms, source provenance, and counts, so the next operation does not have to reconstruct the original document's organization.

The output contains:

- Source identity: source reference and filename as supplied or as stated in the source.
- Subject: the subject's name and contact information as captured in Phase 1, or unknown where the source does not state it.
- Section map: how many sections were identified, what each section is called (heading exactly as written, or unheaded), and where each section begins and ends.
- Per-section atom counts, and the overall atom count.
- Ordered atoms grouped by section, in original document order within each section. For each atom: its source-local ID, section, most precise source location, supporting quotation where the source provides one, atomic proposition, classification and whether it is provisional, date or period text (`UNSPECIFIED` when none is stated), support status (`SOURCE_SUPPORTED_PROPOSED` or `REVIEW_REQUIRED`), and any duplicate or conflict references to other atom IDs in this run.
- Region ledger: for each region, its examined status, its proposed atom IDs, and any unsupported attempts, with reasons.
- Review list: regions and assertions that require review, including atoms whose quotation is blank and atoms that exceed the strongest directly supported claim (mark those `REVIEW_REQUIRED`).
- Unsupported extraction attempts: region reference and reason for each, with no atom ID.

No atom is ever marked as verified by this skill. The only support statuses are `SOURCE_SUPPORTED_PROPOSED` and `REVIEW_REQUIRED`.

## Isolation

Process one original only in one run. No other sources, conversations, general knowledge, or candidates.

| Input | Expected result |
|---|---|
| Two original documents in one invocation | STOP |
| Two originals in separate invocations | Process independently |
| One original with an unreadable page | STOP |
| One original with missing content | STOP |
| One fully readable original with compound assertions | PROCEED |

Do not confuse the multiple-source isolation test with the incomplete-source test. They are separate stops with separate causes.

## Output and check

Before returning the output, check: the section count matches the section map; every atom carries a section and a precise location; per-section counts sum to the total; every duplicate and conflict reference names an atom ID that exists in this run; no atom is marked verified; no partial output is returned from a failed fidelity check.

Test with two originals, as two separate isolated runs, one source at a time — never two sources processed together — and with a document containing a compound assertion and a fully readable document with an ambiguous claim. The first stops on isolation; the second yields separately traceable atoms. Test the scan-first order on a multi-section original: the section map and per-section counts must be complete before any atom is assigned to a section. Test the fidelity gate on an original with one unreadable page: the run stops, no atoms are produced, and the notification names the affected page.
