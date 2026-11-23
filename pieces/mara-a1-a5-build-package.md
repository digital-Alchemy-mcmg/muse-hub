# MARA Flow A — A1 to A5 Build Package
Date: 2026-11-23
From: Muse 1, operating on behalf of the operator, SXV8
Source: MARA A-B-C Collection Inventory 2026-11-23, stage machine board checked live 2026-11-23, A-Scout query to Muse 2, A-Scout Gradio frame walk 2026-11-23.
Status: stage definitions and contracts built and committed. Execution is NOT complete — see Blockers at the end. No listing has been run through A1-A5 yet.

## What Flow A must do, as one run

One position in at A1. One feed out at A5, ready for B1, the workbook door. No envelope.

## A1 — Look for the position
- Inputs: what you are looking for, where to look.
- Outputs: a position worth chasing.
- Allowed: job listings and boards only.
- Intake fields, in order: NAICS industry (exact code, dropdown), SOC code (exact code, dropdown), zip code (5 digits, starts blank), max miles (slider 0-100), min run (1-100), max run (1-100, min cannot be above max).
- Gate: frame refuses to build or confirm without NAICS, SOC, and zip. Frame refuses a code not in the lookup.
- Built: Gradio frame covers A1 intake, verified in Meta's frame walk 2026-11-23: A1 covered for frame scope. Frame writes the query JSON with current_station A1, next_station A2, route A1 through A5. Frame does not itself fetch listings — that belongs to the A1 agent.

## A2 — Break the position up
- Inputs: a found position listing.
- Outputs: the position broken into its pieces — duties, requirements, must-haves, pieces B will need.
- Allowed: the listing itself, no guessing missing details.
- Codes: SOC / NAICS codes label each piece, exact code only, snapped to the lookup, so every piece can be tracked from Scout all the way through B.
- Built: position-level codes only. Frame walk 2026-11-23: A2 partial. The frame gives the position-level NAICS and SOC codes. It does not split a listing into duties / requirements / must-haves, and it does not label each piece separately.
- Still to build: a listing breaker that takes the A1 listing as its only input, splits it into named pieces, applies the exact codes per piece, and passes the piece list to A3 with nothing invented and nothing missing filled in.

## A3 — Sort the pieces
- Inputs: position pieces from A2.
- Outputs: pieces in working order.
- Allowed: sort and label only, do not build yet.
- Built: none. Board shows A3 empty. Frame walk: gap, correctly shown as gap.
- Still to build: a piece list coming in from A2, a tappable sort / order control for those pieces, a tappable label control, a read-only ordered output. Still no build action at A3.

## A4 — Get it ready
- Inputs: sorted position pieces.
- Outputs: a position ready to feed to B.
- Allowed: prepare only, hand nothing off until it is ready.
- Built: none. Board shows A4 empty. Frame walk: gap, correctly shown as gap.
- Still to build: a readiness checklist and gate — checked, complete, and in the shape B expects through the workbook door — that blocks the handoff until it passes. The frame's NAICS/SOC/zip gate is not an A4 readiness gate.

## A5 — Feed to B
- Inputs: a position ready from A4.
- Outputs: a feed ready for B1, the workbook door.
- Allowed: feed to B only, no building here, no envelope needed.
- Built: none as a feed. The old Traveling Envelope is flagged no longer needed and is not used. Frame walk: gap, direct feed not built. Frame sends to A1, not to B.
- Still to build: a direct A-to-B feed that takes the ready position from A4, writes the B1 feed in the workbook-door shape, and hands it to B1 with no envelope.

## Code sources — pointers, not ingestion
- Starter: scout-taxonomy-lookup.xlsx, Drive ID 1adc1Nu8hisZsMIjF1d4CFFZXNDeYkdtEV_B8Y7l4mc8. Tabs NAICS_Lookup (48 codes), SOC_Lookup (63 codes). Verified 2026-11-23, sha256 05e06107a6cec21602b575f20f5e1e4538d64e620d79755dabbf22ca51e48b82.
- NAICS full book: 2022_NAICS_Manual.pdf, Drive ID 1pAD3Qk258n7pjyCP5u4CfgkiMlZEGfyy. Script out NAICS at 2-digit sector and 6-digit level only. Do NOT ingest whole.
- SOC structure: soc-structure-2018.xlsx, Drive ID 1Ln0qZbiDIff1qXT533X_fHZTt1UtNl09, 1,447 codes.
- SOC definitions: soc-2018-definitions.xlsx, Drive ID 1L4tb02G8wzoYLUiI92EUDEjHv5hjyEcD, 1,452 rows.
- Code is the join key. No fuzzy word search.

## Query template
See a-scout-query-template.json in the same commit. All slots start empty. No job, no code, and no zip are invented in the template. The template is filled at run time by the operator.

## Blockers — what would unblock execution
1. A live run input from the operator: NAICS, SOC, zip, max/min run. No position has been given yet, so no listing can be broken up, sorted, readied, or fed.
2. Meta's frame file a_scout_frame.py, in hand here. The frame walk was reported, but the file itself was not in this workspace at check time.
3. Muse 2's A-Scout query execution, from the hub pointer reply 2026-11-23. Muse 2 will verify tabs/counts and build from the files once they are in hand.

## Completion check — Flow A
- A1: done for frame scope. Intake built, JSON out.
- A2: partial. Position-level codes done, listing breaker not built.
- A3: not done. Gap, correctly shown.
- A4: not done. Gap, correctly shown.
- A5: not done. Direct feed not built.
