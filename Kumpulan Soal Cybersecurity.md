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
+ Attachment: `server_log.txt`

### Deskripsi
Sebuah server perusahaan mengalami anomali. Tim keamanan mencurigai ada penyusup yang sempat mengakses sistem, dan jejaknya tertinggal di dalam file log server berukuran besar. Tugas kalian adalah menggali file log tersebut dan menemukan jejak yang ditinggalkan penyusup berupa **_flag_**. 🕵️

Namun, hati-hati di dalam log juga ada beberapa "**_flag palsu_**" yang sengaja disisipkan penyusup untuk mengecoh kalian. Pastikan **_flag_** yang kalian submit sesuai format yang benar: `tecart{...}`.

--.--.--

> [!TIP]
> Mulai dari command paling dasar: `wc -l server_log.txt` untuk tahu seberapa besar file ini, lalu `grep` untuk mencari pattern tertentu.

> [!TIP]
> Format flag yang valid selalu diawali `tecart{`. Gunakan pattern itu secara spesifik saat grep, jangan hanya mencari kata "flag" karena flag palsu justru pakai kata "flag".

> [!TIP]
> Kombinasikan `grep` dengan flag `-o` (only matching) supaya outputnya lebih rapi.

---

## Soal 2 -- "Access Denied"
+ Kategori: Web Exploitation (Basic)
+ Kesulitan: Normal
+ Attachment: `index.html`

### Deskripsi
Sebuah halaman web internal menampilkan pesan "ACCESS DENIED" ke setiap pengunjung. Namun, developer yang membuat halaman ini kurang rapi, ternyata ada komentar developer yang lupa dihapus sebelum halaman ini di-deploy 😯

Tugas kalian adalah buka _source code_ halaman ini dan temukan apa yang di tinggal si developer.

--.--.--

> [!TIP]
> Buka file `index.html` di browser, lalu lihat page source (klik kanan → View Page Source, atau tekan `Ctrl+U`). Bisa juga langsung buka file-nya dengan text editor / `cat index.html`.

> [!TIP]
> Perhatikan bagian yang diapit `<!-- -->` — itu adalah komentar HTML yang tidak tampil di halaman tapi tetap ada di source code.

> [!TIP]
> Apa yang kalian temukan di komentar itu bukan flag secara langsung ada proses encoding yang perlu di-reverse. Kenali dulu ciri-ciri encoding tersebut (perhatikan karakternya: huruf, angka, `+`, `/`, `=` di akhir).

> [!TIP]
> Untuk decode di Linux, command `base64 -d` bisa jadi teman baik kalian.

---

## Soal 3 -- "Cheat Code Breaker"
+ Kategori: Reverse Engineering (Game)
+ Kesulitan: Normal
+ Attachment: `game_check` (binary ELF 64-bit, Linux)

### Deskripsi
Kalian menemukan sebuah binary game indie berjudul **"Dragon Quest CLI"** di forum lama. Konon game ini punya cheat code rahasia untuk membuka secret level, tapi dokumentasinya sudah hilang ditelan waktu.

Tugas kalian adalah melakukan Reverse Engineer binary ini, artinya membongkar program yang sudah dikompilasi untuk memahami apa yang terjadi di dalamnya, tanpa punya source code aslinya. Program ini akan meminta kalian memasukkan sebuah cheat code, lalu mengecek apakah cocok dengan cheat code rahasia yang "ditanam" di dalamnya.

Tujuan kalian adalah mencari tahu apa cheat code itu. Setelah cheat code ditemukan, flag mengikuti format:

```
tecart{<cheat_code_dalam_huruf_kecil>}
```

Contoh: kalau cheat code-nya `HELLO`, maka flag-nya adalah `tecart{hello}`.

> Sebelum menjalankan gamenya lakukan: `chmod +x game_check` lalu `./game_check`

> [!TIP]
> Selalu awali analisis binary yang tidak dikenal dengan `file game_check` untuk tahu jenis binary-nya.

> [!TIP]
> Coba `strings game_check` dulu, tapi jangan kaget kalau cheat code-nya tidak langsung kelihatan di situ. Itu artinya kalian butuh alat yang lebih dalam.

> [!TIP]
> Gunakan `objdump -d game_check` dan cari fungsi bernama `check_cheat`. Perhatikan instruksi `mov` dengan nilai immediate satu-persatu, itu adalah clue untuk karakter cheat code yang disusun byte demi byte, bukan disimpan sebagai satu string utuh.

> [!TIP]
> Immediate value dalam assembly biasanya ditulis dalam hex (misal `0x44`). Sekarang, ubah hex itu ke desimal lalu ke karakter ASCII (tabel ASCII: `0x44` = huruf apa?).

> [!TIP]
> Alternatif: kalau belum nyaman baca assembly, coba jalankan binary di dalam `gdb`, set breakpoint sebelum `strcmp` dipanggil, lalu periksa isi register/stack saat itu.

---

Selamat mengerjakan kalau stuck, gunakan hint secara berurutan yaa. Proses coba-coba adalah bagian penting dari belajar **_Cybersecurity_**. 🚩
