# Reddit Content Machine

**Automated n8n workflow that transforms Reddit discussions into actionable content ideas**

![Version](https://img.shields.io/badge/version-1.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## Overview

The Reddit Content Machine is an intelligent automation that mines Reddit's 100,000+ communities to extract high-engagement discussions, analyzes them with Claude AI, and outputs prioritized content ideas to Airtable.

**Stop wasting 10+ hours/week manually searching for content ideas. Let automation do the work.**

### What It Does

- 🔍 **Mines Reddit**: Automatically fetches top posts from your target subreddits
- 🎯 **Filters Quality**: Only analyzes posts with high engagement (configurable thresholds)
- 🧠 **AI Analysis**: Claude extracts pain points, content angles, and urgency scores
- 📊 **Structured Output**: Saves organized content ideas to Airtable for easy planning
- ⏰ **Runs Daily**: Schedule it to run automatically or trigger manually

### Results

- Generate **90+ content ideas per month** per niche
- Reduce idea generation time from **10h/week to 0h/week**
- Increase content relevance with **real audience pain points**

---

## Quick Start

### Prerequisites

1. **n8n** (Cloud or self-hosted)
2. **Anthropic API Key** ([Get one here](https://console.anthropic.com/))
3. **Airtable Account** with Personal Access Token
4. **Reddit Account** (for User-Agent string)

### Installation

#### Step 1: Import Workflow

1. Download `Reddit_Content_Machine.json`
2. In n8n: **Workflows → Import from File**
3. Select the JSON file

#### Step 2: Configure Credentials

**Anthropic API (Claude)**
1. n8n: **Credentials → Add Credential → HTTP Header Auth**
2. Name: `Anthropic API`
3. Header Name: `x-api-key`
4. Header Value: `YOUR_ANTHROPIC_API_KEY`

**Airtable**
1. n8n: **Credentials → Add Credential → Airtable Token API**
2. Name: `Airtable Personal Access Token`
3. Token: `YOUR_AIRTABLE_PAT`
4. Select your Base and Table

#### Step 3: Setup Airtable Base

Create a new base called **Content Ideas** with a table named **Reddit Content Ideas**.

**Required Fields:**

| Field Name | Type | Options |
|------------|------|---------|
| Content Title | Single line text | - |
| Format | Single select | Blog, Video, Social, Thread |
| Angle | Long text | - |
| Hook | Long text | - |
| Main Problem | Long text | - |
| Search Intent | Single select | Informational, Commercial, Transactional |
| Emotional Triggers | Single line text | - |
| Target Audience | Single line text | - |
| Urgency | Number | Integer, 1-10 |
| Source URL | URL | - |
| Source Title | Long text | - |
| Subreddit | Single line text | - |
| Engagement Score | Number | Integer |
| Comments | Number | Integer |
| Status | Single select | Todo, In Progress, Done, Archived |
| Created | Date | Include time |

**Pro Tip**: Use the "High Urgency" view (Urgency >= 7) to prioritize timely content.

#### Step 4: Configure Reddit User-Agent

1. Open the **Fetch Reddit Posts** node
2. Update the User-Agent header:
   ```
   n8n-reddit-scraper/1.0 (by /u/YOUR_REDDIT_USERNAME)
   ```

#### Step 5: Customize Configuration

Open the **Config** node and set your preferences:

```javascript
{
  subreddits: "hyrox\ncrossfit\nrunning",  // One per line
  minScore: 50,                             // Minimum upvotes
  minComments: 10,                          // Minimum comments
  postsPerSubreddit: 25,                    // Posts to fetch
  timeRange: "week"                         // day/week/month/year/all
}
```

**Recommended Settings:**

| Use Case | minScore | minComments | postsPerSubreddit |
|----------|----------|-------------|-------------------|
| Niche Community | 20 | 5 | 25 |
| Medium Subreddit | 50 | 10 | 25 |
| Large Subreddit | 100 | 25 | 15 |

#### Step 6: Test Run

1. Click **Manual Trigger**
2. Click **Execute Workflow**
3. Check Airtable for results (should see 30-150 ideas)

#### Step 7: Activate Schedule

1. Enable the **Schedule Trigger** (runs daily at 9am)
2. Or customize the cron expression:
   ```
   0 9 * * *  // Daily at 9am
   0 9 * * 1  // Every Monday at 9am
   0 9,15 * * *  // Daily at 9am and 3pm
   ```

---

## How It Works

### Workflow Architecture

```
Trigger (Manual/Schedule)
  ↓
Config (Set subreddit list + parameters)
  ↓
Split Subreddits (Convert to array)
  ↓
Loop: For each subreddit
  ↓
  Fetch Reddit Posts (HTTP → Reddit API)
  ↓
  Split Posts (Array → Individual items)
  ↓
  Filter (Score >= minScore AND Comments >= minComments)
  ↓
  Extract Post Data (Flatten structure)
  ↓
  Fetch Top Comments (HTTP → Reddit API)
  ↓
  Process Comments (Parse and format)
  ↓
  Claude Analysis (AI → Extract insights)
  ↓
  Format Output (Structure for Airtable)
  ↓
Save to Airtable (Batch create records)
```

### Node Details

#### 1. Config Node
**Type**: Set (Manual Values)
**Purpose**: Central configuration for the entire workflow

**Fields:**
- `subreddits`: Newline-separated list of subreddit names
- `minScore`: Minimum post score (upvotes)
- `minComments`: Minimum number of comments
- `postsPerSubreddit`: Number of posts to fetch per subreddit
- `timeRange`: Time period for "top" posts

#### 2. Split Subreddits
**Type**: Code (JavaScript)
**Purpose**: Converts newline-separated string into array

#### 3. Loop Subreddits
**Type**: Split in Batches
**Purpose**: Iterates through subreddit list one at a time

#### 4. Fetch Reddit Posts
**Type**: HTTP Request
**API**: `https://www.reddit.com/r/{subreddit}/top.json`
**Rate Limit**: 60 requests/minute (Reddit API limit)

**Query Parameters:**
- `t`: Time range (day/week/month/year/all)
- `limit`: Number of posts to fetch

#### 5. Split Posts
**Type**: Split Out
**Purpose**: Converts posts array into individual items for processing

#### 6. Filter Engagement
**Type**: Filter
**Purpose**: Removes low-quality posts

**Conditions:**
- Post score >= minScore (AND)
- Comment count >= minComments

**Expected Reduction**: 50-70% of posts filtered out

#### 7. Extract Post Data
**Type**: Set (Manual Values)
**Purpose**: Flattens Reddit's nested structure

**Extracted Fields:**
- title, score, numComments
- url, permalink
- body (post text)
- subreddit, created

#### 8. Fetch Comments
**Type**: HTTP Request
**API**: `{permalink}.json?limit=5`
**Purpose**: Gets top 5 comments for additional context

**Error Handling**: If fails, continues with empty comments

#### 9. Process Comments
**Type**: Code (JavaScript)
**Purpose**: Extracts comment text and scores, formats for Claude

#### 10. Claude Analysis
**Type**: HTTP Request (Anthropic API)
**Model**: claude-sonnet-4-20250514
**Temperature**: 0.3
**Max Tokens**: 1000

**Prompt Structure:**
```
Analysiere diese Reddit-Diskussion und extrahiere Content-Ideen.

**Post:**
Titel: {title}
Subreddit: r/{subreddit}
Score: {score}
Comments: {numComments}

Text:
{body}

**Top Comments:**
{commentsText}

---

Extrahiere im JSON-Format:
{
  "mainProblem": "...",
  "contentIdeas": [...],
  "searchIntent": "...",
  "emotionalTriggers": [...],
  "targetAudience": "...",
  "urgency": 1-10
}
```

**Output**: 3-5 content ideas per post with structured metadata

#### 11. Format Output
**Type**: Code (JavaScript)
**Purpose**: Transforms Claude's JSON into Airtable records

**Creates one record per content idea** (not per post)

#### 12. Save to Airtable
**Type**: Airtable (Create)
**Operation**: Create records
**Options**: Typecast enabled (auto-converts data types)

---

## Configuration Guide

### Choosing Subreddits

**Tips for selecting subreddits:**

✅ **Good Choices:**
- Active communities (>10k members)
- Your target audience
- Mix of broad + niche (e.g., "fitness" + "hyrox")
- High question/discussion rate

❌ **Avoid:**
- Meme-focused subreddits
- Very small communities (<1k members)
- Highly moderated (posts get removed)
- Off-topic for your niche

**Recommended Number:**
- **Start**: 3-5 subreddits
- **Growth**: 5-10 subreddits
- **Enterprise**: Multiple workflows (10+ subs total)

### Adjusting Thresholds

**minScore (Upvotes)**

| Value | Description | Use Case |
|-------|-------------|----------|
| 10-20 | Very loose | Niche communities |
| 50-100 | Moderate | Most subreddits |
| 100+ | Strict | Large/busy subreddits |

**minComments**

| Value | Description | Use Case |
|-------|-------------|----------|
| 5-10 | Loose | Smaller communities |
| 10-20 | Moderate | Most subreddits |
| 25+ | Strict | Need discussion depth |

### Time Range

| Value | Description | Best For |
|-------|-------------|----------|
| day | Last 24 hours | Very active subs, daily runs |
| week | Last 7 days | **Recommended for most** |
| month | Last 30 days | Slower communities |
| year | Last 365 days | Research, evergreen content |
| all | All time top | One-time setup |

---

## Performance & Costs

### Benchmarks

**Single Subreddit (25 posts):**
- Fetch posts: 2s
- Filter + extract: 1s
- Fetch comments: 25s
- Claude analysis: 30s (10 posts after filter)
- Save to Airtable: 5s
- **Total: ~60 seconds**

**Three Subreddits (75 posts):**
- **Total: ~3.5 minutes**
- **Ideas generated: 30-150**

**Ten Subreddits (250 posts):**
- **Total: ~15 minutes**
- **Ideas generated: 100-500**

### API Costs

**Reddit API:**
- **Cost**: Free
- **Limit**: 60 requests/minute
- **Usage**: 2 requests per post (post + comments)

**Claude API (Anthropic):**
- **Model**: claude-sonnet-4-20250514
- **Cost**: ~$0.003 per post
- **Daily (3 subs)**: ~$0.20
- **Monthly (3 subs, daily)**: ~$6

**Airtable API:**
- **Free Tier**: 1,200 records
- **Usage**: ~100 ideas/day = 3,000 records/month
- **Pro Plan**: $10/month (50,000 records)

**Total Monthly Cost:**
- Free tier: **$6/month** (Claude only)
- With Airtable Pro: **$16/month**

**ROI Calculation:**
- Time saved: 40 hours/month
- Value at $50/hour: $2,000/month
- **ROI: 333x** (free tier) or **125x** (paid)

---

## Use Cases

### Content Creator

**Goal**: Never run out of YouTube video ideas

**Setup:**
```
subreddits: "fitness\nyoga\nnutrition"
minScore: 50
minComments: 15
postsPerSubreddit: 25
timeRange: "week"
```

**Result**: 90-150 video ideas/month based on real audience questions

### Marketing Agency

**Goal**: Generate blog topics for 5 clients

**Setup**: Clone workflow 5 times, each with different:
- Subreddits (client-specific)
- Airtable base (or tagged by client)
- Schedule (staggered to avoid rate limits)

**Result**: 50-100 ideas per client per month

### Solo Entrepreneur

**Goal**: Low-cost content automation

**Setup:**
```
subreddits: "Entrepreneur\nstartups\nsaas"
minScore: 100
minComments: 25
postsPerSubreddit: 15
timeRange: "week"
```

**Result**: High-quality discussion topics, <$10/month cost

### Newsletter Writer

**Goal**: Weekly industry insights

**Setup:**
- Run once per week (not daily)
- Higher thresholds (minScore: 200)
- Fewer posts (postsPerSubreddit: 10)
- Export to Google Docs instead of Airtable

---

## Troubleshooting

### Common Issues

#### No Posts Match Filter

**Problem**: All posts filtered out, no results

**Solutions:**
1. Lower `minScore` (try 20-30)
2. Lower `minComments` (try 5-10)
3. Change `timeRange` to "month" or "year"
4. Check if subreddit name is correct

#### Rate Limit Errors (429)

**Problem**: Reddit returns "Too Many Requests"

**Solutions:**
1. Reduce `postsPerSubreddit` (try 15-20)
2. Reduce number of subreddits (<5)
3. Add delay between requests (edit Fetch Reddit Posts node)
4. Use "week" or "month" time range (fewer unique requests)

#### Claude JSON Parse Error

**Problem**: Claude returns text instead of valid JSON

**Solutions:**
1. Check prompt formatting (no broken quotes)
2. The Format Output node has fallback handling
3. Check Claude API response in execution log
4. Increase `max_tokens` if response is truncated

#### Airtable Field Validation Error

**Problem**: "Field value not in select options"

**Solutions:**
1. In Airtable, allow "other" values for single selects
2. Or manually add the new option values
3. The workflow uses "typecast" to auto-create missing options

#### Duplicate Records

**Problem**: Same content idea saved multiple times

**Solutions:**
1. Check Source URL field is populated
2. Add Airtable automation to deduplicate (Source URL)
3. Or use "Update" instead of "Create" in Airtable node

### Error Logs

**Check n8n execution logs:**
1. Workflow → Executions
2. Find failed execution
3. Click on red node to see error
4. Common errors:
   - Network timeout → Increase timeout in HTTP nodes
   - Invalid credentials → Check API keys
   - Rate limit → Add delays between requests

---

## Advanced Configuration

### Custom Claude Prompt

Edit the **Claude Analysis** node to customize the prompt:

**Example: Focus on controversial topics**
```
Analysiere diese Reddit-Diskussion. Fokussiere auf kontroverse Meinungen und Debattenpunkte.

Extrahiere:
- Hauptkontroverse
- Pro/Contra Argumente
- Content-Ideen, die beide Seiten beleuchten
```

**Example: Focus on product recommendations**
```
Analysiere diese Reddit-Diskussion. Extrahiere Produktempfehlungen und Tools, die erwähnt werden.

Extrahiere:
- Erwähnte Produkte/Tools
- Vor- und Nachteile
- Alternative Optionen
- Content-Idee für Vergleichsartikel
```

### Batch Processing

For **10+ subreddits**, split into multiple workflows:

**Workflow 1**: Subreddits 1-5
**Workflow 2**: Subreddits 6-10
**Schedule**: Stagger by 30 minutes

This avoids:
- Long execution times (>30 min)
- Rate limiting issues
- Timeout errors

### Output to Google Sheets

Replace the **Airtable** node with **Google Sheets**:

1. Add Google Sheets credential
2. Use "Append Row" operation
3. Map fields to columns

**Pros**: Free, no record limits
**Cons**: Less structured, no views/filtering

### Webhook Trigger

Replace **Manual/Schedule** triggers with **Webhook**:

**Use Cases:**
- Trigger from Zapier
- Trigger from Airtable button
- Trigger from Slack command

---

## Optimization Tips

### Speed Improvements

**1. Parallel Comment Fetching** (Advanced)
- Currently: Serial (25 posts × 1s = 25s)
- Optimized: Parallel (5s total)
- **How**: Use Loop Over Items node with parallel execution

**2. Batch Claude Requests**
- Currently: 1 post per request
- Optimized: 3-5 posts per request
- **How**: Aggregate posts, modify prompt

**3. Reduce Comment Fetching**
- Only fetch comments for posts without body text
- **How**: Add IF condition before Fetch Comments

### Cost Reduction

**1. Filter Earlier**
- Move Filter node BEFORE Fetch Comments
- Saves 50% of HTTP requests

**2. Use Haiku Model** (Coming soon)
- Faster, cheaper Claude model
- Good enough for content idea extraction

**3. Cache Reddit Responses**
- Store posts in database
- Only analyze new posts
- **How**: Add Postgres/MySQL node

---

## Roadmap

### V2: Keyword Research Integration

**Feature**: Auto-check search volume for content ideas

**APIs**: DataForSEO, Ahrefs, SEMrush
**Logic**: Filter ideas with <500 searches/month
**Benefit**: Only high-traffic topics
**Cost**: +$10/month

### V3: Content Drafting

**Feature**: Auto-generate outlines for high-urgency ideas

**Logic**: Ideas with Urgency >7 → Claude → Google Docs
**Benefit**: 1-click from idea to draft
**Cost**: +$5/month

### V4: Trend Detection

**Feature**: Identify accelerating topics

**Logic**: Compare post dates, flag topics with increasing frequency
**Benefit**: Catch trends early
**Cost**: $0 (logic only)

### V5: Multi-Platform

**Feature**: Add Twitter, LinkedIn, Discord, Forums

**APIs**: Twitter API, LinkedIn API, Discord
**Benefit**: Broader conversation coverage
**Cost**: Variable

---

## FAQ

### Q: Do I need a Reddit API key?

**A**: No! This workflow uses Reddit's public JSON endpoints. Just update the User-Agent.

### Q: How many subreddits can I track?

**A**: Recommended 3-10. For more, use multiple workflows.

### Q: Can I use GPT-4 instead of Claude?

**A**: Yes! Replace the Claude Analysis node with OpenAI's Chat Model node. Update the prompt accordingly.

### Q: Will this get my Reddit account banned?

**A**: No. The workflow respects Reddit's rate limits and uses public endpoints. Just use a proper User-Agent.

### Q: Can I analyze comments-only subreddits?

**A**: Yes! The workflow handles posts with no body text. Comments provide the context.

### Q: How do I avoid duplicate content ideas?

**A**:
1. Use Airtable's duplicate detection (Source URL field)
2. Archive old ideas after 30 days
3. Run workflow less frequently (weekly instead of daily)

### Q: Can I share this with my team?

**A**: Yes! Export the workflow JSON and share. Each user needs their own API keys.

---

## Support & Contributing

### Get Help

- **Issues**: Open an issue on GitHub
- **Questions**: Comment on the blog post
- **n8n Community**: [community.n8n.io](https://community.n8n.io)

### Contributing

Contributions welcome! Areas for improvement:
- Additional language support (prompts)
- Alternative AI models (GPT-4, Gemini)
- Output integrations (Notion, Google Docs)
- Performance optimizations

---

## License

MIT License - Feel free to use, modify, and distribute.

---

## Credits

**Created by**: Phil
**Date**: 2025-11-17
**Version**: 1.0

**Tools Used**:
- n8n (Workflow automation)
- Claude (Anthropic AI)
- Airtable (Database)
- Reddit API (Data source)

---

## Changelog

### v1.0 (2025-11-17)
- ✅ Initial release
- ✅ Core workflow: Reddit → Claude → Airtable
- ✅ 3-5 content ideas per post
- ✅ Configurable subreddit list
- ✅ Daily scheduling
- ✅ Error handling and retry logic
- ✅ Comprehensive documentation

---

**Ready to automate your content ideation? Import the workflow and start generating ideas in 15 minutes.**
