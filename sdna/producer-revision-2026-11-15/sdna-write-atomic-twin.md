---
name: sdna-write-atomic-twin
description: "Produce the atomic-twin document from organized decomposition material: one individually identifiable evidence atom per assertion, in original document order, grouped by section, with full provenance."
---

# sdna-write-atomic-twin

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 2 and 4. This skill is self-contained: it needs only this skill and the organized decomposition material supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

This skill produces a document artifact, not a spreadsheet. The spreadsheet dataframe requirement came from instructions adapted for a different tool, to prevent that tool producing large blocks of unstructured prose. It does not govern this workflow. The document-generation workflow supplied at invocation constructs the document; this skill defines what evidence the document must contain, in what order, and how each atom must be identifiable. No information is discarded simply because the physical output format changes.

## Inputs

- Organized decomposition material supplied at invocation: source identity, subject, section map, per-section atom counts and overall count, and ordered atoms grouped by section, each with its section, precise source location, supporting quotation, proposition, classification, date or period text, support status, and duplicate/conflict references.
- If a completion-record identifier is supplied at invocation, carry it unchanged with the document. If none is supplied, do not invent one; report it as missing input and stop.

If the supplied material is incomplete, marked failed, or missing required elements, stop and report the missing or incomplete input. Do not produce a partial document. A failed source produces no document under this skill.

## Procedure

Produce one atomic-twin document containing every atom from the supplied material, in original document order, grouped by section in the section map's order.

**Empty value rule:** a blank means "not stated in the source". The date or period text for an atom is never blank: it is given as written, or `UNSPECIFIED`.

Each atom in the document must carry all of the following content, individually identifiable for that atom:

| # | Content element | Required | Rule |
|---|---|---|---|
| 01 | Document version | Yes | `SDNA_ATOMIC_TWIN_V1`; same for every atom |
| 02 | Source reference | Yes | The source reference supplied at invocation; same for every atom |
| 03 | Source filename | Yes | Same for every atom |
| 04 | Subject | Yes | The subject whose evidence this is; source-grounded; never taken from incidental mentions of others |
| 05 | Local atom ID | Yes | As supplied; unique; compared as numbers; order = document order |
| 06 | Source section | Yes, if identifiable | Heading as written |
| 07 | Source location | Yes | Most precise locator available |
| 08 | Source quotation | Conditional | Exact source text. If blank: the atom's support status is `REVIEW_REQUIRED` and its ambiguity note states the limitation. |
| 09 | Atomic proposition | Yes | One proposition; qualifiers, quantities, units, and negation kept |
| 10 | Source category | Yes, if identifiable | Source-level label, not a system plane |
| 11 | Provisional domain | Yes | Plane name when the taxonomy status is supplied; descriptive label when provisional |
| 12 | Employer or entity | When stated | — |
| 13 | Role or position | When stated | Stated titles only. Example: a floor manager who bartended is not given the title "Bartender". |
| 14 | Date or period text | Yes | As written, or `UNSPECIFIED` |
| 15 | Source context | When needed | Attribution, qualifiers, negation, action + inseparable outcome |
| 16 | Support status | Yes | `SOURCE_SUPPORTED_PROPOSED` / `REVIEW_REQUIRED` |
| 17 | Semantic ceiling | Yes | The strongest directly supported claim, and no more |
| 18 | Ambiguity note | Conditional | Required when the source quotation is blank |
| 19 | Duplicate reference | When applicable | Existing local atom IDs in this document, separated by `;`; no self-reference |
| 20 | Conflict reference | When applicable | Same as element 19 |
| 21 | Completion-record identifier | Yes, if supplied | Same for every atom |
| 22 | Taxonomy status | Yes | `SUPPLIED` / `PROVISIONAL`; set per atom |

These are content elements in the document, not spreadsheet columns. Their presentation order and layout in the document are determined by the document-generation workflow supplied at invocation, not by this skill. Do not convert the document into a spreadsheet, a row-per-atom table for a spreadsheet, or a sheet export. Do not add spreadsheet headers, frozen rows, protected ranges, or validation rules.

Duplicate and conflict references are review observations, not permanent links between atoms.

Keep local IDs as text so leading zeros survive. Resolve references only after all IDs are present. Cross-references refer only to IDs in this document. Keep the exact quotation distinct from the proposition and its semantic ceiling.

If a passage was locatable but provides no quotable text, keep the atom: quotation blank, support status `REVIEW_REQUIRED`, ambiguity note stating the limitation. If a proposed claim has no identifiable supporting passage, it has no atom in the supplied material and none is created here.

## Output and check

Return the completed atomic-twin document and its atom count. The atom count must equal the overall count in the supplied material; a mismatch stops the run.

Read the document back in full and verify: every atom from the supplied material is present, in original document order, grouped by section; every atom carries all its required content elements; shared elements (document version, source reference, source filename, subject, completion-record identifier) are identical on every atom; all duplicate and conflict references name atoms present in this document. A preview or acceptance that does not include a readable document is not a completed document.

Test a blank quotation with a defensible locator, a missing date, and a reference to a later local atom. Expect `REVIEW_REQUIRED`, `UNSPECIFIED`, and an intact text ID respectively. Test incomplete supplied material: the run stops and no partial document is produced.

When the document is complete and verified readable, this skill's job is done. Stop here.
