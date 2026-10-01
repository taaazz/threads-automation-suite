---
name: post-holic
description: Post-Holic content workflow for Threads automation
category: content-management
version: 1.0.0
---
# Post-Holic Content Workflow Skill

**Version:** 1.0.0  
**Profile:** post-holic  
**Managed By:** Hermes Agent  
**Last Updated:** 2026-09-17  

---

## Overview

This skill governs the Post-Holic content workflow for Threads automation. It encompasses content generation, auto-reply, product promotion, and scheduling operations for the `@dummythingsinside` and `@butterrbutbetterr` Threads accounts.

**Core Philosophy:** Anti-AI-slop, Gen Z voice, verified product knowledge, soft-sell promo, community tags as plain text.

---

## Triggers

Use this skill when running the Post-Holic daily pipeline, handling Threads comments via Zernio, or scheduling promotional content for Pahlawan Digital products.

---

## Workflow: Daily Content Pipeline (post-holic-daily-pipeline)

### 1. GitHub Trending Hunt
- **Tool:** `github-trending-hunter`
- **Filter:** Repos relevant to dev/creator audience
- **Output:** 2 daily tech repos + 1 promo product

### 2. Caption Generation (`caption-generator`)
- **Load:** `humanizer-text` for pattern reference ONLY
- **DO NOT load:** `humanizer` (full anti-AI-slop rewrite) — this bends voice toward blandness
- **Rules embedded in prompt:**
  - No `:` (colon) in daily tech captions
  - No `-` (hyphen/dash) in daily tech captions (allowed in promo bullet points `•`)
  - Max 1 emoji per reply, random 30%
  - Gen Z voice: `gue/lu`, `bangettt`, `siiih`, `gokil`, `mantap`, `kocak`
  - Anti-slop patterns: no bullet points in daily, no template phrases ("senang membantu", "semoga bermanfaat")
  - CTA: soft-sell, ask to comment "komen aja nanti gue spill detailnya"
  - Output: HANYA teks balasan, tanpa pembuka/penutup formal

### 3. Promo Post Formatting
- **Media:** Wajib dari folder `data/media/` sesuai produk
- **Tag community:** Teks biasa di akhir (tanpa `#`), contoh: `"— Pahlawan Digital"`
- **Bullets:** Hanya di promo, format `• fitur teknis`
- **No link di caption:** CTA hanya "komen aja nanti spill", link kirim via auto-reply
- **Product knowledge:** Verified via web scraping `pahlawandigital.com`, JANGAN hallucinate capability

### 4. Scheduling
- **Cron:** `post-holic-daily-3konten` jam 08:00 WIB, post ke 13:00 WIB
- **Retry logic:** Jika gagal (timeout/API error), coba lagi 1 jam kemudian
- **Delivery:** `origin` (kembali ke chat ini)

---

## Workflow: Zernio Auto-Reply (`zernio-auto-reply`)

### 1. Webhook Receiver & Analytics Integration
- **Endpoint:** `postys.duckdns.org/webhooks/zernio`
- **Filter:** Skip own accounts (`dummythingsinside`, `butterrbutbetterr`)
- **Guardrails:** Skip sensitif, OOC, spam, code requests, komentar terlalu pendek tanpa keyword valid
- **Analytics Sync:** Gunakan `/api/v1/analytics?accountIds=...` untuk menarik metrics (likes, comments, shares, views, engagement) sesuai update Zernio Tech Support (September 2026).
- **Error Handling:** Abaikan gangguan sementara (seperti billing 500 dari Zernio) dengan retry logic.

### 2. Draft Generation
- **Prompt Rules (Gen Z Override):**
  - No AI-slop patterns (detailed in product-knowledge.md)
  - RHYTHM: Campur kalimat pendek dan panjang
  - STYLE: Santai, slang natural, opini jujur, tidak templated
  - NO BULET POINT di daily, BOLEH di promo
  - EMOJI: 0-1 emoji secara natural
  - POST-PROCESS: strip `Balasan:`, `Draft:`, `---`, konfirmasi AI

### 3. Approval Flow
- **@dummythingsinside:** AUTO REPLY (langsung approved)
- **@butterrbutbetterr:** MANUAL APPROVAL (Discord `gas <id>` atau `oke <id>`)

### 4. Product Override Logic
- Jika komentar mengandung keyword produk (adgen, ideasy):
  - Override draft jadi: `link detailnya langsung cek di sini ya [URL] + [MEDIA PATH]`
  - Jangan pakai format "spill di komentar"

---

## Product Knowledge Base

**Source:** `data/product-knowledge.md` (verified via web scraping 2026-09-17)

**Key Products:**
1. **AdGen AI** — Visual AI (1 foto model + 1 foto produk → ribuan variasi iklan). Harga: Rp 29.000 promo.
2. **Adgen Pro** — Creative Engine (model + visual + script + voice-over 1 alur). Harga: Rp 59.000 promo. **TIDAK** fitur scraping Meta Ads.
3. **Ideasy + AdScale Lab** — Ide konten + analisis Meta Ads Library. Harga: Rp 249.000 promo.
4. **PersonaCore AI** — Buyer persona & script funnel. Harga: Rp 99.000 promo.
5. **Hero Kilat** — Landing page builder Scalev/Lynk.id. Harga: Rp 199.000 promo.

