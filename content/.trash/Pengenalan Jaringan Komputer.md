# Pertemuan 1 (26-2-2026)

> S1 Informatika UNS – Jaringan Komputer Genap 2025/2026  
> Referensi: Cisco CCNAv7 – Introduction to Networks (ITN)

---

## 📋 Informasi Perkuliahan

|Item|Detail|
|---|---|
|**Bobot**|4 SKS|
|**Jumlah Pertemuan**|14 pertemuan + UTS + UAS|
|**Kehadiran Minimal**|75% dari total pertemuan|

### Komponen Penilaian

|Komponen|Bobot|
|---|---|
|Praktikum|50%|
|UTS|20%|
|UAS|20%|
|Tugas|10%|

---

## 1. Networking Today – Networks Connect Us

Komunikasi di era modern hampir sama pentingnya seperti kebutuhan dasar manusia — udara, air, makanan, dan tempat tinggal. Di dunia saat ini, jaringan komputer memungkinkan kita untuk terhubung satu sama lain seperti yang belum pernah terjadi sebelumnya. Dengan memanfaatkan jaringan, kita dapat dengan mudah berkomunikasi dengan siapapun di seluruh penjuru dunia, tanpa batasan jarak.

Jaringan tidak hanya menghubungkan orang-orang, tetapi juga menghubungkan perangkat, sistem, dan organisasi. Ini adalah fondasi dari dunia digital yang kita tinggali saat ini — dari membuka halaman web, mengirim email, melakukan video call, hingga mengakses layanan cloud.

---

## 2. Komponen Jaringan Komputer

Sebuah jaringan komputer terdiri dari beberapa komponen utama yang bekerja bersama untuk memindahkan data dari satu titik ke titik lain. Komponen-komponen ini dapat dibagi menjadi: host/end device, intermediary device, dan media jaringan.

### 2.1 Peran Host (End Device)

Setiap komputer atau perangkat yang terhubung ke jaringan disebut **host** atau **end device**. Ini adalah titik awal dan titik akhir dari setiap komunikasi data. Ada dua jenis utama host:

**Server** adalah komputer yang menyediakan layanan atau informasi kepada perangkat lain dalam jaringan. Server tidak harus berupa perangkat fisik khusus — sebuah software yang berjalan di komputer biasa pun bisa menjadikannya server. Contoh jenis server:

- **Email Server** – menangani pengiriman dan penerimaan email
- **Web Server** – menyimpan dan menyajikan halaman web
- **File Server** – menyimpan dan berbagi file kepada pengguna jaringan

**Client** adalah komputer atau perangkat yang mengirimkan _permintaan (request)_ kepada server untuk mengambil informasi atau menggunakan layanan. Contoh aktivitas client:

- Mengambil halaman web dari web server (menggunakan browser)
- Mengunduh email dari email server

Hubungan antara client dan server merupakan model komunikasi yang paling umum di jaringan modern, dikenal sebagai model **Client-Server**.

### 2.2 Peer-to-Peer (P2P)

Berbeda dari model client-server, dalam jaringan [[Peer-to-Peer (P2P)]], setiap perangkat dapat berperan sebagai client _sekaligus_ server pada saat yang bersamaan. Tidak ada hierarki yang jelas antara perangkat.

Misalnya, komputer A bisa berbagi printer kepada komputer B (bertindak sebagai server printer), sementara di waktu yang sama komputer A juga mengambil file dari komputer B (bertindak sebagai client).

Karakteristik jaringan P2P:

- Sederhana dan mudah diimplementasikan
- Biaya lebih murah karena tidak memerlukan server khusus
- **Direkomendasikan hanya untuk jaringan yang sangat kecil**, karena tidak scalable dan sulit dikelola keamanannya seiring bertambahnya jumlah perangkat

### 2.3 End Device

