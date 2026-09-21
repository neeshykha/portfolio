# Project State — Shipped Apps Portfolio

**Read this first in any new session (including Ship Sunday runs).** It is the continuity file: current status, queue, and operating rules. Update it every session alongside LEARNING-LOG.md.

**State repo: `neeshykha/portfolio`** (moved from peptide-evidence on 2026-09-14; the copies there are pointer stubs).

## Mission

Aneesh has 17+ production AI automations but nothing public. Every unit of work moves something closer to a URL a recruiter can click. "Done" = live and linkable, never "works on my machine."

## Operating rules

1. Web-first for portfolio pieces. No installs, no Mac apps for public work.
2. 3:1 public-to-personal project ratio.
3. Static-first, backend only when genuinely needed (and then it's a portfolio story).
4. Every session ends with something deployed — live and verified, not just deployable.
5. Append to LEARNING-LOG.md every session: date, shipped, learned, next.
6. Metric that matters: live URLs, not sessions held.
7. Every new live tool gets a card on the hub landing page (`index.html` in this repo) in the same run that ships it.

## Idea pipeline scope (set 2026-08-11)

Work-side: tool building, MCPs, web tools useful in IoT or similar environments — not just support-AI. Personal side: health, gardening, peptides, functional medicine research, tennis, economics, current events, home improvement, exercise, investing. Claude justifies picks; Aneesh vetoes.

## Portfolio queue

| # | Project | Status | Notes |
|---|---------|--------|-------|
| 0 | portfolio hub | **LIVE 2026-09-14** — https://neeshykha.github.io/portfolio/ | Repo `neeshykha/portfolio`: landing page (11 projects in three sections: AI deployment and measurement, support ops tools, outside work), README, and these state files. Rebuilt on the first Claude Code run because the 2026-08-16 bundle was never found locally. That bundle's `specs/kb-health-checker-spec.md` was lost with it and was not recreated. |
| 1 | peptide-evidence | **LIVE** — https://neeshykha.github.io/peptide-evidence/ | 4/43 records published. Record batches are **attended only**: source retrieval needs judgment, and the dataset lives in `~/Documents/ShipSunday/`, which scheduled runs can read but not write. |
| 2 | KB health checker | **LIVE 2026-08-23** — https://neeshykha.github.io/kb-health-checker/ (flagship, "Start here" on the hub) | v1 paste-mode, pure client-side. v2 = URL-fetch mode on Vercel + serverless (CORS). The old hub-bundle rubric spec is gone; write a fresh one as the first step of v2 if it's needed. |
| 3 | MQD calculator ("MQD Runway") | **LIVE 2026-09-14** — https://neeshykha.github.io/mqd-calculator/ | Repo `neeshykha/mqd-calculator`, Pages main/root, About set. Rules encoded as editable data (Sept 2026 snapshot: 5k/10k/15k/28k thresholds, unchanged for 2027 per Dec-2025 Delta announcement; Headstart $2,500/card; Boost $10 Reserve / $20 Platinum). Fixed a "-0 MQD" display bug on exact tier ties before publishing. Audience play (r/delta, FlyerTalk) not done yet; Aneesh's call. |
| 3.5 | scheduled-agent-detector | **LIVE 2026-09-20** — https://neeshykha.github.io/scheduled-agent-detector/ | Friday build, shipped by the Sunday finishing lane. Pages serves from **main / `/docs`**, not root, because the page is `docs/index.html`; the repo README links the bare URL, so `/docs` is the correct source path. Hub card is in the measurement section. |
| 4 | HVAC export cleaner | **Next — unattended OK** (personal slot) | Drag-drop CSV cleaner: port the `hvac-csv-cleaner` skill's rules to browser JS, and build in `~/ship-sunday/deploy/hvac-export-cleaner/`. **Guardrail:** the real exports are iApartments work telemetry, so the public repo gets synthetic sample data only, with no real exports, hub IDs, or property or company names. Load the rules through the `hvac-csv-cleaner` skill; if a scheduled run can't load it, stop and mark this attended only. |
| 5 | KB checker v2 (URL mode) | Queued — **attended only** | Needs Vercel + a serverless function (CORS). As of 2026-09-14 the Vercel CLI isn't installed and no account is linked on the Mac; set that up in an attended session first. |

## Settled decisions — don't re-open these

Aneesh has already ruled on these. Re-proposing them wastes his time.

- **scheduled-agent-detector's demo page keeps its real task IDs** (2026-09-20). Seven names on that page (`daily-job-pipeline`, `filter-domain-paste`, `habit-nagger`, `inbox-junk-sweep`, `morning-brief`, `shelf-audit`, `weekly-podcast-digest`) are exact matches to enabled tasks on this Mac, plus near-matches (`daily-garden-check`, `morning-stand-test`, `old-rainfall-report`, `weekly-people-pick`); only the files and mtimes are synthetic. Raised with him, and **his call was to leave them.** No company names, customers, or credentials are involved. Don't "scrub" this in a later run.
- **The paused Cowork "Ship Sunday" task stays** (2026-09-20). A paused task costs nothing and there's no downside to it sitting there. Stop suggesting the deletion.

## Environment facts (save future sessions the discovery cost)

- **Ship Sunday runs in Claude Code on Aneesh's Mac** (migrated from Cowork cloud runs 2026-09-14). Not the worker node: its reaper kills headless sessions at 900 s, and it's the work machine. Kit lives at `~/ship-sunday/` (`bin/publish.sh`, `RUN-PROMPT.md`, `deploy/<repo>/` build folders); skill at `~/.claude/skills/ship-sunday/`. Runs have full git push, `gh`, full web access, and the local ShipSunday folder.
- GitHub account: **neeshykha**. `gh` is authenticated with SSH as its git protocol. The hub lists every public repo worth citing.
- **Git on the Mac is 2.9.0** (`/usr/local/bin/git`). It has no `git init -b`, so `publish.sh` uses `git init` + `git symbolic-ref HEAD refs/heads/main`. **Push over SSH** (`git@github.com:neeshykha/<repo>.git`): no HTTPS credential helper is configured, so HTTPS pushes fail.
- GitHub Pages pattern: deploy-from-branch, main / root. `~/ship-sunday/bin/publish.sh <repo> <dir> "<description>"` does repo-create → push → Pages API → About in one idempotent command; if it fails partway, fix and re-run it. Verify live with `~/ship-sunday/bin/verify_live.sh <repo>` (retries up to 3 min; first builds took 30 s to 2 min).
- **Not every Friday build serves from the repo root.** `enable_pages.sh` now takes an optional source path: `enable_pages.sh <repo> /docs` for a build whose page is `docs/index.html` (scheduled-agent-detector). Check where the page actually lives before enabling — main/root on a docs-rooted repo still returns 200 at `/docs/` and still looks like a successful run, while the URL the repo's README advertises stays dead.
- **The hub is the superset, and `portfolio_projects.md` has to follow it.** Every repo with a hub card needs a citation entry in `/Users/aneesh/Documents/resume_project/portfolio_projects.md`. Three were missing as of 2026-09-20 (kb-health-checker, mqd-calculator, peptide-evidence) because the 9-14 hub rebuild added cards for repos the Friday routine never touched. Check the full card list against that file's `##` headings every run, not just the repo shipped that day.
- Peptide dataset source of truth: the **ShipSunday project folder** on Aneesh's Mac (as of 2026-08-23, `~/Documents/ShipSunday/` — the folder name is the durable handle, not the path; it has moved before). Publish only index + compounds/ — `working/` stays private. Scrub vendor names before publishing; the dataset index carried vendor references that were neutralized in the published copy.
- State-file continuity: this repo must receive the updated copies (commit + push every run), or the next run re-discovers everything. Local working copies live in `~/ship-sunday/deploy/<repo>` (`publish.sh` turns each build folder into a checkout); this repo's is `~/ship-sunday/deploy/portfolio`, so pull it before reading state.
- Legacy (Cowork cloud, pre-migration): sandbox GitHub proxy was repo-scoped — read-only clones only, push 403, no repo creation (re-confirmed 2026-09-13); scheduled runs had no WebFetch/browser/device bridge; workaround was staged files + manual `/upload/main` steps or Claude-in-Chrome automation in attended sessions.

## Routine

**Ship Sunday** — weekly, Sundays 10:00 AM ET, in Claude Code on Aneesh's Mac (the `ship-sunday` skill, interactively or as a scheduled task). Each run: pull this repo, read this file + LEARNING-LOG.md, deliver the next increment, publish + verify live, add it to the hub, append a log entry, update this file, push.
