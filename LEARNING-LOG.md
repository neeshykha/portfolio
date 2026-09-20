# Learning Log — Shipped Apps Project

Every session appends: date, what shipped, what was learned, what's next. This is data, not bookkeeping.

---

## Entry #1 — 2026-08-11

**Shipped:** `peptide-evidence` — first live public URL of the project.
Repo: https://github.com/neeshykha/peptide-evidence · Site: https://neeshykha.github.io/peptide-evidence/
Published the evidence-brief index + 4 compound records (BPC-157, ipamorelin, PT-141, tesamorelin) with vendor references neutralized and internal `working/` files kept private.

**Decisions made this session:**
- Audited all four candidates. Sequence locked: peptide site (today) → **KB health checker as flagship** (multi-session, Vercel + serverless) → MQD calculator (audience play) → HVAC cleaner (personal slot).
- Routine: **Ship Sunday** — weekly scheduled task that picks up state from this repo and delivers the next increment.
- Idea pipeline broadened beyond support-AI: work-side = tool building, MCPs, IoT-adjacent web tools; personal side = health, gardening, peptides/functional medicine, tennis, economics, current events, home improvement, exercise, investing.

**Learned (deployment track):**
- **A repo is a publishing pipeline, not just backup.** GitHub Pages turns any repo with an `index.html` into a website: Settings → Pages → deploy from branch → main/root. Zero config, zero build step, free hosting at `<user>.github.io/<repo>/`.
- **Static-first architecture.** This site is pure HTML with inline CSS — no build, no dependencies, nothing to break. That's why deployment took one session. The KB checker will need a serverless function (browsers can't fetch cross-origin pages — CORS), which is why it goes on Vercel.
- **Public repo hygiene:** publish the polished artifact, keep working notes private; scrub vendor/personal references before anything goes recruiter-facing; the README is part of the portfolio piece — it explains the *system*, not just the files.
- Constraint discovered: the Cowork cloud sandbox's GitHub proxy is repo-scoped and can't create repos or push to unattached ones. Workaround that works end-to-end: browser automation (repo creation, uploads, Pages config) with files staged through the session outputs folder. Ship Sunday runs will use this same path until a cleaner auth route exists.

**Next increment:** Add remaining compound records in batches (39 to go — each batch is a content update that auto-deploys on commit, reinforcing the git→live pipeline). In parallel, first KB-checker session: spec the grading rubric and scaffold the Vercel project.

## Entry #2 — 2026-08-16 (summary; full entry in the unpublished hub bundle)

**Shipped (pending publish):** Portfolio hub bundle for a new `neeshykha/portfolio` repo — landing page, README, migrated state files, and `specs/kb-health-checker-spec.md`. Delivered to Aneesh with 2-minute manual publish steps; **as of 2026-08-23 the repo does not exist yet**, so the bundle is still sitting in that session's deliverables. Until it's published, scheduled runs fall back to reading state from `peptide-evidence` — which is why this summary entry exists here.

---

## Entry #3 — 2026-08-23

