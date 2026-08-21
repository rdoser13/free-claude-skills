---
name: anti-slop
description: Detects and removes AI-generated fluff from content. Use when reviewing drafts, cleaning AI output, or enforcing a brand voice. Flags issues and rewrites.
---

Scan content for AI slop—overused words, phrases, and structural patterns that signal lazy AI output. Flag every instance, then provide a clean rewrite.

# Input

Accept either:
- Pasted text (user provides content directly)
- File path (read and analyze the file)

If no content provided, ask for it.

---

# Part 1: Structural Red Flags

## Red Flag #1: Binary Contrast Addiction

AI can't resist "it's not X, it's Y":
- "success isn't about working hard, it's about working smart"
- "content isn't about quantity, it's about quality"
- "marketing isn't selling, it's storytelling"

**Fix:** Say what you mean directly. Use specific details instead of broad contrasts.

## Red Flag #2: Triple Threat Syndrome

AI groups things in threes everywhere:
- "fast, efficient, reliable"
- "boost engagement, increase conversions, maximize roi"
- "powerful, simple, transformative"

**Fix:** Vary your rhythm. Sometimes two. Sometimes four. Sometimes just one.

## Red Flag #3: Infomercial Transitions

Cringe questions AI thinks create "engagement":
- "the catch?"
- "want to know the secret?"
- "the brutal truth?"
- "here's the kicker"

**Fix:** If you wouldn't say it in real conversation, don't write it.

## Red Flag #4: Corporate Verb Disease

Stuffy -ing verbs:
- "...highlighting the benefits..."
- "...emphasizing critical importance..."
- "...facilitating better outcomes..."

**Fix:** Use simple, active verbs. "show" not "highlighting." "help" not "facilitating."

## Red Flag #5: Hedging Language

AI loves to clear its throat:
- "it's worth considering..."
- "you might want to think about..."
- "it's important to note that..."

**Fix:** State your opinion. Skip the diplomatic warm-up.

## Red Flag #6: Thesaurus Abuse

Fancy words that should be simple:
- "utilize" → use
- "execute" → do
- "facilitate" → help
- "implement" → start
- "optimize" → improve
- "leverage" → use

**Fix:** Write like you talk.

---

# Part 2: Formatting Giveaways

## Red Flag #7: Arrow Obsession

AI discovered → and won't let go:
- → 10x your results
- → scale faster than ever
- → join today

**Fix:** Use arrows sparingly. One per post maximum.

## Red Flag #8: Emoji Explosion

ChatGPT treats emojis like confetti:
- 🚀 boost productivity now!
- 💡 revolutionary new approach!
- ⭐ transform your business!

**Fix:** One emoji per section. Maybe. Or none.

## Red Flag #9: Em Dash Overdose

AI loves: "this approach—which many experts recommend—can transform your business—if you're willing to put in the work—and see real results."

**Fix:** Mix your punctuation. Commas exist. Periods too.

---

# Part 3: Phrase Patterns That Scream "Robot"

## Pattern #1: "No X. No Y. Just Z."

- "no fluff. no theory. just actionable insights."
- "no gimmicks. no shortcuts. just results."

**Fix:** Literally any other sentence structure.

## Pattern #2: "The game has changed"

And its cousins:
- "game-changer"
- "supercharge your [thing]"
- "this changed everything"

**Fix:** Describe actual change without hyperbole.

## Pattern #3: "Real" Overload

"just real strategy from real experts getting real results with real entrepreneurs."

**Fix:** Show authenticity through specific examples, not by repeating "real."

## Pattern #4: The Serious Pitch

"if you're serious about [goal], let's [cta]"

Every AI-written CTA uses this exact structure.

**Fix:** Vary your calls to action. Be specific about what happens next.

## Pattern #5: "To Your Success"

Email sign-offs like this instantly reveal AI authorship.

**Fix:** Sign off like a human. "cheers," "talk soon," or just your name.

## Pattern #6: Profound But Obvious

"not because of X. but because of Y"
- "i didn't succeed because of luck. but because of hard work."

**Fix:** If everyone already knows it, don't package it as insight.

