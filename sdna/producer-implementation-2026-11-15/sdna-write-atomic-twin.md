---
name: sdna-write-atomic-twin
description: "Produce the atomic twin as a plain-text .txt file from organized decomposition material: manifest front matter, alphabetically labeled sections, employment and job groupings, and individually numbered atomic blurbs with full provenance."
---

# sdna-write-atomic-twin

**Revision:** Amazon producer, 2026-11-15. Implements operator Decisions 2 and 4, plus the operator's U1–U6 resolutions of the same day. This skill is self-contained: it needs only this skill and the organized decomposition material supplied at invocation. It does not require knowledge of any other skill, any later processing, or the wider system.

This skill produces a plain-text `.txt` file, not a spreadsheet. The spreadsheet dataframe requirement came from instructions adapted for a different tool, to prevent that tool producing large blocks of unstructured prose. It does not govern this workflow. No information is discarded simply because the physical output format changes.

## Inputs

- Organized decomposition material supplied at invocation: source identity, subject (name and contact information as captured), section map with alphabetical labels, per-section atom counts and overall count, and ordered atoms grouped by section, each with its section, precise source location, supporting quotation, proposition, classification, employer or entity, role or position, date or period text, support status, and duplicate/conflict references.
- Processing date and time, supplied at invocation.
- Available document or binding identifier, if one exists. If none exists, record it as not available; do not invent one.
- If a completion-record identifier is supplied at invocation, carry it unchanged with the document. If none is supplied, do not invent one; report it as missing input and stop. The completion-record identifier is a completion record only. It is not a permanent document-family UID and must not be presented as one.

If the supplied material is incomplete, marked failed, or missing required elements, stop and report the missing or incomplete input. Do not produce a partial document. A failed source produces no document under this skill.

## Filename

Name the file `LastName.FirstName.SDNA.txt`, using the subject's name exactly as stated in the source. If the last name or first name is not available as stated, do not invent it and do not guess a filename from another name in the source; report the missing naming input and hold.

## Procedure

Produce one plain-text `.txt` file containing every atom from the supplied material, in original document order, grouped by section in the section map's order. The file has three parts: manifest front matter, document body, footer. No unnecessary formatting or metadata beyond what this section names.

### Manifest front matter

- Candidate name, as stated in the source.
- Processing date and time.
- Original document filename.
- Available document or binding identifier, or not available where none exists.
- Executing agent: `Amazon`.
- Necessary pairing metadata: source reference and completion-record identifier, so the twin can be paired with its original document.

Do not record a reasoner, interpreter, model name, or model version in the manifest. The executing agent is Amazon; the manifest identifies who performed the workflow, not the underlying reasoner or interpreter. Do not invent missing reasoner or interpreter metadata.

### Document body

- Original section sequence, in the section map's order.
- Sections labeled alphabetically: A for the first section in original order, B for the second, and so on, using the labels in the supplied section map. Headings are shown exactly as written.
- Employment and job groupings: within each section, atoms are grouped by the employer or entity and role or position as stated in the source. Grouping follows what the source states; no employment or job grouping is invented, and original document order is preserved within each group.
- Individually numbered atomic blurbs starting at 01. Each blurb is numbered by its local atom ID: blurb 01 is local atom ID `001`, blurb 02 is `002`, and so on. The body number and the local atom ID are the same number; no second numbering system is created.
- Preserve source wording, quotations, and source-location references needed for binding, for every blurb.

**Empty value rule:** a blank means "not stated in the source". The date or period text for an atom is never blank: it is given as written, or `UNSPECIFIED`.

Each blurb in the body must carry all of the following content, individually identifiable for that blurb. Elements 01–04 and 21 live in the manifest front matter and apply to every blurb; elements 05–20 and 22 live with the blurb in the body.

| # | Content element | Required | Rule |
|---|---|---|---|
| 01 | Document version | Yes | `SDNA_ATOMIC_TWIN_V1`; same for every blurb |
| 02 | Source reference | Yes | The source reference supplied at invocation; same for every blurb |
| 03 | Source filename | Yes | Same for every blurb |
| 04 | Subject | Yes | The subject whose evidence this is; source-grounded; never taken from incidental mentions of others |
| 05 | Local atom ID | Yes | As supplied; unique; compared as numbers; order = document order |
| 06 | Source section | Yes, if identifiable | Heading as written, with its alphabetical label |
| 07 | Source location | Yes | Most precise locator available |
| 08 | Source quotation | Conditional | Exact source text. If blank: the blurb's support status is `REVIEW_REQUIRED` and its ambiguity note states the limitation. |
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
| 21 | Completion-record identifier | Yes, if supplied | Same for every blurb; a completion record only, never a permanent family UID |
| 22 | Taxonomy status | Yes | `SUPPLIED` / `PROVISIONAL`; set per blurb |

These are content elements in the plain-text file, not spreadsheet columns. Do not convert the file into a spreadsheet, a row-per-atom table for a spreadsheet, or a sheet export. Do not add spreadsheet headers, frozen rows, protected ranges, or validation rules.

Duplicate and conflict references are review observations, not permanent links between blurbs. No permanent document-family UID and no permanent blurb UID is minted in this file. Permanent identity is assigned only by the workbook, after registration.

Keep local IDs as text so leading zeros survive. Resolve references only after all IDs are present. Cross-references refer only to IDs in this file. Keep the exact quotation distinct from the proposition and its semantic ceiling.

If a passage was locatable but provides no quotable text, keep the blurb: quotation blank, support status `REVIEW_REQUIRED`, ambiguity note stating the limitation. If a proposed claim has no identifiable supporting passage, it has no blurb in the supplied material and none is created here.

### Footer

- Total atomic blurb count.
- SHA-256 integrity hash of the manifest front matter and document body as written, excluding the footer hash line itself. Compute the hash after the manifest and body are complete, then write the footer.

## Output and check

Return the completed `.txt` file and its blurb count. The blurb count must equal the overall count in the supplied material; a mismatch stops the run.

Read the file back in full and verify: the filename follows `LastName.FirstName.SDNA.txt`; the manifest carries the candidate name, processing date and time, original filename, available binding identifier or not available, executing agent `Amazon`, and pairing metadata; every blurb from the supplied material is present, in original document order, grouped by alphabetically labeled section and by stated employment or job; every blurb carries all its required content elements; shared elements are identical on every blurb; all duplicate and conflict references name blurbs present in this file; the footer total matches the blurb count; the footer hash matches a fresh hash of the manifest and body. A preview or acceptance that does not include a readable file is not a completed file.

Test a blank quotation with a defensible locator, a missing date, and a reference to a later local atom. Expect `REVIEW_REQUIRED`, `UNSPECIFIED`, and an intact text ID respectively. Test incomplete supplied material: the run stops and no partial file is produced.

When the file is complete and verified readable, this skill's job is done. Stop here. This skill does not save the file to its destination; saving is a separate step, controlled by the execution mode supplied there.
