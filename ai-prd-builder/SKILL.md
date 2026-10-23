---
name: ai-prd-builder
description: >
  Interviews you section by section (Discover, Design, Develop, Deploy) and writes a complete PRD.md
  for a product that uses AI or agents, then checks it against a living checklist that is kept outside
  the skill and produces a pass/fail report. Also upgrades an existing PRD. Use this skill whenever the
  user mentions writing a PRD, a product requirements doc, a spec for an AI or agent product, upgrading
  a PRD for agents, checking a PRD against the checklist, or turning a one-pager or 6-pager into a PRD.md,
  even if they do not name the skill. Not for engineering design docs, writing code, or PRDs for products
  with no AI component.
---

# AI PRD Builder

Version: 1.1   Owner: Mahesh Yadav   Updated: 2026-10-22   History: see CHANGELOG.md

## 1. Purpose and scope

**Outcome:** one PRD.md for an AI product, written from a section-by-section interview and checked against the living checklist, plus a pass/fail report. The unit of value is one checked PRD.

**In scope:** a new PRD from an idea; upgrading an existing PRD; checking a PRD against the checklist; proposing checklist updates after a run.

**Anti-patterns (do not):**
- Write a fact, number, quote or competitor claim without a source or a "proposed" label. People act on PRDs, so a wrong number spreads.
- Invent evidence: interview quotes, customer names, market figures. Leave it as a SET item instead.
- Reuse details from another user's product (the contract example in `references/example-prd.md` is a pattern, never content).
- Copy the checklist into this skill or work from memory of it. Read the file at `CHECKLIST_PATH` every run, because the user edits it between runs.
- Change the checklist file without the user's approval at CP5.
- Drop, blank out or fake a required section. Tag missing data visibly instead.
- Put secrets, confidential data or personal data in any file or in memory.
- Edit this skill's own files or config. Feedback goes to the feedback log, and the owner updates the skill through the skill creator (section 13).

## 2. Triggers and inputs

Typical phrases: "write a PRD for", "PRD for my AI product", "upgrade my PRD for agents", "check my PRD", "turn this 6-pager into a PRD.md".

| Input | Required? | Format and example | If missing or wrong |
|-------|-----------|--------------------|---------------------|
| Product idea or existing PRD | Yes, one of them | A few lines, or a pasted or attached PRD | Ask in Step 0 |
| Folder holding checklist.md | Yes | A connected folder, for example the user's PRD folder | Gate G1 |
| Research on or off | No, default on | "research on" | Use the default |
| Output folder | No | Default is the checklist folder | Ask at CP4 |

## 3. Step 0: intake and validation

1. **Relevance:** is this a PRD for a product with an AI or agent component? If it is a PRD for a non-AI product, say the checklist is built for AI products and ask whether to continue. If it is not a PRD request, say so and stop.
2. **Checklist:** read `checklist.md` from `CHECKLIST_PATH`. If the file is missing or unreadable, stop (gate G1) and offer to create a starter copy from `references/checklist-seed.md` in the user's folder. Creating it is a file write, so it needs a yes at CP1 (gate G5). Keep a count of active rows.
3. **Completeness:** list missing required inputs and ask for them in one message, with a suggested default for each.
4. **Sanity:** is the idea specific enough to interview on (a user, a problem, an AI component)? If not, say what is unclear and suggest an example (gate G6).
5. Restate the product in two lines, the number of active checklist rows, and whether research is on. **CP1.**

## 4. Config

All editable values are in `config.md`: caps, paths, fallbacks, feedback settings. Read it at Step 1. Do not restate its values in this file; refer to keys by name. `OWNER` approves changes to this skill. The checklist is not in config or in this skill: it lives at `CHECKLIST_PATH`.

## 5. Checkpoint index

Every checkpoint waits for the user. If there is no reply, do not proceed.

| ID | After step | Human confirms | Options | If no reply |
|----|------------|----------------|---------|-------------|
| CP1 | Step 0 | Product, checklist loaded (or creating a starter checklist.md), research on or off | Confirm / correct | Wait |
| CP2 | Each section in Step 3 | The section content (Discover, Design, Develop, Deploy, one at a time) | Confirm / edit / answer more | Do not proceed |
| CP3 | Step 5 | Check results and unresolved rows | Deliver as is / fix / cancel | Do not proceed |
| CP4 | Step 6 | Saving the PRD and report, and replacing a file that exists | Replace / keep both / cancel | Do not proceed |
| CP5 | Step 7 | Each proposed checklist change | Add / edit / skip | Do not change the checklist |

## 6. Orchestration

Each step names what goes in, what comes back, and when it is done.

