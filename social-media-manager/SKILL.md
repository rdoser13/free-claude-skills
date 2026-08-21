---
name: social-media-manager
description: Plug-and-play skill for writing high-performing social media captions for videos and images across every major platform. Works with any scheduler (Blotato, Buffer, Hootsuite, Metricool, Publer, Later) or manual posting. Fill in the [BRACKETED] sections with your brand voice and preferences.
model: claude-sonnet-4-6
---

# Social Media Manager

> **How to use this skill:** Replace every `[BRACKETED_PLACEHOLDER]` with your own info — brand voice, posting cadence, platforms you care about. That's it. This skill writes captions. *How* you post them (Blotato, Buffer, manual copy-paste) is up to you.

## What this Skill does
Takes a video or image and writes platform-optimized captions that actually earn attention. Handles hooks, body copy, closings, hashtags, character limits, and platform-specific quirks so you can copy-paste straight into your scheduler of choice — or hand them to any posting tool that accepts text + media.

**What this skill does NOT do:**
- It does not assume you use any specific scheduler
- It does not manage a content database or state file
- It does not auto-post (unless you layer a scheduler on top of it)

**Optional integrations:** If you use a scheduler with an MCP or API (Blotato, Buffer, etc.), you can chain this skill's output into that tool. See the "Optional: Hook Into a Scheduler" section at the bottom.

---

## Use this Skill when
- "Write captions for this video/image"
- "Turn this into posts for every platform"
- "Give me a caption pack for [content]"
- "Repurpose this for social"
- Any request where you need platform-ready social copy

---

## Platforms Covered

| Platform | Video | Image | Hashtags Help? | Character Limit |
|----------|-------|-------|----------------|-----------------|
| YouTube (Shorts) | ✅ | ❌ | ✅ | 5,000 (description) |
| TikTok | ✅ | ✅ | ✅ | 2,200 |
| Instagram (Reels/Posts/Carousels) | ✅ | ✅ | ✅ | 2,200 |
| Threads | ✅ | ✅ | ✅ | **500 (hard)** |
| LinkedIn | ✅ | ✅ | ❌ | 3,000 |
| X / Twitter | ✅ | ✅ | ❌ | **280 (hard)** |
| Facebook | ✅ | ✅ | ❌ | 63,206 |
| Pinterest | ✅ | ✅ | ✅ | 500 (description) |

> Remove rows for any platform you don't use. The two that matter most for character budgeting: **X (280)** and **Threads (500)**.

---

## The Two-Caption System

Instead of writing 6+ unique captions per post, write **two variants** and reuse:

### Caption A — Hashtag Platforms
**Use on:** YouTube, TikTok, Instagram, Threads, Pinterest

- **Hook:** [YOUR_HOOK_RULE — e.g., single punchy sentence, ≤12 words, curiosity or contrarian take]
- **Body:** [YOUR_BODY_RULE — e.g., 2–4 short paragraphs with proof or story]
- **Closing:** [YOUR_CLOSING_RULE — e.g., declarative reframe or sharp analogy, not a question]
- **Hashtags:** [YOUR_HASHTAG_COUNT — e.g., 4 relevant tags at the bottom]
- **Target length:** ≤500 chars so it works on Threads from one write. If longer, also produce a trimmed `caption_threads` version.

### Caption B — No-Hashtag Platforms
**Use on:** LinkedIn, X/Twitter, Facebook

- **Format:** [YOUR_B_RULE — e.g., single paragraph, 2–4 sentences, declarative hook, strategic reframe]
- **No hashtags.**
- **Target ≤280 chars** so it works on X and LinkedIn from the same write. If LinkedIn needs more room, write a longer LinkedIn version and a trimmed `caption_twitter` (≤280) separately.

---

## Content-Type Rules

### For Videos
- Write captions so they make sense *without* watching (80% will scroll past)
- Never say "watch this video" — the video is already attached
- For YouTube Shorts, also write an **SEO title** (≤60 chars, no periods, keyword-forward)
- If you have a transcript, mine it for the strongest line — that's often your hook

### For Single Images / Quote Cards
- Lead with the **insight**, don't describe what's in the image
- Don't repeat the quote verbatim — expand on it
- Shorter is usually better; let the visual do work

### For Carousels
- Hook should tease the **payoff of the last slide**
- Caption adds context the slides don't cover
- End with a line that rewards people who swiped through

### For Memes / Reactions
- Ultra-short caption
- Let the image carry the punchline
- No hashtag stuffing

---

## Mandatory Quality Gates (Before Delivering)

