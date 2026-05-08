<div align="center">

# 🤖 AI Outreach Bot

**Multi-channel automated outreach — email + LinkedIn with AI personalization at scale**

[![Make](https://img.shields.io/badge/Make.com-Core-6D00CC?style=for-the-badge)](https://make.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com)
[![Instantly](https://img.shields.io/badge/Instantly-Email-FF6B35?style=for-the-badge)](https://instantly.ai)
[![Reply Rate](https://img.shields.io/badge/Reply%20Rate-34%25-brightgreen?style=for-the-badge)]()

</div>

---

## Overview

Most outreach fails because it sounds like outreach. This bot sounds like a human — because GPT-4o writes every message based on real data about the prospect.

**Live results:**
- **34%** cold email reply rate (industry benchmark: 8%)
- **22%** lead-to-booked-meeting rate
- **~140** personalized emails sent per day, zero manual writing
- **Auto-books** meetings via Calendly on positive replies

---

## How It Works

### Phase 1: Prospect Intelligence Gathering
For each prospect, the system automatically gathers:

```python
prospect_intel = {
    "linkedin_profile": scrape_linkedin(prospect.linkedin_url),
    "recent_posts": get_last_5_posts(prospect.linkedin_url),
    "company_news": google_news_search(f"{prospect.company} news last 30 days"),
    "tech_stack": builtwith_lookup(prospect.domain),
    "job_postings": scrape_job_boards(prospect.company),  # signals growth/pain
    "funding_data": crunchbase_lookup(prospect.company),
}
```

### Phase 2: AI Personalization Engine

GPT-4o generates a unique email for every prospect using a system prompt that enforces:
- First line references something real (recent post, company news, hiring trend)
- Pain angle matches their likely situation (based on ICP segment + intel)
- CTA is soft — asks a question, not for a meeting
- Sounds like a person, not a marketer

```
Example output:
──────────────────────────────────────────
Subject: ops at Acme after the series B

Hey Sarah,

Saw you're hiring a third ops manager — usually means the manual processes 
that got you to 50 people are starting to crack at 100.

Curious whether that's the main fire right now or if it's more the CRM 
data quality stuff I see a lot of post-funding teams dealing with.

Either way, happy to share what we've built for 3 other companies in 
exactly that stage — no pitch, just a 15-min compare notes.

Worth a quick chat?

Rohan
──────────────────────────────────────────
```

### Phase 3: Multi-Touch Sequence

```
Day 0:  Initial email (AI-personalized first line)
Day 3:  Follow-up — adds social proof ("helped [similar company]...")
Day 7:  "Last touch" — different angle, shorter, direct CTA
Day 14: LinkedIn connection request + short note
Day 17: LinkedIn message — references email thread
```

### Phase 4: Reply Intelligence

Incoming replies are classified by GPT-4o:

```python
REPLY_TYPES = {
    "INTERESTED":    → Book via Calendly link, notify team on Slack
    "NOT_NOW":       → Snooze 45 days, re-enroll with different angle
    "REFERRAL":      → Extract referral name, create new lead, send intro
    "UNSUBSCRIBE":   → Remove from all sequences, add to DNC list
    "OOO":           → Pause sequence until return date
    "OBJECTION":     → AI drafts response, flags for human review
}
```

---

## Make.com Scenario Structure

```
Scenario 1: Lead Intake
  Airtable (new lead) → Intel Gathering → OpenAI → Instantly

Scenario 2: Reply Monitor
  Instantly webhook → OpenAI classifier → Router → Action handler

Scenario 3: LinkedIn Outreach
  Phantombuster → OpenAI → LinkedIn messaging

Scenario 4: Meeting Confirmation
  Calendly webhook → HubSpot update → Slack alert → Thank you email
```

---

## Setup

### Required Accounts
- Make.com (Professional plan or higher)
- Instantly.ai
- OpenAI API
- Phantombuster (LinkedIn automation)
- Calendly
- Airtable or HubSpot

### Configuration

```yaml
# config/outreach.yaml
sequences:
  cold_outreach:
    touches: 5
    spacing_days: [0, 3, 7, 14, 17]
    channels: [email, email, email, linkedin_connect, linkedin_message]

ai:
  model: gpt-4o
  temperature: 0.85       # slightly creative for natural feel
  max_tokens: 300         # keeps emails tight

limits:
  emails_per_day: 150     # per sending account
  linkedin_connects: 25   # LinkedIn daily limit buffer
  min_delay_between_sends: 120  # seconds (humanization)
```

### Import Make Scenarios

1. Download all `.json` files from `/scenarios/`
2. Import into Make.com
3. Add credentials for each service
4. Configure your ICP variables
5. Test with 5 leads before full activation

---

## Compliance

This system is built with deliverability and legal compliance in mind:

- ✅ Unsubscribe processed within minutes
- ✅ CAN-SPAM compliant (physical address, opt-out)
- ✅ GDPR-aware (only public data used for personalization)
- ✅ Sending volume ramped gradually (no account bans)
- ✅ SPF/DKIM/DMARC guidance included in setup docs
- ✅ Spam score checked before send (SpamAssassin)

---

## Performance Dashboard

```
Week of 2026-04-28:
──────────────────────────────
Leads Enrolled:        214
Emails Sent:           486
Open Rate:             61.2%
Reply Rate:            34.1%
Interested Replies:     29
Meetings Booked:        18
No-Shows:                2
Deals Closed (attrib):   4   ($24,800 ARR)
──────────────────────────────
Cost per meeting:      $3.20
Cost per closed deal: $43.60
```

---

<div align="center">

**Built by [Rohan Mukherjee](https://github.com/rohan643) @ Apex Automation Co.**

</div>
