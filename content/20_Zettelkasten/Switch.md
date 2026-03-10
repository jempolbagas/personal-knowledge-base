---
title:
  - Switch
type: Concept
course:
  - Computer Networks
topic:
  - Network Devices
semester: 4
tags:
  - networking
  - switch
  - layer-2
  - MAC
  - LAN
  - computer-networks
created: 2026-03-04
---

# Switch

> Perangkat jaringan yang menghubungkan beberapa perangkat dalam satu jaringan lokal (LAN) dan meneruskan frame data hanya ke perangkat tujuan yang tepat berdasarkan alamat MAC.

^7eddd2

---

## Penjelasan

Switch bekerja pada **Layer 2 (Data Link Layer)** dari model OSI. Berbeda dengan hub yang menyiarkan semua data ke semua port, switch cukup cerdas untuk mengirimkan frame hanya ke port di mana perangkat tujuan terhubung. Kecerdasan ini bersumber dari **MAC address table** (juga disebut CAM table) — sebuah tabel yang memetakan alamat MAC setiap perangkat ke port switch tempat perangkat itu terhubung.

Proses pembelajaran MAC address terjadi secara otomatis. Ketika sebuah frame masuk ke switch, switch membaca **source MAC address** dari frame tersebut dan mencatatnya ke dalam tabel bersama nomor port asalnya. Jika destination MAC address sudah ada di tabel, frame langsung diteruskan ke port yang tepat — proses ini disebut **unicast forwarding**. Jika destination MAC belum dikenal, switch akan melakukan **flooding**: menyiarkan frame ke semua port kecuali port asal, mirip seperti hub, sampai perangkat tujuan merespons dan MAC-nya tercatat.

Switch secara efektif memisahkan **collision domain** — setiap port switch adalah collision domain tersendiri, sehingga dua perangkat bisa berkomunikasi secara simultan tanpa saling mengganggu. Namun secara default, semua port pada switch yang sama masih berada dalam satu **broadcast domain** yang sama, artinya broadcast frame akan diterima oleh semua perangkat. Untuk memisahkan broadcast domain di dalam switch, digunakan teknologi **VLAN (Virtual LAN)**.

Switch modern (Layer 3 switch) bahkan memiliki kemampuan routing terbatas, namun fungsi dasarnya yang mendefinisikan sebuah switch tetaplah: meneruskan frame antar perangkat dalam satu jaringan lokal berdasarkan MAC address secara efisien.

---

## Analogi / Intuisi

Bayangkan sebuah gedung kantor dengan resepsionis yang sangat hafal wajah semua karyawan. Ketika ada paket dikirim ke "Budi di lantai 3, meja 12", resepsionis tidak perlu mengumumkan ke seluruh gedung — ia langsung mengantar ke Budi saja karena sudah tahu persis di mana Budi duduk. Tapi kalau ada karyawan baru yang belum dikenal? Resepsionis terpaksa mengumumkan ke semua lantai dulu sampai si karyawan baru mengangkat tangan dan memperkenalkan diri.

---

## Contoh Konkret

Tiga laptop terhubung ke switch: Laptop A (MAC: `AA:AA`), Laptop B (MAC: `BB:BB`), Laptop C (MAC: `CC:CC`).

**Kondisi awal:** MAC table kosong.

1. Laptop A mengirim frame ke Laptop B.
   - Switch catat: `AA:AA → Port 1` di MAC table.
   - `BB:BB` belum dikenal → Switch **flood** ke Port 2 dan Port 3.
   - Laptop B merespons, switch catat: `BB:BB → Port 2`.

2. Laptop A mengirim frame lagi ke Laptop B.
   - MAC table sudah punya `BB:BB → Port 2`.
   - Switch langsung teruskan **hanya ke Port 2**. Laptop C sama sekali tidak menerima frame ini.

**Hasil:** Komunikasi A↔B tidak mengganggu Laptop C sama sekali — inilah efisiensi switch dibanding hub.

---

## Keterkaitan

- **Bagian dari:** [[Network Devices]], [[OSI Model — Layer 2]]
- **Berhubungan dengan:** [[Router]], [[MAC Address]], [[MAC Address Table]], [[VLAN]], [[Collision Domain]], [[Broadcast Domain]]
- **Digunakan dalam:** [[LAN]], [[Ethernet]]
- **Berlawanan dengan / Jangan bingung dengan:** [[Router]] — Router menghubungkan jaringan *berbeda* via IP address (Layer 3), sedangkan Switch menghubungkan perangkat dalam jaringan yang *sama* via MAC address (Layer 2). Juga jangan bingung dengan [[Hub]] — hub menyiarkan ke semua port tanpa kecerdasan apapun.

---

## Pertanyaan Terbuka

- Bagaimana tepatnya VLAN memisahkan broadcast domain secara logis padahal perangkat terhubung ke switch fisik yang sama?
- Apa yang terjadi jika dua switch saling terhubung membentuk loop? (→ mungkin terkait Spanning Tree Protocol)
- Kapan sebaiknya menggunakan Layer 3 switch dibanding router biasa untuk routing antar VLAN?

---

## Sumber

- Berasal dari: -
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on Data Link Layer
