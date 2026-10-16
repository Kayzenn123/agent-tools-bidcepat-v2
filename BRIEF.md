# BRIEF — BidCepat — 2026-10-16

## Masalah/usecase (1 kalimat + siapa yang kena)
Freelancer Indonesia yang bid proyek di projects.co.id/Sribu sering bingung nulis pesan bid yang sopan-profesional, salah hitung tarif bersih setelah fee platform, dan kena scam karena tidak cek red flag — BidCepat memberi 3 tool client-side gratis: generator draft bid, kalkulator tarif bersih, dan checklist anti-scam interaktif.

## Konsep visual (1 kalimat)
"Kantor pos penawaran": setiap bid adalah kartu pos yang dikirim ke klien — hero bergaya poster film lawas dengan perangko & cap pos, tool disajikan sebagai lembar ledger/buku besar (spreadsheet sebagai UI), semua ornamen hanya garis tanpa fill (gaya wireframe tinta), aksen tulisan tangan Freehand untuk stempel.

## Hasil seed (ringkas, seed.json di workdir)
- domain: kartu pos | layout: spreadsheet sebagai UI | referensi: poster film lawas
- batasan: hanya garis tanpa fill | ikon: isometrik, sumber Tabler
- font: display Candal, body Puritan, aksen Freehand
- gerak: kamera canvas drag+zoom scroll; marquee vertikal di sisi layar; teks outline terisi saat scroll; hover mengubah tema halaman; reveal garis draw-on lalu isi
- palet: light, triadic, baseHue 104 (hijau): bg oklch(0.96 0.037 104) ~ krem kehijauan, surface oklch(0.90 0.040 104), text oklch(0.20 0.040 104), muted oklch(0.45 0.030 104), accent biru oklch(0.63 0.266 224), accent2 magenta oklch(0.62 0.173 344), pop pink oklch(0.82 0.200 321)

## 3 arah desain + terpilih
1. Kartu pos vintage penuh: kertas kusam, perangko, cap pos merah — hangat tapi bisa terasa seperti toko souvenir.
2. Spreadsheet/ledger murni: tabel garis tebal, monospace, seperti buku kas — fungsional tapi kering.
3. Poster film lawas × kantor pos (TERPILIH): judul display raksasa Candal seperti judul film, ticket-stub/kartu pos sebagai motif, ledger garis untuk area tool. Berani, beda dari landing SaaS, masih fungsional karena garis = struktur.

## Keputusan berani
Satu halaman, satu "meja pos": seluruh tool dirancang sebagai dokumen yang bisa diisi — form generator = formulir pos, kalkulator = tabel ledger dengan garis tanpa fill, checklist = daftar periksa bertanda tangan. Hover pada kartu pos mengubah tema halaman (sesuai seed inputMotion) sebagai easter egg.

## Persona/suara
"Petugas loket pos yang ramah dan tegas": menyapa "Halo, kak!", menjelaskan singkat, copy tombol jelas ("Salin draft", "Hitung tarif"), pesan error membantu ("Nama belum diisi — tulis dulu biar draftnya sopan.").

## Palet (harmoni triadic, light)
- Token OKLCH final: --bg oklch(0.96 0.037 104); --surface oklch(0.90 0.040 104); --text oklch(0.20 0.040 104); --muted oklch(0.45 0.030 104); --accent oklch(0.60 0.20 224) (biru tinta, dipergelap utk kontras); --accent-2 oklch(0.58 0.18 344) (magenta); --pop oklch(0.55 0.22 30) (merah cap pos, dipakai <5%).
- Psikologi: krem kehijauan = kertas & ketenangan; merah cap pos = otoritas resmi; biru tinta = kepercayaan.
- Cek kontras AA: text/bg > 12:1; accent pada bg ~ 5.5:1 (teks besar/button outline); pop hanya untuk stempel grafis besar.

## Font (display/body/aksen)
- Display: Candal (rounded geometric tegas, judul poster). Body: Puritan (serif humanis, paragraf panjang terbaca di 390px). Aksen: Freehand (tulisan tangan utk stempel/label).
- Id Fontsource: candal, puritan, freehand — via Astro Fonts API (self-host, subset latin).

