# MARA Flow A — A2-A5 Build Spec
Date: 2026-11-23. Author: Muse 1, operating on behalf of the operator SXV8.
Source: stage machine board (checked live 2026-11-23), A-B-C Collection Inventory 2026-11-23, Meta A-Scout Gradio frame walk (A1 covered, A2 partial, A3 gap, A4 gap, A5 gap).
Status: spec built, execution not complete. No station is claimed done until it runs on a live listing and its output is read back.

## Test inputs in hand (committed to hub main, e6b9c903)
- Run 1 — AI Training, Data Annotation & Rater Work: NAICS 518210 (starter lookup, verified), SOC 43-9021 (full SOC books, verified, not in starter), zip 48393, max miles 20.
- Run 2 — Public Advocacy, Campaign Organizing & Rally Support: NAICS 813940 (not in starter — script from 2022 NAICS Manual), SOC 21-1093 (starter lookup, verified), zip 48393, max miles 20.
- Missing, still needed from the operator: min run and max run for both runs. Left null in the query files. Do not invent them.

## A2 — Break the position up (partial, Meta frame does not cover)
Contract from the board: in = a found listing; out = the position broken into its pieces; allowed = the listing itself, no guessing missing details.
Build:
1. Listing input — a real listing text/URL, not a position-level code summary.
2. Splitter — duties, requirements, must-haves, nice-to-haves, each as a separate piece with the exact source line kept.
3. Piece-level code labelling — each piece carries the position NAICS/SOC codes, and where a piece maps to a different code, that code is labelled per piece, exact code only, snapped on the code, no fuzzy word search.
4. Missing-detail flag — any piece the listing does not supply is flagged missing, never invented.
Acceptance: a Run 1 listing broken into labelled pieces, each piece traceable to one exact listing line, missing pieces flagged, not filled.

## A3 — Sort the pieces (gap)
Contract: in = pieces from A2; out = pieces in working order; allowed = sort and label only, do not build yet.
Build:
1. Sort control over A2 pieces — order by gate order (hard gates first, then soft), not by dropdown list order.
2. Label control — each piece labelled by type (duty / requirement / must-have / nice-to-have) and by gate weight.
3. No building here — no tree, no resume, no B work inside A3.
Acceptance: Run 1 pieces returned in a stated working order, with labels, and the order is reproducible from the same input.

## A4 — Get it ready (gap)
Contract: in = sorted pieces; out = a position ready to feed to B; allowed = prepare only, hand nothing off until ready.
Build:
1. Readiness checklist — every piece sorted and labelled, codes exact, missing pieces flagged, zip / max miles / min-max run present, anti-pattern collected if the operator asked for it.
2. Gate — the position does not leave A4 until every checklist item passes or is explicitly flagged. The A1 NAICS/SOC/zip gate is not an A4 gate.
3. Ready output — one ready-position package in the A-Scout query shape, with station_contracts for A1-A4 attached.
Acceptance: a Run 1 ready package that passes the checklist, or a named list of what fails it — no silent pass.

## A5 — Feed to B (gap, no envelope)
Contract: in = a ready position from A4; out = a feed ready for B1, the workbook door; allowed = feed to B only, no building here, no envelope needed.
Build:
1. Direct feed — ready position goes to B1 in workbook-door shape. The old Traveling Envelope route is not used.
2. Feed output — JSON to B1, not to `scout_a_output` alone. Must name the B1 door it enters and the workbook it feeds.
3. Handoff receipt — B1 confirms receipt, or the feed is marked unreceived, not assumed delivered.
Acceptance: a Run 1 ready package delivered to B1 with a receipt, or a named failure at the door.

## What is NOT in this spec
- No new NAICS/SOC codes invented. Codes not in the starter lookup are scripted from the full books at implementation, per the standing ruling — whole books are not ingested.
- No central-command design. That design is held until the operator releases it; nothing here is built around it.
- No listing fetch at A1. The Gradio frame does not fetch listings; A2 takes a listing the operator or Muse 2 supplies.
