# 🤖 AI Outreach Bot

Multi-channel outreach on autopilot. GPT-4o writes every message from live prospect data.

---

**Results:**

```
Reply rate:      34%   (industry: 8%)
Meeting rate:    22%
Emails/day:      140   (zero manual writing)
```

---

### How It Works

1. **Intel gathering** — LinkedIn posts, company news, job postings, tech stack
2. **AI writes the email** — specific, human, references real data
3. **Sequence runs** — 5 touches across email + LinkedIn over 17 days
4. **Reply classified** — Interested / Not Now / Unsubscribe / OOO / Objection
5. **Auto-routes** — books meeting, snoozes, or DNC depending on reply type

---

### Sequence

| Day | Channel | Type |
|-----|---------|------|
| 0 | Email | AI-personalized intro |
| 3 | Email | Social proof follow-up |
| 7 | Email | Different angle |
| 14 | LinkedIn | Connection + note |
| 17 | LinkedIn | Message referencing email |

---

### Files

```
ai-outreach-bot/
├── workflow/
│   ├── outreach-main.json     # n8n — lead intake + send
│   └── reply-handler.json     # n8n — classify + route replies
├── config/
│   └── outreach.yaml          # Sequence config
└── .gitignore
```

---

### Setup

1. Import both workflow JSONs into n8n
2. Connect: Airtable → OpenAI → Instantly → Calendly → Slack
3. Configure `config/outreach.yaml`
4. Test with 5 leads, check reply classification, then activate

---

<sub>[@rohan643](https://github.com/rohan643)</sub>