## Ikon (gaya isometrik, sumber Tabler via astro-icon)
12+: tabler:mail, tabler:stamp (cek ketersediaan di icons.json), tabler:send, tabler:calculator, tabler:shield-check, tabler:clipboard-check, tabler:copy, tabler:check, tabler:alert-triangle, tabler:coin, tabler:user, tabler:briefcase, tabler:clock, tabler:file-text. Custom (3+): perangko (rect + perforasi), cap pos lingkaran teks, amplop terbuka — SVG inline.

## Gerak (kategori A-F; narasi: surat berjalan lewat meja pos)
- A kamera: zoom-through ringan di hero (teks raksasa → tools), scroll-scrub sederhana.
- B marquee: 2 band vertikal di sisi layar (desktop) berisi kata "BID • KIRIM • MENANG •" berlawanan arah.
- C teks: judul outline terisi (fill) saat scroll.
- D input: hover kartu pos mengubah aksen tema halaman (toggle, bisa dimatikan).
- E reveal: garis draw-on (stroke-dashoffset) lalu isi konten section.
- MODE RINGAN (hardwareConcurrency ≤4 / Save-Data): matikan marquee + zoom, sisakan reveal sederhana.
- Dipangkas bila waktu mepet: F (tidak dipakai), D (opsional), C sebagian — urutan pangkas sesuai ATURAN 2 v5.

## Storyboard hero moment
| Scroll | Terlihat | Kamera | Marquee | Teks | Interaksi |
|---|---|---|---|---|---|
| 0% | Poster: "BIDCEPAT" raksasa + perangko custom | — | band vertikal jalan | outline | CTA "Buat draft bid" |
| 25% | Cara kerja (Steps) | zoom ringan | — | outline terisi | — |
| 50% | Generator draft (formulir) | — | — | — | isi form → draft muncul |
| 75% | Kalkulator ledger + checklist | — | band kedua | — | hitung, centang |
| 100% | FAQ + CTA kirim | — | — | — | salin, bagikan link |

Pertunjukan utama: hero poster — judul raksasa + perangko & cap pos Freehand, tombol CTA dalam 3 detik.

## Konten (15+ item nyata)
Template draft per kategori (4): UI/UX, Web Dev, Desain Grafis, Penulisan Konten — masing-masing 3 paragraf sopan-profesional dengan placeholder terisi dari form. 8 item checklist anti-scam (nasihat umum): DP via rekber, jangan bayar "biaya admin", cek profil & riwayat klien, minta brief tertulis, kontrak/SPK sederhana, waspada tarif tak wajar, jangan kirim file master sebelum lunas, simpan bukti chat. FAQ 5: apakah gratis, data tersimpan di mana (localStorage, tidak dikirim ke server), fee platform berapa (bisa diubah user, [ISI MANUAL] bila tak ada sumber), cara pakai deep-link, cocok untuk platform apa. Easter egg: ketik "pos" 3x → stempel "TERKIRIM!" muncul.

## Teknik visual orisinal (2+)
1. Perangko custom SVG: rect + perforasi (circle pattern) + cap pos lingkaran teks melengkung.
2. Garis draw-on SVG divider antar section (gerigi seperti sobekan perangko).
3. Pola kertas: noise feTurbulence halus di background.

## Suara
Tidak (default mute, bukan kewajiban).

## Fungsi (v2 FASE 1, diringkas)
- Generator: form → draft (template per kategori), tombol salin (clipboard + fallback), validasi spesifik, localStorage versi key, deep-link via URL params, contoh terisi sekali klik ("Isi contoh").
- Kalkulator: hari × tarif harian + fee % (editable, default [ISI MANUAL]/editable) → total kotor, potongan, bersih; format Rp Intl.
- Checklist: 8 checkbox + progress bar + persen, state tersimpan, reset.
- Empty/loading/error state didesain; tanpa backend (100% client-side, static Astro).
