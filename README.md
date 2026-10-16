# BidCepat

**Kantor pos untuk freelancer Indonesia** — tool gratis: generator pesan bid yang sopan-profesional,
kalkulator tarif bersih setelah fee platform, dan checklist anti-scam interaktif. 100% berjalan di browser,
tanpa daftar, tanpa server.

🔗 Live: https://kayzenn123.github.io/agent-tools-bidcepat-v2/ (GitHub Pages; jalur deploy fallback — Vercel MCP write butuh approval yang tak tersedia di subagent)

## Fitur

1. **Generator Pesan Bid** — isi formulir (nama, kategori: UI/UX / Web Dev / Desain Grafis / Penulisan Konten,
   keahlian, pengalaman, estimasi hari, tarif) → draft pesan bid Bahasa Indonesia tersusun otomatis per kategori.
   Tombol salin (dengan fallback), tombol "Isi contoh", validasi per-field, deep-link via URL params
   (`?bid_nama=...`), dan penyimpanan draft di `localStorage`.
2. **Kalkulator Tarif Bersih** — input hari kerja × tarif harian × fee platform (%) → rincian ledger:
   tarif kotor, potongan fee, tarif bersih. Fee platform **bisa diubah sendiri** (tidak ada klaim angka fee tetap).
3. **Checklist Anti-Scam** — 8 pemeriksaan interaktif dengan progress bar, tersimpan otomatis di `localStorage`,
   berisi nasihat umum (DP via rekber, jangan bayar "biaya admin", cek profil klien, dsb).

## Tech

Astro v5 (static) + Tailwind CSS v4 + astro-icon (Tabler) + Astro Fonts API (Candal / Puritan / Freehand, self-hosted).
Nol backend — seluruh logika client-side vanilla JS. Tidak ada tracker/analytics.

## Cara jalanin

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # output ke dist/
```

## QA (2026-10-16, lokal)

| Metrik | Mobile | Desktop |
|---|---|---|
| Lighthouse Performance | 90 | 99 |
| Lighthouse Accessibility | 96 | 96 |
| Lighthouse Best Practices | 100 | 100 |
| Lighthouse SEO | 100 | 100 |
| qa.js (overflow / console / h1 / label) | lolos | lolos |
| FPS CPU throttle 4x | 60.4 | — |

- `npm run check` (astro check + ESLint + Prettier): bersih.
- Tes fungsional Playwright: generate draft, deep-link reload, kalkulator, checklist, validasi error, localStorage — semua lolos, nol `pageerror`.
- Screenshot: `~/agent-lab/proof/bidcepat-2026-10-16/` (mobile-390, desktop-1280, + per-tool).

## Konsep desain

Seed 2026-10-16: domain **kartu pos** × layout **spreadsheet sebagai UI** × referensi **poster film lawas**,
batasan **hanya garis tanpa fill**. Palet light triadic (kertas krem kehijauan, tinta, merah cap pos).
Lihat `BRIEF.md` dan `CRITIQUE.md`.

## Lisensi aset

Font: Candal, Puritan, Freehand (SIL Open Font License, via Fontsource). Ikon: Tabler Icons (MIT).
Perangko & cap pos: SVG digambar sendiri untuk proyek ini.
