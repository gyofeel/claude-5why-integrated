# Output Templates

At the output-selection step (Step 6), fill in the skeleton below matching the format the
user chose.

## Writing-Style Principles (avoid literal-translation phrasing, write naturally)

The output is **something written for the user to read**, not an analysis tool dump. Follow
these principles without exception — even correct data loses its value if the phrasing is
stiff or reads like a literal translation.

- **Don't use the English labels verbatim.** The 5W2H / 6M item names in `method.md`
  (What/Where/Man/Machine, etc.) are internal judgment labels only. In the output, rephrase
  them naturally in the user's own language — not a mechanical word-for-word translation. If
  the user writes in English, still prefer a natural phrasing over the bare category name
  (e.g., "What's going on" rather than a bare "What").
- **Write as narrative sentences, not arrow/symbol chains.** A list like `A → B → C` forces
  the reader to re-interpret it. Spell out the causal chain as flowing sentences — e.g., "We
  asked why, and it turned out to be because ..." — instead.
- **Open each section with a short lead-in.** One or two natural sentences on why this step
  exists, so sections don't feel disconnected from each other.
- **Use a friendly tone.** Write as if explaining directly to the user, not in a stiff report
  register. Open with a brief, welcoming line about what the report is for, and close with an
  encouraging note on what to do next.
- **Table headers in natural language too.** Terms like Severity/Occurrence/Detection/RPN
  should be rendered in the user's language (e.g., "severity / how often / how hard to
  catch / risk score"), with the original term parenthesized once if useful.
- **Don't drop rejected causes silently.** For any candidate that verification rejected,
  note in one sentence why it wasn't the real cause and which surviving cause it folds into
  — so the user never has to ask "wait, what happened to that one?"

---

## ⓐ Markdown Report

Save as `{topic}-5why-integrated-analysis.md` (in the working folder, or wherever the user
specifies). Keep the section order and narrative tone below, but render every label and
sentence naturally in the user's own language per the writing-style principles above — the
English text here is an illustrative example, not fixed wording to copy.

```markdown
# {topic} — Integrated 5 Why Analysis Report

{One or two friendly opening sentences on what this report is for}

## 1. What's the Problem? (5W2H)

| Item | Details |
|---|---|
| What's going on | {…} |
| Where | {…} |
| Since when · how often | {…} |
| Who | {…} |
| Why it matters | {…} |
| How it happens | {…} |
| How big a deal | {…} |

## 2. Casting a Wide Net for Causes (Fishbone/6M)

{One sentence on why several categories were explored instead of drilling into just one}

```mermaid
graph LR
    P[{the problem}]
    Man[People] --> P
    Method[Method] --> P
    Measurement[Measurement] --> P
    Environment[Environment] --> P
    Man1["{cause candidate, as a natural phrase}"] --> Man
    Method1["{cause candidate}"] --> Method
```

(Include only the categories actually brainstormed; omit any that were skipped. Node ids
can stay in English, but the label text should read naturally in the user's language.)

## 3. Digging Into Each Cause with "Why?"

{One sentence noting these went past surface symptoms down to something actionable}

| Angle | How we traced it | Root cause we landed on |
|---|---|---|
| {category} | {Narrative sentences repeating "we asked why, and it turned out ..." from the symptom down. If a chain hits something uncontrollable (e.g., personality), say so briefly and stop there.} | {the actionable cause, as a complete sentence} |
| {category, rejected after verification} | {…} | (confirmed not to be the real cause — state which cause it folds into) |

## 4. Which Cause to Tackle First (FMEA Priority)

{One sentence on why these got scored and ranked — and briefly what the score means}

| Root cause | Severity | How often | How hard to catch | Risk score (RPN) | Rank |
|---|---|---|---|---|---|
| {…} | {1–10} | {1–10} | {1–10} | {S×O×D} | #1 |
| {…} | {1–10} | {1–10} | {1–10} | {S×O×D} | #2 |

## 5. Checking Whether It's Really the Cause

{One sentence on why this step exists — to avoid confirming a cause on a guess}

| Cause | How often it actually happened | Does the timing line up? | Does it differ with/without this cause? | Verdict |
|---|---|---|---|---|
| {…} | {…} | {…} | {…} | ✅ Confirmed / ⚠️ Needs more evidence / ⚠️ Not the real cause |

## 6. So, What Should We Do?

{One sentence noting these are the corrective actions agreed on, in priority order}

**#1 — {cause} (risk score {RPN})**
- **{action name}**: {a natural sentence on why this helps}

**Also worth noting**
- {why any rejected cause wasn't it, and which surviving cause it folds into}
- {if any cause was set aside from scoring, mention it can be revisited later}
```

---

## ⓑ Interactive HTML (Artifact)

Load the `artifact-design` skill first, then build it, and deploy via the Artifact tool. The
"Writing-Style Principles" above apply equally to the copy inside cards and badges — don't
expose raw English abbreviations as labels; write short but natural phrases instead.

**Required components**
1. **Problem-definition card**: show the 5W2H elements as cards/a table (labels in natural language).
2. **Fishbone diagram**: build the actual fishbone shape with custom CSS/SVG (not mermaid) —
   categories branch diagonally off a central spine, with cause candidates as child nodes on
   each branch. Category names in natural language too.
3. **Parallel 5 Why tree/table**: category chains as an accordion or table, written as short
   narrative sentences rather than arrow lists. Highlight the terminal node (root-cause candidate).
4. **FMEA risk-score sorted bar chart or table**: sorted descending by risk score (RPN), with
   top items highlighted. Show the individual severity/occurrence/detection values with
   natural-language labels too.
5. **Verification badges**: per cause, a ✅ (confirmed) / ⚠️ (needs more evidence, or not the
   cause) badge plus a short reason.

**Style rules**
- Self-contained: all CSS/JS inline, no external requests.
- Support both light and dark themes (`prefers-color-scheme` + `data-theme`).
- Responsive: tables/diagrams scroll inside an `overflow-x:auto` container. No horizontal
  scroll on the body.
- `<title>` = "{topic} — Integrated 5 Why Analysis"; example favicon emoji: 🐟 (fishbone) or 🔍.