**End device** adalah titik di mana data berasal atau data diterima. Setiap end device memiliki **alamat** yang digunakan untuk mengidentifikasikannya dalam jaringan. Ketika data dikirim dari satu end device, ia akan melakukan perjalanan melalui jaringan (melewati berbagai intermediary device) hingga akhirnya tiba di end device tujuan.

Contoh end device: komputer desktop, laptop, smartphone, printer jaringan, IP phone, tablet, dan lain-lain.

### 2.4 Intermediary Device

**Intermediary device** adalah perangkat yang bertugas menghubungkan antar end device dan memastikan data dapat berpindah dengan benar dari sumber ke tujuan. Perangkat ini bekerja di "tengah" jaringan.

Contoh intermediary device:

- **Switch** – menghubungkan perangkat dalam satu jaringan lokal (LAN)
- **Wireless Access Point (WAP)** – menyediakan koneksi nirkabel
- **Router** – menghubungkan antar jaringan yang berbeda
- **Firewall** – mengamankan lalu lintas jaringan

Fungsi utama intermediary device:

1. Membuat ulang (_regenerate_) dan meneruskan sinyal data agar tidak melemah saat melewati jarak jauh
2. Menyimpan informasi tentang jalur-jalur yang tersedia di jaringan
3. Memberitahu perangkat lain ketika terjadi error atau kegagalan komunikasi
4. Mengarahkan data melalui jalur alternatif jika jalur utama gagal
5. Mengklasifikasikan dan memprioritaskan pesan sesuai kebutuhan
6. Mengizinkan atau menolak aliran data berdasarkan pengaturan keamanan (_security policy_)

### 2.5 Switch & Router

Saat membangun jaringan untuk skala kecil (_small office/home office_), dua perangkat paling penting yang dibutuhkan adalah **switch** dan **router**.

**Switch** berfungsi untuk menghubungkan semua perangkat dalam satu jaringan lokal — termasuk komputer, printer, dan server — sehingga mereka dapat saling berbagi sumber daya dan berkomunikasi satu sama lain. Switch beroperasi di layer 2 (Data Link Layer) model OSI dan meneruskan data berdasarkan **MAC address**.

**Router** bekerja satu level lebih tinggi dari switch. Jika switch menghubungkan perangkat dalam satu jaringan, maka router menghubungkan _beberapa_ switch (dan jaringannya masing-masing) untuk membentuk jaringan yang lebih besar. Fungsi router:

- Memungkinkan perangkat dalam jaringan lokal untuk mengakses Internet
- Berfungsi sebagai _dispatcher_ — memilih rute terbaik untuk mengirimkan paket data
- Dapat memprioritaskan perangkat atau jenis trafik tertentu di atas yang lain
- Beroperasi di layer 3 (Network Layer) model OSI berdasarkan **IP address**

### 2.6 Media Jaringan Komputer

Data tidak dapat berpindah begitu saja antar perangkat — ia membutuhkan _media_ sebagai jalur transmisi. Ada tiga jenis media jaringan:

**1. Kabel Logam (Copper/Tembaga)**

- Contoh: kabel UTP (Unshielded Twisted Pair), kabel koaksial
- Data dikodekan menjadi **impuls listrik**
- Murah dan mudah dipasang, namun rentan terhadap interferensi elektromagnetik (EMI) dan jarak terbatas

**2. Kabel Serat Optik (Fiber Optic)**

- Terbuat dari serat kaca atau plastik yang sangat tipis
- Data dikodekan menjadi **pulsa cahaya**
- Dapat mengirim data dengan kecepatan sangat tinggi dan jarak yang jauh, namun lebih mahal

**3. Transmisi Nirkabel (Wireless)**

- Data dikodekan melalui **modulasi frekuensi gelombang elektromagnetik**
- Tidak memerlukan kabel fisik, memberikan mobilitas kepada pengguna
- Rentan terhadap interferensi dan gangguan sinyal

---

## 3. Jenis-jenis Jaringan Komputer

### 3.1 LAN (Local Area Network)

