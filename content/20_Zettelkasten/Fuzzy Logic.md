---
title:
  - Fuzzy Logic
type: Concept
course:
  - Artificial Intelligence
topic:
  - Reasoning
semester: 4
tags:
  - artificial-intelligence
  - fuzzy-logic
  - soft-computing
  - reasoning
  - uncertainty
created: 2026-03-06
---

# Fuzzy Logic

> Sistem logika yang bekerja dengan derajat kebenaran antara 0 dan 1 — bukan hanya "benar" atau "salah" — sehingga mampu merepresentasikan konsep samar seperti "agak panas," "cukup tinggi," atau "kemungkinan besar."

---

## Penjelasan

**Fuzzy Logic** adalah bentuk logika bernilai banyak (*many-valued logic*) yang diperkenalkan oleh **Lotfi A. Zadeh** pada tahun 1965 melalui konsep *fuzzy sets*. Berbeda dengan [[Propositional Logic]] dan logika klasik yang hanya mengenal dua nilai kebenaran — benar (1) dan salah (0) — fuzzy logic memperbolehkan nilai kebenaran berupa bilangan real apa pun di antara 0 dan 1. Ini menjadikannya sangat cocok untuk menangani ketidakpastian, kekaburan, dan ketidaktepatan yang melekat dalam penalaran manusia sehari-hari.

Inti dari fuzzy logic terletak pada konsep **fungsi keanggotaan** (*membership function*). Dalam logika klasik, sebuah elemen hanya bisa *termasuk* atau *tidak termasuk* dalam suatu himpunan. Dalam fuzzy logic, setiap elemen memiliki *derajat keanggotaan* yang menunjukkan seberapa kuat elemen tersebut termasuk dalam suatu kategori. Misalnya, suhu 28°C bisa dikatakan "hangat" dengan derajat 0.7 dan "panas" dengan derajat 0.3 — keduanya berlaku bersamaan. Bentuk fungsi keanggotaan yang umum meliputi segitiga (*triangular*), trapesium (*trapezoidal*), dan Gaussian, masing-masing dipilih berdasarkan karakteristik variabel yang dimodelkan.

Sebuah **sistem inferensi fuzzy** (Fuzzy Inference System / FIS) bekerja melalui empat tahap utama: (1) **Fuzzifikasi** — mengubah input numerik tajam (*crisp*) menjadi nilai fuzzy menggunakan fungsi keanggotaan; (2) **Basis aturan** (*rule base*) — kumpulan aturan IF-THEN yang menghubungkan input fuzzy ke output fuzzy, misalnya "JIKA suhu PANAS DAN kelembapan TINGGI MAKA kipas SANGAT CEPAT"; (3) **Mesin inferensi** — mengevaluasi semua aturan yang aktif dan menggabungkan hasilnya; (4) **Defuzzifikasi** — mengubah output fuzzy gabungan kembali menjadi satu nilai numerik tajam yang dapat digunakan untuk aksi nyata. Metode defuzzifikasi yang paling populer adalah *Centroid* (pusat gravitasi dari area di bawah kurva output).

Fuzzy logic merupakan salah satu pilar utama dari **Soft Computing** — paradigma komputasi yang toleran terhadap ketidaktepatan dan ketidakpastian, bersama dengan [[Neural Network]] dan algoritma evolusioner. Pendekatan ini menjembatani kesenjangan antara logika formal yang rigid dan cara manusia sesungguhnya bernalar tentang dunia yang penuh kekaburan.

---

## Analogi / Intuisi

Bayangkan kamu sedang mengemudi dan bertanya pada temanmu: "Apakah jalan ini macet?" Dalam logika klasik, temanmu hanya bisa menjawab "YA" atau "TIDAK" — padahal kenyataannya mungkin "agak macet" atau "lumayan lancar tapi mulai padat." Itulah cara kerja fuzzy logic. Alih-alih memaksa dunia ke dalam kotak hitam-putih, ia mengizinkan "abu-abu" — kamu bisa bilang jalanan ini "macet dengan derajat 0.6" dan "lancar dengan derajat 0.4." Kemudian, berdasarkan derajat kemacetan itu, sistem bisa memutuskan untuk "agak perlambat kecepatan" — bukan berhenti total, bukan juga melaju kencang. Fuzzy logic meniru *cara manusia sesungguhnya berpikir* tentang konsep-konsep yang tidak tegas.