1. **Step 1: sources and mode.** Read `config.md`. If the user gave an existing PRD, audit it against every active checklist row (`references/baseline-prd.md` shows what a typical failing PRD looks like) and show a short table of pass, partial and missing, then continue with it as a draft. If the user gave an idea, continue from scratch. For web research use `FALLBACKS`: if search is unavailable, ask the user to paste the evidence or mark it SET. Done when the mode is clear.
2. **Step 2: research (if on).** Use at most `SEARCHES_PER_RUN` searches. Open the pages whose facts you will use; a search snippet is not a source. Collect: why now, evidence of the problem, competitors and general AI tools, benchmarks. Record URL, date and whether the page was opened. Done when each Discover item has evidence or is marked SET.
3. **Step 3: interview, one section at a time.** Load `references/interview-guide.md`; keep `references/example-prd.md` open as the pattern for depth. For each of Discover, Design, Develop, Deploy: ask at most `QUESTIONS_PER_ROUND_MAX` questions in one message, each with a proposed default, using the multiple-choice tool where available. At most `ROUNDS_PER_SECTION_MAX` rounds per section. Cross-question vague answers. Then show that section's draft text and ask **CP2**. A default the user accepts is labeled proposed in the PRD.
4. **Step 4: draft.** Assemble PRD.md using the structure in `references/design-spec.md`, from the confirmed sections. Done when every required section exists.
5. **Step 5: QA.** Section 11. Maximum `QA_MAX_ATTEMPTS` attempts. **CP3.**
6. **Step 6: deliver.** Save both files as `FILE_NAME_PATTERN` in `OUTPUT_FOLDER`. Look for existing files first. **CP4.** Give the user the PRD, the report and the SET list.
7. **Step 7: checklist proposals.** From the failed and flagged rows and the interview, propose new or changed checklist rows (ID, section, checkpoint, how it is tested). Ask about each at **CP5**. For each approved row, append it to `checklist.md` and add a dated line to `CHECKLIST_CHANGELOG_FILE`. Never delete a row: retire it by status instead.
8. **Step 8: record.** Write the memory entry and the run-log entry (sections 10 and 12).
9. **Step 9: feedback.** Capture feedback and, if due, show the update prompt (section 13), then add the result to the run-log entry. This comes after delivery so it never delays the output.

Stay inside `TOOL_CALLS_PER_STEP` calls per step and `RUN_MINUTES_MAX` minutes per run. If a run needs more, pause and ask.

## 7. Agent roster

Not applicable: single agent. The work is sequential and fits one context.

## 8. Rules and formatting

- Build every required section in `references/design-spec.md`. If something is unknown, show the section with the gap tagged (for example "SET: retention policy"). A visible gap gets fixed; a hidden one gets found by the reader.
- Label every starting number "proposed". Keep a SET list at the end of the PRD for items only the user can confirm or evidence only the user can supply.
- Cite each fact with a link and its date. Mark pages seen only in search as unverified.
- Write for two readers: a person who reads sections 1 and 2, and a coding agent that follows the rest. Give every requirement an ID and a done-when, and put the stop-and-ask rule in the header.
- Define "agent" and other terms in a line when first used, because the user may be new to them.
- The report lists every active checklist row: ID, result (pass, partial, missing), where it is covered, and what to add.

## 9. Guardrails

- **Caps:** values in `config.md`. Count tool calls per step, retries, searches, interview rounds, QA attempts and rebuilds (`REBUILDS_MAX`), and write the counts in the run log.
- **Retries:** at most `RETRIES_PER_CALL` per failing call, with a pause, then stop and escalate. The same error twice in a run means stop.
- **Gates:** stop and ask; never continue on a fired gate.
  - G1 the checklist file is missing, unreadable or empty.
  - G2 not used in this skill.
  - G3 a fact or number cannot be tied to a source or a proposed label (tag it SET or unverified and route it to a checkpoint).
  - G4 a cap was reached.
  - G5 about to write or overwrite a file, or change the checklist.
  - G6 unclear, contradictory or out-of-scope input, or confidential data in the input.
- **No loops without a counter.** No agent calls itself.
- **Side effects** only after an explicit yes. The default is do not proceed.

## 10. Memory protocol

Memory lives in `MEMORY_FOLDER`. At start, read `memory.md` and the file of each agent about to run, as hints, and re-check live data. At the end, append one dated entry: what ran, inputs, outcome, issues, fixes, open items. If a recent entry says `status: running`, ask before continuing. Lessons in memory.md are applied as hints on every run, within the limits in section 13. No secrets, client data or personal data. If the folder is unreachable, say so, write the entry locally and ask the user to upload it.

