---
title:
  - TCP/IP Model
type: Concept
course:
  - Computer Networks
topic:
  - Network Architecture
semester: 4
tags:
  - networking
  - TCP-IP
  - protocol-suite
  - internet
  - reference-model
  - computer-networks
status: 🌿 incubating
created: 2026-03-04
---

# TCP/IP Model

> Model protokol empat lapisan yang menjadi fondasi aktual dari internet — mendefinisikan bagaimana data dikemas, dialamatkan, dikirim, dirutekan, dan diterima di seluruh jaringan yang saling terhubung.

---

## Penjelasan

TCP/IP (Transmission Control Protocol / Internet Protocol) Model — juga dikenal sebagai **Internet Protocol Suite** — adalah kerangka arsitektur yang benar-benar digunakan oleh internet. Berbeda dengan [[OSI Model]] yang bersifat *referensi/konseptual*, TCP/IP adalah *model praktis* yang dikembangkan oleh **DARPA (Defense Advanced Research Projects Agency)** pada tahun 1970-an sebagai bagian dari proyek ARPANET, cikal bakal internet modern.

Model ini terdiri dari **empat lapisan** (bukan tujuh seperti OSI):

| Layer | Nama                  | Setara OSI          | Fungsi Inti                                  | Protokol Kunci              |
| ----- | --------------------- | ------------------- | -------------------------------------------- | --------------------------- |
| 4     | Application           | Layer 5, 6, 7       | Antarmuka aplikasi, format data, sesi        | HTTP, FTP, SMTP, DNS, DHCP  |
| 3     | Transport             | Layer 4              | Pengiriman end-to-end, kontrol aliran/error  | TCP, UDP                    |
| 2     | Internet              | Layer 3              | Pengalamatan logis (IP), routing antar jaringan | IPv4, IPv6, ICMP, ARP    |
| 1     | Network Access (Link) | Layer 1, 2           | Transmisi fisik, pengalamatan MAC, framing   | Ethernet, Wi-Fi, PPP        |

Perbedaan utama dengan OSI: TCP/IP **menggabungkan** Layer 5–7 OSI menjadi satu Application Layer, dan **menggabungkan** Layer 1–2 OSI menjadi satu Network Access Layer. Penyederhanaan ini bukan karena fungsi-fungsi tersebut tidak penting, melainkan karena dalam praktik, pemisahan yang terlalu granular justru mempersulit implementasi tanpa memberikan manfaat nyata.

Nama "TCP/IP" berasal dari dua protokol terpenting dalam suite ini. **TCP (Transmission Control Protocol)** beroperasi di Transport Layer — ia bersifat *connection-oriented*, memastikan data sampai secara utuh, berurutan, dan tanpa error melalui mekanisme three-way handshake, sequence numbering, dan retransmission. **IP (Internet Protocol)** beroperasi di Internet Layer — ia bertanggung jawab atas pengalamatan logis (IP address) dan routing paket antar jaringan. TCP menjamin keandalan; IP menjamin keterjangkauan. Bersama-sama, keduanya membentuk tulang punggung komunikasi internet.

Selain TCP, Transport Layer juga memiliki **UDP (User Datagram Protocol)** — protokol yang tidak menjamin keandalan tetapi jauh lebih cepat karena tidak ada proses handshake atau retransmission. UDP digunakan untuk aplikasi yang membutuhkan kecepatan di atas keandalan: video streaming, voice call, dan online gaming, di mana kehilangan satu paket kecil lebih baik daripada menunggu retransmission yang menyebabkan lag.

---

## Analogi / Intuisi

