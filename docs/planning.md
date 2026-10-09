# PLANNING — Rogue Tank Survival 3D

Disusun 9 Okt 2026. Status: MVP prototipe jadi, belum playtest.

## Tujuan (diputuskan 9 Okt 2026)
**(B) Game penuh** — MVP + polish + deploy + stretch goals.

## Fase 1 — Verifikasi MVP
- [ ] Playtest penuh: main dari wave 1 sampai 10 / game over
- [ ] Catat bug & rasa main (terlalu gampang/susah? kartu membingungkan?)
- [ ] Fix bug yang ditemukan
- [ ] Tuning dasar difficulty wave 1–3

## Fase 2 — Polish (dikerjakan 9 Okt 2026)
- [x] Balance: wave budget dilunakkan (4 + n*2.5), boss HP 900 → 750, bullet speed 30 → 34
- [x] Juice: floating damage numbers (pooled HTML), low-HP vignette pulse
- [ ] Rapikan menu utama & layar game over/victory (opsional, nanti)

## Fase 3 — Deploy ke Vercel (selesai 9 Okt 2026)
- [x] Deploy via dashboard, dapat URL publik: https://core-tank-frontier.vercel.app/
- [ ] Test URL di desktop & HP (ekspektasi: desktop optimal)

## Fase 4 — Stretch (diputuskan: kerjakan berurutan)
- [x] Meta progression + localStorage (upgrade permanen antar-run) — selesai 9 Okt 2026
- [x] Kartu Legendary dengan efek unik (5 kartu: Phoenix, Juggernaut, Sunfall, Phase Drive, Greed) — selesai 9 Okt 2026
- [x] Sistem Evolusi — draft evolusi unik di wave 3/6/9, boleh kumpulkan beberapa varian (6 evolusi: Vampiric, Chrono, Glass Cannon, Titan, EMP, Adrenaline) — selesai 9 Okt 2026
- [x] Multiplayer co-op 2–4 pemain (P2P WebRTC via PeerJS, host-authoritative; room code; difficulty auto-scale by player count) — selesai 9 Okt 2026
- [ ] Varian arena & obstacle
- [ ] Kontrol touch untuk mobile
- [ ] Daily run / leaderboard (butuh backend — scope besar)

## Backlog (ide ditunda)
- [ ] Visual evolution system — tiap part/evolusi mengubah tampilan tank
  (laras AP panjang, scatter lebar, knalpot menyala, pelat armor, Titan membesar, dll.)

## Status (9 Okt 2026)
- MVP prototipe selesai (`index.html`) — sudah cek sintaks + review logika, belum playtest visual.
- Planning disetujui sampai Fase 3; Fase 4 (stretch) ditunda — diputuskan nanti.
- Berikutnya saat lanjut: playtest MVP → bugfix → polish → deploy Vercel.

## Keputusan yang dibutuhkan
1. **Tujuan akhir**: (A) demo playable buat portofolio, atau (B) game penuh?
2. Item stretch mana yang prioritas (jika B)?
