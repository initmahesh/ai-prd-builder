---
skill: ai-prd-builder
file: feedback-log.md (shared)
---
# Feedback log: ai-prd-builder

Every run appends here (SKILL.md section 13). Rows are append-only: never delete a row or change anything but its Status, and Status changes in two cases only: the skill sets lesson for the owner's own preference, and the legalgraph-skill-creator sets everything else when the owner approves an update. No secrets, client names or personal data: describe the problem, not the matter.

## Update prompt state

Each run updates this block at the end (SKILL.md section 13). The skill creator resets it after an update.

Snooze runs left: 0
Last prompt: none (date, run, choice)
Owner told: none (date, run)

## Items

By: owner, user or auto (never a name).
Source: asked (end-of-run answer), cp-edit (user changed output at a checkpoint), cp-reject (user rejected at a checkpoint), qa-flag, gate, cap, owner-note.
Type: bug, wrong-output, preference, missing-feature, process.
Severity: high (wrong or misleading output, or a step that breaks), medium (works but needs a manual fix each time), low (nice to have).
Status: open, lesson (applied as a lesson in memory.md, owner may remove), applied vX.Y, rejected (reason), duplicate of FB-n.

| ID | Date | Version | Run | By | Source | Type | Severity | What happened, in the user's words where possible | Status |
|----|------|---------|-----|----|--------|------|----------|---------------------------------------------------|--------|
