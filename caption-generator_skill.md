---
name: caption-generator
description: Bikin caption kreatif anti-AI-slop dengan voice Gen Z + corporate buat Threads/sosmed. Use when user minta nulis caption, bikin konten, atau revisi teks biar nggak kedengeran kayak AI.
category: copywriting
version: 1.0.0
author: Tazkia & Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [copywriting, caption, gen-z, anti-ai-slop, threads, content-creation]
    related_skills: [humanizer-text, github-trending-hunter, paper-journal-hunter, tech-trend-hunter, zernio-poster]
---

# Caption Generator — Gen Z, Anti AI Slop

Framework bikin caption yang kedengeran ditulis manusia: ada opini, spesifik, relatable. Nggak template, nggak bombastis kosong.

## Trigger
- User minta caption / konten sosmed
- Pipeline Post-Holic (setelah hunt trending)
- **WAJIB:** baca `data/content-feedback.md` dulu — semua feedback user di sana BINDING

## Struktur Caption (fleksibel, bukan rumus kaku)
1. **Hook (1–2 baris pertama):** langsung nyentuh. Pertanyaan relatable, hot take, atau fakta spesifik yang bikin berhenti scroll. Contoh: *"gue baru nyadar 90% repo 'AI wrapper' di trending cuma bungkus API orang."*
2. **Konteks (2–4 baris):** jelasin singkat apa ini, kenapa lagi rame. Kasih angka/use case nyata dari repo.
3. **Opini/Insight:** punya posisi. Setuju/nyinyir/antusias — yang jelas bukan netral robot. Kasih sudut pandang dev yang ngerti.
4. **CTA (opsional):** ajak ngobrol, bukan ajak beli. *"menurut lo worth it gak?"* / *"coba gas, 5 menit."*
5. **Link (WAJIB):** kalau konten soal repo/produk → taruh URL lengkap di baris terakhir caption. JANGAN post soal repo tanpa link. Link = satu-satunya alasan orang pindah dari Threads ke GitHub.

## Updated Guidance (Feedback)
- Hindari pengulangan frasa *gokil bangettt* atau *daginggg bangettt* dalam satu batch caption.
- Sertakan **penjelasan singkat** (1–2 frasa) tentang apa yang repo lakukan / fiturnya utama sebelum CTA.
- Contoh: *"Hindsight nyimpen memori agent, belajar dari pengalaman, jadi agen lebih pinter tiap iterasi"*.
- Tetap pertahankan **Gen Z tone** (slang, double‑letter, maks 2 kalimat), **NO colon** atau dash, **NO emoji**.
- Pastikan **link repo** ada di akhir caption.
- Jika repo bersifat tutorial, beri *hook* belajar dan *CTA* "gas".

## Copywriting Frameworks (WAJIB Dipakai)

Setiap caption HARUS menggunakan salah satu framework berikut. Pilih yang paling cocok untuk konteks repo:

### 1. PAS (Problem → Agitation → Solution) — Default untuk repo teknis
- **Problem:** Sebutkan pain point spesifik (contoh: "Agent kamu repeat error sama terus")
- **Agitation:** Tunjukkan konsekuensi (contoh: "Nggak pakai memory manual = debug berulang")
- **Solution:** Repo sebagai jawabannya (contoh: "Hindsight simpan semua interaksi, belajar otomatis")

### 2. BAB (Before → After → Bridge) — Untuk tool/transformasi
- **Before:** Kondisi sekarang (contoh: "Automation butuh wrapper API manual")
- **After:** Kondisi ideal (contoh: "Cukup bilang perintah alami, agent eksekusi langsung")
- **Bridge:** Repo sebagai jalan (contoh: "CLI-Anything ubah aplikasi jadi agent-native")

### 3. FAB (Feature → Advantage → Benefit) — Untuk fitur spesifik
- **Feature:** Apa yang repo lakukan (contoh: "Notebook siap jalan + modul teori + deployment")
- **Advantage:** Artinya apa praktisnya (contoh: "Nggak perlu nyari tutorial terpisah")
- **Benefit:** Outcome buat user (contoh: "Belajar AI engineering lengkap dari nol di satu tempat")

### 4. Unity Principle (Cialdini) — Selalu sertakan
Gunakan "kita/kitak" untuk shared identity developer Indo:
- "Buat kita yang bikin agent, memory manual itu neraka"
- "Kita semua udah pernah debug error sama berkali-kali"

