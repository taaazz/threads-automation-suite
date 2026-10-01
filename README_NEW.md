# 🧵 Threads Automation Suite (MBG - Merek Bot Gweh)

A comprehensive suite of tools for automating engagement, trend hunting, and promotional activities on the Threads platform. This project integrates AI-driven content generation (Posty) and automated response systems (AwareNest).

## 🚀 Core Modules

### 1. AwareNest (Auto-Reply Agent)
An intelligent agent that monitors Threads posts and replies based on specific triggers and product knowledge.
- **Tech Stack:** Playwright, Python, Zernio API.
- **Key Feature:** Stealth browser automation to bypass Meta's bot detection.
- **Workflow:** State Persistence $ightarrow$ Stealth Interaction $ightarrow$ AI Reply Generation $ightarrow$ Submission.

### 2. Posty (Trend Hunter & Content Creator)
Automates the discovery of trending tech repositories on GitHub and transforms them into human-like Threads posts.
- **Tech Stack:** GitHub API, Zernio API, SerpAPI.
- **Workflow:** GitHub Trending Scan $ightarrow$ Angle Selection $ightarrow$ Anti-Slop Captioning $ightarrow$ Auto-Post.

### 3. Promo-In (Promotional Engine)
Manages the distribution of promotional content and tracks engagement.

## 🛠️ Setup & Installation

### Prerequisites
- Python 3.10+
- Google Chrome / Chromium
- GitHub CLI (`gh`) for repository management

### Quick Start
1. **Install Dependencies:**
   ```bash
   pip install playwright
   playwright install chromium
   ```

2. **Session Setup:**
   Since Meta uses strict bot detection, you must export your login session from a residential IP:
   - Run the session export script (refer to `storage_state.json` logic).
   - Copy `storage_state.json` to your project root.

3. **Configuration:**
   Set up your `.env` file with the following keys:
   - `ZERNIO_API_KEY`: For posting and account management.
   - `SERPAPI_API_KEY`: For research and trend hunting.
   - `FIRECRAWL_API_KEY`: For deep scraping.

## ⚠️ Critical Operational Notes

- **Residential IP Required:** The `write` actions (replying, posting) MUST be executed from a residential IP. VPS/Cloud IPs are often flagged and blocked by Meta.
- **Anti-Bot Evasion:** The system uses `navigator.webdriver = false` and specific Chromium flags to minimize detection risks.
- **Human-Centric Content:** All captions generated follow a strict "Anti-AI Slop" guideline to maintain high engagement and avoid being flagged as spam.

## 📁 Project Structure
- `/autoreply`: Logic for monitoring and responding to comments.
- `/promo-in`: Tools for promotional campaigns.
- `/data`: Storage for logs, dumps, and JSON states.
- `README.md`: Main documentation.
- `ROADMAP.md`: Future development plans.

---
*Developed for the Mebiso ecosystem.*
