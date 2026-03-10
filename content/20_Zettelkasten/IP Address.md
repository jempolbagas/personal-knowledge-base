---
title:
  - IP Address
type: Concept
course:
  - Computer Networks
topic:
  - Network Addressing
semester: 4
tags:
  - networking
  - IP
  - addressing
  - layer-3
  - computer-networks
created: 2026-03-05
---

# IP Address

> Alamat logis 32-bit (IPv4) atau 128-bit (IPv6) yang diberikan kepada setiap perangkat di jaringan komputer agar bisa diidentifikasi dan berkomunikasi — seperti "alamat rumah" di dunia digital.

---

## Penjelasan

IP (Internet Protocol) Address adalah identitas logis yang diberikan kepada setiap perangkat yang terhubung ke jaringan. Berbeda dengan [[MAC Address]] yang bersifat fisik dan permanen (tertanam di hardware), IP address bersifat **logis dan dapat berubah** — sebuah laptop bisa mendapat IP address berbeda setiap kali terhubung ke jaringan yang berbeda. IP address bekerja pada **Layer 3 (Network Layer)** dalam [[OSI Model]] dan pada **Internet Layer** dalam [[TCP-IP Model|TCP/IP Model]], menjadikannya fondasi dari seluruh komunikasi internet.

Sebuah alamat IPv4 terdiri dari **32 bit** yang ditulis dalam format **dotted-decimal** — empat angka desimal (masing-masing merepresentasikan 8 bit atau satu *oktet*) yang dipisahkan oleh titik, misalnya `192.168.1.1`. Setiap oktet memiliki rentang 0–255 karena 8 bit hanya bisa merepresentasikan 2⁸ = 256 nilai. IP address dibagi menjadi dua bagian: **network portion** yang mengidentifikasi jaringan mana perangkat berada, dan **host portion** yang mengidentifikasi perangkat spesifik di dalam jaringan tersebut. Batas antara keduanya ditentukan oleh **subnet mask** — misalnya subnet mask `255.255.255.0` (atau notasi CIDR `/24`) berarti 24 bit pertama adalah bagian jaringan dan 8 bit terakhir adalah bagian host, memberikan 2⁸ - 2 = 254 alamat host yang dapat digunakan (dikurangi 2 karena satu alamat untuk *network address* dan satu untuk *broadcast address*).

Ada dua cara pemberian IP address. **Static IP** diberikan secara manual oleh administrator — cocok untuk server atau perangkat jaringan yang membutuhkan alamat tetap. **Dynamic IP** diberikan secara otomatis oleh **DHCP (Dynamic Host Configuration Protocol)** server — ini adalah cara kebanyakan perangkat kita mendapatkan IP di jaringan sehari-hari. Selain itu, IP address dibagi menjadi **IP publik** (unik secara global di internet, diberikan oleh ISP) dan **IP privat** (hanya unik di dalam jaringan lokal, menggunakan rentang khusus seperti `192.168.x.x`, `10.x.x.x`, atau `172.16.x.x`–`172.31.x.x`). Router menggunakan **NAT (Network Address Translation)** untuk menerjemahkan antara IP privat dan IP publik, memungkinkan banyak perangkat berbagi satu IP publik.

Karena alamat IPv4 yang tersedia terbatas (sekitar 4,3 miliar), dikembangkanlah **IPv6** dengan panjang 128 bit — ditulis dalam notasi heksadesimal yang dipisahkan titik dua, misalnya `2001:0db8:85a3::8a2e:0370:7334`. IPv6 menyediakan jumlah alamat yang praktis tak terbatas (2¹²⁸ ≈ 3,4 × 10³⁸), cukup untuk setiap perangkat IoT di masa depan.

---

## Analogi / Intuisi

IP address itu seperti alamat rumah di dunia nyata. **Network portion** adalah nama jalan atau kompleks perumahan (semua rumah di Jl. Slamet Riyadi berbagi bagian alamat yang sama), dan **host portion** adalah nomor rumahnya (No. 12, No. 14, dst.). Subnet mask berfungsi seperti "kode pos" yang membantu tukang pos menentukan bagian mana dari alamat yang menunjuk ke wilayah dan bagian mana yang menunjuk ke rumah spesifik. Kalau kamu pindah rumah (pindah jaringan), alamat rumahmu berubah — tapi KTP-mu (MAC address) tetap sama.

---

## Contoh Konkret

Di jaringan kantor dengan subnet `192.168.10.0/24`:

- **Network address:** `192.168.10.0` — alamat jaringan itu sendiri, tidak bisa dipakai perangkat.
- **First usable host:** `192.168.10.1` — biasanya dipakai oleh [[Router|router]] sebagai [[Default Gateway]].
- **Contoh host:** PC karyawan A mendapat `192.168.10.50`, printer mendapat `192.168.10.100`.
- **Last usable host:** `192.168.10.254`
- **Broadcast address:** `192.168.10.255` — paket yang dikirim ke alamat ini diterima oleh semua perangkat di jaringan.

Ketika PC karyawan A (`192.168.10.50`) ingin mengirim data ke PC karyawan B (`192.168.10.75`), keduanya berada di jaringan yang sama (`192.168.10.0/24`). [[Switch]] langsung meneruskan frame. Tetapi jika PC A ingin mengakses `google.com` (`142.250.185.14`), IP tujuan berbeda network — maka paket dikirim ke default gateway (`192.168.10.1`) yang kemudian melakukan routing ke internet.

---

## Keterkaitan

- **Bagian dari:** [[Network Addressing]], [[OSI Model — Layer 3]]
- **Berhubungan dengan:** [[MAC Address]], [[Router]], [[Routing Table]], [[Default Gateway]], [[Subnet Mask]]
- **Digunakan dalam:** [[TCP-IP Model|TCP/IP Model]], [[Static Routing]], [[NAT]], [[DHCP]]
- **Berlawanan dengan / Jangan bingung dengan:** [[MAC Address]] — MAC address adalah alamat *fisik* di Layer 2 yang mengidentifikasi hardware; IP address adalah alamat *logis* di Layer 3 yang mengidentifikasi posisi di jaringan. MAC dipakai untuk komunikasi lokal dalam satu LAN, IP dipakai untuk komunikasi antar jaringan.

---

## Pertanyaan Terbuka

- Bagaimana tepatnya proses transisi dari IPv4 ke IPv6 bekerja di dunia nyata — apakah keduanya berjalan bersamaan (dual-stack)?
- Apa implikasi keamanan dari IP address yang bersifat publik — bisakah seseorang "menyerang" hanya dengan mengetahui IP publik?
- Dalam subnetting tingkat lanjut (VLSM), bagaimana cara menentukan ukuran subnet yang optimal untuk setiap departemen?

---

## Sumber

- Berasal dari: [[Pengenalan Jaringan Komputer — CN — 1]], [[Network Operating System — CN — 2]] (IPv4 configuration and subnetting)
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on Network Layer / IPv4 Addresses
- Eksternal: [Cloudflare — What is an IP Address?](https://www.cloudflare.com/learning/dns/glossary/what-is-my-ip-address/)
- Eksternal: [Wikipedia — IP Address](https://en.wikipedia.org/wiki/IP_address)
- Eksternal: [GeeksForGeeks — Introduction of Classful IP Addressing](https://www.geeksforgeeks.org/introduction-of-classful-ip-addressing/)
