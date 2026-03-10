---
Title: Firewall
Type: Concept
Course: Computer Networks
Topic: Network Security
Semester: 4
Tags:
  - network-security
  - firewall
  - computer-networks
Created: 2026-03-04
---

# Firewall

> Sebuah sistem keamanan jaringan yang mengontrol lalu lintas masuk dan keluar berdasarkan aturan yang telah ditetapkan — bertindak sebagai penjaga gerbang antara jaringan yang dipercaya dan yang tidak dipercaya.

---

## Penjelasan

Firewall adalah mekanisme pertahanan pertama (first line of defense) dalam keamanan jaringan. Ia berada di perbatasan antara dua jaringan — paling umum antara jaringan internal sebuah organisasi dan internet — dan membuat keputusan: paket data mana yang boleh lewat dan mana yang harus diblokir. Keputusan itu dibuat berdasarkan serangkaian **aturan (rules/policies)** yang dikonfigurasi oleh administrator jaringan.

Ada beberapa jenis firewall berdasarkan cara kerjanya. **Packet filtering firewall** adalah yang paling sederhana — ia memeriksa setiap paket secara individual berdasarkan header-nya: alamat IP sumber, alamat IP tujuan, port, dan protokol. Jika paket cocok dengan aturan yang melarang, paket diblokir; jika cocok aturan yang mengizinkan, paket diteruskan. **Stateful inspection firewall** bekerja lebih cerdas — ia tidak hanya memeriksa paket individual, tetapi juga melacak *state* dari koneksi yang sedang aktif. Ia tahu apakah sebuah paket adalah bagian dari koneksi yang sah yang sudah dimulai sebelumnya, bukan sekadar paket acak. **Application-layer firewall (proxy firewall)** bekerja di level yang lebih dalam lagi — ia memahami protokol aplikasi seperti HTTP, FTP, atau DNS dan bisa membuat keputusan berdasarkan konten aplikasi, bukan hanya header jaringan.

Firewall bekerja dengan prinsip **default deny** atau **default allow**. Pada konfigurasi default deny (yang lebih aman), semua lalu lintas diblokir kecuali yang secara eksplisit diizinkan. Pada default allow, semua lalu lintas diizinkan kecuali yang secara eksplisit diblokir. Mayoritas firewall produksi menggunakan default deny untuk meminimalkan permukaan serangan.

Penting dipahami bahwa firewall adalah sistem yang *proaktif dan preventif*: ia bertindak sebelum paket mencapai tujuannya. Namun firewall memiliki batasan — ia tidak bisa mendeteksi serangan yang lolos melalui port dan protokol yang diizinkan, tidak bisa menganalisis lalu lintas terenkripsi secara mendalam, dan tidak memberikan visibilitas tentang apa yang terjadi di dalam jaringan setelah paket diizinkan masuk.

---

## Analogi / Intuisi

Firewall itu seperti resepsionis di gedung perusahaan yang punya daftar tamu. Setiap orang yang datang harus melewatinya. Resepsionis melihat kartu identitas (header paket) dan mencocokkan dengan daftar: "Apakah orang dari divisi X boleh masuk ke lantai Y?" Kalau tidak ada di daftar, langsung disuruh balik. Resepsionis ini bekerja sangat cepat dan efisien untuk menyaring orang-orang yang jelas-jelas tidak boleh masuk. Tapi begitu seseorang sudah lolos masuk gedung, resepsionis tidak tahu lagi apa yang dilakukan orang itu di dalam — untuk itu butuh satpam pengawas lain ([[Intrusion Detection System|IDS]]).

---

## Contoh Konkret

Sebuah perusahaan mengonfigurasi stateful inspection firewall dengan aturan berikut: izinkan semua koneksi yang dimulai dari jaringan internal ke internet (outbound), tetapi blokir semua koneksi yang dimulai dari internet ke jaringan internal (inbound) kecuali ke port 443 (HTTPS) pada server web publik mereka. Ketika seorang karyawan membuka browser dan mengakses `google.com`, firewall mengizinkan koneksi keluar dan melacak state-nya — sehingga respons dari Google (yang datang dari internet) tetap diizinkan masuk karena dikenali sebagai bagian dari koneksi sah yang sudah dimulai dari dalam. Namun jika seorang penyerang di internet mencoba membuka koneksi baru langsung ke komputer karyawan di port 22 (SSH), firewall langsung memblokir karena tidak ada aturan yang mengizinkan koneksi inbound seperti itu.

---

## Keterkaitan

- **Bagian dari:** [[Network Security]]
- **Berhubungan dengan:** [[Intrusion Detection System]], [[IDS-Firewall Relationship]]
- **Digunakan dalam:** [[Network Perimeter Defense]], [[DMZ (Demilitarized Zone)]]
- **Berlawanan dengan / Jangan bingung dengan:** [[Intrusion Detection System|IDS]] — Firewall *mencegah* lalu lintas berbahaya masuk; IDS *mendeteksi* serangan yang sudah terjadi atau sedang berlangsung di dalam jaringan

---

## Pertanyaan Terbuka

- Bagaimana firewall menangani lalu lintas HTTPS yang terenkripsi — apakah ia bisa memeriksa isi konten, atau hanya melihat header-nya saja?
- Apa itu Next-Generation Firewall (NGFW) dan apa perbedaan praktisnya dibanding stateful inspection?
- Bagaimana firewall dikonfigurasi di lingkungan cloud (seperti AWS Security Groups) — apakah prinsipnya sama?

---

## Sumber

- Berasal dari: -
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, Chapter on Network Security
