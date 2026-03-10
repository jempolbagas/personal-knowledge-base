---
title:
  - Rules of Inference
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
  - Proof Techniques
semester: 4
tags:
  - discrete-mathematics
  - logic
  - inference
  - proofs
  - formal-reasoning
created: 2026-03-06
---

# Rules of Inference

> Aturan-aturan formal yang memungkinkan kita menarik kesimpulan (**conclusion**) yang pasti valid dari premis-premis (**premises**) yang diketahui — tanpa harus menebak atau berasumsi.

---

## Penjelasan

Rules of inference (aturan inferensi) adalah "mesin" di balik setiap pembuktian matematika yang valid. Jika [[Proposisi|proposisi]] adalah bahan bakunya dan [[Operator Logika]] adalah cara menggabungkannya, maka rules of inference adalah prosedur yang mengolah bahan-bahan tersebut menjadi kesimpulan.

Sebuah **argumen** dalam logika terdiri dari satu atau lebih premis (pernyataan yang diasumsikan benar) dan satu kesimpulan. Argumen disebut **valid** jika kesimpulannya pasti benar *setiap kali* semua premisnya benar. Validitas bukan soal apakah premisnya *benar di dunia nyata* — melainkan apakah *struktur penalaran*-nya benar.

Delapan aturan inferensi fundamental yang paling sering digunakan:

| Aturan | Bentuk | Inti |
|---|---|---|
| **Modus Ponens** | $p, \; p \rightarrow q \;\therefore q$ | "Jika p maka q. p benar. Jadi q benar." |
| **Modus Tollens** | $\lnot q, \; p \rightarrow q \;\therefore \lnot p$ | "Jika p maka q. q salah. Jadi p salah." |
| **Hypothetical Syllogism** | $p \rightarrow q, \; q \rightarrow r \;\therefore p \rightarrow r$ | Rantai implikasi |
| **Disjunctive Syllogism** | $p \lor q, \; \lnot p \;\therefore q$ | Eliminasi salah satu alternatif |
| **Addition** | $p \;\therefore p \lor q$ | Menambah disjungsi |
| **Simplification** | $p \land q \;\therefore p$ | Mengambil satu konjung |
| **Conjunction** | $p, \; q \;\therefore p \land q$ | Menggabung dua fakta |
| **Resolution** | $p \lor q, \; \lnot p \lor r \;\therefore q \lor r$ | Fondasi automated theorem proving |

**Modus Ponens** adalah aturan yang paling intuitif dan paling sering digunakan. **Modus Tollens** adalah pasangannya yang bekerja "mundur" — dari negasi kesimpulan ke negasi hipotesis (terkait erat dengan pembuktian kontrapositif). **Resolution** adalah aturan yang menjadi fondasi algoritma pembuktian otomatis dalam AI — program dapat melakukan pembuktian hanya dengan menerapkan resolution berulang kali.

Sama pentingnya adalah mengenali **fallacies** (kesalahan penalaran yang tampak valid) — khususnya *affirming the consequent* ($p \rightarrow q, \; q \;\therefore p$ — **INVALID**) dan *denying the antecedent* ($p \rightarrow q, \; \lnot p \;\therefore \lnot q$ — **INVALID**).

---

## Analogi / Intuisi

Bayangkan rules of inference seperti langkah-langkah legal dalam permainan catur. Kamu punya posisi awal (premis) dan ingin mencapai posisi akhir (kesimpulan). Setiap langkah harus sesuai aturan — kuda bergerak L, menteri bergerak lurus/diagonal. Kalau kamu membuat langkah ilegal, perpindahanmu tidak sah — tak peduli betapa bagusnya posisi yang kamu capai. Modus Ponens seperti langkah menteri yang lurus ke depan — langsung dan kuat. Modus Tollens seperti langkah kuda yang berbelok — tidak langsung, tapi tetap sah dan sering lebih efektif.

---

## Contoh Konkret

**Pembuktian sederhana menggunakan beberapa rules of inference:**

Premis:
1. "Jika hari ini Senin, maka ada kelas matdis." $\quad (p \rightarrow q)$
2. "Jika ada kelas matdis, maka saya harus bangun pagi." $\quad (q \rightarrow r)$
3. "Hari ini Senin." $\quad (p)$

Langkah pembuktian:

| Langkah | Pernyataan | Justifikasi |
|---|---|---|
| 4 | $q$ ("Ada kelas matdis") | Modus Ponens pada (1) dan (3) |
| 5 | $p \rightarrow r$ ("Jika Senin, harus bangun pagi") | Hypothetical Syllogism pada (1) dan (2) |
| 6 | $r$ ("Saya harus bangun pagi") | Modus Ponens pada (5) dan (3), atau pada (2) dan (4) |

Kesimpulan: $r$ — "Saya harus bangun pagi." ✓

---

## Keterkaitan

- **Bagian dari:** [[Mathematical Logic]], [[Proof Techniques]]
- **Berhubungan dengan:** [[Proposisi]], [[Operator Logika]], [[Logika Predikat]]
- **Digunakan dalam:** Pembuktian matematika (langsung, tidak langsung, kontradiksi), automated theorem proving, formal verification, debugging logical errors
- **Berlawanan dengan / Jangan bingung dengan:** **Fallacies** — argumen yang *tampak* mengikuti aturan inferensi tetapi sebenarnya tidak valid (affirming the consequent, denying the antecedent)

---

## Pertanyaan Terbuka

- Apakah *semua* pembuktian bisa direduksi menjadi serangkaian penerapan rules of inference, atau ada pembuktian yang memerlukan "lompatan kreatif" di luar aturan formal?
- Bagaimana **Resolution** diimplementasikan secara praktis dalam AI (misalnya di Prolog)?
- Apa hubungan antara rules of inference dan **natural deduction** dalam teori bukti?

---

## Sumber

- Berasal dari: [[Logika dan Pencacahan — MD1 — 1]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 1.6
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
