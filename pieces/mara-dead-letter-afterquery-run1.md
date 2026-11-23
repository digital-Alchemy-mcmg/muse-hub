# MARA DEAD LETTER — AfterQuery, Run 1 — REJECT / OUT_OF_SCOPE
Date: 2026-11-23. Decision: REJECT, ERR_A_OUT_OF_SCOPE, citing SF-002.
Job: AfterQuery Experts — AI / ML Engineer — AI Trainer.
Run 1 disk: primary SOC 43-9021, NAICS 518210, zip 48393, min 5 / max 15.
job_uuid: 0b8c9669-a911-51e6-9ed5-0b0667806fed (uuid5, company + title + search URL — see note below)
run_id: RUN1-518210-43-9021-48393-2026-11-23
original_content_sha256: 2575a1a7c666f35c027f271756f3ac5a750bc5107cc9e79a70528b07d3822cb0 (sha256 of verbatim raw_posting, 1,954 chars, extracted from ~/workspace/user/files/indeed-ai-assisted-jobs-novi-mi-2026-11-23.md, section 1 only)
dedupe_sha256: 4cb3c1be1f77400474d88311b7fce556692de7088fc57e4350fbe3c9ccdcf66b (sha256 of company + title + URL)

## Why rejected
- P1–P6 map to SOC 15-1299 (systems/ML engineering), not Run 1 primary SOC 43-9021 (Data Entry Keyers). SF-002.
- Run 1 primary stays at 43-9021. No separate 15-1299 disk has been Operator-approved.
- A5 RELEASE is prohibited: unresolved SF-002, missing raw bytes/hash at dispatch time, SOC collision. No deposit into `to seg B`.
- A3–A5 dispatch commit 4dfc20b4 is HALTED / RECALLED — it was dispatched using P1–P9 while SF-002 was still open, without verbatim raw_posting.

## Note on canonical URL
- No job-specific canonical URL was in the source file. The URL used for dedupe / uuid5 is the Indeed search URL from the source file. That makes job_uuid provisional on that key — if a job-specific canonical URL is supplied, re-mint job_uuid and re-run dedupe, and log the change here, do not silently overwrite this record.

## What was NOT done
- No sealed A-envelope was minted for AfterQuery under Run 1. Sealing requires an authorized disk; Run 1 is not authorized for 15-1299.
- No B4 truth adjudication, no B5 Prism scoring. B1–B3 work in the audit is provisional diagnostic only, not certified: Boundary B gate HARD STOP, 0/9 spans verified, B2 provisional unfrozen, B3 3 UNBOUND (a.1, b.1, b.2) / 3 transferable proposals (a.2, a.3, b.3) / 3 unmarked context (c.1–c.3).
- If the Operator opens a separate 15-1299 disk, AfterQuery can be re-ingested under that disk with this same raw_posting, hash, and job_uuid — do not re-extract from P1–P9.