## Voice Rules (Updated)
- Caption Threads: 1–3 paragraf pendek, total **150–300 karakter** (kalau lebih, bikin thread, bukan 1 post). Nggak harus selalu bullet. Kadang satu kalimat panjang yang mengalir itu lebih manusiawi.
- **DILARANG pakai em dash (—), en dash (–), atau strip buat nyambungin kalimat.** Ganti dengan koma, titik, atau baris baru. Karakter "-" cuma boleh buat angka/nama file/repo.
- **HINDARI penggunaan ":" berulang** — titik dua yang ngejelasin (contoh: *"harganya: $5 per 1M token"*, *"fiturnya: code review, debugging"*) itu pola AI banget. Ganti dengan titik, koma, atau tulis ulang jadi kalimat mengalir: *"harganya $5 per 1M token"*, *"ada code review, debugging, semua lengkap"*. Paling banter 1x per caption, itupun kalau nggak ada cara lain.
- **PAKAI POLA DOUBLE HURUF (SEKADARNYA):** Jangan berlebihan! Maksimal **1 kata double huruf per caption** (contoh: *bangettt* atau *siiih*, jangan digabung keduanya atau diulang di tiap kalimat). Cukup taruh di momen emosi yang pas. Kalau kebanyakan, malah keliatan kaku dan menyelemen.
- **JANGAN menuhin caption sama angka** — 1 angka penting maksimal per caption (stars, harga, skor benchmark). Sisanya ceritain dengan kata: "naik gila-gilaan", "tempo hari masih ribuan", "harganya lumayan murah". Angka yang numpuk (stars + forks + upvotes + tanggal) itu keliatan kayak laporan, bukan obrolan. Detail angka lengkap cukup di laporan ke user, bukan di caption.
- **Formal detector:** kalau kalimatnya bisa dipindah ke email kerja tanpa diubah → terlalu formal, tulis ulang. Tanda formal: "resmi", "menariknya", "relevan banget", "pantas dicoba" dipake berulang. Ganti dengan reaksi natural: "nggak nyangka", "lah kok gitu", "waduh", "seru sih".
- **WAJIB ada detail spesifik (anti-general):** kalau caption bisa dipake buat topik lain tanpa diubah → terlalu general, tulis ulang. Jangkar spesifik yang bikin unik:
  - Nama konkret: nama model (Llama 3.1 8B, GPT-5.6 Sol), nama chip (HC1), nama tool (Claude Code, Codex), nama orang
  - Angka terukur (1 saja): "16.960 token per detik", "48x lebih cepat dari GPU Nvidia"
  - Use case nyata: "agent install package, modify config, jalan unattended"
  - Perbandingan konkret: "beda sama GPU biasa, bobot model di-etch langsung ke silicon"
  - Test: ganti nama topiknya dengan topik lain — kalau caption masih masuk akal, berarti terlalu general.
- Pake emoji secukupnya (**1–2 per caption, maks 3**) biar seru, nggak tiap kalimat. Emoji bukan hiasan — pakai di momen yang emang ngedorong emosi: reaksi (😅😂😳), punchline (🔥💀), atau ajakan (👀). Contoh: *"...debugging jam 2 pagi 😅"*, *"...masih awal sih tapi menarik 👀"*. JANGAN: "🔥🔥🔥", "💯💯", emoji di tiap kalimat, atau emoji yang nggak nyambung sama isi.

## Gaya @gn.hermes (referensi voice — hasil analisis)
Akun Threads `@gn.hermes` (Anak Intern di Pawbytes) narik engagement karena nulis kayak orang ngobrol, bukan nge-review. Pola yang bisa ditiru:
- **Hook-nya penemuan, bukan laporan:** *"baru nemu repo nih..."*, *"72rb stars di GitHub dan gw ngerti kenapa..."* — mulai dari rasa penasaran, bukan "hari ini ada repo X".
- **Nada orang yang lagi riset, bukan yang udah jago:** boleh bilang *"gw cobain pasang ke project, beda bangettt hasilnya"* HANYA kalau beneran dicoba. Kalau belum → *"keliatan menarik, mau gw coba"* / *"pantas dicoba"*.
- **Singkatan santai manusiawi:** *tp* (tapi), *dr* (dari), *doang*, *nih*, *deh*, *yg*, *gak* — wajar di chat, nggak berlebihan.
- **Persona relatable:** kadang nyeletuk konteks pribadi (intern, project kecil, struggle) biar nggak robot.
- **Referensi tokoh/angka spesifik:** nyebut nama (Karpathy, Addy Osmani) atau angka (72rb stars, 26 replies) biar ada jangkar kredibilitas.
- **Campur Inggris dikit:** *"kinda funny how everyone's pitching themselves..."* — wajar buat dev Indonesia.
- Tetap pendek: 150–300 karakter, hook di kalimat pertama.

## 🚫 Guardrail: JANGAN Klaim Pengalaman Palsu
- **DILARANG:** *"gue udah nyoba"*, *"setelah gue pake"*, *"works great for me"*, *"gue tes langsung"* — kalau gue (Posty) nggak beneran nyobain repo/paper itu.
- **Ganti dengan:** *"keliatan menarik"*, *"pantas dicoba"*, *"dari deskripsinya..."*, *"katanya..."*, *"mau gw coba"*, *"ada yang udah nyoba?"*.
- Kalau mau ngasih kesan "hands-on", kutip pengalaman orang lain dengan jelas: *"beberapa dev bilang..."*, *"di thread-nya, author ngejelasin..."* — jangan ngaku pengalaman sendiri.
- Guardrail ini berlaku juga buat paper/jurnal: nggak boleh klaim "gue baca full paper" kalau cuma baca abstrak.

