# Run log: ai-prd-builder

One entry per run, newest at the bottom. Copy the entry format below for each run. Angle brackets mean "fill in".

### Entry format

Run <id> | <date and time> | v<version> | manual or scheduled
Inputs: <resolved inputs>
Data: <source, latest date, rows>   Fallback used: no, or which
Trace:
  1. Step 0 validation: ok or questions asked   CP1: yes or no
  2. Step 2 <agent or step>: tier <tier>, tool calls <n>, retries <n>
  3. Step 4 QA: attempt 1 pass or fail (rows), attempt 2 pass or fail
  4. Step 5 filing and notify: checkpoint results
Gates fired: none, or which and the decision
Feedback: rows logged <FB IDs or none>; update prompt: not due, or shown to owner / other user -> update now, next time, tell the owner, no reply
Outcome: shipped, draft, blocked or cancelled
Effort: agent runs <n>, tool calls <n>, rebuilds <n>, duration <min>
Notes: anything the next run should know

### Entries
