# MARA B4–B5 — Advance Plumbing, Data Entry Specialist - eCommerce — B4 FAIL, B5 REFRACTED
Date: 2026-11-23. job_uuid: 1ba7f305-aaad-520b-b1d0-6512785cfce3. run_id: RUN1-518210-43-9021-48393-2026-11-23.
Source: B1–B3 file MARA-B1-B3-Advance-Plumbing-Run1-2026-11-23.md (18/18 spans verified; B3 proposals only).
Envelope in `to seg B`: https://drive.google.com/file/d/11_JnuxEu3sSVfLU1s0J687vzLH97hoRW/view?usp=drivesdk
Sidecar: https://drive.google.com/file/d/1_Yle3P_oQBpnSV2J1IToMJP2ffXhuDHt/view?usp=drivesdk

## B4 — Gate / Truth Adjudication: FAIL
Rule: every hard-gate node (`*`) must be bound to pass B4 as written. Soft nodes (`≈`) and unmarked context do not block.
| Addr | Force | B3 proposal | B4 verdict |
|---|---|---|---|
| a.1 | * | PR-SERL-001, WH-MCMG-002, WH-GATS-001 (transferable) | PASS — bound, medium confidence (no explicit e-commerce storefront admin atom) |
| a.2 | * | PR-SERL-001, PR-BOBC-001 (transferable) | PASS — bound, medium (no product-page Excel template atom) |
| a.3 | * | UNBOUND — no Walmart/eBay/multi-channel atoms | FAIL — hard gate with no evidence |
| a.4 | * | TC-DEV-001, PR-DRCH-001, PR-SERL-001, WH-MCMG-002 | PASS — bound, medium |
| a.5 | ≈ | PR-SERL-001, PR-TWIN-001 | PASS — soft, bound |
| a.6 | ≈ | PR-TWIN-001, WH-STAP-001 | PASS — soft, bound |
| b.1 | * | PR-SERL-001 only (partial); Power Query, Power BI, pivot tables unattested | FAIL — hard gate, partial only |
| b.2 | ≈ | UNBOUND — no Rithum/Shopify/Unilog/BigCommerce atoms | GAP — soft, does not block, recorded |
| b.3 | * | WH-STAP-001, WH-BOBC-001, WH-BOBC-002, WH-GATS-001, PR-BOBC-001 (inventory branch) | PASS — bound, medium |
| b.4 | ≈ | UNBOUND — no plumbing/home improvement/construction atoms | GAP — soft, does not block, recorded |
| b.5 | * | ED-OCC-001, WH-PAN-001, WH-TWIN-004, WH-PAT-001 | PASS — bound, medium (duplicate of c.3 flagged) |
| b.6 | * | PR-SERL-001, PR-MARA-001, WH-MCMG-002, ED-OU-001 | PASS — bound, medium |
| c.1 | ≈ | WH-TWIN-003, RF-TWIN-001 | PASS — soft, bound |
| c.2 | ≈ | WH-TWIN-001, WH-BOBC-001, WH-STAP-001, RF-TWIN-001 | PASS — soft, bound |
| c.3 | ≈ | Same atoms as b.5 | PASS — soft, bound (duplicate flagged) |
| c.4 | ≈ | WH-TWIN-001, WH-STAP-001, WH-PAN-001 | PASS — soft, bound |
| d.1–d.2 | unmarked | Context only, ID-002 | PASS — context |

Hard gates: 6 of 8 pass. Failures: a.3, b.1. **B4 verdict: FAIL — does not pass as written.** No certified B4 package, no handoff to seg C.

## B5 — Prism Refraction
What survives to C (if B4 is ever re-ruled or the job is re-run with a ruling on the two failures):
- Strongest angle: spreadsheet / data automation — a.1, a.2, a.4, b.6, backed by PR-SERL-001, PR-MARA-001, TC-DEV-001.
- Second angle: inventory / product data — b.3, backed by WH-STAP-001, WH-BOBC-001/002, WH-GATS-001, PR-BOBC-001.
- Supporting angle: communication, organisation, customer service — b.5/b.6, c.1–c.4.
What does NOT survive: a.3 marketplace listing management (no evidence), b.1 Excel tool stack as written (Power Query / Power BI / pivots unattested — claim spreadsheet automation only, not the named tools), b.2 platform tools (no evidence), b.4 plumbing/construction familiarity (no evidence).
Confidence: no node scores high — all bound nodes are transferable, medium at best; b.1 is low-medium (partial). Nothing here is an exact-phrase match.

## What B4/B5 leaves open (operator rulings needed, not assumed)
1. a.3: does a transferable inventory/data argument close a hard gate, or does the gate stay failed?
2. b.1: does PR-SERL-001 spreadsheet automation close the Excel hard gate, or must Power Query / Power BI / pivots be attested?
Until ruled, this job stays at B4 FAIL with no C handoff.
