---
title:
  - Fungsi
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Set Theory
  - Functions
semester: 4
tags:
  - discrete-mathematics
  - functions
  - mapping
  - injective
  - surjective
  - bijective
status: 🌿 incubating
created: 2026-03-06
---

# Fungsi

> Sebuah aturan yang memetakan **setiap** elemen dari satu [[Himpunan|himpunan]] (domain) ke **tepat satu** elemen di himpunan lain (codomain) — tidak boleh ada input yang tidak punya output, dan tidak boleh ada input dengan dua output berbeda.

---

## Penjelasan

Fungsi (function) adalah salah satu konsep paling sentral dalam matematika dan informatika. Secara formal, fungsi $f: A \rightarrow B$ adalah relasi khusus dari [[Himpunan|himpunan]] $A$ ke himpunan $B$ di mana setiap elemen $a \in A$ dipasangkan dengan **tepat satu** elemen $b \in B$. Himpunan $A$ disebut **domain** (semua input yang valid), $B$ disebut **codomain** (semua output yang mungkin), dan himpunan output yang benar-benar dihasilkan disebut **range** (image).

Perbedaan codomain dan range adalah hal yang sering membingungkan tapi krusial. Codomain adalah himpunan "target" yang kita deklarasikan; range adalah subhimpunan codomain yang benar-benar "tertembak" oleh fungsi. Untuk $f(x) = x^2$ dengan $f: \mathbb{R} \rightarrow \mathbb{R}$, codomain-nya adalah $\mathbb{R}$ tapi range-nya hanya $[0, \infty)$ — bilangan negatif tidak pernah menjadi output.

Fungsi diklasifikasikan menjadi tiga jenis penting:
- **Injektif** (one-to-one): input berbeda selalu menghasilkan output berbeda. Tidak ada dua panah yang mengarah ke titik yang sama di codomain.
- **Surjektif** (onto): setiap elemen codomain memiliki setidaknya satu preimage. Tidak ada titik di codomain yang "sendirian" tanpa panah.
- **Bijektif** (one-to-one correspondence): injektif DAN surjektif sekaligus. Setiap input terhubung ke tepat satu output yang unik, dan sebaliknya. Fungsi bijektif adalah satu-satunya fungsi yang memiliki **invers** yang terdefinisi dengan baik.

Dalam informatika, fungsi muncul secara literal sebagai *function* atau *method* dalam setiap bahasa pemrograman, sebagai *hash function* yang memetakan data ke indeks, sebagai *mapping* di database, dan sebagai *transfer function* di neural networks. Sifat injektif/surjektif/bijektif memiliki implikasi langsung — misalnya, fungsi enkripsi *harus* bijektif agar data bisa didekripsi kembali.

---

## Analogi / Intuisi

Bayangkan fungsi sebagai **mesin vending**. Domain adalah semua tombol yang bisa kamu tekan. Codomain adalah semua jenis minuman yang tertulis di katalog mesin. Range adalah minuman yang *benar-benar tersedia* hari ini (mungkin ada yang habis). Aturannya: setiap tombol harus mengeluarkan tepat satu minuman (bukan nol, bukan dua). Kalau mesin injektif, setiap tombol mengeluarkan minuman yang *berbeda*. Kalau surjektif, *setiap* minuman di katalog bisa diakses oleh setidaknya satu tombol. Kalau bijektif, ada korespondensi sempurna satu-satu antara tombol dan minuman.

---

## Contoh Konkret

Misalkan $A = \{1, 2, 3\}$ dan $B = \{a, b, c, d\}$.

**Contoh fungsi injektif (tapi tidak surjektif):**
$$f(1) = a, \quad f(2) = c, \quad f(3) = d$$
Injektif ✓ (setiap output berbeda). Tidak surjektif ✗ (elemen $b$ di codomain tidak memiliki preimage).

**Contoh fungsi surjektif — tidak mungkin dari $A$ ke $B$!**
Karena $|A| = 3 < 4 = |B|$, tidak cukup elemen di domain untuk "menutupi" semua elemen di codomain. Ini mengilustrasikan fakta penting: fungsi surjektif mensyaratkan $|A| \geq |B|$.

**Contoh bijektif:** Jika $B = \{a, b, c\}$:
$$f(1) = b, \quad f(2) = a, \quad f(3) = c$$
Injektif ✓ dan surjektif ✓. Inversnya: $f^{-1}(a) = 2, \; f^{-1}(b) = 1, \; f^{-1}(c) = 3$.

**Fakta penting tentang kardinalitas:**
- Injektif memungkinkan: $|A| \leq |B|$
- Surjektif memungkinkan: $|A| \geq |B|$
- Bijektif memungkinkan: $|A| = |B|$

---

## Keterkaitan

- **Bagian dari:** [[Set Theory]], [[Mathematical Foundations]]
- **Berhubungan dengan:** [[Himpunan]] (fungsi didefinisikan pada himpunan), [[Logika Predikat]] (kuantor digunakan dalam definisi formal)
- **Digunakan dalam:** Pemrograman (functions/methods), kriptografi (bijeksi enkripsi/dekripsi), analisis algoritma, generating functions (MK ini minggu 9–13)
- **Berlawanan dengan / Jangan bingung dengan:** **Relasi** — relasi adalah pasangan terurut *apapun* dari $A \times B$; fungsi adalah relasi dengan syarat tambahan "tepat satu output per input"

---

## Pertanyaan Terbuka

- Apakah setiap fungsi injektif dari himpunan berhingga ke dirinya sendiri pasti bijektif? (Spoiler: ya, ini disebut **Pigeonhole Principle** — topik minggu ke-6)
- Bagaimana konsep injeksi/surjeksi/bijeksi digunakan untuk membandingkan "ukuran" himpunan tak berhingga?
- Dalam pemrograman, apakah fungsi yang memiliki *side effects* masih dianggap "fungsi" secara matematis?

---

## Sumber

- Berasal dari: [[Himpunan dan Fungsi — MD1 — 2]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 2.3
- Referensi: Munir, R. — *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
