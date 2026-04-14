---
title:
  - Perhitungan (Counting)
type: Lecture
course:
  - Discrete Mathematics I
topic:
  - Counting Theory
semester: 2
tags:
  - discrete-mathematics
  - combinatorics
  - counting
  - pigeonhole-principle
  - college
  - lecture-note
status: 🌿 incubating
created: 2026-04-07
---

# Perhitungan (Counting)

**Reference:** Rosen, K.H. *Discrete Mathematics and Its Applications*; Munir, R. *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
**Source:** [[RPS-MD1]]
**Prasyarat:** [[DM1 - 4 - Teknik Induksi & Rekursi]]

---

## Daftar Isi

1. [[#1. Pengantar Teori Perhitungan (Counting Theory)]]
    - [[#1.1 Aturan Penjumlahan (The Sum Rule)]]
    - [[#1.2 Aturan Perkalian (The Product Rule)]]
2. [[#2. The Pigeonhole Principle (Prinsip Sarang Merpati)]]
3. [[#3. Permutasi (Permutations)]]
4. [[#4. Kombinasi (Combinations)]]
5. [[#5. Komparasi Permutasi vs Kombinasi]]
6. [[#Summary — Key Concepts at a Glance]]
7. [[#Active Recall Questions]]

---

## 1. Pengantar Teori Perhitungan (Counting Theory)

Dalam ilmu komputer, **Counting Theory** sangat esensial. Kita menggunakannya untuk menganalisis waktu komputasi (kompleksitas memori dan iterasi), mengukur performa jaringan, mengalokasikan sumber daya komputasi secara dinamis, serta pada bidang keamanan (*cryptography* dan probabilitas *password*).

Terdapat dua prinsip paling mendasar dalam teori perhitungan, yaitu *Sum Rule* dan *Product Rule*.

### 1.1 Aturan Penjumlahan (The Sum Rule)

Apabila sebuah tugas dapat direpresentasikan atau diselesaikan dengan dua cara, di mana cara pertama memiliki $m$ pilihan dan cara kedua memiliki $n$ pilihan, dan **kedua cara tersebut tidak dapat dilakukan secara bersamaan** (*mutually exclusive*), maka total cara untuk menyelesaikan tugas tersebut adalah:
$$ m + n $$

**Contoh Kasus:** Mahasiswa program studi Informatika harus memilih satu buah proyek akhir dari dua direktori riset berbeda. Direktori pertama berisi 15 topik *AI*, dan direktori kedua berisi 10 topik *Cybersecurity*. Maka total probabilitas topik yang bisa dipilih mahasiswa adalah $15 + 10 = 25$ topik.

### 1.2 Aturan Perkalian (The Product Rule)

Apabila sebuah tugas dipecah menjadi rentetan prosedur (*sequence of procedures*) berurutan, misal prosedur pertama dapat dilakukan dengan $m$ cara, dan **setelahnya** prosedur kedua dapat dilakukan dengan $n$ cara, maka kombinasi total cara keseluruhan adalah:
$$ m \times n $$

**Contoh Kasus:** Sebuah sistem login menggunakan format *password* 2 karakter. Karakter pertama harus huruf vokal (*vowels*), dan karakter kedua harus digit *integer* base-10. Jumlah huruf vokal (A, I, U, E, O) adalah 5, dan jumlah digit (0-9) adalah 10. Total *password* mungkin yang di-*generate* adalah $5 \times 10 = 50$ *passwords*.

---

## 2. The Pigeonhole Principle (Prinsip Sarang Merpati)

Konsep dasar The **Pigeonhole Principle** digagas pertama kali secara matematis modern oleh Dirichlet (sehingga kadang disebut *Dirichlet's Box Principle*). 

> [!abstract] Definisi Pigeonhole Principle
> Misalkan terdapat $k$ buah *pigeonholes* (kotak abstrak/sarang). Jika kita memasukkan $N$ objek (merpati) ke dalam kotak-kotak tersebut, di mana ukuran $N > k$, maka **pasti** (dengan jaminan *guaranteed worst-case*) akan ada **setidaknya satu** kotak yang memuat lebih dari satu objek.
> 
> Rumusan generalized: Terdapat satu kotak yang mengandung minimal $\lceil N / k \rceil$ objek.

**Contoh Kasus dalam Sistem (*Hash Collisions*):**
Anggap kita memiliki *hash table* dengan kapasitas $k = 100$ slot indeks memori. Jika kita melakukan *storing* data ke dalam *hash table* sebanyak $N = 101$ entri yang di-*generate*, secara otomatis Prinsip Sarang Merpati memastikan terjadinya setidaknya **satu tabrakan** (*hash collision*), karena jumlah data sudah melewati kapasitas *slots* mutlak sistem.

---

## 3. Permutasi (Permutations)

**Permutations** adalah metode perhitungan pengurutan elemen spesifik dari struktur *set* di mana keberadaan **urutan (*order*) sangatlah diperhatikan atau krusial**. Elemen yang terambil dibedakan oleh posisinya secara mutlak (Contoh: Susunan A-B tidak dianggap sama dengan susunan B-A).

> [!formula] Rumus Permutasi
> Jumlah permutasi *r*-elemen (*subset*) yang diambil berturut-turut dari total himpunan *n*-elemen yang *distinct* dinyatakan dengan notasi $P(n, r)$:
> $$ P(n, r) = \frac{n!}{(n - r)!} $$

-  Kondisi khusus apabila $r = n$ (menyusun seluruh elemen secara keseluruhan iteratif), formulanya berubah ringkas menjadi $P(n, n) = n!$.

**Contoh Kasus:** Sistem memilih tiga *server node* unik (dari 10 total *server node* jaringan) untuk diberi tanggung jawab spesifik (*Load Balancer*, *Primary Database*, *Backup Database*). Karena peran tanggung jawab ini bergantung pada urutan penunjukan, kita memakai permutasi:
$$ P(10, 3) = \frac{10!}{(10-3)!} = \frac{10 \times 9 \times 8 \times 7!}{7!} = 720 $$
Terdapat 720 kemungkinan konfigurasi jaringan server.

---

## 4. Kombinasi (Combinations)

**Combinations** adalah skenario perhitungan tata-atur subset dari himpunan *set* universal di mana keberadaan **urutan (*order*) tidak dipedulikan atau relevan**. Elemen acak yang dikelompokkan dengan material yang sama dianggap utuh satu hitungan asalkan *membership*-nya seragam (Contoh: Kelompok "A-B" dihitung sebagai 1 probabilitas ekuivalen abstrak yang setara dengan kelompok "B-A").

> [!formula] Rumus Kombinasi
> Pembentukan kelompok elemen *r* yang diretas dari himpunan berukuran *n* ditandai logis dengan notasi $C(n, r)$ atau *binomial coefficient* $\binom{n}{r}$:
> $$ C(n, r) = \binom{n}{r} = \frac{n!}{r!(n - r)!} $$

**Contoh Kasus:** Dari kelas berisi deretan 10 *engineering students*, dipilih 3 *students* murni untuk satu kelompok set *Focus Group*. Karena ketiganya mendapat *treatment* seragam *Focus Group* dan urutan terpanggilnya tidak ada peran khusus, digunakan Kombinasi:
$$ C(10, 3) = \frac{10!}{3!(10-3)!} = \frac{10 \times 9 \times 8}{3 \times 2 \times 1} = 120 $$
Terdapat 120 pasang kelompok potensial.

---

## 5. Komparasi Permutasi vs Kombinasi

Pemahaman parameter *urgency of order* membedakan penentuan formula. Tabel ini meringkas kondisi pemakaian murni.

| Sifat Operasi | Permutasi | Kombinasi |
| :--- | :--- | :--- |
| **Pentingnya Urutan (*Order*)** | Relevan (*Order matters*) | Tidak Relevan (*Order does not matter*) |
| **Identitas Konfigurasi** | $\{A, B, C\} \neq \{C, B, A\}$ (2 entitas beda) | $\{A, B, C\} = \{C, B, A\}$ (entitas identik) |
| **Penerapan Kasus** | *Passwords, Role/Position assignment, Scheduling* | *Forming teams, Selecting random sample, Subsets* |
| **Korelasi Formula** | $P(n, r)$ lebih besar atau eksplosif | $C(n, r) = \frac{P(n,r)}{r!}$ (telah direduksi pembagi *redundant order*) |

---

## Summary — Key Concepts at a Glance

| Concept | Definition |
|---|---|
| *The Sum Rule* | Operasi probabilitas penjumlah ( $m+n$ ) kalau dua prosedur sifatnya terputus dan tidak dikerjakan bersama (*mutually exclusive*). |
| *The Product Rule* | Operasi peluang perkalian ( $m \times n$ ) jikalau tugas merupakan urutan kejadian berantai/sekuensial konsekutif. |
| *The Pigeonhole Principle* | Garansi matematis minimum tumpang-tindih (paling tidak berjumlah $\lceil N/k \rceil$) ketika rentang probabilitas $N$ melampaui batasan kapasitas ketersediaan $k$. |
| *Permutations* | Metode *counting* tata-urut selektif objek jika rotasi urutan membedakan nilai parameter hasil komputasi *($Order$ dipedulikan)*. |
| *Combinations* | Metode komputasi perhitungan selektif susunan murni jika skema klasifikasi acak dianggap *uniform/identik* *($Order$ tak dipedulikan)*. |

---

## Active Recall Questions

> [!question]- 1. Saat mengembangkan *routing algorithm* jaringan yang harus mengevaluasi seluruh rute perjalanan dari sumber ke mesin *endpoint* tujuan berdasar topologi 5 nodes unik, perlukah Anda mengenakan kaidah Kombinasi atau Permutasi dalam iterasi kalkulasinya? Dan jelaskan alasannya!
> Evaluasi rute tersebut harus dieksekusi dengan model kalkulasi **Permutations**. Alasannya jelas, algoritma penentu alur paket data seperti *routing* mementingkan urutan interkomunikasi berantai antar *nodes*. Alur *Node A $\rightarrow$ Node C $\rightarrow$ Node B* memiliki topologi sirkuit perantara beban jarak yang berbeda dengan *Node A $\rightarrow$ Node B $\rightarrow$ Node C*. Order sangat signifikan di *network routing*.

> [!question]- 2. Anda mendesain enkripsi primitif di mana basis kunci akses adalah acak $n$-karakter menggunakan alfabet standar 26 huruf alfabet universal tanpa membedakan kapital (A-Z). Jika program mengizinkan perulangan pengisian karakter yang sama berulang kali, haruskah anda memakai *Permutations*? Bagaimana fungsi perhitungannya?
> Jika sistem tersebut **mengizinkan karakter berulang** (*replacement allowed*), formula murni asli $P(n,r)$ milik standar permutasi tidak serta-merta berlaku tepat karena permutasi $P(n, r)$ mengasumsikan tarikan *distinct* pasca pengambilan tanpa mengembalikannya (*without replacement*). Dalam sistem *password* iteratif berulang karakter A dapat muncul lebih dari 1 kali (A A A). Kita harus membangunya murni dari parameter **Aturan Perkalian (*Product Rule*)**: untuk $r$ letak karakter, masing-masingnya punya 26 peluang. Total kemungkinannya murni $26^r$.

> [!question]- 3. Bagaimana *The Pigeonhole Principle* mendemonstrasikan fenomena paradoks ulang tahun (*Birthday Paradox*) di mana terdapat dua orang atau lebih memiliki basis bulan lahir sama di suatu kerumunan berjumlah hanya selusin (13 orang)?
> Terdapat 12 bulan dalam setahun (Ini merupakan set konstanta *pigeonholes* atau sarangnya, yakni $k=12$). Kita mempunyai 13 orang tak terhubung dalam kelas (Ini merupakan variabel $N$ merpati/objek, $N=13$). Karena $N > k$, sesuai The Pigeonhole Principle, dirumuskan $\lceil 13/12 \rceil = \lceil 1.08 \rceil = 2$. Artinya, matematika menjamin secara telak setidaknya terdapat satu spesifik bulan di mana 2 orang merayakan ulang tahun yang seragam pada bulan tersebut.
