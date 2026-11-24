---
name: software-deal-checker
description: Checks whether a software or SaaS deal, discount or pricing plan is actually worth it, and researches software purchases before you pay. It works out the real cost over 24 months, finds what the plan renews at, reads the cancel and refund terms, compares tools on true cost, shortlists options for a job, and sets up an AI assistant task that watches pricing pages and reminds you before a trial or discount renews. Use it whenever someone asks "is this deal good", "is this Black Friday / Cyber Monday / lifetime deal worth it", "what will this tool really cost me", "compare the pricing of X and Y", "which plan should I buy", "find me the best tool for X under $Y", "when does this renew", or wants to cut, audit or renegotiate software subscriptions, even if they never say "deal" or "skill". Also use it for AppSumo-style lifetime deals, annual vs monthly decisions, seat-based pricing, usage or credit-based pricing, and renewal reminders.
---

# Software Deal Checker

Most software deals are judged on the banner: "50% off". The banner is the least useful number on the page. What matters is what you pay over the time you will actually use the tool, what it renews at, and how hard it is to leave. This skill makes the agent read the pricing pages, do the math in the open, and say "not stated" instead of guessing.

It works for a Black Friday sale, but it is just as useful in March when a trial is about to convert, or when a team is deciding between two tools.

## The rules that make this work

1. **Use the pages, not memory.** Prices change constantly, and a model's training data is out of date the day it ships. Read the live offer page and the normal pricing page, or ask the user to paste them. If neither is available, say so and stop. A confident wrong price is worse than no answer.
2. **"Not stated" is a valid answer.** When a page doesn't say what a plan renews at, whether the discount is first-year only, or how to cancel, write "not stated". Never fill the gap with what is typical. The gaps are often the most important finding, because they are where year two gets expensive.
3. **Show the math.** Every total gets its line items: date, amount, what it covers. Anyone should be able to check it with a calculator.
4. **Compare against normal annual billing, not the "was" price.** A banner's crossed-out price is usually the monthly rate times twelve. Many "Black Friday" deals are the normal annual discount with a costume on.
5. **Price the plan the person will actually use.** Seats, usage limits, credits and billing period change the answer more than the discount does. A big discount on a tier they outgrow by month four saves nothing.
6. **Never buy, sign up or enter payment details.** This skill researches and recommends. The person clicks buy.
7. **Pages can hide things from agents.** Offers sometimes live in popups, banners rendered by scripts, or checkout-only codes that a page fetch never sees. If a page looks incomplete, say what you could and couldn't see, and tell the person to confirm the price at checkout.

## What to ask for first

Before doing any math, get these. Ask in one short message, and only for what's missing:

- **The tool(s)** and, ideally, links to the offer page and the normal pricing page (or pasted text from both)
- **The plan they'd use:** tier, number of seats, monthly or annual, and any usage they expect (credits, contacts, minutes, projects)
- **How long they expect to use it.** Default to 24 months if they don't know, since that captures one full renewal on an annual plan.
- **What it replaces**, if anything. A tool that replaces another bill is judged on the net cost.

## Mode 1: Check one deal

Use this when someone has a specific offer in front of them.

Work through these in order and report in this format:

```
DEAL: [tool, plan, the offer in one line, end date if stated]

WHAT'S DISCOUNTED
- Plans and billing period it applies to
- New customers only? First term only? Add-ons, credits or bonus months?

24-MONTH COST ON THIS DEAL
- [date] [amount] [what it covers]
- ...
- Total: $X

SAME 24 MONTHS AT NORMAL PRICES
- Monthly billing: $X
- Annual billing: $X

RENEWAL AND EXIT
- Renews at: [price, or "not stated"]
- Auto-renews: [yes / no / not stated]
- How to cancel: [steps, or "not stated"]
- Refund window: [terms, or "not stated"]

VERDICT: [Real deal | Normal annual discount in a costume | Depends on how you buy | Skip | Not enough information]
[One or two sentences on why, naming the single number that decided it.]
```

How to pick the verdict:
- **Real deal:** the 24-month total beats normal annual billing by a meaningful amount, and the renewal price is stated.
- **Normal annual discount in a costume:** the "deal" price is about what annual billing costs anyway.
- **Depends on how you buy:** the value only shows up for some buyers (bonus credit you may not spend, extra months that may extend the term instead of lowering the price, a code that only applies to some plans).
- **Skip:** the person doesn't need the tool, would buy the wrong tier to get the discount, or the year-two cost wipes out the saving.
- **Not enough information:** the pages leave out something that changes the answer. Say exactly what to ask the vendor.

