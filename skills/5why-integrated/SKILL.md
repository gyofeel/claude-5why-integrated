---
name: 5why-integrated
description: >
  When the user brings a problem, this skill frames it with 5W2H, expands the cause
  space with a Fishbone/6M diagram, traces root-cause candidates through parallel
  multi-path 5 Whys per category, prioritizes them with FMEA (RPN), verifies with
  evidence, and drives corrective-action design — the extended integrated 5 Why
  methodology. Produces a Markdown report or an interactive HTML artifact. Use when
  the user says things like "run an integrated 5 Why analysis", "help me find the
  root cause", "let's fishbone this", "prioritize with FMEA", "why is this problem
  happening", "/5why-integrated", or otherwise signals they want to dig into a root
  cause systematically.
---

# 5why-integrated — Extended Integrated 5 Why Root Cause Skill

## Purpose

To compensate for the "single-path bias" and "lack of reproducibility" that plague
standalone 5 Why analysis, this skill guides the user **conversationally, one step
at a time** through: problem framing (5W2H) → cause-space expansion (Fishbone/6M) →
parallel multi-path 5 Why → risk quantification (FMEA/RPN) → evidence-based
verification and corrective-action design — then produces a final artifact.

Theory, checklists, and the FMEA scoring anchors live in
[references/method.md](references/method.md); output skeletons live in
[references/output-templates.md](references/output-templates.md).

## Core Principles

- **Ask one thing at a time.** Never dump all questions at once. Wait for the
  user's answer before moving on.
- Never re-ask for information the user already gave — only fill in the gaps.
- At the end of each step, briefly read back what's been gathered so far for
  confirmation.
- Verification (FMEA scoring, evidence checks) repeats until it actually passes.
  Don't wave it through.
- **Use AskUserQuestion for structured choices** — 6M category selection,
  narrowing root-cause candidates, and FMEA S/O/D scoring (§2, §4). Keep
  narrative answers (5W2H, Why chains) as free text — turning those into
  fixed options would lose information.

---

## Workflow (6 Steps)

Track progress by turning each step into a todo item.

### Step 1 — Problem Framing (5W2H, conversational)

Ask the 7 elements from `method.md §2` in order, **one at a time**: What / Where /
When / Who / Why (significance) / How / How much.

Once all 7 are collected, read back a problem statement for confirmation:
*"In X, since Y, at Z scale — is that right?"*

### Step 2 — Cause-Space Expansion (Fishbone/6M)

First, present the 6 categories from `method.md §3` (Man/Machine/Material/
Method/Measurement/Environment) via **AskUserQuestion (multiSelect)** and have
the user pick the ones that seem relevant in one shot (each option's description
gives a short definition of the category). **Encourage at least 2 selections** —
narrowing to just one defeats the whole point of this skill (preventing
single-path bias).

For each selected category, brainstorm possible causes with the user in free
text (category-level causes are narrative, so don't turn them into options).

### Step 3 — Parallel Tabular 5 Why

For each brainstormed category/candidate cause, run an independent "why?" chain
in parallel. No fixed 5 levels required — stop a chain once it reaches the
actionable-root-cause bar from `method.md §4` (controllable, correctable,
verifiable with data). If a chain stops too early at a surface symptom, push it
further.

### Step 4 — Narrow Candidates + FMEA Scoring

Present all derived root-cause candidates via **AskUserQuestion (multiSelect)**
and ask the user to narrow to the ones worth prioritizing (not an exhaustive
scoring pass). Put the candidate name in the option label and a short summary
of its Why chain in the description.

For each narrowed candidate, score Severity/Occurrence/Detection separately via
**AskUserQuestion (single-select)** — present the anchor points from
`method.md §5` (1/4/7/10, abbreviated to fit AskUserQuestion's 4-option limit)
directly as option label+description for the user to pick (no free-typed
numbers — scoring without anchored criteria breaks consistency). After scoring,
compute RPN (S×O×D) and sort descending.

### Step 5 — Verification and Corrective-Action Design

Starting from the highest-RPN cause, check evidence using the `method.md §6`
checklist (frequency data / timing match / condition contrast). If not all
three are confirmed, treat the cause as speculative and discuss how to gather
data before moving to corrective action. Only for causes with confirmed
evidence, co-design corrective actions with the user.

### Step 6 — Output Selection

**Right before generating anything**, ask the user for the format (use
AskUserQuestion):
- ⓐ **Markdown report** — a `.md` containing 5W2H, Fishbone (mermaid), the
  parallel 5 Why table, the FMEA (RPN) table, verification evidence, and
  corrective-action design
- ⓑ **Interactive HTML** — a web page (Artifact) visualizing the fishbone,
  the FMEA RPN chart, and verification badges

Fill in the matching skeleton from `references/output-templates.md`, following its
**writing-style principles** (write in the user's own language, avoid stiff
literal-translation phrasing, use complete narrative sentences instead of arrow
chains, add a short friendly intro/lead-in per section) — the output is
something the user reads and acts on, not a data dump:
- **ⓐ chosen** → save a `.md` file following the template.
- **ⓑ chosen** → load the `artifact-design` skill first, then deploy the HTML
  via the Artifact tool.

After generating, tell the user where the output was saved (path or URL).

---

## Don't

- Dump every question at once — it breaks the conversational-guidance intent.
- Lock in a root cause off a single candidate without checking other 6M
  categories — preventing single-path bias is this skill's whole reason for
  existing.
- Assign FMEA scores unilaterally without evidence — always judge against the
  anchor table together with the user.
- Skip the verification (evidence-check) step and jump straight to
  corrective-action design — preventing speculative confirmation is the point
  of this methodology.
- Decide the output format on your own — always ask the user in Step 6.
