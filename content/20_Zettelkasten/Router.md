---
title:
  - Router
type: Concept
course:
  - Computer Networks
topic:
  - Network Devices
semester: 4
tags:
  - networking
  - router
  - layer-3
  - IP
  - forwarding
  - computer-networks
status: 🌿 incubating
created: 2026-03-04
---

# Router

> Perangkat jaringan yang menghubungkan dua atau lebih jaringan berbeda dan menentukan jalur terbaik untuk meneruskan paket data berdasarkan alamat IP tujuan.

---

## Penjelasan

Router bekerja pada **Layer 3 (Network Layer)** dari model OSI. Tugasnya bukan sekadar meneruskan data — ia membuat *keputusan routing*, yaitu memilih jalur mana yang paling optimal untuk mengirimkan sebuah paket dari sumber ke tujuan. Keputusan ini dibuat berdasarkan **routing table**, sebuah tabel yang menyimpan daftar jaringan yang dikenal beserta interface atau next-hop yang harus digunakan untuk mencapainya.

Router membaca **IP address** pada header paket (bukan MAC address), sehingga ia mampu membedakan jaringan yang berbeda. Inilah yang membuat router bisa menghubungkan jaringan LAN dengan internet, atau menghubungkan dua LAN yang terpisah secara logis. Setiap kali paket tiba, router membuka header IP-nya, mencari entri yang cocok di routing table, lalu meneruskan paket ke interface yang sesuai — sebuah proses yang disebut **packet forwarding**.

Routing table bisa diisi dengan dua cara: **static routing**, di mana admin secara manual mendefinisikan rute; atau **dynamic routing**, di mana router saling bertukar informasi rute menggunakan protokol seperti RIP, OSPF, atau BGP. Dynamic routing jauh lebih skalabel untuk jaringan besar karena router bisa otomatis menyesuaikan diri ketika topologi berubah.

Selain forwarding, router modern juga sering menjalankan fungsi tambahan seperti NAT (Network Address Translation), DHCP server, [[Firewall|firewall]] sederhana, hingga QoS (Quality of Service). Namun fungsi inti yang mendefinisikan sebuah router tetaplah: menghubungkan jaringan berbeda dan membuat keputusan routing berdasarkan IP.

---

## Analogi / Intuisi

Bayangkan sistem pos antar kota. Kamu kirim surat dari Surakarta ke Jakarta. Surat itu tidak langsung terbang ke Jakarta — ia diteruskan melalui kantor pos (router) di Semarang, lalu ke kantor pos di Cirebon, lalu akhirnya ke Jakarta. Setiap kantor pos membaca alamat tujuan di amplop (IP address), lalu memutuskan kantor pos mana yang harus menerima surat itu selanjutnya (next-hop). Kantor pos tidak peduli isi suratnya — ia hanya peduli ke mana surat itu harus pergi.

---

## Contoh Konkret

Kamu di laptop (IP: `192.168.1.5`) ingin mengakses Google (`8.8.8.8`). Laptop menyadari bahwa `8.8.8.8` bukan bagian dari jaringannya sendiri (`192.168.1.0/24`), maka paket dikirim ke **default gateway** — yaitu router rumahmu (IP: `192.168.1.1`).

Router menerima paket, membuka header IP, dan melihat tujuannya `8.8.8.8`. Ia mencari di routing table-nya:

| Network       | Next-Hop / Interface |
|---------------|----------------------|
| 192.168.1.0/24 | Interface LAN        |
| 0.0.0.0/0      | 203.0.113.1 (ISP)    |

Tidak ada entri spesifik untuk `8.8.8.8`, maka ia pakai **default route** (`0.0.0.0/0`) dan meneruskan paket ke router ISP. Proses ini berulang di setiap router sepanjang jalur hingga paket mencapai server Google.

---

## Keterkaitan

- **Bagian dari:** [[Network Devices]], [[OSI Model — Layer 3]]
- **Berhubungan dengan:** [[Switch]], [[IP Address]], [[Routing Table]], [[Default Gateway]]
- **Digunakan dalam:** [[Internetworking]], [[WAN]], [[NAT]]
- **Berlawanan dengan / Jangan bingung dengan:** [[Switch]] — Switch bekerja di Layer 2 dan hanya menghubungkan perangkat dalam satu jaringan yang sama, bukan antar jaringan berbeda.

---

## Pertanyaan Terbuka

- Bagaimana tepatnya algoritma OSPF memilih jalur terpendek, dan apa bedanya dengan Dijkstra's algorithm secara umum?
- Dalam NAT, bagaimana router melacak koneksi mana milik perangkat mana jika banyak perangkat berbagi satu IP publik?
- Kapan static routing lebih baik dari dynamic routing dalam skenario nyata?

---

## Sumber

- Berasal dari: -
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on Network Layer
