# 5why-integrated

An interview-driven skill that fixes the two classic failure modes of the 5 Whys — single-path bias and irreproducibility — by combining it with 5W2H, Fishbone/6M, and FMEA.

You describe a problem and the skill walks you through it one question at a time: framing it with 5W2H, expanding the cause space across the six Fishbone categories (Man/Machine/Material/Method/Measurement/Environment), tracing an independent Why-chain per category instead of one linear guess, scoring the resulting candidates with FMEA (Severity × Occurrence × Detection → RPN), and checking each top candidate against real evidence before it lets you move to corrective-action design.

> Language-agnostic: the skill's own instructions are written in English, but it interviews and reports in whatever language you use.

## Why

- **No single-path bias** — causes are brainstormed across independent Fishbone categories before any Why-chain starts, instead of picking one and drilling down blind.
- **No guessed root cause** — every top-RPN candidate is checked against frequency data, timing match, and condition contrast before it becomes a corrective action.
- **Prioritized, not just listed** — FMEA (Severity/Occurrence/Detection → RPN) ranks root-cause candidates instead of treating them as equally important.
- **You pick the output** — right before generating, it asks for a Markdown report, a PDF, or a format you describe yourself, so the deliverable fits how you'll use it.

## Pipeline

1. **Problem framing (5W2H)** — What / Where / When / Who / Why / How / How much, asked one at a time.
2. **Cause-space expansion (Fishbone/6M)** — pick relevant categories (Man/Machine/Material/Method/Measurement/Environment), brainstorm causes per category.
3. **Parallel multi-path 5 Why** — an independent Why-chain per candidate cause, stopping at an actionable, verifiable root cause instead of forcing exactly 5 levels.
4. **FMEA scoring** — narrow to priority candidates, score Severity/Occurrence/Detection (1–10 anchored scale), rank by RPN.
5. **Verification & corrective-action design** — check frequency/timing/condition evidence for top-RPN causes before designing fixes.
6. **Deliverable** — choose a Markdown report, a PDF, or a format you describe (e.g. interactive HTML); it generates and hands back the location.

## Install

In Claude Code:

```
/plugin marketplace add gyofeel/claude-5why-integrated
/plugin install 5why-integrated@claude-5why-integrated
```

## What's inside

```
skills/5why-integrated/
├── SKILL.md
└── references/
    ├── method.md            # 5W2H/6M/FMEA theory + scoring anchors + verification checklist
    └── output-templates.md  # Markdown/PDF report skeleton + custom-format (e.g. HTML) build guide
```

## License

MIT — see [LICENSE](LICENSE).
