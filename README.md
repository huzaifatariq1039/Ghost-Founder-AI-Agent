# 👻 Ghost-Founder 

> **A fully autonomous multi-agent AI system that runs my personal brand on LinkedIn, X (Twitter), and Instagram — so I can focus on actually building things.**

I built this because I was tired of two things: posting generic "AI thought leader" slop that sounds like everyone else, and spending hours writing content that gets buried anyway. Ghost-Founder v3.0 is my answer — a `n8n`-powered Council of Expert AI agents that knows my real projects, my actual voice, and the difference between a high-value investor DM and a bot comment.

This isn't a template. It's a system designed around my specific context — WebCorps, PulseQ, Pashto GPT, and everything in between.

---

## 🧠 The Council of Experts (Multi-Model Architecture)

Instead of routing everything through one LLM, I use four specialized models, each doing what it's actually good at:

| Agent | Model | Role |
|---|---|---|
| 🎯 The Strategist | **Claude Opus 4.6** | Weekly brand audit, theme direction, platform strategy |
| 📚 The Archivist | **Gemini Pro** | Technical fact-checking against my real portfolio |
| ⚡ The Speedster | **Llama 4 on Groq** | High-speed creative drafting, triage, validation |
| 🔬 The Validator | **Llama 4 on Groq** | Shadow-ban risk scoring, authenticity check, dwell-time simulation |

The Strategist gets Claude Opus because brand strategy is high-stakes reasoning — it needs to understand my "me vs. me" voice, not just output motivational fluff. Gemini handles the context vault because it can hold my entire project history in memory at once. Groq runs everything time-sensitive because latency actually matters for engagement triage.

---

## 🔁 How It Works — The Three-Agent Loop

```
DAILY TRIGGER (24h schedule)
        │
        ▼
┌─────────────────────────────────────────────────────────┐
│  PIPELINE 1: CONTENT CREATION                           │
│                                                         │
│  Apify Scraper → Strategist → Archivist → Creative      │
│       ↓               ↓           ↓           ↓        │
│  Trending Topics  Weekly Theme  Tech Brief  Full Draft  │
│                                                         │
│  → Validator → WhatsApp Preview → !Approve → Publish    │
└─────────────────────────────────────────────────────────┘

ENGAGEMENT WEBHOOK (real-time)
        │
        ▼
┌─────────────────────────────────────────────────────────┐
│  PIPELINE 2: SMART TRIAGE                               │
│                                                         │
│  Incoming Comment/DM                                    │
│       │                                                 │
│       ├── High-Value → Priority WhatsApp Alert          │
│       │   (Investor/Client)   + "Who's Who" Summary     │
│       │                       + Draft DM                │
│       │                       + Log to Leads Sheet      │
│       │                                                 │
│       └── Low-Value  → Witty Auto-Reply Draft           │
│           (General)                                     │
└─────────────────────────────────────────────────────────┘

WEEKLY (alongside content)
        │
        ▼
┌─────────────────────────────────────────────────────────┐
│  PIPELINE 3: PROACTIVE COMMUNITY MANAGER                │
│                                                         │
│  Identifies 3 key players in AI/HealthTech/Space niches │
│  → Drafts authentic opening comments                    │
│  → Sends targets to WhatsApp for review                 │
└─────────────────────────────────────────────────────────┘
```

---

## ✨ Features

### 🎯 Deep Personal Context (Not Generic RAG)
The Archivist knows my actual projects. When writing about "AI in Healthcare," it references my real experience onboarding hospitals at Rufaydah Medical Complex with PulseQ — not some hallucinated case study. It knows WebCorps, Pashto GPT, my n8n automation work, my GDG involvement, and my IST coursework. Every post is technically grounded.

### 🔒 Shadow-Ban Risk Detection
Before anything goes live, the Validator scores it 0–100 across:
- Shadow-ban risk (low / medium / high) with specific reasons
- Authenticity score — penalizes AI slop and generic buzzwords
- Dwell-time simulation (estimated read time per platform)
- Best post time in Pakistan timezone
- Red flags list with specific lines to fix

### 📱 WhatsApp Human-in-the-Loop
I never publish without seeing it first. The workflow sends me a full preview via WhatsApp:

```
🤖 Ghost-Founder v3.0 — Weekly Content Package
📅 Sunday, April 5, 2026

🎯 Weekly Theme: AI in Space Tech — local angle
✅ Validation Score: 87/100
⚠️ Shadow-Ban Risk: low
🎭 Authenticity: 91/100
⏰ Best Post Time (PK): 8:00 PM PKT

📝 LinkedIn Hook:
"Three months ago I asked: can we build a hospital..."

📊 Verdict: APPROVE

👇 Reply !Approve to publish all platforms
```

One reply — `!Approve` — triggers publishing to LinkedIn and X simultaneously.

### 🐦 Full X Thread Automation
X posts go out as a properly chained 5-tweet thread, not a single orphaned tweet. Each reply is linked to the previous tweet's ID so the thread structure is preserved.

### 📊 Google Sheets Logging
Every content package and every high-value lead gets logged to Google Sheets automatically:
- **Content-Queue sheet**: full post history with validation scores, status, timestamps
- **Leads sheet**: all high-value engagements with triage data, draft DMs, follow-up status

### 🌐 Proactive Community Manager
The system doesn't just react — it finds conversations I should initiate. Each week it identifies 3 key accounts in my niches (AI in Space, HealthTech, Pakistan tech ecosystem) and drafts authentic opening comments that add real value, not "Great post!" spam.

---

## 🗂️ Node Map (43 Nodes, 42 Connections)

| # | Node | Type | Purpose |
|---|------|------|---------|
| 1 | Daily Strategy Trigger | Schedule | Fires every 24 hours |
| 2 | Manual/WhatsApp Webhook | Webhook | Receives `!Approve` signal |
| 3 | Check !Approve Signal | IF | Routes approval vs. new run |
| 4 | Apify - Scrape Trending Topics | HTTP | Fires Apify actor for trend data |
| 5 | Wait for Apify Actor | Code | 15s delay for actor completion |
| 6 | Apify - Fetch Scraped Results | HTTP | Retrieves actor dataset |
| 7 | The Strategist (Claude Opus 4.6) | HTTP | Weekly strategy JSON |
| 8 | Parse Strategist Output | Code | Extracts JSON from Claude response |
| 9 | The Archivist (Gemini Pro) | HTTP | Technical content brief |
| 10 | Parse Archivist Output | Code | Extracts JSON from Gemini response |
| 11 | Creative Agent (Llama 4 on Groq) | HTTP | Full content package draft |
| 12 | Parse Creative Output | Code | Extracts content package |
| 13 | Validator Agent (Shadow-Ban Check) | HTTP | Validates + scores content |
| 14 | Build WhatsApp Preview | Code | Assembles preview message |
| 15 | Log to Google Sheets (Content-Queue) | Google Sheets | Logs full package |
| 16 | Send WhatsApp Preview | HTTP | Sends preview via CallMeBot |
| 17 | Approval Gate | IF | Auto-approve if score ≥ threshold |
| 18 | Fetch Approved Content | Code | Retrieves content for publishing |
| 19 | Post to LinkedIn | LinkedIn | Publishes LinkedIn post |
| 20 | Post to X - Thread Start | Twitter | Posts tweet 1 |
| 21–24 | X Thread Tweet 2–5 | Twitter | Chained thread replies |
| 25 | Update Sheet: Mark Published | Google Sheets | Updates status |
| 26 | WhatsApp: Publish Confirmation | HTTP | Confirms delivery |
| 27 | Engagement Webhook | Webhook | Receives comments/DMs |
| 28 | Smart Triage (Llama 4 - Fast) | HTTP | Classifies engagement tier |
| 29 | Parse Triage Result | Code | Extracts triage JSON |
| 30 | High Value vs Low Value Split | IF | Routes by tier |
| 31 | Low Value: Quick Reply Draft | HTTP | Generates brief witty reply |
| 32 | Format Low-Value Reply | Code | Cleans reply output |
| 33 | Build High-Value Notification | Code | Assembles priority alert |
| 34 | WhatsApp: Priority Alert | HTTP | Sends investor/client alert |
| 35 | Log Lead to Google Sheets (Leads) | Google Sheets | Logs high-value contact |
| 36 | Sentiment Analysis (Llama 4) | HTTP | Parallel sentiment scan |
| 37 | Proactive Community Manager | HTTP | Finds engagement targets |
| 38 | Parse Community Opportunities | Code | Extracts opportunities |
| 39 | WhatsApp: Community Targets | HTTP | Sends weekly targets |
| 40 | Webhook Response | Respond to Webhook | Returns 200 to caller |
| 41 | Engagement Webhook Response | Respond to Webhook | Returns 200 to caller |
| 42 | Revision: Log & Notify | Code | Handles rejected content |
| 43 | WhatsApp: Revision Alert | HTTP | Sends revision notice |