---

## Contoh Konkret

**Sistem kontrol AC otomatis menggunakan Fuzzy Logic:**

Misalkan sebuah AC pintar menggunakan FIS dengan input "suhu ruangan" dan output "kecepatan kipas."

**Langkah 1 — Fuzzifikasi:**
Suhu ruangan terukur = 27°C. Berdasarkan fungsi keanggotaan:
- μ_dingin(27) = 0.0 (tidak termasuk "dingin")
- μ_hangat(27) = 0.6 (cukup "hangat")
- μ_panas(27) = 0.3 (sedikit "panas")

**Langkah 2 — Aturan fuzzy:**
- Aturan 1: JIKA suhu HANGAT MAKA kipas SEDANG → aktif dengan derajat 0.6
- Aturan 2: JIKA suhu PANAS MAKA kipas CEPAT → aktif dengan derajat 0.3

**Langkah 3 — Inferensi:**
Kedua aturan aktif, menghasilkan area output fuzzy gabungan.

**Langkah 4 — Defuzzifikasi (metode Centroid):**
Dari area gabungan, dihitung pusat gravitasinya → hasil: kecepatan kipas = 62% (dari kecepatan maksimum).

Hasilnya bukan "kipas mati" atau "kipas maksimum" — melainkan *nilai proporsional* yang halus dan responsif terhadap kondisi nyata.

---

## Keterkaitan

- **Bagian dari:** [[Soft Computing]], [[Reasoning]]
- **Berhubungan dengan:** [[Propositional Logic]], [[First Order Logic]], [[Neural Network]], [[Machine Learning]], [[Expert System]]
- **Digunakan dalam:** [[Intelligent Agent]] (sebagai komponen penalaran), [[Control Systems]], [[Robotics]], [[Natural Language Processing]]
- **Berlawanan dengan / Jangan bingung dengan:** [[Propositional Logic]] — logika klasik yang hanya mengenal benar/salah secara absolut. Juga jangan bingung dengan *probabilitas* — fuzzy logic mengukur *derajat keanggotaan* (seberapa cocok sesuatu termasuk dalam kategori), bukan *peluang kejadian* (seberapa mungkin sesuatu terjadi).

---

## Pertanyaan Terbuka

- Bagaimana cara menentukan bentuk dan parameter fungsi keanggotaan yang optimal? Apakah selalu ditentukan oleh pakar, atau bisa dipelajari secara otomatis (misalnya dengan [[Neural Network]])?
- Dalam kasus apa fuzzy logic lebih unggul dibandingkan pendekatan probabilistik seperti Bayesian inference, dan kapan sebaliknya?
- Bagaimana fuzzy logic diterapkan dalam konteks project AI di kuliah — apakah bisa dikombinasikan dengan algoritma searching atau learning yang telah dipelajari di pertemuan sebelumnya?

---

## Sumber

- Berasal dari: [[Konsep Kecerdasan Buatan - AI - 2]] (Week 10–12 RPS: "Propositional Logic, First Order Logic, Fuzzy Logic")
- Berasal dari: [[RPS-AI]] (Bahan Kajian — Reasoning: fuzzy logic)
- Referensi: Russell, S. & Norvig, P. — *Artificial Intelligence: A Modern Approach*, 3rd Ed.
- Referensi: Suyanto — *Artificial Intelligence: Searching, Reasoning, Planning and Learning*, 2007
- Eksternal: [Wikipedia — Fuzzy Logic](https://en.wikipedia.org/wiki/Fuzzy_logic)
- Eksternal: [GeeksForGeeks — Fuzzy Logic Introduction](https://www.geeksforgeeks.org/fuzzy-logic-introduction/)
- Eksternal: [Britannica — Fuzzy Logic](https://www.britannica.com/technology/fuzzy-logic)
- Eksternal: [TechTarget — Fuzzy Logic](https://www.techtarget.com/searchenterpriseai/definition/fuzzy-logic)
