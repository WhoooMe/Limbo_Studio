# 🚩 Welcome to CTF Practice Set!
### Haaii... Para Calon Cyber Warrior 👋☺️
Sebelumnya selamat ya buat kalian yang sudah berhasil lolos jadi maba UNUD, akhirnya perjuangan panjang kalian selama ini kebayar juga! 🎉
<br> Sebagai maba, pasti banyak banget nihh.. hal baru yang bakal kalian temuin ke depannya, misal; mata kuliah baru, dosen baru, sistem SKS yang pastinya ngebuat kalian penasaran dan makin semangat buat kuliahnya 😎

Nah, salah satu hal yang ingin kami perkenalkan dan nggak kalah seru adalah dunia **<em>Cybersecurity</em>**. Buat kalian yang udah mikir dunia **<em>Cyber</em>** itu susah, tenang aja kok, kalian nggak perlu jago ngoding atau paham sistem OS Linux dari nol. Justru soal-soal ini dibikin khusus buat kalian yang bener-bener baru pertama kali nyoba. 🙌

Kalau stuck, itu wajar banget buat semua orang, bahkan yang ahli **<em>Cybersecurity</em>** sekalipun, juga sering banget Googling, buka dokumentasi, atau nanya ke temen. Itu bukan tanda kalian kurang pintar, tapi tanda kalian lagi beneran belajar. 💪

Gak usah lama-lama, Yukk langsung kita mulai! 🚀

--.--.--

## 🌕 Prologue ##
Sebelum mulai, ada beberapa hal penting yang wajib kalian tau nihh:

- 🚩 **Format flag:** semua jawaban harus mengikuti format `tecart{...}`
- 🎯 **Tugas kalian:** temukan **_flag_** yang tersembunyi di setiap soal, lalu submit sesuai formatnya
- 💡 **Hint:** ngerasa stuck?, tenang ada hint yang siap bantu kalian di setiap soal kokk..
- ⏱️ **Waktu:** Take Your Time 😉 

Sudah siap bantai? Lanjut ke soal pertama! 👇

## Soal 1 -- "Log Digger"
+ Kategori: General Skills (Linux)
+ Kesulitan: Easy

### Deskripsi
Sebuah server perusahaan mengalami anomali. Tim keamanan mencurigai ada penyusup yang sempat mengakses sistem, dan jejaknya tertinggal di dalam file log server berukuran besar. Tugas kalian adalah menggali file log tersebut dan menemukan jejak yang ditinggalkan penyusup berupa **_flag_**.

Namun, hati-hati di dalam log juga ada beberapa "**_flag palsu_**" yang sengaja disisipkan penyusup untuk mengecoh kalian. Pastikan **_flag_** yang kalian submit sesuai format yang benar: `tecart{...}`.

### Attachment
- `server_log.txt`

### Hint
1. Mulai dari command paling dasar: `wc -l server_log.txt` untuk tahu seberapa besar file ini, lalu `grep` untuk mencari pattern tertentu.
2. Format flag yang valid selalu diawali `MENTOR{`. Gunakan pattern itu secara spesifik saat grep, jangan hanya mencari kata "flag" — karena flag palsu justru pakai kata "flag".
3. Kombinasikan `grep` dengan flag `-o` (only matching) supaya outputnya lebih rapi.

---

## Soal 2 — "Cheat Code Breaker"
**Kategori:** Reverse Engineering (Game)
**Kesulitan:** Sedang
**Poin saran:** 250

### Deskripsi
Kalian menemukan sebuah binary game indie berjudul **"Dragon Quest CLI"** di forum lama. Konon game ini punya cheat code rahasia untuk membuka secret level, tapi dokumentasinya sudah hilang ditelan waktu.

Reverse engineer binary ini untuk menemukan cheat code yang benar. Setelah cheat code ditemukan, flag mengikuti format:

```
MENTOR{<cheat_code_dalam_huruf_kecil>}
```

Contoh: kalau cheat code-nya `HELLO`, maka flag-nya adalah `MENTOR{hello}`.

### Attachment
- `game_check` (binary ELF 64-bit, Linux)

> Sebelum menjalankan: `chmod +x game_check` lalu `./game_check`

### Hint
1. Selalu awali analisis binary yang tidak dikenal dengan `file game_check` untuk tahu jenis binary-nya.
2. Coba `strings game_check` dulu — tapi jangan kaget kalau cheat code-nya tidak langsung kelihatan di situ. Itu artinya kalian butuh alat yang lebih dalam.
3. Gunakan `objdump -d game_check` (atau Ghidra/IDA kalau sudah familiar) dan cari fungsi bernama `check_cheat`. Perhatikan instruksi `mov` dengan nilai immediate satu-persatu — itu adalah karakter cheat code yang disusun byte demi byte, bukan disimpan sebagai satu string utuh.
4. Immediate value dalam assembly biasanya ditulis dalam hex (misal `0x44`). Ubah ke desimal lalu ke karakter ASCII (tabel ASCII: `0x44` = huruf apa?).
5. Alternatif: kalau belum nyaman baca assembly, coba jalankan binary di dalam `gdb`, set breakpoint sebelum `strcmp` dipanggil, lalu periksa isi register/stack saat itu.

---

## Soal 3 — "Access Denied"
**Kategori:** Web Exploitation (Basic)
**Kesulitan:** Normal (pengantar)
**Poin saran:** 100

### Deskripsi
Sebuah halaman web internal menampilkan pesan "ACCESS DENIED" ke setiap pengunjung. Namun, developer yang membuat halaman ini kurang rapi — ada komentar developer yang lupa dihapus sebelum halaman ini di-deploy.

Buka source code halaman ini dan temukan apa yang tertinggal.

### Attachment
- `index.html`

### Hint
1. Buka file `index.html` di browser, lalu lihat page source (klik kanan → View Page Source, atau tekan `Ctrl+U`). Bisa juga langsung buka file-nya dengan text editor / `cat index.html`.
2. Perhatikan bagian yang diapit `<!-- -->` — itu adalah komentar HTML yang tidak tampil di halaman tapi tetap ada di source code.
3. Apa yang kalian temukan di komentar itu bukan flag secara langsung — ada proses encoding yang perlu di-reverse. Kenali dulu ciri-ciri encoding tersebut (perhatikan karakternya: huruf, angka, `+`, `/`, `=` di akhir).
4. Untuk decode di Linux, command `base64 -d` bisa jadi teman baik kalian.

---

## Cara Submit
Flag dikirim dalam format: `MENTOR{...}`. Pastikan tidak ada spasi atau karakter tambahan yang tidak sengaja ter-copy.

Selamat mengerjakan — kalau stuck, gunakan hint secara berurutan sebelum langsung minta jawaban ke mentor. Proses coba-coba (dan gagal!) adalah bagian penting dari belajar cybersecurity. 🚩