Bayangkan internet seperti sistem pengiriman paket global. **Network Access Layer** adalah jalan raya, truk, dan pelabuhan — infrastruktur fisik yang mengangkut barang. **Internet Layer** (IP) adalah sistem alamat dan peta — ia menentukan "paket ini harus ke Jalan Slamet Riyadi No. 12, Surakarta" dan memilih rute terbaik melewati kota-kota perantara. **Transport Layer** (TCP/UDP) adalah jasa kurir — TCP seperti kurir premium yang memeriksa paket sebelum dan sesudah dikirim, meminta tanda tangan penerima, dan mengirim ulang jika hilang; UDP seperti tukang koran yang melemparkan koran ke halaman — cepat, tapi kalau koran nyangkut di pohon, ia tidak akan kembali. **Application Layer** adalah isi paket dan cara pemesannya — apakah kamu pesan via website (HTTP), email (SMTP), atau telepon (DNS lookup → koneksi).

---

## Contoh Konkret

Kamu mengetik `google.com` di browser dan menekan Enter:

1. **Application Layer:** Browser menggunakan **DNS** untuk menerjemahkan `google.com` menjadi IP address (misal `142.250.185.14`), lalu mengirim **HTTP GET** request.
2. **Transport Layer:** Request dipecah menjadi **segment TCP**. TCP melakukan **three-way handshake** (SYN → SYN-ACK → ACK) dengan server Google untuk membuka koneksi. Setiap segment diberi sequence number.
3. **Internet Layer:** Setiap segment dibungkus menjadi **packet IP** dengan source IP (misal `192.168.1.5`, IP laptopmu) dan destination IP (`142.250.185.14`). Router-router di sepanjang jalur membaca destination IP dan meneruskan paket ke hop berikutnya.
4. **Network Access Layer:** Paket dibungkus menjadi **frame Ethernet** dengan source MAC (laptopmu) dan destination MAC (router/default gateway). Frame dikonversi menjadi sinyal listrik/cahaya dan dikirim melalui kabel.

Di server Google, proses terbalik terjadi: sinyal → frame → packet → segment → HTTP request diterima → server merespons dengan halaman web → respons dikirim balik melalui empat lapisan yang sama.

---

## Keterkaitan

- **Bagian dari:** [[Network Architecture]]
- **Berhubungan dengan:** [[OSI Model]], [[IP Address]], [[Router]], [[Switch]], [[Default Gateway]], [[Routing Table]]
- **Protokol kunci:** [[TCP]], [[UDP]], [[IP]], [[HTTP]], [[DNS]]
- **Digunakan dalam:** [[Internet]], [[LAN]], [[WAN]], [[Internetworking]]
- **Berlawanan dengan / Jangan bingung dengan:** [[OSI Model]] — OSI adalah model *referensi/teoritis* dengan 7 lapisan; TCP/IP adalah model *praktis/implementasi* dengan 4 lapisan yang benar-benar digunakan internet. Keduanya menggambarkan hal yang sama dari granularitas yang berbeda.

---

## Pertanyaan Terbuka

- Mengapa TCP menggunakan three-way handshake (tiga langkah) dan bukan dua atau empat? Apa yang akan gagal jika hanya dua langkah?
- Dalam situasi praktis apa sebaiknya developer memilih UDP di atas TCP, dan bagaimana mereka menangani masalah kehilangan paket secara manual?
- Bagaimana tepatnya NAT (Network Address Translation) bekerja di Internet Layer — apakah ia mengubah header IP, header TCP, atau keduanya?
- Apa perbedaan praktis antara IPv4 dan IPv6 selain panjang alamat? Apakah IPv6 mengubah cara kerja routing atau transport?

---

## Sumber

- Berasal dari: [[CN - 1 - Pengenalan Jaringan Komputer]] (Week 3–4 RPS: "Protocol suite, standard organization, reference model")
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on TCP/IP Protocol Suite
- Referensi: Tanenbaum, A.S. — *Computer Networks*, 4th Ed. — Chapter on Internet Protocols
- Eksternal: [Wikipedia — Internet Protocol Suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)
- Eksternal: [Cloudflare — What is TCP/IP?](https://www.cloudflare.com/learning/ddos/glossary/tcp-ip/)
- Eksternal: [freeCodeCamp — TCP/IP Model Explained](https://www.freecodecamp.org/news/what-is-tcp-ip-layers-and-protocols-explained/)
