# Extended Integrated 5 Why Methodology Reference

> Source: `studio_tool/documents/5why-expanded/5why-통합방법론.md` (5W2H → Fishbone/6M →
> tabular parallel 5 Why → FMEA/RPN → data-driven verification & corrective-action design,
> a 5-stage integrated theory)

Theory, checklists, and scoring anchors this skill consults at each analysis step. Never
expose this verbatim to the user — use it only as internal judgment criteria.

## 1. Why 5 Why Alone Isn't Enough

- Card's (2016) core critique: "the depth of the fifth why is arbitrary — it has no
  correlation with the actual root cause," and "results aren't reproducible — different
  people land on different causes." Every step of this skill directly targets these two flaws.
- Single-path bias (accidentally picking just one cause) → Step 2 (Fishbone/6M) compensates by covering breadth.
- Lack of reproducibility (multiple root causes may coexist) → Step 3 (tabular parallel tracking) compensates.
- No prioritization among causes → Step 4 (FMEA/RPN) compensates.
- Speculative confirmation of a root cause → Step 5 (data-driven verification) compensates.
- Academic evidence: even this combination, without a standardized verification procedure,
  reportedly fails to establish a consistent causal relationship in nearly half of cases —
  so the verification step (Step 5) must never be skipped or treated as a formality. Even if
  the user is in a hurry and says "let's just go with this," at minimum confirm whether
  supporting data exists before moving on.

## 2. The 7 Elements of 5W2H (Problem Framing)

Ask each element one at a time. If the user already answered an element while describing
the problem, don't ask it again.

- **What**: What is the problem? (Be specific about the symptom — "quality is bad" vs. "defect rate rose to X%")
- **Where**: Where does it occur? (process/department/system/screen, etc.)
- **When**: Since when, and how often does it happen?
- **Who**: Who discovered it / who is affected?
- **Why (significance)**: Why does this need to be addressed now? (impact if left unaddressed)
- **How**: How was it discovered/observed? (measurement method, discovery circumstances)
- **How much**: What's the scale? (frequency, cost, number of cases/people affected, etc.)

Once all 7 are collected, read back a one-paragraph problem statement for confirmation:
*"In X, since Y, at Z scale — is that right?"*

## 3. The Fishbone 6M Categories (Cause-Space Expansion)

- **Man**: skill level, training, procedure non-compliance, communication
- **Machine**: equipment aging/failure, misconfiguration, insufficient maintenance
- **Material**: raw material quality, supplier variation, spec mismatches
- **Method**: work procedures, missing/faulty standards, workflow design
- **Measurement**: measuring-tool error, unclear inspection criteria, data-collection errors
- **Environment**: physical environment (temperature/humidity, etc.), organizational culture, external regulation/market shifts

Covering every category isn't mandatory — if a category is clearly irrelevant, it can be
skipped after confirming with the user (following the same cognitive-load principle as
mece's "2–5 categories"). However, deciding to look at just one category defeats this
skill's whole reason for existing (preventing single-path bias), so encourage covering at
least 2 categories.

## 4. Actionable-Root-Cause Stopping Criteria (Parallel Multi-Path 5 Why)

Repeat "why?" for each candidate cause, but **do not force a fixed 5 levels.** End a chain
once it meets any of these conditions:

- Any further "why" would fall outside what the organization can control (e.g., nothing
  beyond "because of the economic downturn" can be acted on)
- The cause has reached a level correctable by a concrete action (process change, training,
  equipment replacement, etc.)
- The cause is in a form verifiable with data (frequency, timing, and conditions can be specified)

If a chain stops too early (still at a surface symptom), push it further. If it escapes to
an unsubstantiated external factor ("just bad luck") with no evidence, pull it back and ask
one more why.

## 5. FMEA 1–10 Scoring Anchors (AIAG-style, abbreviated to 4 tiers)

When scoring during the conversation, briefly present these anchor points to the user and
let the user's judgment finalize the score — never assign scores unilaterally. AskUserQuestion
only allows up to 4 options, hence the 4-tier abbreviation — the underlying scale is still
1–10 (if the user says "somewhere in between," round to the nearest anchor).

| Score | Severity | Occurrence | Detection (lower = riskier) |
|---|---|---|---|
| 1 | Little to no impact | Rarely happens (less than once a year) | Almost certainly caught beforehand |
| 4 | Minor to noticeable loss/complaint | Occasional to frequent (roughly quarterly to monthly) | Coin-flip odds of being caught |
| 7 | Serious loss, major impact on customers/operations | Frequent (roughly weekly) | Hard to detect, mostly discovered after the fact |
| 10 | Safety/regulatory/catastrophic loss | Constant (nearly every time) | Essentially undetectable, no way to know before it happens |

RPN = Severity × Occurrence × Detection (max 1000). Rank causes by descending RPN. If RPN
ties, prioritize the one with the higher Severity.

## 6. Verification-Step Checklist

For top-RPN causes, confirm all of the following before moving to corrective-action design:

- Is there **frequency data** showing this cause actually occurred?
- Does the **timing** of this cause's occurrences line up with when the problem occurred?
- Can the **condition contrast** be explained (what's different when this cause is present vs. absent)?
- If even one of the above three can't be confirmed, treat the cause as speculative —
  discuss how to gather data before designing corrective action (don't jump straight to it).
