---
title:
  - Himpunan
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Set Theory
semester: 4
tags:
  - discrete-mathematics
  - sets
  - data-structures
  - foundations
status: 🌿 incubating
created: 2026-03-06
---

# Himpunan

> Kumpulan objek yang **terdefinisi dengan jelas**, **tidak terurut**, dan **tanpa duplikasi** — struktur paling fundamental dalam matematika yang menjadi fondasi hampir semua konsep lain.

---

## Penjelasan

Himpunan (set) adalah konsep dasar yang menopang seluruh bangunan matematika modern. Secara informal, himpunan adalah koleksi objek yang masing-masing disebut **elemen** atau **anggota**. Notasi: $a \in A$ berarti "$a$ adalah elemen dari himpunan $A$", dan $a \notin A$ berarti sebaliknya.

Dua sifat yang membedakan himpunan dari struktur lain: (1) **tidak terurut** — $\{1, 2, 3\} = \{3, 1, 2\}$, urutan penulisan tidak berpengaruh; dan (2) **tidak ada duplikasi** — $\{1, 1, 2\} = \{1, 2\}$, elemen yang sama hanya dihitung sekali. Ini kontras dengan **list** dalam pemrograman yang terurut dan mengizinkan duplikasi, atau **multiset** yang mengizinkan duplikasi tapi tidak terurut.

Himpunan bisa dideskripsikan dengan dua cara utama. **Roster method** mendaftar semua elemen secara eksplisit: $A = \{2, 4, 6, 8\}$. **Set-builder notation** mendefinisikan berdasarkan sifat: $A = \{x \in \mathbb{Z} \mid x \text{ genap dan } 0 < x \leq 8\}$. Set-builder notation jauh lebih powerful untuk himpunan besar atau tak berhingga.

Konsep-konsep turunan yang penting: **subhimpunan** ($A \subseteq B$ jika setiap elemen $A$ juga ada di $B$), **power set** ($\mathcal{P}(A)$ — himpunan dari semua subhimpunan $A$, dengan $|\mathcal{P}(A)| = 2^{|A|}$), dan **Cartesian product** ($A \times B$ — himpunan semua pasangan terurut). Operasi-operasi pada himpunan (union $\cup$, intersection $\cap$, difference $-$, complement $\overline{A}$) mengikuti hukum-hukum aljabar yang secara struktural identik dengan [[Operator Logika|logika proposisional]], terhubung melalui [[Hukum De Morgan]].

Dalam informatika, himpunan ada di mana-mana: tipe data `Set` dalam Python/Java, operasi `UNION`/`INTERSECT`/`EXCEPT` di SQL, himpunan state dalam automata, domain dan range [[Fungsi|fungsi]], dan himpunan entitas dalam database relasional.

---

## Analogi / Intuisi

Bayangkan himpunan seperti sebuah **kantong transparan** — kamu bisa melihat apa yang ada di dalamnya, tapi posisi objek di dalam kantong tidak penting (tidak terurut). Kalau ada dua kelereng merah identik, kantong tetap menganggapnya sebagai satu jenis (tidak ada duplikasi). Himpunan kosong ($\emptyset$) seperti kantong yang ada tapi kosong — ia tetap sebuah kantong, hanya tanpa isi.

---

## Contoh Konkret

Misalkan $A = \{1, 2, 3, 4\}$ dan $B = \{3, 4, 5, 6\}$, dengan $U = \{1, 2, 3, 4, 5, 6, 7\}$.

| Operasi | Hasil | Penjelasan |
|---|---|---|
| $A \cup B$ | $\{1, 2, 3, 4, 5, 6\}$ | Semua elemen di $A$ atau $B$ |
| $A \cap B$ | $\{3, 4\}$ | Elemen di $A$ dan $B$ |
| $A - B$ | $\{1, 2\}$ | Elemen di $A$ tapi tidak di $B$ |
| $\overline{A}$ | $\{5, 6, 7\}$ | Elemen di $U$ tapi tidak di $A$ |
| $\mathcal{P}(\{3, 4\})$ | $\{\emptyset, \{3\}, \{4\}, \{3, 4\}\}$ | Semua subhimpunan dari $A \cap B$ |

Power set dari $A \cap B$ memiliki $2^2 = 4$ elemen. Power set dari $A$ sendiri memiliki $2^4 = 16$ elemen.

---

## Keterkaitan

- **Bagian dari:** [[Set Theory]], [[Mathematical Foundations]]
- **Berhubungan dengan:** [[Proposisi]] (korespondensi logika-himpunan), [[Hukum De Morgan]], [[Fungsi]] (fungsi didefinisikan di atas himpunan)
- **Digunakan dalam:** Database relasional, tipe data `Set`, teori bahasa formal, definisi relasi, combinatorics
- **Berlawanan dengan / Jangan bingung dengan:** **List** (terurut, ada duplikasi) dan **Multiset/Bag** (tidak terurut, ada duplikasi)

---

## Pertanyaan Terbuka

- Mengapa $\emptyset$ adalah subhimpunan dari *setiap* himpunan — bahkan dari dirinya sendiri? Apakah ini hanya konvensi atau ada justifikasi logis yang mendalam?
- Dalam konteks implementasi, Python `set` menggunakan hash table — apa implikasi ini terhadap elemen-elemen yang boleh dimasukkan (harus hashable)?
- Apa paradoks Russell, dan bagaimana teori himpunan aksiomatik (ZFC) menghindarinya?

---

## Sumber

- Berasal dari: [[Himpunan dan Fungsi — MD1 — 2]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 2.1–2.2
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
