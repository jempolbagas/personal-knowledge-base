---
title:
  - Operator Logika
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
semester: 4
tags:
  - discrete-mathematics
  - logic
  - connectives
  - boolean-algebra
created: 2026-03-06
---

# Operator Logika

> Simbol-simbol yang menghubungkan [[Proposisi|proposisi-proposisi]] sederhana menjadi proposisi majemuk — seperti kata "dan", "atau", "bukan", dan "jika...maka" dalam bahasa formal matematika.

---

## Penjelasan

Operator logika (logical connectives) adalah alat untuk membangun **proposisi majemuk** (compound propositions) dari proposisi-proposisi sederhana. Tanpa operator logika, kita hanya bisa membuat pernyataan tunggal yang terisolasi. Dengan operator logika, kita bisa mengekspresikan penalaran, kondisi, dan hubungan antar pernyataan secara presisi.

Ada enam operator utama yang perlu dikuasai:

| Operator | Nama | Simbol | Arti |
|---|---|---|---|
| Negasi | NOT | $\lnot p$ | kebalikan dari $p$ |
| Konjungsi | AND | $p \land q$ | $p$ dan $q$ keduanya benar |
| Disjungsi | OR | $p \lor q$ | setidaknya salah satu benar (inklusif) |
| Disjungsi Eksklusif | XOR | $p \oplus q$ | tepat salah satu benar |
| Implikasi | IF...THEN | $p \rightarrow q$ | jika $p$ maka $q$ |
| Biimplikasi | IFF | $p \leftrightarrow q$ | $p$ jika dan hanya jika $q$ |

Setiap operator logika memiliki **tabel kebenaran** yang mendefinisikan nilainya secara tepat untuk semua kemungkinan input. Tabel kebenaran inilah yang menjadi definisi formal — bukan kata-kata bahasa sehari-hari yang bisa ambigu.

Yang paling kontra-intuitif adalah **implikasi** ($p \rightarrow q$). Implikasi hanya bernilai False ketika hipotesis ($p$) benar tetapi kesimpulan ($q$) salah. Jika hipotesis salah, implikasi **selalu bernilai True** — ini disebut **vacuous truth**. Konsep ini krusial untuk pembuktian matematis, karena banyak teorema dinyatakan dalam bentuk implikasi.

Dalam informatika, operator logika muncul di mana-mana: conditional statements (`if`, `else`), loop conditions (`while`), bitwise operations, query SQL (`AND`, `OR`, `NOT`), dan desain rangkaian digital (gerbang logika AND, OR, NOT, XOR).

---

## Analogi / Intuisi

Bayangkan operator logika seperti **gerbang tol** di jalan raya proposisi. Setiap gerbang menerima satu atau dua jalur masuk (input) dan mengeluarkan satu jalur (output: benar atau salah). Gerbang AND hanya membuka palang jika *kedua* jalur masuk aktif. Gerbang OR membuka jika *salah satu* jalur aktif. Gerbang NOT membalik — kalau jalur masuk aktif, palang justru menutup, dan sebaliknya.

---

## Contoh Konkret

Misalkan $p$: "Hari ini hujan" dan $q$: "Saya bawa payung."

| Ekspresi | Bacaan | Nilai jika hujan & bawa payung |
|---|---|---|
| $\lnot p$ | "Hari ini tidak hujan" | False |
| $p \land q$ | "Hujan dan saya bawa payung" | True |
| $p \lor q$ | "Hujan atau saya bawa payung (atau keduanya)" | True |
| $p \rightarrow q$ | "Jika hujan maka saya bawa payung" | True |
| $p \leftrightarrow q$ | "Hujan jika dan hanya jika saya bawa payung" | True |

Kasus menarik: jika **tidak hujan** ($p$ = F) dan **bawa payung** ($q$ = T):
- $p \rightarrow q$ = **True** (vacuous truth — janji tidak dilanggar karena kondisinya tidak terjadi)
- $p \leftrightarrow q$ = **False** (karena keduanya harus bernilai sama)

---

## Keterkaitan

- **Bagian dari:** [[Mathematical Logic]]
- **Berhubungan dengan:** [[Proposisi]], [[Hukum De Morgan]], [[Rules of Inference]]
- **Digunakan dalam:** Tabel kebenaran, pembuktian formal, conditional programming, SQL queries, digital circuit design
- **Berlawanan dengan / Jangan bingung dengan:** **Operator aritmatika** ($+$, $-$, $\times$) — operator logika bekerja pada nilai kebenaran, bukan bilangan

---

## Pertanyaan Terbuka

- Mengapa implikasi didefinisikan agar vacuous truth bernilai True — apakah ada justifikasi selain "karena definisinya begitu"?
- Bagaimana **precedence** (urutan prioritas) operator logika mengikuti konvensi? Apakah $\lnot$ selalu dievaluasi duluan, lalu $\land$, lalu $\lor$?
- Apakah XOR bisa diekspresikan menggunakan AND, OR, dan NOT saja?

---

## Sumber

- Berasal dari: [[Logika dan Pencacahan — MD1 — 1]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 1.1–1.2
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
