# 🧵 Post-Holic Threads Automation

A comprehensive suite of tools and skills for the Hermes Agent `post-holic` profile. This repository focuses on content creation, auto-reply management, and promotional workflows for Threads accounts `@dummythingsinside` and `@butterrbutbetterr`.

## 🔗 Official Threads Accounts
- **@dummythingsinside** — Primary automation account (Auto-reply: FULL AUTO)
- **@butterrbutbetterr** — Secondary account (Auto-reply: MANUAL APPROVAL via Discord)

## 🧠 Skills Architecture

This project runs on **Hermes Agent** with a custom profile `post-holic`. The following skills orchestrate the automation:

### Core Skill: `post-holic`
**File:** `.hermes/profiles/post-holic/skills/post-holic/SKILL.md`

Govern the entire Post-Holic workflow including:
- **Daily Content Pipeline** (`post-holic-daily-pipeline`)
- **Zernio Auto-Reply** (`zernio-auto-reply`)
- **Product Knowledge Management**
- **Cron Job Definitions**

#### Sub-skills Used:

| Skill | Purpose | Trigger |
|-------|---------|---------|
| `github-trending-hunter` | Scans GitHub Trending daily for dev/tech repos | Daily pipeline |
| `caption-generator` | Generates anti-AI-slop captions with Gen Z voice | Daily pipeline, Auto-reply |
| `zernio-poster` | Posts to Threads via Zernio API (media + caption) | Daily pipeline, Auto-reply |
| `zernio-auto-reply` | Handles incoming comments webhook, generates replies | Hourly cron + webhook |
| `humanizer-text` | Reference patterns only (NOT full rewrite) | Caption generation |
| `tech-trend-hunter` | Researches new tech trends beyond GitHub | Weekly/Manual |
| `content-strategy-agent` | Weekly content strategy review | Weekly cron |

### Anti-AI-Slop Rules (Embedded in `caption-generator`)
- **NO** colons (`:`) in daily tech captions
- **NO** hyphens/dashes (`-`) in daily tech captions (bullets `•` allowed in promo only)
- **Max 1 emoji** per reply, ~30% chance
- **Gen Z voice:** `gue/lu`, `bangettt`, `siiih`, `gokil`, `mantap`, `kocak`
- **Anti-slop patterns:** no bullet points in daily, no template phrases ("senang membantu", "semoga bermanfaat")
- **CTA:** Soft-sell only — "komen aja nanti gue spill detailnya"
- **Output:** ONLY reply text, no formal openers/closers

### Product Knowledge Base
**Source:** `data/product-knowledge.md` (verified via web scraping pahlawandigital.com)

**Products:**
1. **AdGen AI** — Visual AI (1 model + 1 product → thousands of ad variations) — Rp 29.000 promo
2. **Adgen Pro** — Creative Engine (model + visual + script + voice-over) — Rp 59.000 promo
3. **Ideasy + AdScale Lab** — Content ideas + Meta Ads Library analysis — Rp 249.000 promo
4. **PersonaCore AI** — Buyer persona & funnel script — Rp 99.000 promo
5. **Hero Kilat** — Landing page builder (Scalev/Lynk.id) — Rp 199.000 promo

## ⏰ Cron Jobs

### `post-holic-daily-3konten`
- **Schedule:** `0 8 * * *` (08:00 WIB) → posts at 13:00 WIB
- **Skills Loaded:** `post-holic-daily-pipeline`, `github-trending-hunter`, `caption-generator`, `zernio-poster`
- **Output:** 2 tech repos + 1 promo product
- **Retry Logic:** On failure (timeout/API error), retry 1 hour later
- **Delivery:** `origin` (returns to this chat)

### `zernio-comment-notify-hourly`
- **Schedule:** `0 * * * *` (every hour)
- **Skills Loaded:** `zernio-auto-reply`, `zernio-poster`
- **Function:** Checks for new comments, processes via webhook logic
- **Status:** Active

## 🛠️ Setup & Installation

### Prerequisites
- Python 3.10+
- Google Chrome / Chromium
- GitHub CLI (`gh`) for repository management
- Hermes Agent installed

### Quick Start
1. **Install Dependencies:**
   ```bash
   pip install playwright
   playwright install chromium
   ```

2. **Hermes Profile Setup:**
   ```bash
   # Ensure profile 'post-holic' exists with skills loaded
   hermes profile use post-holic
   ```

3. **Session Setup (CRITICAL):**
   Since Meta uses strict bot detection, you MUST export your login session from a residential IP:
   - Run session export script (refer to `storage_state.json` logic in autoreply/)
   - Copy `storage_state.json` to project root

4. **Configuration (`.env`):**
   ```bash
   ZERNIO_API_KEY=your_key
   SERPAPI_API_KEY=your_key
   FIRECRAWL_API_KEY=your_key
   # Hermes will load these from profile config
   ```

## ⚠️ Critical Operational Notes

- **Residential IP Required:** Write actions (replying, posting) MUST execute from residential IP. VPS/Cloud IPs are flagged/blocked by Meta.
- **Anti-Bot Evasion:** Uses `navigator.webdriver = false` and Chromium flags to minimize detection.
- **Human-Centric Content:** All captions follow strict "Anti-AI Slop" guidelines for high engagement.
- **Two .env Files Must Sync:** `/root/autoreply/.env` (webhook service) and `post-holic/.env` (posting) — mismatch causes 401 on replies.
- **Product Knowledge Verification:** All product claims must match `data/product-knowledge.md`. No hallucination allowed.

## 📁 Project Structure
```
/
├── autoreply/              # Webhook receiver, comment processor, Zernio integration
│   ├── zernio_hermes_autoreply.py
│   ├── check_new_comments.py
│   └── .env (WEBHOOK SERVICE)
├── data/                   # Logs, posted_repos.json, product-knowledge.md, media/
├── .hermes/
│   └── profiles/post-holic/
│       ├── skills/         # post-holic, caption-generator, etc.
│       ├── config.yaml
│       └── .env (POSTING SERVICE)
├── README.md               # This file
└── ROADMAP.md
```

## 🔧 Skill Workflows

### Daily Content Pipeline (`post-holic-daily-3konten`)
```
1. GitHub Trending Hunt → github-trending-hunter
2. Select 2 tech repos + 1 promo product
3. caption-generator → Generate anti-slop caption (Gen Z voice, no banned patterns)
4. zernio-poster → Upload media + POST /api/v1/posts
5. Save posted_repos.json, update promo-log.md
```

### Zernio Auto-Reply Flow
```
1. Webhook receives comment @dummythingsinside
2. Filter: Skip own accounts, sensitive, OOC, spam, code requests
3. Guardrails: Skip if too short without valid keyword
4. Prompt Rules → Generate reply (Gen Z Override, anti-slop)
5. Post-process: strip meta-text, confirm AI markers
6. @dummythingsinside: AUTO REPLY → POST Zernio
7. @butterrbutbetterr: MANUAL APPROVAL → Discord notification
8. REPLY TERKIRIM KE THREADS
```

---

*Developed for the Mebiso ecosystem. Powered by Hermes Agent.*
