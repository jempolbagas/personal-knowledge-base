---
title:
  - Logika Predikat
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
semester: 4
tags:
  - discrete-mathematics
  - logic
  - predicates
  - quantifiers
  - formal-reasoning
created: 2026-03-06
---

# Logika Predikat

> Perluasan dari logika proposisional yang memungkinkan kita berbicara tentang **variabel**, **objek**, dan **sifat-sifatnya** — dengan menggunakan **kuantor** (∀ dan ∃) untuk mengikat variabel menjadi pernyataan yang bernilai benar atau salah.

---

## Penjelasan

Logika proposisional memiliki satu keterbatasan besar: ia hanya bisa menangani pernyataan yang sudah pasti benar atau salah. Ia tidak bisa mengekspresikan pernyataan tentang *variabel* — seperti "$x > 5$" yang kebenarannya tergantung pada nilai $x$. Di sinilah **logika predikat** (predicate logic, atau first-order logic) mengambil alih.

Sebuah **predikat** adalah pernyataan yang mengandung satu atau lebih variabel. Notasi: $P(x)$ berarti "pernyataan $P$ tentang $x$." Predikat sendiri *bukan* [[Proposisi|proposisi]] — ia adalah **fungsi proposisional** yang menjadi proposisi ketika variabelnya diberikan nilai konkret ($P(7)$: "7 adalah bilangan prima" → True) atau diikat oleh **kuantor**.

Dua kuantor utama:

**Kuantor Universal** ($\forall$) — "untuk semua": $\forall x \, P(x)$ berarti "$P(x)$ benar untuk *setiap* $x$ dalam domain." Untuk membantahnya, cukup temukan satu **counterexample** — satu nilai $x$ di mana $P(x)$ salah.

**Kuantor Eksistensial** ($\exists$) — "terdapat setidaknya satu": $\exists x \, P(x)$ berarti "ada setidaknya satu $x$ dalam domain sehingga $P(x)$ benar." Untuk membantahnya, kamu harus menunjukkan bahwa *tidak ada satupun* $x$ yang memenuhi.

Salah satu aturan paling penting dalam logika predikat adalah **negasi kuantor**, yang merupakan bentuk [[Hukum De Morgan]] untuk kuantor:

$$\lnot(\forall x \, P(x)) \equiv \exists x \, \lnot P(x)$$
$$\lnot(\exists x \, P(x)) \equiv \forall x \, \lnot P(x)$$

Artinya: "tidak semua mahasiswa lulus" sama dengan "ada mahasiswa yang tidak lulus." Dan "tidak ada mahasiswa yang lulus" sama dengan "semua mahasiswa tidak lulus."

Logika predikat adalah fondasi dari bahasa pemrograman deklaratif (Prolog), formal specification, database query (SQL `WHERE EXISTS`, `FOR ALL`), dan verifikasi formal perangkat lunak.

---

## Analogi / Intuisi

Kalau logika proposisional seperti kalimat-kalimat lengkap ("Langit biru", "2+2=4"), maka logika predikat seperti *template* kalimat dengan lubang yang bisa diisi: "__ adalah bilangan prima." Lubangnya bisa diisi siapa saja — 7 (True), 4 (False). **Kuantor** seperti instruksi: $\forall$ berarti "coba isi lubang itu dengan *semua* kemungkinan — apakah semuanya benar?", dan $\exists$ berarti "coba isi — apakah *setidaknya satu* benar?"

---

## Contoh Konkret

**Domain:** $\mathbb{Z}^+$ (bilangan bulat positif).
**Predikat:** $P(x)$: "$x^2 \geq x$."

**Evaluasi $\forall x \, P(x)$:**
- $P(1)$: $1 \geq 1$ ✓
- $P(2)$: $4 \geq 2$ ✓
- $P(3)$: $9 \geq 3$ ✓
- Untuk setiap $x \in \mathbb{Z}^+$, $x^2 = x \cdot x \geq x \cdot 1 = x$ (karena $x \geq 1$).
- Jadi $\forall x \in \mathbb{Z}^+, \; x^2 \geq x$ → **True** ✓

**Negasi:** $\lnot(\forall x \, P(x)) \equiv \exists x \, (x^2 < x)$.
Apakah ada bilangan bulat positif yang kuadratnya lebih kecil dari dirinya sendiri? Tidak — jadi negasinya **False**, yang konsisten dengan pernyataan asli yang True.

**Nested quantifiers (kuantor bersarang):**
$$\forall x \, \exists y \, (x + y = 0)$$
"Untuk setiap $x$, terdapat $y$ sehingga $x + y = 0$."
Dalam $\mathbb{Z}$: True (pilih $y = -x$). Dalam $\mathbb{Z}^+$: False (tidak ada bilangan bulat positif yang jumlahnya dengan $x$ positif menghasilkan 0).

Perhatikan: **urutan kuantor penting!** $\forall x \, \exists y$ ≠ $\exists y \, \forall x$ secara umum.

---

## Keterkaitan

- **Bagian dari:** [[Mathematical Logic]]
- **Berhubungan dengan:** [[Proposisi]] (predikat menjadi proposisi setelah variabel diikat), [[Hukum De Morgan]] (negasi kuantor), [[Himpunan]] (set-builder notation menggunakan predikat), [[Fungsi]] (definisi formal menggunakan kuantor)
- **Digunakan dalam:** SQL (`EXISTS`, `NOT EXISTS`, `WHERE`), Prolog (pemrograman logika), formal verification, [[Rules of Inference]] untuk kuantor
- **Berlawanan dengan / Jangan bingung dengan:** **Logika proposisional** — logika proposisional tidak bisa menangani variabel atau kuantor; logika predikat adalah *superset*-nya

---

## Pertanyaan Terbuka

- Bagaimana menangani kuantor bersarang yang lebih dari dua level? Apakah ada strategi sistematik untuk mengevaluasinya?
- Apakah ada situasi praktis di mana $\forall x \exists y \, P(x,y)$ dan $\exists y \forall x \, P(x,y)$ keduanya benar?
- Bagaimana logika predikat terhubung ke **first-order logic** dan **higher-order logic** — apa yang "first-order" artinya?

---

## Sumber

- Berasal dari: [[Logika dan Pencacahan — MD1 — 1]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 1.4–1.5
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
- Eksternal: [Wikipedia — First-order Logic](https://en.wikipedia.org/wiki/First-order_logic)
