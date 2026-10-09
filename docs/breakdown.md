# BREAKDOWN — Rogue Tank Survival 3D (Three.js)

**Konsep:** Roguelike survival arena. Kamu = 1 tank vs wave musuh tanpa akhir.
Tiap wave selamat → draft 1 dari 3 kartu part → tank makin kuat → wave makin
brutal. Mati = run selesai. Kamera isometric 3D (Three.js).

---

## 1. Core Loop

```
Menu → Run dimulai (tank standar)
  → Wave N: survive (bunuh semua / bertahan X detik)
  → Draft: pilih 1 dari 3 kartu part (game pause)
  → Wave N+1 (lebih sulit)
  → ... Boss tiap 5 wave
  → Mati → scrap dihitung → upgrade permanen → Run baru
```

Satu run ideal: 10–20 menit. Fokus: keputusan draft + positioning.

## 2. Sistem Part & Kartu (jantung roguelike-nya)

**Slot part tank (6):**

| Slot | Yang diubah | Contoh kartu |
|---|---|---|
| Hull | Max HP, armor | Reinforced Plating (+40 HP), Reactive Armor (20% negate hit) |
| Tracks | Move speed, turn rate | Racing Treads (+25% speed), All-Terrain (no slow di obstacle) |
| Turret | Rotation speed, slot senjata | Fast Traverse (+50% putar), Dual Mount (+1 proyektil) |
| Cannon | Damage, fire rate, tipe peluru | AP Rounds (pierce +damage), Scatter Gun (5 peluru menyebar), Railgun (lambat, damage besar), Missile Pod (homing) |
| Engine | Boost/special resource | Turbocharger (+speed, +turn), Overdrive (dash dengan cooldown) |
| Utility | Efek pasif/aktif | Nanobot Repair (regen HP), Energy Shield (serap damage), Mine Layer, Magnet (radius pickup) |

**Rarity:** Common (putih) → Rare (biru) → Epic (ungu) → Legendary (oranye).
Bobot rarity naik seiring wave. Legendary = mengubah playstyle
(mis. "setiap kill meledak").

**Aturan draft:** 3 kartu random per jeda wave, boleh reroll 1x (bayar scrap).
Kartu duplikat = stack/level-up (maks Lv 3).

## 3. Kontrol & Kamera Isometrik

- **Gerak:** WASD / panah (tank maju-mundur + putar), atau twin-stick
  (gerak WASD + turret ngikut mouse) — pilih twin-stick, lebih fun.
- **Tembak:** klik/tahan mouse (atau auto-fire toggle).
- **Spesial:** Space = ability dari part Utility/Engine (dash, shield).
- **Kamera:** `OrthographicCamera`, offset klasik isometric
  (mis. posisi (12, 14, 12) lihat ke tank), follow pakai lerp biar smooth,
  zoom tetap. Screen shake saat kena hit / ledakan.

## 4. Musuh & Wave Director

**Tipe musuh:**

| Tipe | Perilaku |
|---|---|
| Chaser | Ngejar, nabrak (melee) |
| Speeder | Cepat, HP tipis, datang bergerombol |
| Gunner | Jaga jarak, nembak proyektil |
| Heavy | Lambat, HP tebal, damage besar |
| Boss (tiap 5 wave) | HP bar besar, pola serangan (spread shot, charge, summon) |

**Scaling:** `HP *= 1.15^wave`, `damage *= 1.08^wave`, jumlah & variasi naik.
Spawn dari tepi arena, dengan indikator peringatan 1 detik (fair).

**Arena:** 1 map per run (varian obstacle: kotak, tembok). Obstacle = cover
sekaligus halangan gerak. Batas arena jelas.

## 5. Struktur Roguelike

- **Permadeath per run.** Mati = mulai dari tank standar lagi.
- **Meta progression:** scrap (dari kill) → upgrade permanen antar-run
  (+5% HP, +3% damage, 1 reroll gratis, dsb.). Disimpan di `localStorage`.
- **Pickup di arena:** scrap (mata uang), repair kit (HP), magnet otomatis
  jika punya part Magnet.

## 6. Arsitektur Teknis (Three.js)

- **Model:** low-poly dari primitive (`BoxGeometry`, `CylinderGeometry`) —
  tank = hull box + turret cylinder + laras box + track box. Tanpa asset eksternal.
- **Material/lighting:** `MeshLambertMaterial` + HemisphereLight +
  DirectionalLight. Shadow opsional (matikan demi performa, atau blob shadow).
- **Collision:** 2D circle collider di bidang XZ (jangan pakai physics engine —
  overkill untuk arcade begini).
- **Performa:** `InstancedMesh` untuk peluru & musuh sejenis, object pooling
  (jangan `new` tiap frame), batasi musuh aktif (~40).
- **Game loop:** `requestAnimationFrame` + fixed timestep untuk logika
  (biar konsisten di semua refresh rate).
- **UI:** HTML/CSS overlay (HUD, draft kartu, menu) — jangan gambar UI di canvas.
- **Audio:** WebAudio prosedural (beep/boom sederhana), tanpa file audio.

## 7. Struktur File (prototipe: single file)

```
index.html          # seluruh game dalam satu file (tanpa build step)
docs/
  breakdown.md      # dokumen ini
  planning.md       # planning & roadmap
```

> Catatan: breakdown awal merencanakan struktur multi-file `src/`.
> Untuk prototipe, semuanya digabung ke satu `index.html` agar tinggal
> double-click langsung main. Bisa dipecah lagi saat codebase membesar.

## 8. MVP vs Stretch

**MVP (bisa main & fun):**
- [ ] Gerak + tembak twin-stick, kamera isometric follow
- [ ] 3 tipe musuh (chaser, gunner, speeder) + scaling wave
- [ ] 10 kartu part (2 per slot) + draft 1-dari-3
- [ ] 10 wave + 1 boss sederhana
- [ ] HUD (HP, wave, scrap), layar game over, restart

**Stretch:**
- [ ] 20+ kartu, rarity Legendary dengan efek unik
- [ ] 3+ tipe musuh, boss dengan pola serangan
- [ ] Meta progression + localStorage
- [ ] Partikel ledakan, screen shake, SFX lengkap
- [ ] Varian arena & obstacle
- [ ] Daily run / leaderboard (butuh backend)

## 9. Risiko & Keputusan Penting

1. **Twin-stick vs tank-control klasik** → pilih twin-stick (lebih accessible).
2. **Balance kartu** → taruh semua angka di `config.js`, tuning iteratif.
3. **Scope creep** → kunci MVP dulu; tiap fitur stretch = 1 kartu terpisah.
4. **Performa** → pooling + instancing dari awal, jangan retrofit belakangan.
