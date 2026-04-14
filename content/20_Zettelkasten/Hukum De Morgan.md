---
title:
  - Hukum De Morgan
type: Concept
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
  - Set Theory
semester: 4
tags:
  - discrete-mathematics
  - logic
  - sets
  - de-morgan
  - equivalence
status: 🌿 incubating
created: 2026-03-06
---

# Hukum De Morgan

> Sepasang aturan yang menunjukkan bagaimana **negasi** berinteraksi dengan **AND/OR** (dalam logika) atau **intersection/union** (dalam himpunan) — intinya: negasi "membalik" operator dan menyebar ke setiap komponen.

---

## Penjelasan

Hukum De Morgan (De Morgan's Laws) adalah dua ekuivalensi logis yang ditemukan oleh matematikawan Augustus De Morgan pada abad ke-19. Hukum ini berlaku di **dua domain sekaligus** — logika proposisional dan teori himpunan — yang menjadikannya salah satu hukum paling universal dalam matematika diskrit.

**Dalam logika proposisional:**

$$\lnot(p \land q) \equiv (\lnot p) \lor (\lnot q)$$
$$\lnot(p \lor q) \equiv (\lnot p) \land (\lnot q)$$

Aturan pertama mengatakan: "bukan (p dan q)" sama dengan "bukan p **atau** bukan q." Aturan kedua: "bukan (p atau q)" sama dengan "bukan p **dan** bukan q." Perhatikan polanya: negasi masuk ke dalam, dan **AND berubah menjadi OR** (dan sebaliknya).

**Dalam teori himpunan:**

$$\overline{A \cap B} = \overline{A} \cup \overline{B}$$
$$\overline{A \cup B} = \overline{A} \cap \overline{B}$$

Bentuknya identik — ganti $\lnot$ dengan komplemen ($\overline{\phantom{A}}$), $\land$ dengan $\cap$, dan $\lor$ dengan $\cup$.

Mengapa hukum ini begitu penting? Karena ia muncul di hampir setiap konteks penalaran formal. Dalam pemrograman, De Morgan membantu menyederhanakan kondisi boolean yang kompleks. Dalam SQL, ia mengubah `NOT (A AND B)` menjadi `(NOT A) OR (NOT B)`. Dalam desain sirkuit digital, ia memungkinkan implementasi gerbang menggunakan jenis gerbang yang lebih sedikit (misalnya mengubah AND+NOT menjadi NAND saja). Dalam pembuktian matematika, ia digunakan untuk menegasikan proposisi universal dan eksistensial.

---

## Analogi / Intuisi

Bayangkan sebuah klub eksklusif dengan dua syarat masuk: kamu harus **tinggi DAN pakai jas**. Siapa yang *tidak* diizinkan masuk? Orang yang **tidak tinggi ATAU tidak pakai jas** (atau keduanya). Kamu tidak perlu melanggar *kedua* syarat — melanggar *salah satu* saja sudah cukup untuk ditolak. Itulah De Morgan: negasi dari "A dan B" adalah "bukan A **atau** bukan B."

Sebaliknya, jika syaratnya "tinggi ATAU pakai jas" (cukup salah satu), maka yang ditolak adalah orang yang **tidak tinggi DAN tidak pakai jas** — harus melanggar *keduanya* untuk benar-benar gagal.

---

## Contoh Konkret

**Dalam pemrograman — menyederhanakan kondisi:**

Misalkan kamu punya:
```python
if not (is_admin and is_active):
    deny_access()
```

Menggunakan De Morgan, ini ekuivalen dengan:
```python
if (not is_admin) or (not is_active):
    deny_access()
```

Kedua versi berperilaku identik, tetapi versi kedua sering lebih mudah dibaca karena setiap kondisi diperiksa secara eksplisit.

**Dalam logika — pembuktian via tabel kebenaran:**

| $p$ | $q$ | $p \land q$ | $\lnot(p \land q)$ | $\lnot p$ | $\lnot q$ | $\lnot p \lor \lnot q$ |
|---|---|---|---|---|---|---|
| T | T | T | **F** | F | F | **F** |
| T | F | F | **T** | F | T | **T** |
| F | T | F | **T** | T | F | **T** |
| F | F | F | **T** | T | T | **T** |

Kolom $\lnot(p \land q)$ dan $\lnot p \lor \lnot q$ identik di setiap baris → ekuivalen. ✓

---

## Keterkaitan

- **Bagian dari:** [[Mathematical Logic]], [[Himpunan|Set Theory]]
- **Berhubungan dengan:** [[Proposisi]], [[Operator Logika]], [[Himpunan]]
- **Digunakan dalam:** Simplifikasi boolean, SQL query optimization, digital circuit design (NAND/NOR gates), pembuktian matematika
- **Berlawanan dengan / Jangan bingung dengan:** **Hukum Distributif** — distributif menyebarkan operator *ke dalam* (misal: $p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$), sedangkan De Morgan menyebarkan *negasi* ke dalam sambil membalik operator

---

## Pertanyaan Terbuka

- Apakah De Morgan bisa di-generalisasi untuk lebih dari dua operand? (Misal: $\lnot(p \land q \land r) \equiv \lnot p \lor \lnot q \lor \lnot r$?)
- Bagaimana De Morgan diterapkan dalam konteks **kuantor** (quantifiers)? Apakah $\lnot(\forall x \, P(x)) \equiv \exists x \, \lnot P(x)$ ini bentuk De Morgan juga?

---

## Sumber

- Berasal dari: [[Logika dan Pencacahan — MD1 — 1]], [[Himpunan dan Fungsi — MD1 — 2]]
- Referensi: Rosen, K.H. — *Discrete Mathematics and Its Applications* — Chapter 1.3, 2.2
- Eksternal: [Wikipedia — De Morgan's Laws](https://en.wikipedia.org/wiki/De_Morgan%27s_laws)
