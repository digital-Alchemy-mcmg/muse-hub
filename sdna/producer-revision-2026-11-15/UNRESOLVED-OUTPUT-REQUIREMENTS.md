# Unresolved output-format requirements — Four producer skills — 2026-11-15

These are genuinely missing requirements found during the revision. No replacement was invented for any of them. Each needs an operator decision before the revised skills can be loaded and run end to end.

## U1 — Atomic-twin document format
- Question: what is the physical format of the Amazon atomic-twin document? (File type, document structure, how the 22 content elements per atom are laid out in the document.)
- Status: not established in any material inspected. The spec defines a 22-column dataframe; Decision 2 removes that requirement without naming the replacement.
- Impact: `sdna-write-atomic-twin` defines *what* each atom must contain and in what order, and states that presentation is the document-generation workflow's. It cannot by itself tell an agent what file to create.
- Needed: operator to name the document format and, if there is one, the template or layout rule.

## U2 — Destination and naming for the placed pair
- Question: where do the completed atomic-twin document and its completion receipt go, and under what naming convention?
- Status: not established for the Amazon workflow. The original destination (Google Sheet in `02_ATOMIC_TWINS`) was removed by Decision 2 as an obsolete export instruction. No replacement destination is named in the directive or in the materials inspected.
- Impact: `sdna-set-twin-down` holds and places nothing when no destination is supplied, by design. Until U2 is decided, every set-down run will hold.
- Needed: operator to name the destination (space / folder / location as the workflow understands it) and the naming convention.

## U3 — Completion-receipt physical format
- Question: is the separate completion receipt still a `.json` file (spec D.2), or is it a document in the same Amazon document workflow as the twin?
- Status: the receipt is retained as a separate completion record (the package's first-cut success evidence is a paired twin + receipt export), and its 16 content elements are preserved. Its file format is not decided in the directive.
- Impact: `sdna-write-decomposition-receipt` records the 16 elements and flags the format as missing when none is supplied at invocation, rather than inventing one.
- Needed: operator to confirm JSON, document, or another format — and, if JSON, to confirm the 16 keys keep their R01–R16 names.

## U4 — Completion-record identifier allocation
- Question: who supplies the shared completion-record identifier (the value formerly field 21 / R01), and when is it allocated?
- Status: the original skill required "the shared decomposition receipt ID allocated for this generation by the workflow" and stopped if unassigned. That allocation step still has no named owner in the Amazon workflow.
- Impact: twin and receipt skills both stop if no identifier is supplied. Until U4 is decided, runs will stop at that input check.
- Needed: operator to name who allocates the identifier and at which workflow stage.

## U5 — Document-generation workflow binding
- Question: how does the Amazon workflow construct the atomic-twin document, and how does it invoke these four skills (in what order, with what inputs passed between them)?
- Status: Decision 2 states Amazon "uses its document-generation workflow to construct the atomic-twin document", but no workflow definition, stage binding, or input-passing rule for these skills was supplied in the directive or found in the materials inspected.
- Impact: the skills are written to accept their inputs "as supplied at invocation" and to stop when a required input is missing. That is correct per Decision 4, but it means the end-to-end sequence cannot be run until the workflow supplies those inputs.
- Needed: operator / workflow builder to define the invocation sequence and the artifact passed at each step. This is workflow work, not a change to any individual skill.

## U6 — Interpreter identity for the receipt (R06/R07)
- Question: what values go in the receipt's interpreter ID and version?
- Status: the spec leaves these as supplied values. No Amazon value was established.
- Impact: minor; the receipt skill stops if they are not supplied at invocation.
- Needed: operator to name the interpreter ID/version to record, or to confirm they are supplied by the workflow at invocation.

## What is NOT unresolved
- Whether a receipt is retained: yes — paired twin + receipt is the package's first-cut success evidence.
- Whether PARTIAL output survives: no — Decision 3 removes it; every receipt is COMPLETE with R14 empty and R16 null.
- Whether the 22 twin elements and 16 receipt elements are preserved: yes — all preserved as content, in the revised skills.
- Whether the six downstream skills change: no — untouched in this revision. If a format conflict is later found in one of them (for example, a downstream skill expecting a Sheets dataframe), it must be documented as a specific conflict under the directive's Revision Scope, not resolved by weakening these four decisions.