**Local Area Network (LAN)** adalah infrastruktur jaringan yang mencakup **area geografis kecil** — misalnya satu gedung, satu lantai, atau satu kampus. Karakteristik LAN:

- Menghubungkan end device dalam area yang terbatas
- Dikelola oleh **satu organisasi atau individu**
- Menyediakan koneksi dengan **bandwidth berkecepatan tinggi** ke perangkat internal
- Contoh: jaringan di kantor, laboratorium komputer, atau rumah

### 3.2 WAN (Wide Area Network)

**Wide Area Network (WAN)** adalah infrastruktur jaringan yang mencakup **area geografis yang luas** — bisa antar kota, antar negara, bahkan antar benua. Karakteristik WAN:

- Menghubungkan beberapa LAN yang terpisah secara geografis
- Biasanya dikelola oleh **satu atau beberapa penyedia layanan (ISP)**
- Menyediakan koneksi dengan **bandwidth yang lebih rendah** dibandingkan LAN (karena jarak yang lebih jauh)

| LAN       | WAN                            |                                 |
| --------- | ------------------------------ | ------------------------------- |
| Cakupan   | Area terbatas (gedung, kampus) | Area luas (kota, negara, benua) |
| Pengelola | Satu organisasi/individu       | Penyedia layanan (ISP)          |
| Bandwidth | Tinggi                         | Lebih rendah                    |

### 3.3 Internet

**Internet** adalah kumpulan dari ribuan LAN dan WAN yang saling terhubung di seluruh dunia. Tidak ada satu entitas pun yang memiliki atau mengelola Internet secara keseluruhan — Internet adalah jaringan yang terdesentralisasi.

Cara kerjanya secara sederhana:

- Setiap rumah, kantor, atau organisasi memiliki **LAN** mereka sendiri
- LAN-LAN tersebut terhubung satu sama lain melalui **WAN**
- WAN menggunakan berbagai media: kabel tembaga, kabel fiber optic, dan transmisi nirkabel
- Kumpulan semua WAN yang saling terkoneksi ini membentuk **Internet**

### 3.4 Intranet

**Intranet** adalah jaringan internal yang bersifat **privat** milik suatu organisasi. Konsepnya mirip dengan Internet (menggunakan teknologi yang sama), namun aksesnya dibatasi — hanya anggota organisasi atau orang yang memiliki otorisasi yang dapat mengaksesnya.

Intranet digunakan untuk:

- Berbagi dokumen internal perusahaan
- Sistem manajemen karyawan
- Portal informasi internal organisasi

### 3.5 Extranet

**Extranet** adalah ekstensi dari intranet yang memungkinkan akses terbatas kepada pihak luar yang dipercaya — seperti supplier, pelanggan, atau mitra bisnis — tanpa memberikan akses penuh ke seluruh jaringan internal.

Contoh penggunaan extranet:

- Perusahaan yang memberi akses portal pemesanan kepada supplier dan kontraktor dari luar
- Rumah sakit yang menyediakan sistem booking online bagi dokter praktik luar untuk membuat jadwal pasien
- Kantor dinas pendidikan yang memberikan akses informasi anggaran kepada sekolah-sekolah di daerahnya

Secara visual, hubungan ketiga konsep ini dapat digambarkan sebagai lingkaran konsentris:

- **Intranet** = lingkaran terdalam (hanya untuk perusahaan)
- **Extranet** = lingkaran tengah (untuk supplier, pelanggan, kolaborator)
- **Internet** = lingkaran terluar (seluruh dunia)

---

## 4. Internet Connection – Converged Network

### 4.1 Sebelum Converged Network

Di masa lalu, sebuah organisasi yang ingin membangun infrastruktur komunikasi harus membangun **tiga jaringan terpisah**:

1. **Jaringan komputer** – untuk data
2. **Jaringan telepon** – untuk suara
3. **Jaringan broadcast** – untuk video/televisi

Masing-masing jaringan ini menggunakan:

- Kabel yang berbeda
- Teknologi yang berbeda untuk menyalurkan sinyal
- Aturan dan standar yang berbeda

Hal ini tentu sangat tidak efisien dari sisi biaya, infrastruktur, dan manajemen.

### 4.2 Converged Network

**Converged network** (jaringan konvergen) adalah solusi modern di mana **data, suara, dan video** semuanya dikirimkan melalui **satu infrastruktur jaringan yang sama**, menggunakan **serangkaian aturan dan standar yang sama**.

Keuntungan converged network:

- Lebih hemat biaya (satu infrastruktur untuk semua layanan)
- Lebih mudah dikelola
- Lebih fleksibel dan scalable

Inilah yang menjelaskan mengapa saat ini kita bisa melakukan **video call**, **telepon**, dan **browsing internet** semuanya melalui satu koneksi internet yang sama.

---

## 5. Reliable Network – Network Architecture

Membangun jaringan tidak cukup hanya dengan menghubungkan perangkat-perangkat. Jaringan yang baik harus **andal (reliable)** — artinya ia harus dapat diandalkan oleh penggunanya kapan saja. **Network architecture** adalah kerangka teknologi yang mendukung infrastruktur jaringan agar dapat memindahkan data secara efisien dan andal.

Ada **empat karakteristik dasar** yang harus dipenuhi oleh arsitektur jaringan yang baik:

### 5.1 Fault Tolerance

**Fault tolerance** adalah kemampuan jaringan untuk **terus beroperasi** meskipun ada komponen yang mengalami kegagalan. Jaringan yang fault-tolerant dirancang untuk:

- Membatasi jumlah perangkat yang terdampak ketika terjadi kegagalan
- Memungkinkan pemulihan yang cepat setelah kegagalan terjadi

Cara utama mencapai fault tolerance adalah dengan **redundancy** — menyediakan **beberapa jalur (path)** antara sumber dan tujuan. Jika satu jalur gagal, data akan secara otomatis dialihkan melalui jalur lain. Pengguna biasanya tidak menyadari bahwa kegagalan terjadi karena perpindahan jalur berlangsung secara transparan.

> **Analogi:** Seperti jalan tol yang memiliki beberapa jalur — jika satu jalur macet atau rusak, kendaraan dialihkan ke jalur lain sehingga lalu lintas tetap berjalan.

### 5.2 Scalability

**Scalability** adalah kemampuan jaringan untuk **berkembang dengan cepat dan mudah** untuk mengakomodasi pengguna baru dan aplikasi baru, **tanpa mengurangi kualitas layanan** bagi pengguna yang sudah ada.

Scalability dicapai dengan cara network designer mengikuti **standar dan protokol** yang sudah ditetapkan. Dengan adanya standar ini, vendor hardware dan software dapat terus mengembangkan produk mereka tanpa harus merancang ulang aturan-aturan dasar jaringan. Akibatnya, jaringan baru dapat ditambahkan ke infrastruktur yang ada dengan mudah.

> **Analogi:** Seperti sistem kelistrikan standar — karena semua perangkat elektronik menggunakan standar tegangan yang sama (220V di Indonesia), kita bisa terus menambahkan perangkat baru tanpa harus mengganti seluruh instalasi listrik.

### 5.3 Quality of Service (QoS)

**Quality of Service (QoS)** adalah mekanisme yang digunakan untuk memastikan bahwa layanan jaringan yang kritis mendapatkan **prioritas bandwidth** yang memadai, sehingga kualitas layanan tetap terjaga bagi semua pengguna.

Mengapa QoS diperlukan? Bayangkan situasi di mana bandwidth jaringan terbatas, namun banyak pengguna mengakses jaringan secara bersamaan:

- Pengguna A sedang melakukan **video call** (butuh bandwidth stabil dan low-latency)
- Pengguna B sedang **mengunduh file besar** (butuh bandwidth besar tapi tidak sensitif terhadap delay)
- Pengguna C sedang **browsing web** (kebutuhan bandwidth sedang)

