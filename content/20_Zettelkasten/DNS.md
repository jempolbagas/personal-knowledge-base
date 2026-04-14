---
title:
  - DNS
type: Concept
course:
  - Computer Networks
topic:
  - Network Protocols
semester: 4
tags:
  - networking
  - DNS
  - name-resolution
  - application-layer
  - computer-networks
status: 🌿 incubating
created: 2026-03-05
---

# DNS (Domain Name System)

> Sistem yang menerjemahkan nama domain yang mudah dibaca manusia (seperti `google.com`) menjadi alamat IP yang dimengerti komputer (seperti `142.250.185.14`) — pada dasarnya, DNS adalah "buku telepon" internet.

---

## Penjelasan

DNS (Domain Name System) adalah salah satu protokol paling fundamental di internet. Ia bekerja pada **Application Layer** di [[TCP-IP Model|TCP/IP Model]] (Layer 7 di [[OSI Model]]) dan menggunakan **port 53** — baik melalui UDP (untuk query standar yang cepat) maupun TCP (untuk transfer zona dan respons yang besar). Tanpa DNS, kita harus menghafal deretan angka IP address untuk setiap website yang ingin dikunjungi — sesuatu yang mustahil mengingat ada lebih dari satu miliar website di internet.

Struktur DNS bersifat **hierarkis dan terdistribusi**. Tidak ada satu server pun yang menyimpan seluruh database DNS internet. Sebaliknya, informasi tersebar di jutaan server yang tersusun dalam hierarki. Di puncak hierarki ada **13 kelompok Root Name Server** (dilabel A sampai M) yang mengetahui lokasi semua **TLD (Top-Level Domain) server** — server yang menangani domain tingkat atas seperti `.com`, `.org`, `.id`, `.edu`. TLD server kemudian mengetahui lokasi **Authoritative Name Server** untuk setiap domain spesifik — misalnya, authoritative server untuk `uns.ac.id` menyimpan catatan resmi yang memetakan domain tersebut ke IP address-nya. Seluruh sistem ini bekerja secara kooperatif: setiap level hanya perlu tahu satu langkah di bawahnya.

Proses resolusi DNS melibatkan dua jenis query. **Recursive query** terjadi ketika perangkat (client) meminta DNS resolver (biasanya disediakan oleh ISP atau layanan seperti Google `8.8.8.8` atau Cloudflare `1.1.1.1`) untuk memberikan jawaban final — resolver bertanggung jawab penuh mencari IP address yang diminta. Untuk mencari jawaban, resolver kemudian menggunakan **iterative query** — ia bertanya ke Root server, mendapat rujukan ke TLD server, bertanya ke TLD server, mendapat rujukan ke authoritative server, lalu akhirnya mendapat IP address yang diminta. Setiap langkah, server yang ditanya hanya memberikan "petunjuk" ke server berikutnya, bukan jawaban final.

Untuk menghindari proses query berulang yang lambat, DNS sangat bergantung pada **caching**. Setiap jawaban DNS disertai **TTL (Time to Live)** — angka dalam detik yang menentukan berapa lama jawaban boleh disimpan dalam cache. Browser, sistem operasi, dan DNS resolver semuanya menyimpan cache. Inilah mengapa saat kamu mengunjungi website yang sama untuk kedua kalinya, halaman terbuka jauh lebih cepat — DNS tidak perlu melakukan resolusi penuh lagi.

DNS juga menyimpan berbagai jenis **record** selain pemetaan nama-ke-IP: **A record** (IPv4), **AAAA record** (IPv6), **CNAME** (alias domain), **MX** (mail server), **NS** (name server), **TXT** (teks bebas, sering dipakai untuk verifikasi), dan lainnya. Setiap record memiliki fungsi spesifik yang memungkinkan infrastruktur internet bekerja — misalnya, MX record menentukan ke mana email untuk domain tertentu harus dikirim.

---

## Analogi / Intuisi