---

## 🛠️ Setup

### Prerequisites
- n8n (self-hosted or cloud) — v1.0+
- Google account (Sheets + OAuth2)
- LinkedIn Developer App (OAuth2)
- X / Twitter Developer App (OAuth2)
- CallMeBot WhatsApp API (free)
- API Keys: Anthropic, Groq, Gemini, Apify

---

### Step 1 — Import the Workflow

1. Open n8n → **Workflows** → **Import from File**
2. Upload `ghost_founder_v3_workflow.json`
3. The workflow loads with all 43 nodes

---

### Step 2 — Configure Credentials

In n8n, go to **Settings → Credentials** and create the following:

#### Anthropic API Key
```
Name:  Anthropic API Key
Type:  HTTP Header Auth
Header Name:  x-api-key
Header Value:  sk-ant-...
```

#### Groq API Key
```
Name:  Groq API Key
Type:  HTTP Header Auth
Header Name:  Authorization
Header Value:  Bearer gsk_...
```

#### Gemini API Key
```
Name:  Gemini API Key
Type:  HTTP Header Auth (used as query param in node)
Header Value:  AIza...
```

#### Apify API Key
```
Name:  Apify API Key
Type:  HTTP Header Auth
Header Name:  Authorization
Header Value:  Bearer apify_api_...
```

#### Google Sheets
```
Name:  Google Sheets OAuth2
Type:  Google Sheets OAuth2 API
→ Follow n8n OAuth2 flow
```

#### LinkedIn
```
Name:  LinkedIn OAuth2
Type:  LinkedIn OAuth2 API
→ Follow n8n OAuth2 flow
→ Scopes needed: w_member_social, r_liteprofile
```

#### X / Twitter
```
Name:  X / Twitter OAuth2
Type:  Twitter OAuth2 API
→ Follow n8n OAuth2 flow
→ Requires Twitter Developer App with OAuth 2.0 enabled
```

---

### Step 3 — Configure WhatsApp (CallMeBot)

1. Send a WhatsApp message to `+34 644 51 82 28` saying: `I allow callmebot to send me messages`
2. You'll receive an API key in reply
3. In the workflow, find all 5 WhatsApp nodes and replace:
   - `YOUR_PHONE_NUMBER` → your number with country code, no `+` (e.g. `923001234567`)
   - `YOUR_CALLMEBOT_APIKEY` → your received key

The 5 nodes to update:
- `Send WhatsApp Preview`
- `WhatsApp: Publish Confirmation`
- `WhatsApp: Priority Alert`
- `WhatsApp: Community Targets`
- `WhatsApp: Revision Alert`

---

### Step 4 — Google Sheets Setup

Create a Google Sheet with two tabs:

**Tab 1: `Content-Queue`**
```
Timestamp | Week_Theme | Validation_Score | Shadow_Ban_Risk | 
Authenticity_Score | Verdict | LinkedIn_Hook | LinkedIn_Body | 
LinkedIn_Hashtags | X_Thread | Instagram_Caption | Visual_Prompt | 
Best_Post_Time | Status | Green_Flags | Red_Flags | Published_At
```

**Tab 2: `Leads`**
```
Timestamp | Name | Platform | Message | Intent | 
Who_Is_This | Urgency | Suggested_Reply | Draft_DM | Status
```

Then copy the Sheet ID from the URL:
```
https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID_HERE/edit
```

