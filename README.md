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

## Had versi ini
- Ini ialah RPG 2D top-down asas, bukan permainan 3D atau dunia terbuka berskala besar.
- Chat dunia global disimpan dan live; sistem DM peribadi, guild, pertarungan, inventori item, NPC quest interaktif dan bilik/zon berasingan belum dibina.
- Kelajuan/kapasiti multiplayer sebenar bergantung pada had Realtime dan pelan Supabase.
- GitHub Pages belum diterbitkan secara automatik. Ujian pelayar sebenar memerlukan URL deployment dan akaun pemain yang diluluskan.
- Haloje Delivery dan NH TRADE EMPIRE belum disambungkan kepada sumber data operasi mereka; dashboard memaparkan status tiada data dan tidak mereka-reka angka.

## Struktur
- `index.html` — halaman permainan
- `style.css` — visual responsif
- `app.js` — auth, dunia 2D, realtime, chat dan sistem RPG

## Keselamatan akaun Master
- Tiada kata laluan akaun Master ditulis dalam HTML, JavaScript, CSS, README atau ZIP.
- Untuk menukar kata laluan, log masuk menggunakan akaun Master yang sah. Panel `MASTER CONTROL` menyediakan borang pertukaran kata laluan melalui Supabase Auth (`auth.updateUser`). Masukkan kata laluan baharu dan pengesahannya di laman permainan; ia tidak disimpan ke fail projek.
- `sb_publishable_...` dalam `app.js` ialah kunci publishable yang memang digunakan oleh aplikasi browser. Ia bukan `service_role` atau secret key. Jangan sekali-kali menambah secret/service-role key ke GitHub.
- Label MASTER di senarai online disahkan menggunakan RPC pangkalan data, bukan berdasarkan nilai role yang dihantar oleh browser pemain.
