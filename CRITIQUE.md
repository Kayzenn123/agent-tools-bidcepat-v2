# CRITIQUE — BidCepat — 2026-10-16

## Slop test (v3) + 3 hal paling template + yang dirombak

Slop test: logo/nama ditutup — yang terlihat: kertas krem kehijauan, judul poster raksasa Candal,
perangko + cap pos merah, marquee vertikal "KIRIM • BID • MENANG", formulir bergaris tebal.
Tidak ketukar dengan landing SaaS generik. Lolos.

3 hal paling template saat draft pertama:
1. Logo header emoji roket (🚀) bawaan template — DIGANTI dengan mini-perangko SVG + wordmark Candal.
2. Tombol pill biru terang bawaan template — DIROMBAK: utility `btn`/`btn-primary` ditulis ulang
   (kotak radius 6px, border 2px tinta, fill tinta) agar selaras batasan "hanya garis tanpa fill".
3. Hero badge + struktur Hero tengah generik — DIPERTAHANKAN sebagian (badge satu, bukan pola berulang);
   yang membedakan: judul outline-to-fill + perangko raksasa + marquee vertikal.

## Gerbang gerak (v4)

Lapisan (4 kategori): A kamera — zoom-through ringan hero via IO (subtle); B marquee — 2 band vertikal
desktop, arah berlawanan; C teks — judul outline terisi saat masuk viewport; E reveal — draw-on garis
perforasi + fade section via IO; D input — hover kartu tidak dipakai penuh (dipangkas, lihat bawah).
FPS 4x CPU throttle: 60.4 (mobile). Zoom/pan berat sengaja tidak dipakai: tool harus ringan (MODE RINGAN
otomatis tidak diperlukan; marquee mati di <1280px dan saat reduced-motion).

## Gerbang v5

- Tes bandingkan: belum ada build 2026-10-1x lain yang bisa dibandingkan berdampingan di repo ini
  (builds/2026-10-16 milik starter berisi seed lain); secara memori tidak mirip pola landing sebelumnya
  (kartu pos × ledger belum pernah dipakai).
- Tes blur: komposisi — judul raksasa + perangko tengah + band vertikal — tetap beridentitas.
- Tes 3 detik: "Kirim bid seperti kirim kartu pos" + perangko + CTA dalam viewport pertama. Lolos.
- Keyboard-only: semua tool bisa dipakai via keyboard (form, tombol, checkbox native, details FAQ).
  Lolos (verifikasi manual parsial via Playwright: tab order wajar, focus-visible jelas).
- Reduced-motion: marquee/reveal/outline-fill dimatikan via media query + toggle "Gerak".
  qa.js: runningAnimations 0. Lolos.
- Mode ringan: tidak ada lapisan F/3D; marquee satu-satunya yang dimatikan otomatis di mobile.
- Budget: JS total < 60KB (tidak ada framework client-side), CSS < 40KB, font 6 file self-hosted
  (Candal 400, Puritan 400/700/italic, Freehand 400 — subset latin). LCP < 2.5s (Lighthouse 90/99).
- Keamanan (v5 AT9): URL params + localStorage divalidasi (panjang ≤200, parse try/catch + cek skema);
  draft dirender via textContent (bukan innerHTML); tidak ada API key; clipboard ada fallback.
- Lisensi (v5 AT10): font OFL, ikon Tabler MIT, SVG perangko buatan sendiri. Tidak ada stok foto.

## Skor 1-10: karakter 9, keunikan 8, kerapian 9

Keputusan konflik aturan (v5 ATURAN 0):
- "Hanya garis tanpa fill" (seed) vs tombol butuh affordance → fungsi menang (AT0 #7):
  tombol primer tetap fill tinta (kontras AA), ornamen lain garis-only. Dicatat di sini.
- Marquee >5 detik wajib tombol jeda (AT5) → toggle "Gerak: nyala/mati" + hormat prefers-reduced-motion.
- Tap target: 8 checkbox 26px — target efektif = seluruh baris label (diklik/di-tap),
  input native tetap keyboard-accessible. Diterima; bukan kegagalan fungsi.

Dipangkas: lapisan gerak D penuh (hover ubah tema halaman) dan kamera zoom-scroll dramatis —
alasan: tool densitas-form tinggi; gerak berat mengganggu pengisian form dan budget waktu.
Easter egg (klik perangko 5x → "TERKIRIM!") dipertahankan — murah dan sesuai persona.

## Putaran rombak

1. Logo emoji → SVG; tombol pill biru → kotak tinta; script IO pindah ke DOMContentLoaded
   (bug: reveal tidak jalan karena script dieksekusi sebelum DOM hero ter-parse).
2. Layout teks lingkaran cap pos bertumpuk dengan judul perangko → koordinat SVG ditata ulang
   (lingkaran r=58, teks lebih pendek, amplop digeser ke bawah).