Bayangkan kamu ingin menelepon restoran "Warung Solo Asli" tapi tidak hafal nomornya. Kamu membuka kontak di HP (cache lokal) — tidak ada. Kamu telepon layanan informasi 108 (DNS resolver): "Tolong carikan nomor Warung Solo Asli." Operator 108 tidak langsung tahu, jadi ia menelepon pusat informasi nasional (Root server): "Di mana info untuk restoran .id?" Pusat nasional menjawab: "Tanya kantor info Jawa Tengah (TLD server)." Operator 108 menelepon Jawa Tengah, yang menjawab: "Tanya kantor info Kota Surakarta (authoritative server)." Akhirnya kantor Surakarta memberikan nomor telepon yang benar. Operator 108 menyampaikan nomor itu ke kamu — dan mencatat di bukunya (cache) supaya kalau ada yang bertanya lagi, tidak perlu ulang semua langkah.

---

## Contoh Konkret

Kamu membuka browser dan mengetik `uns.ac.id`:

1. **Browser cache check:** Browser memeriksa apakah sudah tahu IP `uns.ac.id` dari kunjungan sebelumnya. Belum ada.

2. **OS cache check:** Sistem operasi memeriksa cache DNS lokal dan file `hosts`. Belum ada.

3. **Recursive query ke resolver:** OS mengirim query ke DNS resolver yang dikonfigurasi (misal `8.8.8.8`, Google Public DNS): "Apa IP address `uns.ac.id`?"

4. **Resolver → Root server (iterative):** Resolver bertanya ke Root server. Root server menjawab: "Saya tidak tahu `uns.ac.id`, tapi server yang menangani `.id` ada di `ns1.id` (IP: `xxx.xxx.xxx.xxx`)."

5. **Resolver → TLD server `.id` (iterative):** Resolver bertanya ke TLD server `.id`. TLD server menjawab: "Domain `ac.id` ditangani oleh name server `ns1.ac.id` (IP: `yyy.yyy.yyy.yyy`)."

6. **Resolver → Authoritative server `ac.id` (iterative):** Resolver bertanya ke authoritative server. Server menjawab: "`uns.ac.id` → A record → `103.xx.xx.xx`." *(IP fiktif)*

7. **Resolver → Browser:** Resolver mengirim jawaban final ke OS, yang meneruskan ke browser. Resolver juga menyimpan hasil ini di cache selama TTL yang ditentukan (misal 3600 detik = 1 jam).

8. **Browser connect:** Browser menggunakan IP `103.xx.xx.xx` untuk memulai koneksi TCP ke web server UNS.

---

## Keterkaitan

- **Bagian dari:** [[Network Protocols]], [[TCP-IP Model|TCP/IP Model — Application Layer]]
- **Berhubungan dengan:** [[IP Address]], [[HTTP]], [[UDP]], [[TCP]]
- **Digunakan dalam:** [[Internet]], [[Web Browsing]], [[Email Systems]]
- **Berlawanan dengan / Jangan bingung dengan:** **ARP** — ARP menerjemahkan IP address ke [[MAC Address]] dalam satu LAN (Layer 2↔3); DNS menerjemahkan nama domain ke [[IP Address]] di level aplikasi (Layer 7↔3). Keduanya adalah "sistem terjemahan," tapi bekerja di lapisan dan cakupan yang sangat berbeda.

---

## Pertanyaan Terbuka

- Bagaimana **DNS over HTTPS (DoH)** dan **DNS over TLS (DoT)** meningkatkan privasi dibanding DNS biasa? Apa trade-off-nya?
- Apa yang terjadi jika authoritative server sebuah domain down — apakah website langsung tidak bisa diakses, atau cache menyelamatkan?
- Bagaimana **DNS poisoning/spoofing** bekerja, dan apa mekanisme pertahanan modern (DNSSEC) untuk mencegahnya?
- Dalam arsitektur microservice, bagaimana internal DNS (service discovery) berbeda dari DNS internet publik?

---

## Sumber

- Berasal dari: [[CN - 1 - Pengenalan Jaringan Komputer]] (implied: internet infrastructure), [[TCP-IP Model]] (Application Layer protocols)
- Referensi: Forouzan, B.A. — *Data Communications and Networking*, 5th Ed. — Chapter on Application Layer / DNS
- Eksternal: [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
- Eksternal: [Wikipedia — Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)
- Eksternal: [freeCodeCamp — How DNS Works](https://www.freecodecamp.org/news/what-is-dns/)
