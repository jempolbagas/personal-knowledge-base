---
title:
  - MAC Address
type: Concept
course:
  - Computer Networks
topic:
  - Network Addressing
semester: 4
tags:
  - networking
  - MAC
  - layer-2
  - data-link
  - hardware-address
  - computer-networks
status: 🌳 evergreen
created: 2026-03-05
---

# MAC Address

> Alamat fisik unik sepanjang 48-bit yang tertanam di setiap kartu jaringan (NIC) saat diproduksi — seperti "nomor seri" yang mengidentifikasi perangkat secara permanen di level hardware.

---

## Penjelasan

MAC (Media Access Control) Address adalah identitas unik yang diberikan oleh **pabrik pembuat** kepada setiap Network Interface Controller (NIC) — baik itu kartu Ethernet, chip Wi-Fi, atau adapter Bluetooth. MAC address bekerja pada **Layer 2 (Data Link Layer)** dari [[OSI Model]] dan merupakan mekanisme utama yang digunakan [[Switch]] untuk meneruskan frame data ke perangkat yang tepat di dalam satu jaringan lokal ([[LAN]]).

Sebuah MAC address terdiri dari **48 bit** (6 byte) yang ditulis dalam format **heksadesimal**, biasanya dipisahkan oleh titik dua atau tanda hubung: misalnya `00:1A:2B:3C:4D:5E` atau `00-1A-2B-3C-4D-5E`. Dari 48 bit ini, terdapat pembagian yang penting: **3 byte pertama (24 bit)** disebut **OUI (Organizationally Unique Identifier)**, yaitu kode yang diberikan oleh IEEE kepada setiap produsen perangkat jaringan. Misalnya, semua perangkat buatan Cisco akan memiliki OUI yang sama di awal MAC address-nya. **3 byte terakhir (24 bit)** adalah identifier unik yang diberikan oleh produsen itu sendiri untuk membedakan setiap perangkat yang mereka produksi. Kombinasi OUI + identifier ini menjadikan setiap MAC address secara teoris **unik secara global** — tidak ada dua NIC di dunia yang seharusnya memiliki MAC address yang sama.

Dalam konteks komunikasi jaringan, MAC address berperan krusial pada level lokal. Ketika sebuah perangkat ingin mengirim data ke perangkat lain dalam satu LAN, ia membutuhkan MAC address tujuan. Proses penerjemahan dari [[IP Address]] ke MAC address dilakukan oleh protokol **ARP (Address Resolution Protocol)**: perangkat pengirim menyiarkan pertanyaan "Siapa yang punya IP `192.168.1.5`?" ke seluruh jaringan (broadcast), dan perangkat yang memiliki IP tersebut merespons dengan MAC address-nya. Setelah diketahui, MAC address digunakan sebagai alamat tujuan di header **frame** Ethernet, lalu [[Switch]] membaca alamat tersebut dan meneruskan frame hanya ke port yang tepat berdasarkan **MAC address table** (CAM table) yang dimilikinya.

Meskipun MAC address dirancang permanen, pada praktiknya ia bisa diubah secara software melalui teknik yang disebut **MAC spoofing**. Ini bisa digunakan untuk tujuan sah (misalnya menjaga privasi di jaringan Wi-Fi publik) maupun tujuan jahat (menyamar sebagai perangkat lain). Selain itu, ada juga alamat MAC khusus: `FF:FF:FF:FF:FF:FF` adalah **broadcast MAC address** — frame yang ditujukan ke alamat ini akan diterima oleh semua perangkat di jaringan.

---

## Analogi / Intuisi

Kalau [[IP Address]] adalah alamat rumah yang bisa berubah saat kamu pindah, maka MAC address adalah **nomor KTP** — nomor tetap yang melekat padamu sejak lahir (sejak perangkat diproduksi). Tiga digit pertama KTP menunjukkan provinsi tempat kamu terdaftar (OUI = pabrik pembuat), dan digit sisanya unik untuk setiap individu (device identifier). Di dunia jaringan, [[Switch]] berperan seperti tukang pos di dalam satu komplek perumahan: ia tidak perlu tahu alamat lengkap (IP), cukup tahu wajah (MAC) dan rumah mana (port) setiap penghuni tinggal.

---

## Contoh Konkret

Laptop A (MAC: `AA:BB:CC:11:22:33`, IP: `192.168.1.5`) ingin mengirim data ke Printer B (MAC: `DD:EE:FF:44:55:66`, IP: `192.168.1.20`). Keduanya terhubung ke [[Switch]] yang sama.

1. **ARP Request:** Laptop A belum tahu MAC address Printer B. Ia mengirim ARP broadcast: "Siapa yang punya IP `192.168.1.20`? Beritahu `AA:BB:CC:11:22:33`." Frame ini dikirim ke destination MAC `FF:FF:FF:FF:FF:FF` — switch mem-flood ke semua port.

2. **ARP Reply:** Printer B mengenali IP-nya dan merespons secara unicast: "IP `192.168.1.20` ada di MAC `DD:EE:FF:44:55:66`." Laptop A menyimpan informasi ini di **ARP cache**-nya.

3. **Data Transfer:** Laptop A membuat frame Ethernet dengan:
   - Source MAC: `AA:BB:CC:11:22:33`
   - Destination MAC: `DD:EE:FF:44:55:66`
   - Di dalamnya terbungkus paket IP dengan source `192.168.1.5` → dest `192.168.1.20`.

4. **Switch Forwarding:** Switch membaca destination MAC `DD:EE:FF:44:55:66`, mencari di MAC address table, menemukan bahwa MAC itu ada di Port 3, dan meneruskan frame **hanya ke Port 3**. Perangkat lain di jaringan tidak menerima frame ini.

---

## Keterkaitan

- **Bagian dari:** [[Network Addressing]], [[OSI Model — Layer 2]]
- **Berhubungan dengan:** [[Switch]], [[IP Address]], [[ARP]], [[Ethernet]], [[MAC Address Table]]
- **Digunakan dalam:** [[LAN]], [[VLAN]], [[Frame Forwarding]]
- **Berlawanan dengan / Jangan bingung dengan:** [[IP Address]] — IP address adalah alamat *logis* (Layer 3) yang bisa berubah dan digunakan untuk routing antar jaringan; MAC address adalah alamat *fisik* (Layer 2) yang permanen dan digunakan untuk forwarding dalam satu jaringan lokal.

---

## Pertanyaan Terbuka

- Jika MAC address seharusnya unik secara global, apa yang terjadi jika dua perangkat di jaringan yang sama kebetulan memiliki MAC yang sama (karena bug manufaktur atau spoofing)?
- Bagaimana perangkat modern yang memiliki fitur "randomized MAC address" (iOS, Android) memengaruhi keamanan dan manajemen jaringan?
- Mengapa router perlu mengganti destination MAC address setiap kali meneruskan paket ke hop berikutnya, tetapi tidak mengganti destination IP?

---

## Sumber

- Berasal dari: [[CN - 1 - Pengenalan Jaringan Komputer]] (intermediary devices, switch), [[CN - 2 - Network Operating System]] (network topology)
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on Data Link Layer
- Eksternal: [Wikipedia — MAC Address](https://en.wikipedia.org/wiki/MAC_address)
- Eksternal: [GeeksForGeeks — MAC Address in Computer Networks](https://www.geeksforgeeks.org/mac-address-in-computer-networks/)
- Eksternal: [Cloudflare — What is a MAC Address?](https://www.cloudflare.com/learning/network-layer/what-is-a-mac-address/)
