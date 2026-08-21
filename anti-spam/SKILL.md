---
name: anti-spam
description: "Evergreen pass/fail gate that detects scaled-content and mass-generation signatures in AI-drafted blog posts BEFORE publishing — the patterns Google spam systems and LLMs actually penalize (templated skeletons, cluster duplication, publish bursts, programmatic footprints). Works for ANY website: point it at the draft plus the site's existing post corpus. Use on every AI-generated blog post and for cluster audits. Trigger phrases: 'anti spam', 'spam check', 'scaled content check', 'will this get penalized', 'mass-generated check'. Do NOT use for style/wording slop (use anti-slop) or fact accuracy (use accuracy-verifier) — this gate is about scale patterns, not sentences. If you maintain a site-tuned variant of this gate, use that instead when the site matches."
version: 1.1.2
---

# Anti Spam — Scaled-Content Signature Gate (any website)

Google and Bing do not penalize AI-generated content for being AI-generated, and no ranking treatment exists for AI watermarks (see your own provenance/watermark policy notes, if any). What gets penalized is **scaled content abuse**: clusters of pages that share templated skeletons, near-duplicate substance, machine publish cadence, and uniform commercial footprints — regardless of who or what wrote them. Cluster-scoring systems (S-CTS class) score the CLUSTER, so a post that is individually clean can still be penalized by the company it keeps. This gate checks both levels, on any site.

## Hard prohibitions (read first)
- **NEVER attempt to strip, launder, paraphrase-away, or otherwise defeat an AI watermark** (text watermark or C2PA metadata). It is model-level, carries no ranking penalty, and quality-destroying "humanizer" rewrites are the thing that IS penalized. This skill removes penalty-attracting *patterns*, never provenance marks.
- **Never claim the content is human-written.** The honest position is "human-reviewed and human-owned."
- This gate judges and reports; the maker rewrites. On FAIL, fix and re-run — do not ship on a promise.

## Input
A draft file path (or pasted draft) + the target site + where that site's existing post corpus lives. Cluster checks need the sibling corpus; acquire it by whichever applies:
- **Git-based site:** read post files from the REMOTE default branch (detached worktree of `origin/main` or equivalent) — never trust a local checkout that another session may have parked on a branch.
- **CMS site (WordPress etc.):** pull posts via the CMS REST API or read-only MCP tools.
- **No repo/API access:** pull the sitemap (parse `<loc>` with python `re.findall`, never `grep -c` — sitemaps are often one line) and fetch rendered pages.
If the corpus is unreachable, run the page-level checks and report the cluster checks as **NOT RUN** — never as passed. If the site has its own rules file or style guide, read it first; site rules override the generic thresholds below.

---

## Gate 1 — Verbatim duplication vs siblings (ceiling: 5%)
Compute 8-gram word-shingle overlap (strip HTML/markdown; exclude boilerplate the site legitimately repeats, e.g. a mandated disclosure block) between the draft and EVERY sibling post. Overlap = shared shingles / smaller doc.
- **FAIL** if any pair ≥5%. Report the pair and extract the shared shingle runs — they locate the copied passages.
- Fix = replace the shared passages with different **facts** (topic-specific mechanics, data, examples), not paraphrase. Shingles are verbatim-only, a floor; semantic scorers also catch paraphrased twins, so reworded template text still fails the spirit of this gate.
- Re-measure after fixing — de-templating passes have been observed to "complete" without actually changing the numbers. Where page templates inject shared blocks, measure RENDERED/built output, not source strings (rendered duplication has measured ~2x the source-level figure).

```python
# shingle sweep sketch
import re, itertools, pathlib
def shingles(t, n=8):
    w = re.sub(r'<[^>]+>|[#*`>\[\]()]', ' ', t).lower().split()
    return set(tuple(w[i:i+n]) for i in range(len(w)-n+1))
