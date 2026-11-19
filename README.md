# NEW WORLD DIGITAL — 2D Multiplayer RPG

Versi web 2D top-down untuk GitHub Pages, menggunakan Supabase Auth, Database dan Realtime.

## Fungsi yang disediakan
- Daftar dan log masuk pemain melalui Supabase Auth.
- Pemain yang telah diluluskan MASTER ADMIN boleh masuk ke dunia.
- Peta 2D Pekan Permulaan dengan pergerakan papan kekunci, anak panah dan butang sentuh.
- Kehadiran pemain online (Supabase Realtime Presence).
- Pergerakan avatar pemain lain secara langsung (Realtime Broadcast).
- Sembang dunia global yang disimpan dalam pangkalan data dan dipaparkan secara langsung.
- Misi harian, XP, level, leaderboard dan bekalan coin maya 21,000,000.
- Panel MASTER ADMIN berdasarkan role `MASTER_ADMIN`.

## Jalankan secara tempatan
Buka `index.html` melalui pelayan web statik (contohnya VS Code Live Server atau `python -m http.server 8080`), kemudian lawati `http://localhost:8080`.
Jangan bergantung pada `file://` kerana sesetengah pelayar menyekat permintaan rangkaian daripada fail tempatan.

## Terbitkan ke GitHub Pages
1. Ekstrak ZIP ini.
2. Muat naik **semua fail di dalam folder** (index.html, app.js, style.css, README.md) ke root repository GitHub.
3. Buka Settings → Pages.
4. Pilih Deploy from a branch → `main` → `/ (root)` → Save.
5. Buka URL GitHub Pages yang diberikan.

## Backend
Aplikasi disambungkan kepada projek Supabase yang telah dikonfigurasi. Migrasi `new_world_digital_persistent_world_chat` menambah jadual sembang, RLS dan RPC `world_send_chat`. Jadual sembang telah dimasukkan ke publication `supabase_realtime`.

Kunci `sb_publishable_...` dalam app.js ialah publishable key untuk klien web. **Jangan sekali-kali masukkan service_role key atau secret key ke dalam fail frontend / GitHub.**

## Akaun dan akses
- Pemain perlu mendaftar dan menunggu kelulusan MASTER ADMIN jika proses kelulusan akaun digunakan.
- Akaun Master perlu mempunyai rekod `player_admin_roles.role = 'MASTER_ADMIN'`.
- Master ditandakan berdasarkan role pangkalan data, bukan nama paparan.

## Status dan skop versi ini
- Ini ialah RPG 2D top-down web yang boleh dimainkan melalui pelayar, bukan permainan 3D atau dunia terbuka berskala besar.
- Versi ini mempunyai 100 wilayah procedural, rumah/interior, 8 makhluk teman, penjaga wilayah, misi harian, XP, coin maya, kod jemputan, item skuter maya dan bazar coin maya.
- Kawalan: WASD/anak panah atau butang sentuh; F interaksi; G serang penjaga; E buka gerbang; V skuter; R terbang; ESC keluar rumah.
- Prestasi telefon: animasi dunia dihadkan kepada 20 FPS pada peranti yang melaporkan memori rendah dan 30 FPS pada peranti lain; pergerakan multiplayer dihadkan kepada kira-kira 8 siaran sesaat; animasi dihentikan ketika tab tidak aktif.
- Kemajuan quest disimpan dalam profil Supabase; kedudukan terakhir turut dicache pada peranti dan diasingkan mengikut akaun.
- Chat dunia global disimpan dan live. DM peribadi, guild, pertarungan PvP, inventori item umum, NPC quest bercabang dan zon berasingan belum disediakan.
- Pendaftaran menggunakan Supabase Auth dan aliran kelulusan sedia ada. Pemain yang belum diluluskan tidak boleh memasuki dunia; MASTER ADMIN perlu meluluskan permohonan mengikut sistem pendaftaran projek.
- Backend Supabase projek `HALOJE-METAVERSE` telah disemak: jadual profil, wallet, misi, statistik, chat, jemputan, inventori skuter dan pasaran wujud; migrasi permainan dan peluasan telah direkodkan. Ini bukan bukti ujian end-to-end menggunakan dua akaun pelayar.
- GitHub Pages mesti diterbitkan oleh pemilik repository. Ujian deployment sebenar, pendaftaran akaun baharu dan multiplayer dua peranti masih perlu dibuat selepas fail ini dimuat naik.
- Haloje Delivery dan NH TRADE EMPIRE belum disambungkan kepada sumber data operasi; dashboard tidak mereka-reka angka.