Jika tidak ada QoS, semua trafik diperlakukan sama. Akibatnya, video call bisa menjadi terputus-putus karena bandwidth dipakai habis oleh unduhan file.

Dengan **kebijakan QoS**, router dapat:

- Mengidentifikasi jenis-jenis trafik yang berbeda
- Memberikan **prioritas lebih tinggi** kepada trafik yang sensitif terhadap delay (seperti VoIP/suara dan video)
- Memberikan **prioritas lebih rendah** kepada trafik yang tidak sensitif terhadap delay (seperti unduhan file)

**Congestion** terjadi ketika permintaan bandwidth melebihi kapasitas bandwidth yang tersedia. QoS adalah alat utama untuk mengelola kondisi congestion ini.

### 5.4 Security

**Security (keamanan)** dalam jaringan mencakup perlindungan terhadap infrastruktur jaringan itu sendiri dan data yang mengalir di dalamnya. Ada dua jenis keamanan utama:

**Keamanan Infrastruktur Jaringan:**

- Keamanan fisik perangkat jaringan (mencegah akses fisik yang tidak terotorisasi ke router, switch, server, dll.)
- Mencegah akses logis yang tidak terotorisasi ke perangkat (misalnya melalui password, enkripsi konfigurasi)

**Keamanan Informasi:**

- Perlindungan data yang sedang dikirimkan melalui jaringan
- Memastikan hanya pihak yang berwenang yang dapat membaca, mengubah, atau menghapus data

#### Tiga Tujuan Utama Keamanan Jaringan (CIA Triad)

|Tujuan|Penjelasan|
|---|---|
|**Confidentiality (Kerahasiaan)**|Hanya penerima yang dituju yang dapat membaca data|
|**Integrity (Integritas)**|Jaminan bahwa data tidak diubah selama proses transmisi|
|**Availability (Ketersediaan)**|Jaminan bahwa data dapat diakses secara tepat waktu oleh pengguna yang berwenang|

#### Jenis Ancaman Keamanan

**Ancaman Internal:**

- Perangkat yang hilang atau dicuri oleh orang dalam
- Kesalahan tidak disengaja oleh karyawan (human error)
- Karyawan yang bersifat jahat (_malicious insider_)

**Ancaman Eksternal:**

- Virus, worm, dan trojan horse
- Spyware dan adware
- Zero-day attack (serangan yang memanfaatkan celah yang belum diketahui)
- Threat actor attack (serangan oleh hacker/peretas)
- Denial of Service (DoS) attack – membanjiri sistem hingga tidak bisa melayani pengguna normal
- Intersepsi data (penyadapan)
- Pencurian identitas

#### Komponen Keamanan Jaringan

Untuk jaringan rumah atau _small office_:

- **Perangkat lunak antivirus dan antispyware** pada setiap end device
- **Firewall** untuk memblokir akses yang tidak terotorisasi dari luar

Untuk jaringan yang lebih besar (enterprise):

- **Dedicated firewall system** – perangkat keras firewall khusus
- **Access Control Lists (ACL)** – aturan yang mengontrol trafik masuk/keluar
- **Intrusion Prevention Systems (IPS)** – sistem yang secara aktif mencegah serangan
- **Virtual Private Networks (VPN)** – membuat "terowongan" terenkripsi untuk komunikasi yang aman melalui jaringan publik

---

## 6. Network Trend

Tren jaringan terus berkembang seiring dengan perubahan kebutuhan pengguna dan kemajuan teknologi. Berikut beberapa tren utama:

### 6.1 Bring Your Own Device (BYOD)

**BYOD** adalah kebijakan yang memungkinkan karyawan atau pengguna untuk membawa dan menggunakan **perangkat pribadi mereka sendiri** (laptop, tablet, smartphone, e-reader) untuk mengakses sumber daya jaringan organisasi.

