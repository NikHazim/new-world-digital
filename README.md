# NEW WORLD DIGITAL

Permainan web berasaskan browser dengan Supabase Auth + PostgreSQL. Bukan demo statik: pendaftaran, login, kelulusan akaun sedia ada, misi harian, XP, level, virtual coin, papan kedudukan dan dashboard MASTER ADMIN menggunakan backend Supabase.

## Fail
- `index.html` — aplikasi utama
- `style.css` — reka bentuk responsif
- `app.js` — logik permainan dan sambungan Supabase

## Deploy ke GitHub Pages
1. Buat repository GitHub bernama `new-world-digital`.
2. Upload ketiga-tiga fail di root repository (bukan dalam subfolder).
3. Buka **Settings → Pages**.
4. Pada **Build and deployment**, pilih **Deploy from a branch**.
5. Pilih branch `main`, folder `/ (root)`, kemudian Save.
6. Buka URL GitHub Pages yang diberikan.

## Backend
Aplikasi disambungkan ke projek Supabase `gwysrnefgwlafbfdyjyy`. Publishable key berada di frontend dan dilindungi oleh RLS. Jangan masukkan `service_role` key ke GitHub.

Migration `new_world_digital_playable_game_core` telah digunakan pada Supabase:
- 21,000,000 had bekalan virtual coin.
- Ganjaran misi harian; satu tuntutan bagi setiap misi bagi setiap pemain setiap hari (waktu Malaysia).
- Halving ganjaran setiap 210,000 tuntutan global.
- XP, level, statistik misi dan leaderboard.
- Dashboard MASTER ADMIN dengan sejarah 14 hari.
- Haloje Delivery dan NH Trade Empire akan memaparkan `BELUM ADA DATA TERKINI` sehingga sistem sumber masing-masing disambungkan. Dashboard tidak mereka angka.

## Perkara penting
- Akaun baharu masuk status menunggu kelulusan. MASTER ADMIN sedia ada boleh meluluskan melalui sistem pengurusan pendaftaran Supabase yang telah tersedia.
- Coin ialah mata wang maya permainan sahaja, bukan wang, pelaburan atau cryptocurrency dunia sebenar.
- Permainan memerlukan internet dan CDN Supabase JS.
- Jalankan ujian sebenar melalui browser selepas deploy, khususnya pendaftaran, email confirmation dan log masuk.