## Pengoptimuman Android
- Satu gelung permainan sahaja digunakan oleh modul expansion.
- Canvas mengekalkan nisbah 960×520 dan dikecilkan secara responsif oleh CSS.
- Pergerakan dihantar melalui Realtime secara terkawal dan bukannya pada setiap frame.
- Cache kemajuan menggunakan kunci berasingan bagi setiap akaun pemain.

## Struktur
- `index.html` — halaman permainan
- `style.css` — visual responsif
- `app.js` — auth, dunia 2D, realtime, chat dan sistem RPG

## Keselamatan akaun Master
- Tiada kata laluan akaun Master ditulis dalam HTML, JavaScript, CSS, README atau ZIP.
- Untuk menukar kata laluan, log masuk menggunakan akaun Master yang sah. Panel `MASTER CONTROL` menyediakan borang pertukaran kata laluan melalui Supabase Auth (`auth.updateUser`). Masukkan kata laluan baharu dan pengesahannya di laman permainan; ia tidak disimpan ke fail projek.
- `sb_publishable_...` dalam `app.js` ialah kunci publishable yang memang digunakan oleh aplikasi browser. Ia bukan `service_role` atau secret key. Jangan sekali-kali menambah secret/service-role key ke GitHub.
- Label MASTER di senarai online disahkan menggunakan RPC pangkalan data, bukan berdasarkan nilai role yang dihantar oleh browser pemain.

## WORLD EXPANSION UPDATE — 100 MAPS

This build adds a 100-region campaign with procedural biome layouts, explorable house interiors, five relic objectives per region, original companion creatures, guardian battles and locked gates. A region only unlocks after the player collects all five relics, befriends at least one creature and defeats its guardian. Guardian battles require multiple companion attacks.

### Original companions and travel
- Eight original creature concepts are included: Mossprout, Emberlynx, Tiderill, Zephyroo, Cragbit, Luminel, Noctusk and Bloomanta.
- Zephyroo and Bloomanta unlock the flying travel skill. Press `R` to toggle flight after befriending one.
- Referral reward is a **virtual NWD scooter**, not a physical motorcycle. Press `V` to mount/dismount after receiving it.
- `F` interacts, `G` attacks the guardian, `E` opens the next gate when its quest is complete, `ESC` exits a house.

### Procedural original music
Each map generates its own short ambient melody in the browser using Web Audio oscillators, a map-specific pitch/tempo pattern and synthesized tones. No commercial soundtrack, samples or copied game music is bundled. Start audio with **MAIN MUZIK MAP** after a user gesture. Procedural generation avoids embedding third-party tracks; it cannot guarantee that a generated note sequence will never coincidentally resemble another work.

### Referrals and virtual scooter
- Every player receives a generated invite code on first opening the invitation panel; this includes Master.
- A new player enters the inviter's code during registration. After the new profile is approved and they sign in, the referral is claimed once.
- The new player and inviter each receive one in-game scooter item.
- The scooter has no physical-world value and is not a promise to deliver a real motorcycle.

### Player coin market
- Players can list NWD virtual coins at a chosen virtual coin price.
- Listed coins are held in escrow by the database function. Buying transfers the listed coins and pays the seller; cancelling refunds the seller.
- This is a game-only market, not cash trading or a real cryptocurrency exchange.

### Database additions
The Supabase migration `nwd_world_expansion_referrals_market` adds invite codes, referral records, virtual vehicle inventory and market listings, with authenticated RPC functions. The client uses the existing public/publishable key; never put a Supabase secret or service-role key in GitHub.

### Progress and testing note
Campaign progress is written into the player's `avatar_config` and cached locally. Movement positions are local to the browser session. This update has passed JavaScript syntax checks and the database objects/functions have been verified. A real two-account browser test and live GitHub Pages deployment still need to be performed after these files are uploaded.

## Patch 2026-11-19 — world render / mobile controls
- World initialization no longer waits for invite, vehicle, and market network requests before starting the game loop. Slow or unavailable backend calls should not leave the map blank.
- Added `addStyles()` call for the expansion panels.
- Mobile movement buttons now use pointer capture and clear held keys on pointer release / window blur.
- This patch fixes client-side startup and movement handling. Creature card inventory, public coin ledger, QR transfers, and the 50-year issuance schedule require the matching database migration/RPC layer and are not activated by this client patch alone.