**Shipped:** **KB Health Checker v1** — the flagship (queue #2) is now built and deploy-ready as a pure client-side app.
Deliverables staged: `kb-health-checker/index.html` + `README.md`. Target: new repo `neeshykha/kb-health-checker` → GitHub Pages.

Paste a help-center article (HTML or plain text) → AI-readiness grade across 5 weighted categories (structure/chunkability 25%, answer clarity 25%, self-containment 20%, machine readability 15%, language quality 15%), with per-finding "why this matters for retrieval" explanations and concrete fixes. Built-in good/bad example articles demonstrate the rubric. Verified in headless Chromium: good sample grades 100/A, bad sample 45/F, zero console errors.

**Key scope decision:** v1 is *paste-mode*, which needs no serverless function — CORS only blocks *fetching other sites' pages*, not analyzing pasted content. That unblocked shipping the flagship from a scheduled run (no browser, no WebFetch, no deploys available) and turns the Vercel + serverless work into a clean v2 increment (URL mode: paste a help-center link, grade every article) instead of a prerequisite. Lesson: **when a project's hard dependency only blocks part of the value, ship the unblocked part first.**

**Career-signal note:** the README frames the tool as encoded production diagnostic knowledge ("the copilot gave a wrong answer and the root cause was the content, not the model") — Framework #1 (SME First, Then Encode) made concrete and clickable.

**Learned (environment):** scheduled Ship Sunday runs can *author and verify* (Playwright + bundled Chromium works headlessly for smoke tests) but cannot deploy or retrieve web pages. Increment types that fit scheduled runs: specs, static apps, client-side code, repo-clone work. Peptide record batches and Pages/Vercel config need attended sessions.

**Next increment:** (a) Aneesh publishes: the hub bundle (from 8-16) and kb-health-checker (from today) — ~4 minutes total; (b) next attended session: reconcile this rubric with `specs/kb-health-checker-spec.md` from the hub bundle, then start KB checker v2 (Vercel serverless URL mode) or a peptide record batch; (c) next scheduled run: MQD calculator scaffold is the best static-first candidate if v2 needs attended time.

---

## Entry #4 — 2026-09-13

**Shipped:** **MQD Runway** (queue #3) — Delta Medallion status calculator, built and deploy-ready as a pure client-side single file.
Deliverables staged: `mqd-calculator/index.html` + `README.md`. Target: new repo `neeshykha/mqd-calculator` → GitHub Pages.

Enter current MQDs, planned Delta flight spend, and Delta Amex cards (Boost + Headstart) → projected year-end MQDs on a runway meter with all four tier markers, per-tier gap analysis ("close it with $X fare or $Y Reserve spend"), and a mileage-run calculator (MQD yield, cost-per-MQD, does-it-close-the-gap verdict). Inputs persist in localStorage so it works as a season-long tracker. Verified in headless Chromium: 16/16 checks (math, rule edits, persistence, 400px viewport, zero console errors).

**Key design decision — rules as data, not code.** The queue note said this project "needs attended web access" to verify current MQD rules. The unblock: every program number (thresholds, Boost rates, Headstart) lives in an editable, dated rules panel that all calculations read from. WebSearch (titles only) confirmed 2027 thresholds unchanged from 2026, which de-risked the Sept-2026 snapshot; and if anything changes, users fix it in the UI in seconds. Same lesson-shape as KB checker v1: **re-scope the increment so the blocked dependency stops being a dependency.** A loyalty calculator that hardcodes rules dies at the next program change anyway — the constraint forced the better design.

**Environment re-check:** push from scheduled runs still 403 (tested per the 8-23 note). kb-health-checker confirmed published (repo exists, main branch). Portfolio hub repo still not created as of today — bundle from 8-16 is four weeks unpublished.

**Next increment:** (a) Aneesh publishes: mqd-calculator (~2 min) and, still pending, the hub bundle from 8-16; (b) next attended session: KB checker v2 (Vercel URL mode) or a peptide record batch; (c) next scheduled run: HVAC export cleaner (queue #5) is the static-first candidate — the cleaning rules are already encoded in the hvac-csv-cleaner skill, so it's a pure port job.

---

## Entry #5 — 2026-09-14

**Shipped:** the **Ship Sunday → Claude Code migration kit** — skill, headless run prompt, idempotent `publish.sh` (gh repo create → push → Pages API → About), first-run backlog checklist, and the MQD Runway deploy files bundled in.

**Decision (Aneesh's call):** move the whole weekly routine to Claude Code. Rationale: every cloud run ended in "files + manual upload steps" because the sandbox couldn't push or create repos; Claude Code with `gh` closes the last mile, and its full web access also unblocks the parked retrieval work (peptide batches, KB checker v2). The continuity design transfers unchanged — state files in git are environment-agnostic by construction, which is what made this migration a file-copy instead of a rewrite.

**Learned:** when an automation's environment can't reach the finish line, the fix isn't better handoff instructions — it's moving the automation to where the credentials live. Three runs of polished manual publish steps still produced a four-week-unpublished hub; one authenticated `gh repo create` beats all of it.

**Next:** first Claude Code run clears the backlog (publish mqd-calculator, hub, state files — see kit `first-run.md`), then turn off the Cowork scheduled task. Queue after that: KB checker v2 or first peptide record batch, both now unblocked in any run.

---

## Entry #6 — 2026-09-14 (first Claude Code run)

**Shipped:** two new live URLs and a new home for state.
- **MQD Runway:** https://neeshykha.github.io/mqd-calculator/ (repo `neeshykha/mqd-calculator`, About set, 200 in 30 s).
- **Portfolio hub:** https://neeshykha.github.io/portfolio/, rebuilt from scratch since the 8-16 bundle never turned up locally. It links 11 projects in three sections, not just the three Ship Sunday tools, because the other public repos are the stronger recruiter evidence and a hub that skips them undersells the account. kb-health-checker gets the "Start here" slot.
- **State moved** to `neeshykha/portfolio`; peptide-evidence keeps pointer stubs.

**Learned:** the kit had never run on the machine that would own it, and it showed. Three bugs surfaced in the first few minutes, none of which a sandbox without push access could have hit: `publish.sh` pushed over HTTPS with no credential helper configured, `git init -b` doesn't exist in git 2.9.0, and the skill called `bin/publish.sh` by a relative path. The second one failed after `gh repo create`, leaving an empty public repo; because the script was idempotent, the fix was one line and a re-run. That's the practical case for idempotent deploy scripts: a partial failure turns into a retry instead of a cleanup. Also caught before publishing: MQD Runway printed "-0 MQD" on an exact tier tie, because negating zero in JS gives -0.

**Environment:** runs live on Aneesh's Mac, not the worker node (the worker's reaper kills headless sessions at 900 s, and it's the work machine). SSH remotes, git 2.9.0 quirks, and kit paths are recorded in PROJECT-STATE.md.

**Next:** (a) Aneesh turns off the Cowork "Ship Sunday" scheduled task; (b) next run: KB checker v2 (URL mode) or the first peptide record batch, both unblocked; (c) optional: post MQD Runway to r/delta or FlyerTalk, Aneesh's call.

---

## Entry #7 — 2026-09-20 (scheduled run)

**Shipped:** **scheduled-agent-detector** is live — https://neeshykha.github.io/scheduled-agent-detector/ (repo `neeshykha/scheduled-agent-detector`, Pages on, About set, 200 on the first verify attempt). It was Friday's build sitting as a public repo with no page and no hub card, which is exactly the "waiting to ship" shape the finishing lane exists for. A nightly detector that judges each scheduled agent by whether its expected artifact moved, never by the run's own report, with a named failure signature on every miss and an explicit list of what it can't vouch for. Hub card added in the "Deploy AI, then measure whether it worked" section, second slot behind deflection-audit.

**Also closed a backlog nobody had noticed:** three repos with hub cards — kb-health-checker, mqd-calculator, and peptide-evidence — had no entry in `portfolio_projects.md`, including the flagship that holds the "Start here" badge on the hub. All three written from their own READMEs and pushed (`b9caa60`). The hub and the citation file had been drifting apart since the hub was rebuilt on 9-14, because that rebuild added cards for repos the Friday routine had never touched. Worth a standing check: the hub is the superset, so anything it links needs a citation entry, not the other way around.

**Learned:** `enable_pages.sh` assumed main/root, and this build serves from `docs/index.html`. Enabling main/root would have "worked" — the page would answer at `/docs/` — and quietly broken the URL the repo's own README advertises. Pages takes `/docs` as a source path, which puts the page back at the bare repo URL. The script now takes an optional source-path argument defaulting to `/`, so the next docs-rooted build is one flag instead of a hand-built API call. Small thing, but it's the same failure shape the detector itself is about: the run would have ended green with a live 200, and the link in the README would have been dead.

**Next:** HVAC export cleaner (queue #4, unattended OK) is the next static-first build if no Friday repo is waiting. KB checker v2 still needs an attended session for the Vercel setup, and peptide record batches still need attended write access to `~/Documents/ShipSunday/`.
