---
title:
  - Proposisi
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
semester: 4
tags:
  - discrete-mathematics
  - logic
  - proposition
  - formal-reasoning
created: 2026-03-06
---

# Proposisi

> Sebuah pernyataan deklaratif yang bisa dinilai bernilai **benar** atau **salah** — tidak pernah keduanya sekaligus, dan tidak pernah "tidak tentu."

---

## Penjelasan

Proposisi (proposition) adalah unit terkecil dari logika formal. Ia adalah kalimat pernyataan yang memiliki **nilai kebenaran** (truth value) yang definitif: benar (True / T) atau salah (False / F). Prinsip ini disebut **prinsip bivalen** (principle of bivalence) — setiap proposisi harus tepat salah satu dari dua nilai itu.

Mengapa proposisi penting? Karena seluruh bangunan logika matematika, pembuktian, dan reasoning dalam ilmu komputer berdiri di atas proposisi. Ketika kamu menulis *conditional statement* dalam program (`if`, `while`), kamu sedang mengevaluasi proposisi. Ketika kamu mendesain query database, kamu menyusun proposisi. Ketika kamu merancang sirkuit digital, gerbang logika-nya mengimplementasikan operasi atas proposisi.

Penting untuk membedakan apa yang **bukan** proposisi: pertanyaan ("Berapa umurmu?"), perintah ("Tutup pintu!"), dan ekspresi yang kebenarannya tergantung pada variabel bebas ("$x + 1 = 5$"). Ekspresi terakhir disebut **fungsi proposisional** — ia baru menjadi proposisi setelah variabelnya diikat oleh suatu nilai atau oleh [[Logika Predikat|kuantor]].

Proposisi dilambangkan dengan huruf kecil: $p$, $q$, $r$, dst. Proposisi-proposisi sederhana bisa digabungkan dengan [[Operator Logika]] untuk membentuk **proposisi majemuk** (compound proposition) yang lebih kompleks.

---

## Analogi / Intuisi

Bayangkan proposisi seperti lampu yang punya saklar: ia hanya bisa **nyala** (True) atau **mati** (False). Tidak ada posisi setengah-nyala. Sebuah pertanyaan atau perintah tidak punya saklar sama sekali — mereka bukan lampu, mereka bukan proposisi.

---

## Contoh Konkret

Evaluasi mana yang merupakan proposisi:

1. "Surabaya adalah ibu kota Jawa Timur." → ✅ Proposisi (True)
2. "3 + 5 = 9" → ✅ Proposisi (False)
3. "Apakah kamu mahasiswa?" → ❌ Bukan proposisi (ini pertanyaan)
4. "$n$ adalah bilangan genap" → ❌ Bukan proposisi, ini **fungsi proposisional** — kebenarannya tergantung nilai $n$.
5. "Setiap bilangan prima lebih besar dari 1 adalah ganjil." → ✅ Proposisi (False — karena 2 adalah prima dan genap)

---

## Keterkaitan

- **Bagian dari:** [[Mathematical Logic]]
- **Berhubungan dengan:** [[Operator Logika]], [[Logika Predikat]], [[Hukum De Morgan]]
- **Digunakan dalam:** [[Rules of Inference]], pembuktian matematika, conditional statements dalam pemrograman, query database
- **Berlawanan dengan / Jangan bingung dengan:** **Fungsi Proposisional** — ekspresi dengan variabel bebas yang *belum* bernilai benar/salah sampai variabelnya diikat

---

## Pertanyaan Terbuka

- Apakah Goldbach's Conjecture ("setiap bilangan genap >2 adalah jumlah dua prima") termasuk proposisi, padahal belum dibuktikan benar atau salah?
- Bagaimana logika multi-valued (fuzzy logic) menangani kasus di mana prinsip bivalen tidak berlaku?

---

## Sumber

- Berasal dari: [[Logika dan Pencacahan — MD1 — 1]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 1.1
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
