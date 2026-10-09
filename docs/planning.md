# PLANNING — Rogue Tank Survival 3D

Disusun 9 Okt 2026, diperbarui 10 Okt 2026.
Status: **live** di https://core-tank-frontier.vercel.app/ — fitur stretch hampir selesai.

## Tujuan (diputuskan 9 Okt 2026)
**(B) Game penuh** — MVP + polish + deploy + stretch goals. ✅ diputuskan & dikerjakan.

## Fase 1 — Verifikasi MVP
- [ ] Playtest penuh oleh manusia: main dari wave 1 sampai 10 / game over (belum pernah)
- [ ] Catat bug & rasa main (terlalu gampang/susah? kartu membingungkan?)
- [ ] Fix bug yang ditemukan
- [ ] Tuning dasar difficulty wave 1–3
- Catatan: verifikasi otomatis sudah ekstensif (selftest multiplayer 26/26,
  touchtest 9/9, logic test 22/22) — tapi belum ada playtest manusia penuh.

## Fase 2 — Polish (dikerjakan 9 Okt 2026)
- [x] Balance: wave budget dilunakkan (4 + n*2.5), boss HP 900 → 750, bullet speed 30 → 34
- [x] Juice: floating damage numbers (pooled HTML), low-HP vignette pulse
- [ ] Rapikan menu utama & layar game over/victory (opsional, nanti)

## Fase 3 — Deploy ke Vercel (selesai 9 Okt 2026)
- [x] Deploy via dashboard, dapat URL publik: https://core-tank-frontier.vercel.app/
- [x] Test di desktop (otomatis via browser, 9–10 Okt 2026)
- [ ] Test di HP fisik (kontrol touch & auto-aim belum diuji tangan langsung)

## Fase 4 — Stretch (diputuskan: kerjakan berurutan)
- [x] Meta progression + localStorage (upgrade permanen antar-run) — selesai 9 Okt 2026
- [x] Kartu Legendary dengan efek unik (5 kartu: Phoenix, Juggernaut, Sunfall, Phase Drive, Greed) — selesai 9 Okt 2026
- [x] Sistem Evolusi — draft evolusi unik di wave 3/6/9, boleh kumpulkan beberapa varian (6 evolusi: Vampiric, Chrono, Glass Cannon, Titan, EMP, Adrenaline) — selesai 9 Okt 2026
- [x] Multiplayer co-op 2–4 pemain (P2P WebRTC via PeerJS, host-authoritative; room code; difficulty auto-scale by player count) — selesai 9 Okt 2026
  - E2E verified 9 Okt 2026 (live, 2 browser sessions + deterministic loopback selftest `?selftest=1`):
    lobby/kode room, guest join P2P, snapshot host→guest (tank+musuh+HUD), input guest→host (gerak & tembak ter-spawn),
    damage host→guest, auto-scale difficulty (12 musuh wave 1 untuk 2 pemain), overlay "menunggu wave berikutnya" saat guest mati.
  - 4 pemain verified 10 Okt 2026 (`?selftest=1&guests=3`, 26/26 PASS): 3 guest P2P + lobby 4 pemain, input/gerak/tembak tiap guest,
    draft per pemain tersinkron (tiap guest dapat part berbeda), kill → respawn wave 2 dengan 50% HP (70 HP terukur).
  - By design: host keluar → room bubar (belum ada host migration).
  - Perbaikan dari hasil uji: spawn protection 2 dtk tiap mulai wave; counter "sisa musuh" guest kini termasuk antrian spawn.
- [x] Varian arena & obstacle — selesai (10 agen, 10 Okt 2026)
  5 tema arena (Reruntuhan Baja, Gurun Senja, Kutub Es, Rawa Neon, Kawah Vulkanik;
  ganti tiap 2 wave, boss wave 10 selalu Kawah Vulkanik), obstacle circle-collider
  deterministik (mulberry32 + runSeed, 5 gaya layout, sinkron host→guest),
  spawn aman & hindari spawn player. Verified: selftest 12/12 PASS (tanpa regresi co-op).
- [x] Kontrol touch untuk mobile — selesai (10 agen, 10 Okt 2026)
  Joystick kiri dinamis, sentuh kanan = aim + auto-fire, tombol DASH & SUARA,
  CSS responsif + viewport mobile. Verified: `?touchtest=1` 9/9 PASS.
  Desktop mouse/keyboard tidak berubah.
- [x] Perbaikan mobile lanjutan — selesai (10 Okt 2026, commit 5c128e0)
  Auto-targeting: turret otomatis membidik musuh terdekat (radius 48, termasuk
  boss); aim manual jadi fallback saat tidak ada musuh. Dash jadi kemampuan
  dasar semua pemain (sebelumnya terkunci di part Overdrive); Overdrive
  di-rework jadi pengurang cooldown dash 6→4 dtk (Phase Drive tetap 3 dtk +
  damage). Tombol fullscreen: LAYAR PENUH di menu + LAYAR di HUD touch.
  Verified: logic test auto-aim 6/6 PASS (Node), syntax OK.
  Catatan: dash baseline adalah perubahan desain (dulu eksklusif Overdrive).
- [x] Stage intro "GENERATING WORLD" + bangunan destructible — selesai (10 Okt 2026, commit 183f9cdf2)
  Tiap wave: overlay GENERATING WORLD + progress bar, bangunan jatuh dari langit
  satu per satu (stagger deterministik, efek debu + bunyi thud + squash saat
  mendarat, tank didorong keluar dari zona jatuh). Musuh/boss baru spawn setelah
  semua bangunan mendarat. Bangunan bisa dihancurkan peluru pemain (HP
  30+r*14) -> pecah jadi 10 puing dinamis (fisika jatuh-pantul-fade).
  Sinkron host->guest via event 'obst'; guest menjalankan animasi intro lokal.
  Verified: logic test 22/22 PASS (Node), syntax OK.
- [ ] Daily run / leaderboard (butuh backend — scope besar)

## Backlog (ide ditunda)
- [ ] Visual evolution system — tiap part/evolusi mengubah tampilan tank
  (laras AP panjang, scatter lebar, knalpot menyala, pelat armor, Titan membesar, dll.)

## Status (10 Okt 2026)
- Game live di Vercel, semua stretch selesai kecuali Daily run/leaderboard.
- Head commit: `183f9cdf2` (stage intro + destructible buildings).
- Yang belum: playtest manusia penuh wave 1–10, tuning difficulty dari data,
  rapikan menu/game-over/victory, test HP fisik, visual evolution system,
  daily run/leaderboard (butuh backend), host migration (opsional).
- Rekomendasi berikutnya: playtest penuh → tuning → polish menu.

## Keputusan (semua sudah diputuskan)
1. ~~Tujuan akhir: (A) demo / (B) game penuh?~~ → **(B)**, 9 Okt 2026.
2. ~~Item stretch mana yang prioritas?~~ → Berurutan: meta → legendary →
   evolusi → multiplayer → arena → touch → stage intro. Daily run/leaderboard
   terakhir (butuh backend).