Replace `YOUR_GOOGLE_SHEET_ID` in these two nodes:
- `Log to Google Sheets (Content-Queue)`
- `Log Lead to Google Sheets (Leads)`

---

### Step 5 — Configure Engagement Webhooks

The engagement pipeline receives real-time comment/DM data. The webhook URL will be:
```
https://your-n8n-instance.com/webhook/engagement-webhook
```

Send POST requests to this URL with this payload structure:
```json
{
  "platform": "linkedin",
  "sender_name": "Jane Smith",
  "sender_bio": "Partner @ XYZ Ventures | HealthTech investor",
  "sender_connections": "500+",
  "sender_profile": {},
  "message": "Really interesting take on clinical AI — are you open to a quick call?",
  "comments": []
}
```

> I use Zapier or Make.com as a bridge to pipe LinkedIn notifications into this webhook, since LinkedIn's native webhook support is limited.

---

### Step 6 — Personalize the Context Vault

The Archivist and Strategist nodes contain hardcoded context about my projects. To adapt this for your own use, update the system prompts inside:

- **`The Strategist (Claude Opus 4.6)`** node → `system` field
- **`The Archivist (Gemini Pro)`** node → first part of the `text` content

Replace references to my projects with yours:
```
PulseQ → your startup name
WebCorps → your agency/company
Rufaydah Medical Complex → your real clients
Pashto GPT → your NLP/ML project
IST Islamabad → your university
GDG → your community involvement
```

---

### Step 7 — Activate

1. Enable the workflow in n8n (toggle the Active switch)
2. The daily trigger fires automatically at the configured interval
3. First run will take ~2-3 minutes (Apify scrape + 4 LLM calls)
4. Check WhatsApp for your first content preview

---

## 📁 Project Structure

```
ghost-founder-v3/
├── ghost_founder_v3_workflow.json   # n8n workflow — import this
└── README.md                        # This file
```

---

## ⚠️ Known Limitations

**Nano Banana 2 (Visual Remixing)** — The workflow outputs a `visual_prompt` field for every piece of content, but the actual image generation/remixing is not automated yet. Nano Banana 2's API isn't publicly available at this time. I currently take the prompt and run it manually through my preferred image tool.

**Instagram Publishing** — Meta's API doesn't allow direct text post publishing for personal profiles (only business accounts via the Graph API). The Instagram caption is generated and logged to Sheets, but auto-publishing requires a connected Instagram Business Account through Meta's API separately.

**Apify Actor Delay** — I hardcoded a 15-second wait for the Apify actor to complete. On slow days or heavy scrapes this might time out. Increase the delay in the `Wait for Apify Actor` code node if needed.

**Engagement Webhook Bridging** — LinkedIn and X don't natively POST to webhooks on every comment. I bridge this via Zapier/Make.com watching my notifications — there's a few-minute delay on engagement detection.

---

## 🔑 Environment Summary

| Variable | Where to set | Notes |
|---|---|---|
| `YOUR_GOOGLE_SHEET_ID` | 2 Google Sheets nodes | Copy from sheet URL |
| `YOUR_PHONE_NUMBER` | 5 WhatsApp nodes | No `+`, with country code |
| `YOUR_CALLMEBOT_APIKEY` | 5 WhatsApp nodes | From CallMeBot setup |
| Anthropic API Key | n8n Credentials | Claude Opus 4.6 access |
| Groq API Key | n8n Credentials | Free tier works |
| Gemini API Key | n8n Credentials | Gemini Pro access |
| Apify API Key | n8n Credentials | Actor: `nwua9Gu5YrADL7ZDj` |
| Google Sheets OAuth2 | n8n Credentials | Standard OAuth flow |
| LinkedIn OAuth2 | n8n Credentials | Developer app required |
| Twitter OAuth2 | n8n Credentials | Developer app required |

---

## 🧑‍💻 Built By

**Huzaifa** — CS student at IST Islamabad, founder of [WebCorps](https://webcorps.io), building PulseQ (AI in Healthcare) and Pashto GPT.

I build things that do the work I don't have time for. This is one of them.

---

*Ghost-Founder v3.0 — April 2026*