Keuntungan BYOD:

- Pengguna lebih nyaman menggunakan perangkat yang sudah familiar
- Meningkatkan fleksibilitas dan produktivitas
- Mengurangi biaya pengadaan perangkat oleh organisasi

Tantangan BYOD:

- Mengelola keamanan perangkat yang beragam lebih kompleks
- Organisasi perlu kebijakan yang jelas terkait data apa yang boleh diakses dari perangkat pribadi

### 6.2 Online Collaboration (Kolaborasi Online)

Kolaborasi online memungkinkan orang-orang untuk **bekerja bersama pada proyek yang sama** meskipun berada di lokasi yang berbeda secara fisik. Alat kolaborasi modern menyediakan fitur seperti video conferencing, berbagi layar, edit dokumen bersama, dan pesan instan.

Contoh alat kolaborasi:

- **Cisco Webex** – platform kolaborasi enterprise
- **Zoom** – populer untuk video meeting
- **Google Meet** – terintegrasi dengan ekosistem Google

### 6.3 Cloud Computing (Komputasi Awan)

**Komputasi awan** memungkinkan pengguna dan organisasi untuk menyimpan data, menjalankan aplikasi, dan mengakses layanan komputasi melalui **Internet** — bukan dari perangkat atau server lokal mereka sendiri.

Manfaat cloud computing:

- Penyimpanan file pribadi dan backup data secara online
- Aplikasi dapat diakses dari perangkat apa pun dan di mana pun
- Memungkinkan bisnis untuk menyajikan layanan kepada pengguna di seluruh dunia
- Perusahaan kecil tidak perlu membangun data center sendiri — mereka cukup **menyewa layanan** dari penyedia cloud yang lebih besar

Contoh layanan cloud: Google Drive, Dropbox, Microsoft Azure, Amazon Web Services (AWS).

Semua ini dimungkinkan oleh adanya **data center** — fasilitas besar berisi ribuan server yang selalu aktif dan terhubung ke Internet.

---

## 📝 Ringkasan Konsep Kunci

|Konsep|Definisi Singkat|
|---|---|
|**Host / End Device**|Perangkat yang menjadi sumber atau tujuan data|
|**Server**|Host yang menyediakan layanan/informasi|
|**Client**|Host yang meminta layanan/informasi|
|**P2P**|Jaringan di mana setiap perangkat bisa menjadi client dan server|
|**Intermediary Device**|Perangkat yang menghubungkan end device (switch, router, dll.)|
|**Switch**|Menghubungkan perangkat dalam satu LAN|
|**Router**|Menghubungkan antar LAN/jaringan berbeda|
|**LAN**|Jaringan area lokal (satu gedung/kampus)|
|**WAN**|Jaringan area luas (antar kota/negara)|
|**Internet**|Kumpulan LAN dan WAN yang terhubung global|
|**Intranet**|Jaringan privat internal organisasi|
|**Extranet**|Intranet yang dibuka aksesnya untuk pihak luar terpercaya|
|**Converged Network**|Satu jaringan untuk data, suara, dan video|
|**Fault Tolerance**|Kemampuan jaringan tetap beroperasi saat terjadi kegagalan|
|**Redundancy**|Penyediaan beberapa jalur alternatif|
|**Scalability**|Kemampuan jaringan berkembang tanpa menurunkan kinerja|
|**QoS**|Manajemen prioritas bandwidth berdasarkan jenis trafik|
|**CIA Triad**|Confidentiality, Integrity, Availability|
|**Congestion**|Kondisi saat permintaan bandwidth melebihi kapasitas|
|**BYOD**|Kebijakan penggunaan perangkat pribadi untuk keperluan kerja|
|**Cloud Computing**|Layanan komputasi berbasis Internet|

---

_Catatan ini dibuat berdasarkan materi perkuliahan Pengenalan Jaringan Komputer, S1 Informatika UNS, Genap 2025/2026._