```

## Gate 2 — Structural skeleton (H2 fingerprint)
Extract the draft's H2s and compare against the sibling corpus histogram.
- **FAIL** if any of the draft's H2 strings (exact match) already appears on 3+ sibling posts, or if the draft shares ≥3 identical H2s with any single sibling.
- **Exemption:** headings that drive structured-data extraction keep their required shape (e.g. a parser that emits FAQPage JSON-LD from an H2 ending in "FAQs", or HowTo schema from "How to..."). Check the site's build code before renaming any schema-bearing heading — make such headings descriptive-but-conforming ("Social Media API FAQs"), never bare-template.
- Closer headings are the classic offender (audited sites have shipped one identical closer H2 on 60-94% of all posts). A closer's *function* is fine; its *name* must belong to this post.
- Vary the substance under the headings too — five distinct openings leading to one identical checklist is the same defect one level down.

## Gate 3 — Metadata and title footprint
- **FAIL** if the meta description shares its first 6 words with any sibling, exceeds ~150 chars, self-promotes the site's own product ("X is my pick", price hooks), or reuses a templated frame.
- **FAIL** if a numbered title repeats the cluster's dominant count (histogram the siblings; don't default every listicle to "7"). Vary the count to fit the real list.
- Anchor text for internal links must not repeat an exact-match anchor already used for the same target on other posts.

## Gate 4 — Publish cadence (the most machine-obvious signature)
Observed across production sites: walls of 9-15 posts on a single date, 21 posts in a 4-day window, and a 30x monthly discontinuity against a decade-long baseline. "Publish bursts inconsistent with human cadence" is an explicit cluster-scoring input, and a wall of one date is visible to anyone on the public blog index.
- **FAIL** if publishing this post puts >1 net-new post on today's date for this site (batch sessions are how bursts happen; pace daemons/crons at ~1/day).
- **FAIL** if the plan sets a future publish date, or back-dates/staggers dates to fake a cadence — both manufacture the footprint.
- Edits: a substantive full rewrite may reset the publish date (cap ~5 resets per site per day); lighter edits take the site's modified/updated date instead. Classify edit weight by reading the diff, not counting lines.

## Gate 5 — Commercial-pattern uniformity
- **Self-crowning:** if the site's own product is ranked #1 in a roundup/comparison, the entry MUST carry a genuine, post-specific limitation, with the qualifying condition fused into the same sentence as the recommendation (a lifted chunk must not travel without its condition). Read the caveat sentence alone, out of context — if it endorses a competitor instead, rewrite it. FAIL on a crown with no caveat, a caveat identical to a sibling's, or an off-criterion concession.
- **Wedge/angle dedup:** the draft's opening and its core argument may not reuse a sibling's wedge. FAIL on a shared opening-sentence shape across the cluster.
- **Link footprint:** every named tool/competitor gets a real external link (scale with list length); no lone commercial link padded by filler links; monetized links carry whatever disclosure the site's compliance rules require.
- **Thin/bloat band:** FAIL under 800 words (unless an explicitly sanctioned short genre for that site); flag if >40% over the live category average for that site.

## Gate 6 — Substance floor (what makes the page worth existing)
FAIL if the draft has none of: a firsthand/proprietary hook, original data or a verified primary-source fact competitors don't cite, real screenshots/assets, or a genuinely distinct POV. A clean-but-interchangeable page is what "scaled content abuse" describes; passing gates 1-5 with commodity content is still a fail here. (Facts themselves are an accuracy gate's job; this gate asks whether the page adds anything.)

---

## Output format

```
# Anti Spam Report — <slug> → <site>
Gate 1 Duplication:    PASS | FAIL (pairs + %) | NOT RUN
Gate 2 Skeleton:       PASS | FAIL (offending H2s)
Gate 3 Metadata:       PASS | FAIL (violation)
Gate 4 Cadence:        PASS | FAIL (today's count / date plan)
Gate 5 Commercial:     PASS | FAIL (which sub-check)
Gate 6 Substance:      PASS | FAIL (what's missing)
VERDICT: SHIP-ELIGIBLE | HOLD (fix list, ranked)
```

Any FAIL = HOLD. When run unattended (cron/batch): skip-on-doubt — a skipped publish costs nothing; a burst or template footprint compounds across the whole cluster. After fixes, re-run the failed gates against the real artifact (built/rendered output for template-driven sites, not source strings).

## Relationship to other gates
Run this LAST among content gates, before any final ship/no-ship judgment: style/slop gates check sentences, accuracy gates check facts, voice gates check register — anti-spam is the only gate that looks OUTSIDE the draft at the cluster and the calendar. Never assume another gate covered it: a post can pass every page-level gate and still be the 15th identical-skeleton post dated today.