## Mode 2: Compare tools on true cost

Use this when someone is choosing between two or more tools for the same job.

1. Confirm all the tools can actually do the job the person described. A cheap tool missing a must-have feature is not a cheaper option.
2. Price each one on the same plan size, the same billing period and the same 24 months.
3. Include the costs people forget: extra seats, overage or credit top-ups, required add-ons, migration or setup fees, and anything it replaces.
4. Present a table, then a pick:

```
| Tool | Plan priced | 24-month total | Renews at | Cancel terms | Missing for this job |
|------|-------------|----------------|-----------|--------------|----------------------|

PICK: [tool], because [one reason tied to their use]. [The trade-off they're accepting.]
```

Take a side. A neutral spec sheet makes the person do the work the skill exists to do.

## Mode 3: Research the best option for a job

Use this when someone says "find me a tool for X" or "what's the best X under $Y".

1. Restate the job and the must-haves in one line, and confirm the budget and team size.
2. Build a shortlist of 3-5 tools from sources you can open (the vendors' own sites, docs, and independent reviews). Say where each candidate came from.
3. Read each tool's pricing page, then run Mode 2 on the shortlist.
4. Flag anything you couldn't verify. "Their pricing page requires a demo call" is a finding, not a gap to paper over.

Don't recommend a tool on reputation alone. If you can't open its pricing page or docs, it doesn't make the shortlist.

## Mode 4: Watch prices and set renewal reminders

Personal AI assistants with scheduled tasks can do the boring part, checking pages every day and reminding people before they get charged. Claude, ChatGPT, Gemini and Meta Muse all offer some form of scheduled or recurring task. What each one can do on a schedule (open a web page, send an email, push a phone notification) varies by assistant and plan, so tell the person to run the task once by hand before trusting it.

Offer this scheduled task for watching deals:

```
Every morning at 8 a.m. [time zone] until [end date], open these pages:
[pricing or deal page 1]
[pricing or deal page 2]
On the first run, write down each page's price, plan and end date.
On every run after that, compare with the last run and message me only
if something changed. Quote the exact line from the page. If a page
won't load or hides the price two days in a row, tell me instead of
guessing. Never buy anything or enter payment details.
```

And this one for renewals and trials:

```
[3 days] before [date], remind me that [tool] renews at [price] on [date].
Include the cancel link or steps: [paste them]. Ask me one question:
keep it, downgrade it, or cancel it?
```

Two limits to tell the person:
- The assistant needs to remember the last run to spot a change. If it can't keep notes between runs, have it save each run to a doc or note it can reread.
- A daily check uses part of the assistant's usage limits. Treat every alert as "go look", then confirm on the vendor's page before paying.

## Mode 5: Audit current subscriptions

Use this when someone wants to cut their software bill.

1. Get the list: tool, plan, price, billing period, renewal date. A card statement or the receipts folder in their inbox is the fastest source.
2. For each one, ask what it does that nothing else on the list does, and when they last used it.
3. Sort into **keep**, **downgrade** (a cheaper tier covers their actual use), **consolidate** (another tool they pay for already does this) and **cancel**.
4. Total the monthly and yearly savings, then offer to set Mode 4 renewal reminders for anything they're unsure about.

## Lifetime deals

Lifetime deals (AppSumo and similar) need extra checks, because "lifetime" means the lifetime of the product, not the buyer:
- What happens to lifetime buyers if the company changes plans, gets acquired or shuts down? Check the terms.
- Are usage limits, seats or future features capped for lifetime buyers?
- How long has the company existed, and when did the product last ship an update?
- Is there a refund window, and how long is it?

Verdict guidance: a lifetime deal is good when the person would use the tool for longer than the break-even point against the normal plan, and the product looks likely to be around that long. Say what the break-even month is.

## Before you hand it over

Check the output against this list:
- Every price came from a page you read or text the person pasted, and you said which.
- Every total shows its line items.
- Every unknown says "not stated".
- The verdict or pick is one clear call, with the number that decided it.
- You told the person to confirm the final price at checkout.
- Nothing was bought, and no payment details were entered.
