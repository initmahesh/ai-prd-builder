# AI PRD Builder

A Claude skill that interviews you section by section (Discover, Design, Develop, Deploy) and writes a complete `PRD.md` for a product that uses AI or agents. It then checks the PRD against a living checklist that is kept outside the skill, and produces a pass/fail report. It also upgrades an existing PRD.

Built from the research outline "Learn to Build PRDs for Humans and AI Agents" by Mahesh Yadav.

## What is in this repo

| Path | What it is |
|---|---|
| `ai-prd-builder/` | The skill source (SKILL.md, config, references, tests). Zip this folder as `ai-prd-builder.skill` to install it. |
| `ai-prd-builder/references/example-prd.md` | A complete PRD that passes the checklist (a pattern, not content). |
| `ai-prd-builder/references/baseline-prd.md` | A traditional PRD that fails it, for comparison. |
| `checklist/checklist.md` | The living checklist: 31 starting rows. Lives OUTSIDE the skill. |
| `checklist/checklist-changelog.md` | Dated record of every checklist change. |

## Install and first run

1. Zip the `ai-prd-builder` folder (`zip -r ai-prd-builder.skill ai-prd-builder`) and upload it in Claude under Settings, then Skills.
2. Copy the `checklist` folder somewhere you own and connect that folder to your Claude session.
3. Say: "Write a PRD for [your AI product]", or paste an existing PRD and say "check my PRD". The skill reads `checklist.md` from the folder you connected. If it is missing, it offers to create one.
4. Answer the questions one section at a time. You get `PRD-[product].md` and a pass/fail report.

## The living checklist

- Edit `checklist.md` by hand, or approve additions the skill proposes after each run.
- Never delete rows: set Status to retired and note why in `checklist-changelog.md`.
- Each team may keep its own copy.

## Owner notes

- Owner: Mahesh Yadav. Version 1.1 (2026-10-22).
- Feedback from every run is logged; after 3 open items the skill offers "Update now", which opens the skill creator with the feedback loaded.
- Before wide sharing, set `MASTER_COPY` and `MEMORY_FOLDER` in `ai-prd-builder/config.md` and name a reviewer in `ai-prd-builder/HANDOFF.md`.
