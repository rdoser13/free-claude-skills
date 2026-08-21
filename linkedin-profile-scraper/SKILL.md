---
name: linkedin-profile-scraper
description: Scrape LinkedIn profile post data using the Apify LinkedIn Profile Post Scraper and export it as a structured CSV. Use this skill when the user wants to pull LinkedIn post metrics, analyze LinkedIn content performance, scrape a LinkedIn profile's posts, or export LinkedIn engagement data. Also trigger when the user mentions Apify and LinkedIn together, or asks about post-level LinkedIn analytics.
disable-model-invocation: true
argument-hint: [linkedin-profile-url]
---

# LinkedIn Profile Post Scraper

Scrape a LinkedIn profile's posts via the Apify LinkedIn Profile Post Scraper actor and export the results as a clean, analysis-ready CSV.

## Prerequisites

- An Apify API token. The user must provide this or have it set as an environment variable (`APIFY_API_TOKEN`). If neither exists, ask for it before proceeding. The free Apify tier works for small runs.
- The target LinkedIn profile URL (e.g., `https://www.linkedin.com/in/username/`)

## Step 1: Validate inputs

1. Confirm the Apify API token is available — check `$APIFY_API_TOKEN` env var first, then ask the user.
2. Confirm a valid LinkedIn profile URL was provided as the argument (`$ARGUMENTS`). It should match the pattern `https://www.linkedin.com/in/...`.
3. Ask how many posts to scrape if not specified. Default to 50.

## Step 2: Run the Apify actor

Use the Apify REST API to trigger the LinkedIn Profile Post Scraper actor (`curious_coder/linkedin-profile-post-scraper`).

```bash
curl -X POST "https://api.apify.com/v2/acts/curious_coder~linkedin-profile-post-scraper/runs?token=$APIFY_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "profileUrls": ["<LINKEDIN_PROFILE_URL>"],
    "maxPosts": <NUMBER_OF_POSTS>
  }'
```

Wait for the run to complete by polling the run status endpoint. Then fetch the dataset items from the default dataset.

## Step 3: Transform into CSV

Parse the raw JSON output and map it to these columns:

| Column | Source | Notes |
|---|---|---|
| Date | `postedAt` or `postedDate` | Format as `YYYY-MM-DD` |
| Post URL | `postUrl` or `url` | Full LinkedIn post URL |
| Post Type | `type` | Normalize to: `text`, `image`, `linkedinVideo`, `article`, `document`, `poll` |
| Likes | `likeCount` or `numLikes` | Integer, default 0 if missing |
| Comments | `commentCount` or `numComments` | Integer, default 0 if missing |
| Shares | `shareCount` or `numShares` | Integer, default 0 if missing |
| Engagement Score | Calculated | See formula below |
| Post Text (First 300 chars) | `text` or `postText` | Truncate to 300 characters. Escape commas and newlines for CSV safety |

**Field name flexibility:** Apify actor output schemas change over time. The field names above are common variants — inspect the actual JSON keys returned and map accordingly. If a field is missing entirely, log a warning and default to `0` for numeric fields or `"N/A"` for text fields.

## Step 4: Calculate Engagement Score

Use a weighted formula normalized to a 0–10 scale:

```
Raw Score = Likes × 1 + Comments × 3 + Shares × 2
```

- Comments are weighted 3x because they require the most effort and signal genuine interest.
- Shares are weighted 2x because they extend reach and imply endorsement.
- Likes are weighted 1x as baseline engagement.

After computing raw scores for all posts, normalize to 0–10:

```
Engagement Score = (Raw Score / Max Raw Score in Dataset) × 10
```

Round to one decimal place. The highest-performing post always scores 10.0 and everything else is relative to it.

**Edge case:** If all posts have zero engagement, set all scores to 0.

## Step 5: Export and deliver

1. Write the CSV to the current working directory as `linkedin-posts-YYYY-MM-DD.csv` (using today's date).
2. Sort rows by date descending (newest first).
3. Print a summary to the terminal:
   - Total posts scraped
   - Date range covered
   - Average engagement score
   - Top 3 posts by engagement score (show date, type, score, and first 80 chars of text)
4. Tell the user where the file was saved.

## Troubleshooting

- **401 or 403 from Apify**: The API token is invalid or expired. Ask the user to verify it.
- **Empty dataset**: The actor may have failed silently. Check the Apify run log URL (returned in the run response) and share it with the user.
- **Missing fields in output**: Apify actors update their schemas. Inspect the raw JSON first and adapt the field mapping. Don't fail hard — default missing values and warn the user.
- **Rate limiting**: If scraping a large number of posts (200+), the actor run may take several minutes. Poll with a 10-second interval and let the user know it's running.
