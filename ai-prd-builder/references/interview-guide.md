# Interview guide: ai-prd-builder

Read this in Step 3. For each section: the goal, what sufficient looks like, questions with a proposed default, and probes. Ask at most `QUESTIONS_PER_ROUND_MAX` questions per round and `ROUNDS_PER_SECTION_MAX` rounds per section. Skip anything already answered. After a section, show its draft text and ask CP2.

Contents: 1 How to use it, 2 Discover, 3 Design, 4 Develop, 5 Deploy, 6 Cross-question patterns, 7 Existing PRD mode

## 1. How to use it

- Offer a proposed default for every question. People correct a good default faster than they invent an answer. A default the user accepts is labeled proposed in the PRD.
- Use the multiple-choice tool where available, recommended option first, with a few words on why you ask.
- Explain terms (agent, ground truth, ontology) in a line when first used.
- Never invent evidence. If the user has none, mark SET.

## 2. Discover

**Goal:** prove the product deserves to exist and name its riskiest assumption.
**Sufficient:** C01 to C04, C16 to C18 can be answered from the draft.

Questions:
1. Who has the pain, and what is the evidence? Default: ask for 3 users and one number (hours, cost, error rate). If none, SET.
2. What is the North Star and the first three steps to it? Default: propose from the idea.
3. Why now and why you? Default: propose from research (Step 2), each point cited.
4. Gap test: why not ChatGPT or Claude Code? Options (pick all that apply): restrictions (regulated or government use, learning outside the general tool); no shared learning across users; long-horizon craft needing a specific planner; quality from your data and ontology; accountability and security. Default: the ones that fit the research; rule: if fewer than 3 hold for a target customer, say so.
5. Riskiest assumption and the test that would kill it. Default: the belief that users will trust the output enough to act on it; test with a shadow study and a number.
6. MEP: smallest version that can be scored. Default: one use case, one workflow, 25 labeled examples.

Probes: "What would make you stop building?" "Who is unhappy if this is wrong?" "Which part of the gap test would a skeptical customer attack?"

## 3. Design

**Goal:** make the product trustworthy and bounded.
**Sufficient:** C05 to C08, C19 to C21.

Questions:
1. Who are the roles, who approves what, and where does the system pause in each journey? Default: one human approver per consequential action.
2. What must the user see to trust an answer? Default: the five layers (answer with confidence, plan, knowledge used, iterations, checks) plus a validate list.
3. Never-do list and priority order. Default: never send or sign for the user, never write to external systems without recorded approval, never invent facts, never mix customers' data; priority safety, honesty about uncertainty, policy compliance, helpfulness.
4. Escalation triggers. Default: low confidence on a high-risk item, topic outside the rules, conflicting data, unknown type, repeated tool failure, out-of-purpose request.

Probes: "If it is wrong here, who finds out and how?" "What would you refuse to automate?"

## 4. Develop

**Goal:** define "good" before building and limit what the system can touch.
**Sufficient:** C09 to C12, C22 to C26.

Questions:
1. For each requirement, what is done-when? Default: write R-01 and up with a testable condition.
2. Helpful, honest, harmless: what question must each response pass? Default: helpful (uses the rules, saves time, covers what matters), honest (cites sources, states uncertainty, no invention, confidence matches accuracy), harmless (inside tool permissions, no cross-customer data, stops on never-do).
3. Ground truth: where does it come from, who validates it, what thresholds? Default: 25 labeled cases, a named expert owner, 95 percent accuracy and 95 percent recall on high-risk items (proposed), plus 30 adversarial cases.
4. Tools: list each with what it reads, writes and who approves. Default: read-only unless a write is essential, human approval per write.
5. What do you track per customer, workflow and agent? Default: interactions, tokens, accuracy, acceptance, cost.
6. Security, privacy, privilege, retention? Default: SET for retention; no training on customer data without written consent.

## 5. Deploy

**Goal:** limit risk, spend and speed of spread.
**Sufficient:** C13 to C15, C27, C28.

Questions:
1. Rollout stages and the accuracy needed to enter each. Default: shadow, 10, 30, 80, 100 percent, each with entry numbers and stop conditions (proposed).
2. What pauses the system or restores the last good state? Default: accuracy under threshold, write mismatch rate, any critical harmless failure, cost over ceiling.
3. Cost ceiling and what ROI looks like. Default: per-unit ceiling below a share of price, daily and monthly caps, warn at 80 percent, hard stop at 100.
4. Autonomy boundary: what may the system do alone, and when does that expand? Default: drafts autonomous; consequential writes need approval until accuracy holds for weeks.
5. Intended use and alerts for anything else. Default: alert and block unsupported types, volume spikes, requests outside the purpose.
6. Owners, support and pricing meter. Default: product owns metrics and spec, engineering reliability, a named expert owns ground truth.

## 6. Cross-question patterns

| The user says | It hides | Ask |
|---------------|----------|-----|
| "It should be accurate" | No test | "What number counts as accurate? How will you check?" |
| "The AI will handle it" | No boundary | "Which decision would you never leave to it?" |
| "Users will love it" | No evidence | "Name two users and what they said." |
| "We'll add safety later" | Missing guardrails | "What is the worst thing it could do on day one?" |
| "Like ChatGPT but for X" | No gap test | "What can ChatGPT not do here, and why?" |
| "I don't know" | Gap | Offer a labeled default or add it to the SET list. |

## 7. Existing PRD mode

Audit the draft against every active checklist row first. Show pass, partial and missing as a table. Keep the user's good content; do not rewrite what already passes. Interview only on rows that are partial or missing, in the same four sections.
