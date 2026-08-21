---
name: skill-auto-improve
description: "Passive skill improvement system that runs silently during normal skill use. NOT user-invocable — this is an internal behavior directive. Claude evaluates every skill output against the skill's own rules, logs failure patterns, and automatically patches skills when 3+ similar failures accumulate. No dashboard, no test runs — real usage is the test suite."
user-invocable: false
disable-model-invocation: false
---

# Skill Auto-Improve

This is not a skill you run. It's a behavior you follow every time you execute any skill.

---

## the rule

After delivering output from ANY skill, silently evaluate that output against the skill's own instructions. If something failed, log it. When failures pile up, fix the skill. That's it.

---

## what counts as a failure

A failure is when the output violates the skill's own rules or the user rejects/corrects the output. Specifically:

1. **Skill rule violation** — the output breaks an explicit instruction in the skill (e.g., skill says "never use semicolons" and the output has semicolons)
2. **User correction** — the user says "no, redo this," "that's wrong," "change X to Y," or otherwise rejects the output
3. **User edit-after-delivery** — the user accepts the output but immediately asks for specific changes that the skill should have handled
4. **Repeated manual instruction** — the user gives the same guidance that isn't in the skill (e.g., they keep saying "make it shorter" every time you run the email skill)

**What is NOT a failure:**
- User changes their mind about the brief (that's a scope change, not a skill failure)
- Output is correct but the user wants a different creative direction
- One-off edge cases that won't recur

---

## step 1: silent eval (every skill run)

After delivering skill output, do a quick internal check — do NOT output this to the user:

1. Re-read the skill's key rules (you already have them in context)
2. Check: did the output follow every rule?
3. Check: did the user accept the output without corrections?

If everything passed — done. Move on. No logging needed.

If something failed — go to step 2.

---

## step 2: log the failure

Write a single line to the skill's improvement log. The log lives at:

```
[skill-folder]/improvements.log
```

Create the file if it doesn't exist. Each line is a single failure entry:

```
[date] | [failure type] | [what failed] | [what the skill says vs what happened]
```

**Example entries:**

```
2026-03-17 | rule violation | output used "delve" | Anti-slop list prohibits "delve" but it appeared in paragraph 3
2026-03-17 | user correction | user said "too long" | Skill says 1200-1500 words, output was 1,847 words
2026-03-18 | repeated instruction | user said "add more line breaks" | Skill has no rule about line break frequency
2026-03-19 | user correction | user said "don't start with a question" | Skill has no rule about opening patterns
```

Keep entries short. One line per failure. No paragraphs.

---

## step 3: check if a fix is needed

After logging a failure, scan the full `improvements.log` for that skill. Count similar failures.

**Fix threshold: 3+ similar failures.**

"Similar" means the same root cause — not identical wording, but the same underlying problem. Examples:

- "too long" + "way too wordy" + "cut this down" = 3 similar failures (verbosity)
- "used delve" + "used vibrant" + "used landscape" = 3 similar failures (banned words slipping through)
- "no line breaks" + "wall of text" + "add spacing" = 3 similar failures (formatting density)

If fewer than 3 similar failures — stop. Don't fix yet. The pattern hasn't proven itself.

If 3+ similar failures — go to step 4.

---

## step 4: patch the skill

Make ONE targeted change to the skill file. Follow these rules:

**What to change:**
- Add a specific instruction that addresses the failure pattern
- Tighten a vague instruction to be more explicit
- Add an anti-pattern ("Do NOT...") for a recurring mistake
- Move a buried instruction higher if it's being ignored due to position
- Add a concrete example showing the correct behavior

**What NOT to change:**
- Don't rewrite the skill from scratch
- Don't change multiple things at once
- Don't add vague instructions ("be better at formatting")
- Don't make the skill longer without a specific reason
- Don't touch parts of the skill that are working fine

**After patching:**

1. Add a brief note at the bottom of `improvements.log`:

```
--- FIX APPLIED [date] ---
Problem: [one sentence describing the pattern]
Change: [one sentence describing what was added/changed in the skill]
Location: [which section of the skill was modified]
---
```

2. Clear the resolved failure entries from the log (delete the lines that this fix addresses) so they don't trigger another fix later.

3. Tell the user in ONE line what you did:

> "Updated [Skill Name]: added rule about [X] based on [N] recent failures."

That's it. Don't ask for approval. Don't explain at length. Just inform and move on.

---

## when NOT to auto-fix

- **The failure is ambiguous** — you're not sure if it's a skill problem or a one-off. Wait for more data.
- **The fix would contradict another rule in the skill** — flag it to the user instead of creating a conflict.
- **The skill is working well overall** — 1-2 failures across dozens of runs is noise, not signal. Don't over-optimize.
- **The fix would make the skill significantly longer** — if the skill is already near the 500-line limit, consider tightening existing rules instead of adding new ones.

---

## the test

This system is working if:

1. Skills get slightly better over time without you asking
2. You stop having to give the same correction twice
3. Fixes are small, targeted, and don't break other things
4. The improvements.log stays short (failures get resolved, not accumulated)
5. You barely notice this is happening — it's just background maintenance
