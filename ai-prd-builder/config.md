# Config: ai-prd-builder

Values only, no logic. Every key is used by a step in SKILL.md. The owner edits this file.

## OWNERSHIP
OWNER = Mahesh Yadav
SCHEDULE = on demand
MASTER_COPY = (unset)
# Shared folder holding the master copy of this skill. Set it before the first update.

## PATHS
CHECKLIST_PATH = (ask the user for the connected folder holding checklist.md)
CHECKLIST_CHANGELOG_FILE = checklist-changelog.md
OUTPUT_FOLDER = (same folder as checklist.md unless the user names another)
FILE_NAME_PATTERN = PRD-product-slug.md and PRD-product-slug-checklist-report.md
MEMORY_FOLDER = (unset)
RUN_LOG_PATH = logs/run-log.md

## DATA SOURCES
FALLBACKS = web search and page fetch -> user pastes the evidence -> mark as SET and continue

## CAPS
QA_MAX_ATTEMPTS = 2
RETRIES_PER_CALL = 2
TOOL_CALLS_PER_STEP = 15
REBUILDS_MAX = 2
RUN_MINUTES_MAX = 45
SEARCHES_PER_RUN = 8
ROUNDS_PER_SECTION_MAX = 2
QUESTIONS_PER_ROUND_MAX = 4

## FEEDBACK
FEEDBACK_QUESTION = on
IMPROVE_THRESHOLD = 3
IMPROVE_SNOOZE_RUNS = 5
SKILL_CREATOR = legalgraph-skill-creator