**Anti-Hallucination Rules:**
- Jangan klaim "scraping ratusan iklan" kecuali produk spesifik yang support fitur itu
- Fokus pada fitur yang terverifikasi di landing page resmi
- Semua harga dan fitur harus sesuai `data/product-knowledge.md`

---

## Tag Community Rule

**Promo posts only:**
- Tambahkan tag di akhir caption sebagai teks biasa
- Contoh: `"— Pahlawan Digital"` (BUKAN `#PahlawanDigital`)
- Daily tech posts: TIDAK pakai tag community

---

## Cron Jobs

### `post-holic-daily-3konten`
- **Schedule:** `0 8 * * *` (08:00 WIB) + manual trigger
- **Skills:** `post-holic-daily-pipeline`, `github-trending-hunter`, `caption-generator`, `zernio-poster`
- **Status:** Aktif, retry-on-fail dijalankan 1x perjam

### `zernio-comment-notify-hourly`
- **Schedule:** `0 * * * *` (setiap jam)
- **Skills:** `zernio-auto-reply`, `zernio-poster`
- **Status:** Aktif, monitoring komentar baru

---

## Pitfalls & Troubleshooting

### 1. Humanizer Overuse
- **Gejala:** Konten terasa "AI-ish", formal, tanpa soul
- **Penanganan:** Lepaskan `humanizer` skill sepenuhnya di pipeline caption. Gunakan Gen Z Override di prompt rules saja.

### 2. Link di Caption
- **Gejala:** Caption terlihat "spam" atau "AI-generated"
- **Penanganan:** Jangan menyisipkan URL link di caption promo. CTA: "komen aja nanti spill"

### 3. Kolon dan Strip
- **Gejala:** `:` dan `-` terlalu banyak di daily tech
- **Penanganan:** Filter otomatis di prompt rules. Hanya promo yang bole punya bullet `•`.

### 4. Media Skip
- **Gejala:** Promo post tanpa gambar = engagement turun
- **Penanganan:** Selalu cek folder `data/media/` sebelum schedule. Jika missing, jadwal jadi "draf" dulu.

### 5. Cron Timeout
- **Gejala:** Job gagal tiba-tiba
- **Penanganan:** Cron sudah dilengkapi retry-on-fail (1 jam kemudian). Cek log `last_status` dan `last_delivery_error`.

---

## Support Files

**`references/product-verification.md`** — Catatan verifikasi produk dari web scraping (tidak termirror upstream docs, hanya catatan yang relevan untuk task)

**`templates/caption-template.md`** — Template caption awal yang bisa dimodifikasi per post

**`scripts/verify-product-knowledge.sh`** — Script cek cepak apah produk knowledge sudah aktual (grep URL, harga, fitur kunci)

---

## Skill Interaction Map

```
post-holic-daily-pipeline
      │
      ├─► github-trending-hunter  ──► List repo trending
      ├─► caption-generator       ──► Generate anti-slop caption
      │
      ▼
zernio-poster
      │   ├─ Upload media
      │   ├─ POST /api/v1/posts
      │   └─ Return post_id + platformPostUrl
      │
      ▼
SAVE: posted_repos.json, promo-log.md

┌──────────────────────────────────────────────────────┐
│ zernio-auto-reply (:8000)                           │
│   │                                                   │
│   ├─ Filter own accounts                              │
│   ├─ Guardrails (skip sensitif, OOC, spam)           │
│   ├─ Prompt Rules (Gen Z Override) → Hermes CLI      │
│   ├─ Post-process strip meta-text                    │
│   ├─ Simpan pending_replies                          │
│   ├─ Auto-approve @dummythingsinside → POST Zernio     │
│   └─ Manual approve @butterrbutbetterr → Discord     │
│       notif → wait `gas <id>`                         │
│                                                     │
│   ▼                                                   │
│   REPLY TERKIRIM KE THREADS                           │
└──────────────────────────────────────────────────────┘
```

---

## Update History

**v1.0.0** — 2026-09-17
- Inisialisasi skill ini setelah sesi edukasi pengguna tentang anti-AI-slop, voice Gen Z, aturan format, dan logika cron retry.
- Semua aturan diambil dari feedback user selama sideng 5+ turn konsultasi.
- product-knowledge.md divisualisasi dari web scraping pahlawandigital.com.
- Tag community diterapkan sebagai teks biasa (bukan hashtag).
- "Pahlawan Digital" dilarang dari konten utama.
- Format CTA diubah jadi "komen aja nanti gue spill detailnya".

---

## Related Skills

- `caption-generator` — Digunakan untuk generate caption (tanpa humanizer full pass)
- `zernio-auto-reply` — Digunakan untuk auto-reply Threads comments
- `github-trending-hunter` — Digunakan untuk hunt repo trending harian
- `tech-trend-hunter` — Digunakan untuk riset tren teknologi

---

## References

**`references/product-verification.md`** — Catatan detail produk dari scraping pahlawandigital.com  
**`templates/caption-template.md`** — Template caption awal per post  
**`scripts/verify-product-knowledge.sh`** — Script cek produk knowledge aktual

---