## Pattern #7: Short Hook Questions

- "the best part?"
- "want access?"
- "ready to level up?"

**Fix:** Ask real questions that require thought to answer.

## Pattern #8: "Enter: [Thing]"

- "enter: my revolutionary framework"
- "enter: the solution you've been searching for"

**Fix:** Just introduce the thing normally.

## Pattern #9: "Stopped Me in My Tracks"

"yesterday my mentor said something that stopped me in my tracks:"

**Fix:** Describe actual impact without melodrama.

---

# Part 4: Content Red Flags

## Red Flag #10: Symbol Obsession

AI loves telling you what things "represent" instead of what happened:
- "this symbolizes..."
- "which reflects..."
- "emphasizing the importance of..."

**Fix:** Say what happened. Say what you learned. Skip the literary analysis.

## Red Flag #11: The Generic Case Study

When AI lacks real data, it invents people. Usually named Sarah Chen.

**Fix:** Use actual examples from your life. Real names (with permission). Real numbers.

## Red Flag #12: Everything Changed

- "the strategy that changed everything"
- "this one shift transformed my entire business"

**Fix:** Describe specific changes with specific metrics.

---

# Slop Word List

**Single words to flag:**
delve, tapestry, vibrant, landscape, realm, embark, excels, vital, comprehensive, intricate, pivotal, moreover, arguably, notably, spark, sparked, supercharge, supercharged, enhance, navigate, ignite, ignited, robust, multi-faceted, solely, crucial, ensure, portray, ongoing, vigilance, intriguing, holistic, game-changer, revolutionary, unleash, cutting-edge, synergy, seamlessly, transformative

**Phrases to flag:**
- "Dive into..."
- "Silver bullet"
- "Unlock your potential"
- "It's important to note / remember"
- "Important to consider"
- "Based on the information provided"
- "Remember that"
- "Navigating the landscape of / complexities of"
- "Delving into the intricacies"
- "A testament to"
- "It's worth considering"
- "You might want to think about"
- "The catch?"
- "Want to know the secret?"
- "The brutal truth?"
- "Here's the kicker"
- "The best part?"
- "Ready to level up?"
- "Enter:"
- "Stopped me in my tracks"
- "Changed everything"
- "To your success"
- "If you're serious about"
- "No X. No Y. Just Z." structure

**Structural patterns to flag:**
- Starting social posts with "I"
- Excessive exclamation points (more than 1)
- Semicolons (never use)
- More than 2 em dashes per paragraph
- More than 1 arrow (→) per post
- More than 2 emojis per section
- Binary contrast structure overuse ("it's not X, it's Y")
- Triple groupings in every list

---

# Output Format

## 1. Slop Report

List every instance found by category:

**Slop Words:**
```
[word] — "[context snippet]"
```

**Phrase Patterns:**
```
[pattern name] — "[context snippet]"
```

**Structural Issues:**
```
[issue type] — "[description]"
```

**Total:** X issues found

## 2. Clean Rewrite

Rewrite following the brand voice (if a voice/style guide is available, follow it; otherwise default to the rules below):
- Punchy, plainspoken, confident
- Short sentences (8-15 words average)
- Active voice, subject-verb-object
- 8th-grade reading level
- Short paragraphs (2-3 sentences max)
- Lead with the point
- Specific examples over vague claims
- Write like you talk

---

# Example

**Input:**
"It's important to note that we need to delve into the comprehensive landscape of AI tools to unlock your marketing potential. The best part? This game-changing approach will supercharge your results."

**Slop Report:**

**Slop Words:**
- `delve` — "delve into the comprehensive"
- `comprehensive` — "the comprehensive landscape"
- `landscape` — "comprehensive landscape of AI"
- `supercharge` — "supercharge your results"
- `game-changing` — "game-changing approach"

**Phrase Patterns:**
- `Hedging Language` — "It's important to note that"
- `Unlock your potential` — "unlock your marketing potential"
- `Short Hook Question` — "The best part?"

**Total:** 8 issues found

**Clean Rewrite:**
"Here's what you need to know about AI marketing tools. Pick two. Test them for a week. Keep the one that saves you time."