## 🔗 Link: WAJIB Bisa Dibuka
- Setiap link di caption (repo GitHub / paper arXiv) HARUS diverifikasi dulu:
```bash
curl -s -o /dev/null -w "%{http_code}" -I "<URL>"
```
- `200` → aman. `301/302` → pakai URL final (ikutin redirect). `404` → cari link yang bener atau buang topik itu.
- **`403` belum tentu mati** — banyak situs berita block curl (openai.com, axios, nytimes). Kalau kena 403, verifikasi ulang pakai `web_extract`; kalau kebaca → link valid.
- Link yang belum diverifikasi → JANGAN dipakai di caption. Lapor "link tidak terverifikasi".
- Link repo GitHub: `https://github.com/owner/repo` (bukan link yang belom tentu). Link paper: `https://arxiv.org/abs/<id>`.


## 🚫 Banned Words / AI Slop Detector
Kalau ketemu frasa ini di draft → TULIS ULANG:
- "In today's fast-paced world", "In the ever-evolving landscape"
- "🚀", "game-changer", "revolutionize", "unlock the power of", "elevate your", "supercharge"
- "delve into", "let's dive in", "embark on", "journey"
- "It's important to note", "In conclusion", "Furthermore", "Moreover"
- "Whether you're a beginner or an expert"
- "This is a game-changing tool that empowers developers"
- Emoji spam, "🔥🔥🔥", "💯💯"
- Kalimat tanpa isi: "This project is really cool and useful!"
- Em dash (—) / en dash (–) sebagai penghubung kalimat. Ganti pakai koma/titik/baris baru.

## Self-Check Checklist (sebelum kirim)
- [ ] Pake emoji 1–2 per caption di momen emosional (bukan spam)?
- [ ] Ada 1–2 kata dengan pola double huruf (ihh, bolehh, bangettt, siiih)?
- [ ] Kedengeran kayak orang ngobrol? Baca keras-keras — kalau kaku, revisi.
- [ ] Ada opini/posisi? (bukan sekadar deskripsi netral)
- [ ] Ada detail spesifik? (nama repo, angka stars, use case)
- [ ] Max 1–2 slang per kalimat, nggak ada slang basi?
- [ ] Nggak ada frasa banned list di atas?
- [ ] Nggak ada karakter "—" / "–" buat nyambungin kalimat?
- [ ] Nggak ada pola ":" yang ngejelasin berulang (max 1x, atau 0)?
- [ ] Maksimal 1 angka penting (sisanya kata-kata)?
- [ ] Ada detail spesifik (nama model/chip/tool, angka, use case nyata)?
- [ ] Caption masih masuk akal kalau topiknya diganti topik lain? (kalau iya → general, tulis ulang)
- [ ] Nggak kedengeran formal (bisa masuk email kerja = tulis ulang)?
- [ ] Link repo/produk (URL lengkap) ada di caption?
- [ ] Link udah diverifikasi bisa dibuka (HTTP 200/redirect OK)?
- [ ] Nggak ada klaim "gue udah nyoba/pake" yang palsu?
- [ ] Panjang 150–300 karakter?
- [ ] Hook-nya bikin penasaran?
- [ ] Kalau caption bisa ditulis ChatGPT dengan template yang sama → tulis ulang.

## Contoh: Sebelum → Sesudah (standar kualitas)

### ❌ Sebelum (panjang, AI, pake em dash, tanpa link)
Addy Osmani — mantan Chrome dev advocate yang terkenal — bikin repo agent-skills: production-grade engineering skills buat AI coding agent. Bukan sekadar prompt, tapi prosedur lengkap biar agent kerja kayak senior dev: code review, debugging, testing, sampai deploy. 85 ribu stars, dan hari ini masih naik +680. Yang gue suka: ini ngeformalin pola yang udah kita terapin — agent nggak cukup dikasih instruksi, dia butuh skill yang reusable. Gratis, coba gas.

### ✅ Sesudah (pendek, manusia, Gen Z, ada link)
Addy Osmani (yang dulu di Chrome) bikin kumpulan "skill" buat AI coding agent. bukan prompt random, ini prosedur lengkap: code review, debugging, testing, deploy. jadi agent bisa kerja kayak senior dev beneran. 85k stars dan masih nambah. gratisan, gas cobain

https://github.com/addyosmani/agent-skills

## Referensi
- Kalau draft masih kedengeran AI, jalankan lewat skill `humanizer-text` buat polesan ekstra.
- Panjang ideal Threads: 200–450 karakter. Lebih dari itu bikin thread, bukan 1 post.

## Verify
- Baca draft keras-keras + jalankan checklist. Kalau lolos semua, caption siap post.
