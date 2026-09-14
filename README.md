# Shipped tools

**Live:** https://neeshykha.github.io/portfolio/

The public index of what I've built: AI deployment and measurement projects, support operations tools, and a few things from outside work. The landing page links each one, and the ones that run in a browser open with nothing to install.

This repo is also the control file for **Ship Sunday**, the weekly routine that ships them.

## What's here

| File | What it is |
|---|---|
| `index.html` | The landing page |
| `PROJECT-STATE.md` | The queue, operating rules, and environment facts. Every run reads it first. |
| `LEARNING-LOG.md` | One entry per run: what shipped, what was learned, and what's next |

## How the routine works

Each Sunday a Claude Code run pulls this repo, reads the state file, ships one increment to a live URL, and pushes the updated state and log back. The rule is that a run ends with something a person can click; "works on my machine" doesn't count.

State lives in git rather than in any one environment. That's what let the routine move from a cloud sandbox, which could build but couldn't deploy, to a machine with real credentials by copying two files.

---

Support operations leader who builds with AI · [github.com/neeshykha](https://github.com/neeshykha) · Atlanta