**1. Engagement test.** For every caption, ask: *"Would I stop scrolling and actually engage with this if I saw it on my feed?"* If the honest answer is no → rewrite. Boring-but-accurate fails.

**2. Brand voice check.** [PLUG IN YOUR VOICE/ANTI-SLOP RULES HERE — e.g., banned words, structural red flags, tone guardrails]

**3. Character count check.** Run this before presenting anything:
```python
checks = {
    "caption_a": (caption_a, 500),
    "caption_b": (caption_b, 280),
}
for name, (text, limit) in checks.items():
    status = "OK" if len(text) <= limit else f"OVER by {len(text) - limit}"
    print(f"{name}: {len(text)} chars [{status}]")
```
If either fails, **fix before presenting**. Do not hand the user broken captions.

---

## Standard Output Format

When you finish a caption pack, present it like this so it's copy-paste friendly:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📹 [Content title or filename]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎬 YOUTUBE TITLE (if video):
[Title here — 58 chars]

📝 CAPTION A (YouTube / TikTok / Instagram / Threads / Pinterest):
[Full caption with hashtags]
— 487 chars

📝 CAPTION B (LinkedIn / X / Facebook):
[Full caption, no hashtags]
— 268 chars

🧵 THREADS OVERRIDE (only if Caption A > 500):
[Trimmed version]
— 498 chars

🐦 X OVERRIDE (only if Caption B > 280):
[Trimmed version]
— 278 chars
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

This format works whether the user is pasting into Blotato, Buffer, Metricool, Publer, Later, or a Google Doc for manual posting.

---

## Workflow

### Step 1 — Intake
Ask the user only for what's missing:
- The content (video file, image file, public URL, or transcript)
- Topic/context if it's not obvious
- Any platforms to skip
- Any must-include keywords, links, or CTAs

### Step 2 — Generate
For each piece of content:
1. Write `caption_a` and `caption_b`
2. If video → also write a YouTube title
3. If Caption A > 500 chars → write `caption_threads`
4. If LinkedIn version > 280 chars → write `caption_twitter`
5. Run the three quality gates
6. Fix anything that fails before moving on

### Step 3 — Deliver
Present using the Standard Output Format above. The user takes it from there — pasting into their scheduler, editing, or posting manually.

### Step 4 (Optional) — Iterate
If the user pushes back on voice, hook, or angle: rewrite the specific caption, re-run the quality gates, re-present. Don't rewrite what wasn't flagged.

---

## Caption Character Limits Reference

| Platform | Limit | Why it matters |
|----------|-------|----------------|
| **X/Twitter** | 280 | Hard limit. Even with media attached. Most schedulers hard-reject. |
| **Threads** | 500 | Hard limit. Most schedulers hard-reject. |
| Pinterest | 500 | Description field |
| Instagram | 2,200 | |
| TikTok | 2,200 | |
| LinkedIn | 3,000 | |
| YouTube | 5,000 | Description field |
| Facebook | 63,206 | Effectively unlimited |

**Posting logic rule of thumb:**
- Threads → use `caption_threads` if it exists, else `caption_a`
- X/Twitter → use `caption_twitter` if it exists, else `caption_b`

---

## Optional: Hook Into a Scheduler

If the user wants this skill to *also* schedule the posts (not just write them), they'll need to plug in a scheduler. Common options:

- **Blotato** (has an MCP — easiest for Claude Code users)
- **Buffer** (API)
- **Publer / Metricool / Later** (API)
- **Make.com / Zapier** (webhook bridge to anything)
- **Manual** (just copy-paste from the output)

When a scheduler is connected, extend Step 3 with:
1. Ask the user for post date/time (convert to UTC)
2. Loop through platforms and post via the scheduler's tools/API
3. Return the resulting post IDs or URLs to the user
4. Handle per-platform errors gracefully — log failures, continue the rest, report at the end

**Pro tip:** Keep caption generation and scheduling as separate concerns. The captions are the valuable artifact. Scheduling is just plumbing.

---

## First-Run Checklist

- [ ] Filled in `[YOUR_HOOK_RULE]`, `[YOUR_BODY_RULE]`, `[YOUR_CLOSING_RULE]`, `[YOUR_HASHTAG_COUNT]` for Caption A
- [ ] Filled in `[YOUR_B_RULE]` for Caption B
- [ ] Added your brand voice / anti-slop rules to the Quality Gates section
- [ ] Removed any platforms you don't use from the platform tables
- [ ] Decided whether you want this to just write captions (default) or also schedule them (optional section)
