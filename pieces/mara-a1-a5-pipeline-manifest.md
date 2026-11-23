# MARA A1-A5 Pipeline Manifest — Building in the Hub
Date: 2026-11-23. Orchestrator: Muse 1 (digital-Alchemy-mcmg), operating on behalf of the operator SXV8.
Repo: digital-Alchemy-mcmg/muse-hub, branch main. All pipeline work lives here, in `pieces/` and in `MUSE-TO-MUSE.md`.
Stop gate: A5. No Flow B work until the Operator releases the next flow.

## Roster
- Orchestrator: Muse 1 — dispatch, polling, Friction Log, main commits after Worker ready signals.
- Worker: Muse 2 (metconmg / Calico) — A1 + A2.
- Worker: Muse 3 (sxv8hq / Reddington) — A3 + A4 + A5.
- Verifier: none staffed — verification reverts to the Operator.

## Pipeline — one long throughout run
| Station | Owner | In | Out | Status 2026-11-23 ~06:34 EST |
|---|---|---|---|---|
| A1 Look for the position | Muse 2 | NAICS + SOC + zip + max/min run + max miles | Query JSON, route A1-A5 | Dispatched, in progress. Run 1 + Run 2 codes verified by Muse 1. Min/max run still missing — leave null, do not invent. |
| A2 Break the position up | Muse 2 | A real listing | Pieces, each labelled with exact code, traced to one exact listing line, missing flagged | Dispatched, in progress. Needs a live listing — none in hand yet. |
| A3 Sort the pieces | Muse 3 | A2 pieces | Pieces in working order, labelled hard gates first | Dispatched, waiting on A2 pieces. |
| A4 Get it ready | Muse 3 | Sorted pieces | Ready position, readiness checklist passed or failures named | Dispatched, waiting on A3. |
| A5 Feed to B | Muse 3 | Ready position | Feed to B1, workbook door, with receipt | Dispatched, waiting on A4. STOP at this gate. |

## Test runs in hand
- Run 1 — AI Training: NAICS 518210, SOC 43-9021, zip 48393, max miles 20, min run 5, max run 15 (operator, 2026-11-23 ~06:36 EST).
- Run 2 — Public Advocacy: NAICS 813940, SOC 21-1093, zip 48393, max miles 20, min run 5, max run 15 (operator, 2026-11-23 ~06:36 EST).
- Alternatives: NAICS 541690, SOC 15-1299 (Run 1); NAICS 813319, SOC 13-1161 (Run 2).

## Files in the hub, for the Workers
- `pieces/mara-a1-a5-build-package.md` — Flow A stage definitions/contracts.
- `pieces/a-scout-query-template.json` — query template, all slots empty.
- `pieces/a-scout-run1-ai-training-48393.json` / `pieces/a-scout-run2-public-advocacy-48393.json` — Run 1 / Run 2 queries.
- `pieces/mara-a2-a5-build-spec.md` — A2-A5 build spec with acceptance per station.
- `pieces/NAICS_Lookup.csv` (48 codes) / `pieces/SOC_Lookup.csv` (63 codes) — starter lookup, converted from scout-taxonomy-lookup.xlsx (sha256 05e06107a6cec21602b575f20f5e1e4538d64e620d79755dabbf22ca51e48b82). This answers Muse 2's share ask of 2026-11-23 ~05:55 EST: the lookup is now in the hub, reachable by both Workers. Full SOC books (1,447 / 1,452 rows) remain in Drive by ID — script out only needed codes, do not ingest whole books.
- Muse 2's agent spreadsheet workbook (14 sheets, retrieval + verification per plane, Initial-Prompts) is the door into B1 and the runner/retrieval instructions — use it, do not rebuild it.

## Rules the Workers must confirm in their own hub section, next polling cycle
1. Restate your job in your own words.
2. State what files are in hand, and what is still missing, by name.
3. State your task branch name.
4. Report progress / blockers / ready signals here, every 30 minutes. No relay through the Operator.
5. Out-of-scope: STOP and emit a `[SCOPE-FLAG]` to the Orchestrator. No silent improvisation.
6. When ready: tell the Orchestrator here with files + commit SHA. The Orchestrator makes the main commit.

## Open blockers (Orchestrator-held)
- Min run / max run — RESOLVED 2026-11-23 ~06:36 EST: min 5, max 15, both runs.
- One live listing for A2 — not in hand yet.
- Muse 3 polling confirmation — not yet seen in its hub section as of 2026-11-23 ~06:34 EST.
