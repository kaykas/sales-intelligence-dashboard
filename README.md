# Sales Intelligence Dashboard

A daily AI-powered view of sales team activity — who's doing their core work, where pipeline is moving, what managers need to address — without anyone touching Salesforce manually.

Built by a sales leader who is not an engineer, in a few hours, using Claude.

## What it does

Every day, the loop:
1. Pulls activity data from your CRM (Salesforce, HubSpot, or similar)
2. Computes the metrics that actually predict outcomes (call volume, pipeline movement, deal velocity)
3. Renders a clean HTML dashboard accessible to any browser
4. Optionally sends a Slack/email digest to managers

## What it shows

```
SALES ACTIVITY — June 26

TEAM ACTIVITY TODAY
Rep             Calls   Meetings   Pipeline Added
Anna Grace B.   4       2          $22K
Amy Beck        3       1          $14K
Jacob Cowan     1       0          $0      ← follow up

NEW BUSINESS PIPELINE
Stage           Count   Value
Discovery       12      $180K
Proposal Sent   7       $94K
Close/Won       2       $38K

SIGNAL
Budget-qualified deals close at 3.2x vs unqualified.
3 open deals are 14+ days stale with no next step set.
```

## Setup

### 1. What you need

- CRM API access (Salesforce, HubSpot, or CSV export)
- A machine to run it on (Mac with launchd, any server, Vercel serverless)
- Claude API key (for the narrative/signal layer)

### 2. Configure

```env
ANTHROPIC_API_KEY=your_key
CRM_TYPE=salesforce          # or hubspot, csv
SALESFORCE_INSTANCE_URL=...
SALESFORCE_ACCESS_TOKEN=...
DASHBOARD_PASSWORD=optional  # password-protect the HTML output
SLACK_WEBHOOK=optional       # post digest to Slack
```

### 3. Run

```bash
python3 dashboard.py --output dashboard.html
# Open dashboard.html in browser
# Or deploy to Vercel: vercel deploy
```

### 4. Make it yours

Edit `metrics.py` to define:
- Which reps are on which teams
- What counts as "core work" for your business (calls? demos? proposals?)
- What thresholds trigger a flag
- Which signals predict outcomes in your sales motion

## The pattern

This is an example of a **reporting loop** — reads raw data from one system, applies business logic, renders a human-readable view.

The same pattern works for:
- Customer health dashboard (reads CRM + support tickets + usage)
- Engineering velocity view (reads GitHub + Jira + deploy frequency)
- Content performance tracker (reads analytics + publish cadence)

## Related

- [prd-loops](https://github.com/kaykas/prd-loops) — turn a problem into a spec
- [meeting-briefing-loop](https://github.com/kaykas/meeting-briefing-loop) — daily briefing from your meetings
- [executive-coach-platform](https://github.com/kaykas/executive-coach-platform) — coaching from your meetings
