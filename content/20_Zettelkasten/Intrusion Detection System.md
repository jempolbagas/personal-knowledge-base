---
title: Intrusion Detection System (IDS)
type: Concept
course: Computer Networks
topic: Network Security
semester: 4
tags:
  - network-security
  - IDS
  - monitoring
  - threat-detection
  - computer-networks
created: 2026-03-04
---

# Intrusion **Detection** System (IDS)

> Sebuah sistem yang memantau lalu lintas jaringan atau aktivitas sistem secara real-time untuk mendeteksi tanda-tanda serangan atau pelanggaran kebijakan keamanan, lalu memberikan peringatan kepada administrator.

---

## Penjelasan

Intrusion Detection System (IDS) adalah komponen keamanan jaringan yang bertugas sebagai "mata" — ia mengamati apa yang terjadi di dalam jaringan atau pada sebuah host, kemudian menentukan apakah aktivitas yang terjadi mencurigakan atau berbahaya. Berbeda dengan sistem yang aktif memblokir, IDS secara fundamental bersifat *pasif*: tugasnya adalah mendeteksi dan melaporkan, bukan mencegah.

Ada dua jenis IDS berdasarkan lokasi pemantauan. **Network-based IDS (NIDS)** ditempatkan di titik strategis dalam jaringan — biasanya di belakang [[Firewall|firewall]] — untuk menganalisis lalu lintas yang melewatinya. Ia memeriksa setiap paket data yang lewat dan mencari pola yang dikenal sebagai tanda serangan. **Host-based IDS (HIDS)** sebaliknya dipasang langsung pada sebuah perangkat (server, workstation) dan memantau aktivitas di tingkat sistem operasi: log file, panggilan sistem, perubahan pada file kritis, dan sebagainya.

IDS mendeteksi ancaman melalui dua pendekatan utama. **Signature-based detection** bekerja seperti antivirus — ia membandingkan lalu lintas dengan database pola serangan yang sudah dikenal (*signature*). Pendekatan ini akurat untuk serangan yang sudah terdokumentasi tetapi tidak mampu mendeteksi serangan baru yang belum ada signaturenya. **Anomaly-based detection** terlebih dahulu mempelajari perilaku "normal" jaringan, lalu menandai segala sesuatu yang menyimpang secara signifikan dari baseline tersebut. Pendekatan ini lebih baik dalam mendeteksi ancaman baru, tetapi rentan menghasilkan *false positive* — menandai aktivitas sah sebagai ancaman.

Keterbatasan utama IDS adalah ia tidak bisa *bertindak*. Ketika serangan terdeteksi, IDS hanya mengirim alert. Respons aktual — memblokir IP, menutup koneksi, atau mengkarantina host — harus dilakukan oleh sistem atau manusia lain. Inilah yang membedakannya dari [[Intrusion Prevention System (IPS)|IPS]] (Intrusion *Prevention* System), yang merupakan evolusi dari IDS dengan kemampuan tindakan aktif.

---

## Analogi / Intuisi

Bayangkan IDS sebagai satpam CCTV di sebuah gedung kantor. Satpam itu duduk di ruang monitor, mengawasi semua kamera, dan mencatat setiap aktivitas mencurigakan. Kalau ada orang yang masuk lewat pintu darurat atau berkeliaran di area terlarang, satpam itu langsung radio ke security lain atau catat di laporan. Tapi ia sendiri tidak bergerak dari kursinya untuk menghentikan orang itu — ia hanya mendeteksi dan melaporkan. Itulah IDS: pengawas yang sangat waspada, tapi tidak punya tangan untuk bertindak sendiri.

---

## Contoh Konkret

Sebuah perusahaan menjalankan NIDS di jaringan internalnya. Suatu malam, seorang penyerang mencoba melakukan **port scanning** — mengirimkan paket ke ratusan port berbeda pada sebuah server dalam waktu singkat untuk mencari celah yang terbuka. IDS mendeteksi pola ini karena ada *signature* untuk port scan (misalnya: lebih dari 100 koneksi ke port berbeda dari satu IP dalam 10 detik). IDS kemudian membuat log kejadian dan mengirimkan alert email ke tim security. Tim security lalu melihat alert tersebut, memverifikasi bahwa itu bukan aktivitas sah, dan secara manual memblokir IP penyerang di [[Firewall|firewall]]. Perhatikan: IDS hanya mendeteksi dan melaporkan — tindakan blokir dilakukan secara terpisah.

---

## Keterkaitan

- **Bagian dari:** [[Network Security]]
- **Berhubungan dengan:** [[Firewall]], [[IDS-Firewall Relationship]]
- **Digunakan dalam:** [[Network Monitoring]], [[Security Operations Center (SOC)]]
- **Berlawanan dengan / Jangan bingung dengan:** [[Intrusion Prevention System (IPS)]] — IPS adalah IDS yang bisa *bertindak aktif* memblokir ancaman secara otomatis, bukan hanya melaporkan

---

## Pertanyaan Terbuka

- Bagaimana NIDS bisa menganalisis lalu lintas yang sudah terenkripsi (HTTPS/TLS)? Apakah ia bisa melihat isi paketnya?
- Seberapa akurat anomaly-based detection di jaringan yang lalu lintasnya sangat dinamis (misalnya kampus)? Apakah false positive menjadi masalah besar?
- Apa perbedaan praktis antara IDS dan SIEM (Security Information and Event Management) dalam implementasi nyata?

---

## Sumber

- Berasal dari: -
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, Chapter on Network Security
