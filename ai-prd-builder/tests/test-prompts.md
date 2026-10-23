# Test prompts: ai-prd-builder

Re-run after every meaningful change.

| # | Type | Prompt | Expected behaviour |
|---|------|--------|--------------------|
| 1 | Normal case | "Write a PRD for an AI assistant that reviews vendor invoices and posts approved ones to our accounting system." Checklist folder connected. | CP1 first; one section at a time, each with proposed defaults and CP2; PRD.md and report produced; every active checklist row appears in the report; files saved only after CP4 |
| 2 | Data gap | Same request, but checklist.md is missing from the folder | Gate G1 fires; the skill offers a starter copy and writes nothing until the user says yes |
| 3 | Ambiguous input | "Write me a PRD." | One message of clarifying questions with suggested defaults; no research or drafting started |
| 4 | Out of scope | "Write the engineering design doc for our login service." | Declines or redirects; says it is for PRDs of AI products |
| 5 | Forced QA failure | Interview where the user cannot give any numbers, thresholds or evidence and refuses SET placeholders | Exactly two QA attempts, then delivery marked "checklist not passed" with unresolved rows listed; never a third attempt |
| 6 | Feedback capture | Normal run; at the end the user answers the feedback question and edits a section at a CP2 checkpoint | Two rows appended to feedback-log.md (asked, cp-edit) with no confidential data; no change to the skill's files |
| 7 | Update prompt | Feedback log holds 3 open rows; run once as the owner, once as another user | Owner: after delivery, Update now / Next time; either sets the snooze; Update now hands off with the hand-off block. Other user: Tell the owner / Next time; the note is sent only on a yes |
| 8 | Checklist growth | After a run, a gap appears that no checklist row covers | At CP5 the skill proposes a new row; it is appended to checklist.md and logged in checklist-changelog.md only after approval; nothing is deleted |
| 9 | Existing PRD | User pastes a traditional PRD | Audit table of pass, partial and missing first; interview only on partial and missing rows; good content kept |
