# Hand-off: ai-prd-builder

## What it does
Interviews a user section by section (Discover, Design, Develop, Deploy) about a product with AI or agents, researches with cited sources, writes PRD.md, and checks it against a living checklist kept in the user's own folder. It also upgrades an existing PRD. Output: PRD.md and a pass/fail report. After each run it proposes checklist additions, which the user approves.

## Owner and reviewer
Owner: Mahesh Yadav   Reviewer: to be named before sharing with other teams

## How to install or share
The skill works the same either way, because its safeguards are inside its own files.
1. If your organisation lets you add skills, upload the packaged skill from the Claude app's skill settings.
2. Otherwise keep the folder in the shared team location and attach SKILL.md and its references to a shared project or the session.
3. Each user connects a folder that holds checklist.md. If there is none, the skill offers to create it from the starter copy.

## First-run checklist
- [ ] Inputs for the first run are ready: a product idea or an existing PRD, and the folder for checklist.md
- [ ] The checklist folder is connected and writable
- [ ] Run the test prompts in tests/test-prompts.md
- [ ] If sharing memory, set MEMORY_FOLDER in config.md and confirm users can append to feedback-log.md

## Reading the logs
Run log: `RUN_LOG_PATH` in config.md. Review after the first five runs, then monthly: caps nearly hit, checklist rows that fail often (candidates for stronger interview questions), checkpoints always approved unchanged.

## The living checklist
It lives in the user's folder as checklist.md, with checklist-changelog.md beside it. Edit by hand or approve proposals at CP5. Never delete rows: retire them. Teams may keep their own copies.

## Feedback and changing the skill
Users' feedback is logged automatically in `feedback-log.md` in the memory folder. When enough builds up, the skill offers the owner "Update now", which opens the legalgraph-skill-creator with the feedback loaded. You can also start it any time by saying "apply feedback to ai-prd-builder".
Only the owner edits the master copy (`MASTER_COPY` in config.md). Every change gets a CHANGELOG entry listing the feedback IDs it closes. After an update, install the new version: the skill cannot replace itself.
