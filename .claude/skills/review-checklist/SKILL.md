---
name: review-checklist
description: Reviews a product brief against a fixed six-point checklist (owner, success measure, problem before fix, scope match, success metric, timeline) before it goes any further. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief file or wiki page and asks for the usual check.
---

# Review checklist

Run the same check on any brief, every time. The user points at a brief (a file path, a wiki page, or pasted text). Read all of it first, then check each item below.

## The checks

1. **Owner.** The brief names one person who owns it. A team, a role with no name, or "TBD" fails.
2. **How we'll know it worked.** The brief says what outcome would show success, in plain terms, not just what will be built.
3. **Scope matches.** Compare the scope stated at the start (goals, summary, "in scope") with what the end commits to (requirements, rollout, next steps). Flag anything added, dropped, or reworded so it means something different.
4. **Problem before fix.** The problem is explained, with evidence where it exists, before any solution appears. Fail it if the fix comes first, or the problem is only implied by the fix.
5. **Success metric.** A named metric with a baseline (where it is now) and a target (where it should get to). A metric with no baseline fails; say so.
6. **Timeline.** Dates or a release/quarter, with at least one milestone. "Soon" or "next quarter" with nothing behind it is a partial pass at best.

## How to review

- Judge only what the brief says. Do not fill gaps from other sources or assume something is covered because it ought to be.
- For each check give a verdict: **Pass**, **Partial**, or **Fail**, plus one line of evidence: quote or point to the section. For Partial or Fail, say what is missing.
- Do not rewrite the brief or invent the missing owner, metric, or dates. Say what is needed and who could supply it, if the brief or the user's context makes that clear.

## Output

Use this shape every time:

```
Brief: <title or path>

| # | Check | Verdict | Evidence / what's missing |
|---|-------|---------|---------------------------|
| 1 | Owner | ... | ... |
| 2 | How we'll know it worked | ... | ... |
| 3 | Scope matches | ... | ... |
| 4 | Problem before fix | ... | ... |
| 5 | Success metric | ... | ... |
| 6 | Timeline | ... | ... |

Result: <n> of 6 pass.
Fix first: <the one or two gaps that matter most, in order>
```

Keep it to one screen. End there; no extra commentary.
