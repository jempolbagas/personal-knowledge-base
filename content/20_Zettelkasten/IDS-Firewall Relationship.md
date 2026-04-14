---
title: IDS-Firewall Relationship
type: Concept
course: Computer Networks
topic: Network Security
semester: 4
tags:
  - network-security
  - IDS
  - firewall
  - defense-in-depth
  - layered-security
  - computer-networks
  - "#status/evergreen"
status: 🌿 incubating
created: 2026-03-04
---

# IDS-Firewall Relationship

> [[Firewall]] dan IDS adalah dua lapisan pertahanan yang saling melengkapi — firewall mencegah ancaman di pintu masuk, sementara IDS mengawasi apa yang terjadi setelah itu, bersama-sama membentuk strategi keamanan berlapis.

---

## Penjelasan

Firewall dan IDS sering disebut bersama karena keduanya adalah komponen inti keamanan jaringan, tetapi keduanya memiliki peran yang sangat berbeda dan tidak bisa saling menggantikan. Memahami hubungan keduanya adalah memahami konsep **defense-in-depth** — filosofi keamanan yang menyatakan bahwa tidak ada satu mekanisme pertahanan pun yang cukup sendirian.

Firewall bekerja di **perimeter** — ia berdiri di batas jaringan dan membuat keputusan akses sebelum lalu lintas masuk. Ia bersifat *preventif*: tujuannya adalah mencegah ancaman yang sudah dikenal atau lalu lintas yang tidak diizinkan agar tidak pernah sampai ke dalam jaringan. Ini sangat efektif, tapi memiliki blind spot: ia tidak bisa memblokir apa yang tidak ia kenali sebagai ancaman, dan begitu lalu lintas diizinkan masuk, firewall selesai dengan tugasnya.

Di sinilah IDS mengambil peran. IDS bekerja di **dalam** jaringan — ia memantau lalu lintas yang sudah lolos dari firewall dan mencari tanda-tanda serangan atau perilaku mencurigakan. Serangan yang berhasil menyamar sebagai lalu lintas sah (misalnya eksploitasi melalui port 80 yang memang terbuka), atau ancaman yang berasal dari dalam jaringan sendiri (insider threat), atau malware yang sudah terlanjur masuk — semua ini adalah wilayah kerja IDS, bukan firewall.

Dalam arsitektur jaringan nyata, keduanya biasanya ditempatkan secara berurutan. Firewall diletakkan paling depan menghadap internet, membentuk perbatasan pertama. IDS ditempatkan di belakang firewall, memantau lalu lintas di jaringan internal. Dengan susunan ini, firewall menyaring sebagian besar noise (lalu lintas jelas-jelas berbahaya atau tidak relevan), sehingga IDS bisa fokus menganalisis lalu lintas yang lebih refined — mengurangi beban kerja IDS dan meningkatkan akurasi deteksinya. Tanpa firewall di depan, IDS akan kewalahan dengan volume lalu lintas dan menghasilkan terlalu banyak false positive.

Evolusi alami dari kombinasi ini adalah **IPS (Intrusion Prevention System)** — sebuah sistem yang menggabungkan kemampuan deteksi IDS dengan kemampuan tindakan aktif firewall. IPS tidak hanya mendeteksi dan melaporkan, tetapi juga bisa secara otomatis memblokir koneksi, mereset sesi, atau mengubah aturan firewall secara dinamis sebagai respons terhadap ancaman yang terdeteksi.

---

## Analogi / Intuisi

Bayangkan sebuah gedung kantor mewah. **Firewall** adalah resepsionis di pintu masuk utama: memeriksa identitas setiap tamu, mencocokkan dengan daftar undangan, dan menolak masuk siapa pun yang tidak ada di daftar. Tapi resepsionis tidak bisa mengawasi semua orang begitu mereka sudah di dalam gedung. **IDS** adalah jaringan kamera CCTV plus satpam yang berkeliling di dalam gedung — mengamati perilaku semua orang yang sudah masuk, mencatat aktivitas mencurigakan, dan memanggil bala bantuan jika ada yang berulah. Keduanya dibutuhkan: resepsionis yang ketat mengurangi jumlah orang mencurigakan di dalam gedung, dan satpam di dalam menangkap yang berhasil lolos. Tanpa resepsionis, satpam akan kewalahan. Tanpa satpam, seseorang yang lolos dari resepsionis bisa bebas berbuat apa saja.

---

## Contoh Konkret

Sebuah penyerang mencoba dua jalur serangan terhadap jaringan sebuah perusahaan. **Jalur pertama:** penyerang mencoba menghubungi database server internal langsung dari internet di port 3306 (MySQL). Firewall langsung memblokir koneksi ini — tidak ada aturan yang mengizinkan koneksi inbound ke port tersebut. IDS bahkan tidak perlu terlibat. **Jalur kedua:** penyerang mengirimkan email phishing ke seorang karyawan, yang kemudian mengklik link dan mengunduh malware. Malware ini berkomunikasi keluar melalui port 443 (HTTPS) — port yang diizinkan firewall karena terlihat seperti lalu lintas web biasa. Firewall tidak memblokir ini karena secara aturan koneksi outbound di port 443 diperbolehkan. Namun IDS mendeteksi pola komunikasi yang aneh: koneksi ke IP asing yang tidak dikenal dengan interval yang sangat teratur setiap 30 detik (ciri khas *command-and-control traffic*). IDS mengirimkan alert ke tim security, yang kemudian mengisolasi komputer karyawan tersebut. Kasus ini menunjukkan dengan jelas mengapa kedua sistem dibutuhkan.

---

## Keterkaitan

- **Bagian dari:** [[Network Security]], [[Defense-in-Depth]]
- **Berhubungan dengan:** [[Firewall]], [[Intrusion Detection System (IDS)]]
- **Digunakan dalam:** [[Network Architecture Design]], [[Security Operations Center (SOC)]]
- **Berlawanan dengan / Jangan bingung dengan:** [[IPS (Intrusion Prevention System)]] — IPS adalah sistem yang menggabungkan fungsi keduanya dalam satu komponen terintegrasi dengan kemampuan respons aktif

---

## Pertanyaan Terbuka

- Dalam skenario apa sebaiknya IDS ditempatkan *sebelum* firewall, bukan sesudahnya? Apakah ada alasan valid untuk itu?
- Bagaimana organisasi kecil yang tidak punya tim security penuh bisa memanfaatkan IDS jika tidak ada yang memantau alertnya 24/7?
- Apa trade-off antara menggunakan IPS terintegrasi vs kombinasi firewall + IDS terpisah dalam hal performa dan fleksibilitas?

---

## Sumber

- Berasal dari: -
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, Chapter on Network Security
