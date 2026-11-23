# MARA A1 Verification — Run 1 and Run 2
Date: 2026-11-23. Verified by: Muse 1, Orchestrator, operating on behalf of the operator SXV8.
Source files: scout-taxonomy-lookup.xlsx (sha256 05e06107a6cec21602b575f20f5e1e4538d64e620d79755dabbf22ca51e48b82), soc-structure-2018.xlsx (1,447 codes), soc-2018-definitions.xlsx (1,452 rows).
Status: A1 verification complete for both runs. A2 still needs one live listing — none in hand yet.

## Run 1 — AI Training, Data Annotation & Rater Work
- NAICS 518210 — Computing Infrastructure Providers, Data Processing, Web Hosting, and Related Services — VERIFIED in starter lookup NAICS_Lookup (48 codes).
- SOC 43-9021 — Data Entry Keyers — VERIFIED in full SOC books (structure + definitions), NOT in starter SOC_Lookup (63 codes).
- Alternatives (not the primary codes): NAICS 541690, SOC 15-1299 — both VERIFIED in full books, NOT in starter.
- Zip 48393 — 5 digits, valid format.
- Max miles 20. Min run 5. Max run 15 (operator, 2026-11-23 ~06:36 EST).
- Query JSON: pieces/a-scout-run1-ai-training-48393.json — route A1-A5, current_station A1, next_station A2.

## Run 2 — Public Advocacy, Campaign Organizing & Rally Support
- NAICS 813940 — Political Organizations — NOT in starter lookup (48 codes). To be scripted from 2022 NAICS Manual at implementation, per ruling — do not ingest whole manual.
- SOC 21-1093 — Social and Human Service Assistants — VERIFIED in starter lookup SOC_Lookup and in full SOC books.
- Alternatives (not the primary codes): NAICS 813319, SOC 13-1161 — SOC 13-1161 VERIFIED in full SOC books.
- Zip 48393 — 5 digits, valid format.
- Max miles 20. Min run 5. Max run 15 (operator, 2026-11-23 ~06:36 EST).
- Query JSON: pieces/a-scout-run2-public-advocacy-48393.json — route A1-A5, current_station A1, next_station A2.

## A1 acceptance — passed
- Every primary code is an exact code, snapped on the code, no fuzzy word search.
- Zip is 5 digits. Max miles, min run, max run are all present.
- No code was invented. Codes not in the starter were flagged, not filled from memory.

## Next station
- A2 (Muse 2, Worker): take a real listing for Run 1 first, split into duties / requirements / must-haves, each piece labelled with its exact code, traced to one exact listing line, missing details flagged, never invented. BLOCKED on a live listing — awaiting the Operator.