## 11. QA

Checklist for the finished PRD: `references/qa-checklist.md` (checks of the PRD itself, plus one row per active row in the living checklist). Maximum `QA_MAX_ATTEMPTS` attempts. Attempt 1 fails: fix only the failed rows. Attempt 2 fails: stop and follow the failure policy: deliver the PRD marked "checklist not passed" with the unresolved rows listed at the top of the report. Every row is a Flag: nothing blocks delivery, and Flag rows are listed first in the report. The QA report gives the result, attempts used, one line per row with evidence, and the date of each source.

## 12. Output, filing and notification

Save to `OUTPUT_FOLDER` as `FILE_NAME_PATTERN`. Before saving, look for an existing file with the same name and ask: replace, keep both with a version suffix, or cancel. After saving, tell the user where the files are, with the report's flags first. Append the run-log entry to `RUN_LOG_PATH` (template in `logs/run-log.md`). `SCHEDULE` is on demand: this skill is always started by the user, and it never saves files or changes the checklist without an approval.

## 13. Feedback and updates

Feedback is captured on every run, but it never changes this skill directly. The skill cannot rewrite its own installed files, and an unreviewed change could quietly remove a safeguard. Changes go through the skill creator, approved by `OWNER`.

The log is `feedback-log.md` in `MEMORY_FOLDER` (the scaffolded `memory/feedback-log.md` is its starting copy). If the folder is unreachable, follow the memory protocol: write locally and ask the user to upload it.

**Capture (every run, after delivery).**
- If `FEEDBACK_QUESTION` is on and the run is attended, ask once: "Anything to change next time? (optional)". An empty reply, "no" or "all good" logs nothing.
- Log these without asking, one row each: the user edited or rejected output at a checkpoint, a QA Flag or Block row, a gate fired, a cap was reached.
- Set type and severity from the definitions in the log. By is owner, user or auto (never a name). Describe the problem, not the client or matter. No secrets or personal data.

**Lessons (light, automatic learning).** If the owner states a presentation preference ("always put the summary first"), add it to the Lessons section of memory.md, set that row's status to lesson, and apply it from the next run. Lessons may change wording, order, layout and default inputs only. They never change caps, gates, checkpoints, QA rows, recipients, filing or anything in `config.md`. Other users' preferences stay open for the owner, because memory is shared by the whole team.

**Update prompt (end of run).** Rows logged in this run count. The prompt is due when open rows reach `IMPROVE_THRESHOLD`, or any open row has severity high, and "Snooze runs left" is 0. If this run logged a high row, set the snooze to 0 first. If not due, lower "Snooze runs left" by one (not below 0) and stop.
- **Who is the user.** Use the name the session gives (account or introduction); if unknown, ask once. No answer means not the owner.
- **Scheduled or unattended run:** do not ask. Include `OWNER` in this run's notification with one line: "N feedback items are waiting for an update".
- **The owner:** show the open count and the high rows, then two options. **Update now** (recommended when any open row is high): set "Snooze runs left" to `IMPROVE_SNOOZE_RUNS` so the prompt does not repeat while the update is in progress, then hand off as below. **Next time:** set "Snooze runs left" to `IMPROVE_SNOOZE_RUNS`.
- **Anyone else:** if "Owner told" already has a date, say in one line that the owner knows and stop. Otherwise offer **Tell the owner** (record today's date and run in "Owner told", draft a short note to `OWNER` with the open count and the high rows, and send it only if the user says yes, gate G5; otherwise give the user the text) or **Next time** (no change; a non-owner never snoozes the owner's prompt).
- **No reply:** the same as Next time for that user. Record "Last prompt" as date, run and choice. This prompt is not a checkpoint: nothing changes until the owner approves a change plan inside the skill creator.
- Add the feedback rows and the prompt result to this run's run-log entry.

**Hand-off (Update now).** Load the `SKILL_CREATOR` skill and start it with this block, so it goes straight to feedback intake without a new interview:

```
FEEDBACK HAND-OFF
skill: <name>   version: <version from the header>   owner: <OWNER>
master copy: <MASTER_COPY>
feedback log: <MEMORY_FOLDER>/feedback-log.md
open items: <FB IDs with severity, high then medium then low, oldest first>
```

The skill creator shows a change plan for approval, applies only what the owner approves, bumps the version, adds a regression test per fixed item, re-runs QA, marks the rows and resets the prompt state. The skill creator then tells the owner to install the new version. If `SKILL_CREATOR` is not installed, say so in one line, keep the rows open, and tell the owner to install it and then say "apply feedback to <name>".

## 14. Changelog

See CHANGELOG.md.
