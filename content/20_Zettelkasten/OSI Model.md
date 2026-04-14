---
title:
  - OSI Model
type: Concept
course:
  - Computer Networks
topic:
  - Network Architecture
semester: 4
tags:
  - networking
  - OSI
  - reference-model
  - layered-architecture
  - computer-networks
  - "#status/evergreen"
status: 🌿 incubating
created: 2026-03-04
---

# OSI Model

> Sebuah model referensi berlapis tujuh yang membagi fungsi komunikasi jaringan menjadi lapisan-lapisan terpisah, sehingga setiap lapisan bisa berkembang, dipahami, dan di-debug secara independen.

---

## Penjelasan

OSI (Open Systems Interconnection) Model adalah kerangka konseptual yang dikembangkan oleh **ISO (International Organization for Standardization)** pada tahun 1984. Tujuannya bukan untuk menjadi protokol yang benar-benar diimplementasikan, melainkan untuk menjadi **bahasa bersama** — sebuah cara universal bagi insinyur dan mahasiswa jaringan untuk memahami, merancang, dan men-troubleshoot sistem komunikasi tanpa harus mengetahui detail teknis setiap vendor.

Model ini membagi proses komunikasi jaringan menjadi **tujuh lapisan**, dari yang paling dekat dengan pengguna (Layer 7 — Application) hingga yang paling dekat dengan kabel fisik (Layer 1 — Physical). Setiap lapisan memiliki tanggung jawab yang jelas dan hanya berkomunikasi dengan lapisan tepat di atas dan di bawahnya melalui antarmuka yang terdefinisi. Ketujuh lapisan tersebut adalah:

| Layer | Nama              | Fungsi Inti                                    | Satuan Data |
| ----- | ----------------- | ---------------------------------------------- | ----------- |
| 7     | Application       | Antarmuka langsung dengan aplikasi pengguna    | Data        |
| 6     | Presentation      | Format, enkripsi, kompresi data                | Data        |
| 5     | Session           | Membuka, memelihara, menutup sesi komunikasi   | Data        |
| 4     | Transport         | Pengiriman end-to-end, flow/error control      | Segment     |
| 3     | Network           | Routing, pengalamatan logis (IP)               | Packet      |
| 2     | Data Link         | Pengiriman node-to-node, pengalamatan fisik    | Frame       |
| 1     | Physical          | Transmisi bit mentah melalui media fisik       | Bit         |

Ketika data dikirim, ia bergerak **dari Layer 7 ke Layer 1** — setiap lapisan menambahkan header-nya sendiri (**encapsulation**). Saat diterima, data bergerak naik dari Layer 1 ke Layer 7, dan setiap lapisan membaca lalu melepas header yang relevan (**de-encapsulation**). Proses ini memungkinkan setiap lapisan bekerja tanpa perlu tahu detail internal lapisan lain — prinsip yang disebut **abstraksi berlapis** (layered abstraction).

Dalam praktik nyata, internet tidak menggunakan OSI secara langsung — ia menggunakan **TCP/IP Model** yang lebih sederhana (4 lapisan). Namun OSI tetap menjadi alat pembelajaran dan komunikasi yang tak tergantikan karena granularitasnya yang lebih halus memudahkan proses troubleshooting dan diskusi teknis.

---

## Analogi / Intuisi

Bayangkan kamu mengirim surat internasional. Kamu (Layer 7) menulis isi surat. Temanmu yang fasih bahasa asing menerjemahkannya (Layer 6). Sekretaris membuka dan menutup sesi korespondensi (Layer 5). Jasa kurir menjamin paket sampai utuh dan berurutan (Layer 4). Kantor pos menentukan rute antar kota dan negara (Layer 3). Tukang pos lokal mengantarkan dari kantor pos ke rumah tujuan (Layer 2). Dan truk, pesawat, atau kapal yang membawa surat secara fisik adalah Layer 1. Setiap "lapisan" tidak perlu tahu cara kerja lapisan lain — tukang pos tidak perlu bisa bahasa asing, dan penerjemah tidak perlu tahu rute pengiriman.

---

## Contoh Konkret

Kamu membuka browser dan mengakses `https://uns.ac.id`.

1. **Layer 7 (Application):** Browser mengirim HTTP GET request.
2. **Layer 6 (Presentation):** Data dienkripsi menggunakan TLS (karena HTTPS).
3. **Layer 5 (Session):** Sesi TLS handshake dibuka antara browser dan server.
4. **Layer 4 (Transport):** Data dipecah menjadi segment TCP dengan port tujuan 443.
5. **Layer 3 (Network):** Setiap segment dibungkus menjadi packet dengan IP address tujuan server UNS.
6. **Layer 2 (Data Link):** Packet dibungkus menjadi frame Ethernet dengan MAC address router (default gateway).
7. **Layer 1 (Physical):** Frame dikonversi menjadi sinyal listrik/cahaya dan dikirim melalui kabel.

Di sisi server UNS, proses terbalik terjadi: sinyal → frame → packet → segment → data terenkripsi → data asli → halaman web ditampilkan di browser.

---

## Keterkaitan

- **Bagian dari:** [[Network Architecture]]
- **Berhubungan dengan:** [[TCP/IP Model]], [[Encapsulation]], [[Protocol]]
- **Anak konsep:** [[OSI Model — Layer 2]], [[OSI Model — Layer 3]]
- **Digunakan dalam:** [[Network Troubleshooting]], [[Network Design]]
- **Berlawanan dengan / Jangan bingung dengan:** [[TCP-IP Model|TCP/IP Model]] — TCP/IP adalah model *praktis* yang digunakan internet (4 lapisan); OSI adalah model *referensi/pembelajaran* (7 lapisan). Keduanya menggambarkan hal yang sama dari perspektif berbeda.

---

## Pertanyaan Terbuka

- Mengapa internet "memilih" TCP/IP daripada OSI sebagai standar implementasi — apa kelemahan OSI yang membuatnya kalah secara praktis?
- Apakah pembagian Layer 5, 6, 7 yang terpisah masih relevan di era modern, mengingat di TCP/IP ketiganya digabung menjadi satu Application Layer?
- Bagaimana tepatnya proses encapsulation bekerja sehingga setiap layer bisa menambahkan header tanpa "merusak" data dari layer di atasnya?

---

## Sumber

- Berasal dari: [[CN - 1 - Pengenalan Jaringan Komputer]] (Week 3–4 RPS: "reference model")
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on OSI Model
- Referensi: Tanenbaum, A.S. — *Computer Networks*, 4th Ed.
- Eksternal: [Cloudflare — What is the OSI Model?](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)
- Eksternal: [Imperva — OSI Model](https://www.imperva.com/learn/application-security/osi-model/)
- Eksternal: [Wikipedia — OSI Model](https://en.wikipedia.org/wiki/OSI_model)
