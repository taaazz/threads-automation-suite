# 🧵 Post-Holic Threads Automation Suite

Automation engine and content workflow for Threads using Hermes Agent (Profile: `post-holic`). This project manages daily content pipelines, trend hunting, auto-replying, and promotional distribution via **Zernio API** (100% REST API, no browser automation/Playwright required).

## 🔗 Official Threads Accounts
- **@dummythingsinside** — Primary automation account (Auto-reply: FULL AUTO)
- **@butterrbutbetterr** — Secondary account (Auto-reply: MANUAL APPROVAL)

---

## 🛠️ Skills Dipakai (Hermes Skills Engine)

Sistem ini digerakkan oleh kombinasi skills bawaan di profile `post-holic`:

### 1. Core Workflow
- **`post-holic`** (Main Orchestrator)
  Mengarahkan seluruh siklus posting, jadwal, aturan bahasa Gen Z, dan manajemen product knowledge.
- **`post-holic-daily-pipeline`**
  Menjalankan pipeline harian: ambil trending $ightarrow$ bikin caption $ightarrow$ posting ke Threads.

### 2. Trend Hunting & Research
- **`github-trending-hunter`**
  Mengambil repo tech/dev yang sedang naik daun di GitHub Trending (Daily/Weekly) untuk dijadikan materi konten.
- **`tech-trend-hunter`**
  Riset tambahan seputar rilis AI model, framework, atau tren teknologi terbaru di luar GitHub.

### 3. Content & Anti-Slop Generation
- **`caption-generator`**
  Membuat caption anti-AI-slop bergaya Gen Z + Corporate (menggunakan framework PAS/BAB/FAB & Unity Principle "kita/kitak").
- **`humanizer-text`**
  Referensi pola penulisan alami manusia (menghindari frasa robotik, emoji berlebihan, dan titik dua `:`) .

### 4. Publishing & Auto-Reply (Zernio API)
- **`zernio-poster`**
  Mengunggah gambar (presigned upload) dan mengirimkan postingan ke Threads via Zernio REST API (`POST /api/v1/posts`).
- **`zernio-auto-reply`**
  Menerima webhook komentar Threads dari Zernio, menyaring spam/bot, lalu menghasilkan balasan relevan secara otomatis.
- **`zernio-webhook-management`**
  Mengelola konfigurasi endpoint webhook dan signature verification.

---

## 📁 Susunan Folder Project

```text
/root/.hermes/profiles/post-holic/
├── config.yaml                     # Config profile post-holic (API keys, active skills)
├── .env                            # Key Zernio API, SerpAPI, Firecrawl
│
├── skills/                         # Direktori Modul / Skills Hermes
│   ├── post-holic/                 # Skill Utama
│   │   └── SKILL.md
│   ├── copywriting/                # Generasi Caption & Style Guardrails
│   │   └── caption-generator/
│   │       └── SKILL.md
│   ├── research/                   # Hunter Skill (GitHub & Tech Trends)
│   │   ├── github-trending-hunter/
│   │   │   └── SKILL.md
│   │   └── tech-trend-hunter/
│   │       └── SKILL.md
│   └── social-media/               # Zernio Integration & Pipeline Skills
│       ├── post-holic-daily-pipeline/
│       │   └── SKILL.md
│       ├── zernio-poster/
│       │   └── SKILL.md
│       ├── zernio-auto-reply/
│       │   └── SKILL.md
│       └── zernio-webhook-management/
│           └── SKILL.md
│
├── autoreply/                      # Service Webhook Standalone (Python FastAPI/Flask)
│   ├── zernio_hermes_autoreply.py   # Handler webhook komentar Zernio
│   ├── auto_reply_worker.py        # Worker pemprosesan queue balasan
│   ├── autoreply.db                # SQLite database log balasan
│   └── .env                        # Mirroring env khusus webhook service
│
└── data/                           # Storage & Knowledge Base
    ├── posted_repos.json           # Log repo agar tidak ter-post 2x
    ├── product-knowledge.md        # Knowledge base Pahlawan Digital (AdGen, Ideasy, dll)
    └── media/                      # Aset gambar promo/produk
```

---

## 🔄 Alur Kerja Sistem (Workflow Pipeline)

### 1. Pipeline Konten Harian (Cron: 08:00 WIB)
```text
[Cron Job] ──> github-trending-hunter
                     │ (Filter repo tech/dev)
                     ▼
             caption-generator
                     │ (Terapkan framework PAS/BAB/FAB, anti-AI-slop, link repo)
                     ▼
               zernio-poster
                     │ (Upload gambar ke Zernio ──> POST /api/v1/posts)
                     ▼
             [Published di Threads] ──> Simpan ke data/posted_repos.json
```

### 2. Alur Auto-Reply Komentar (Real-Time Webhook)
```text
[Komentar di Threads]
         │
         ▼
[Zernio Webhook] ──> /autoreply/zernio_hermes_autoreply.py
                             │
                             ├─► Cek Signature & Filter akun sendiri
                             ├─► Cek Keyword Produk (AdGen, Ideasy, dll)
                             ├─► Generate Balasan via LLM (Gen Z Voice, Tanpa Link di Main)
                             │
                             ▼
                   zernio-poster (API Reply)
                             │
                             ▼
                  [Balasan Terbit di Threads]
```

---

## ⏰ Cron Jobs

- **`post-holic-daily-3konten`**
  - **Schedule:** `0 8 * * *` (Setiap jam 08:00 WIB)
  - **Tugas:** Menjalankan pipeline 2 konten tech/repo + 1 konten promo produk.
- **`zernio-comment-notify-hourly`**
  - **Schedule:** `0 * * * *` (Setiap jam)
  - **Tugas:** Memeriksa log balasan dan performa engagement.

---

*Powered by Hermes Agent profile `post-holic` & Zernio REST API.*
