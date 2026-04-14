---
title:
  - Himpunan dan Fungsi
type: Lecture
course:
  - Discrete Mathematics I
topic:
  - Set Theory
  - Functions
semester: 4
tags:
  - discrete-mathematics
  - sets
  - functions
  - college
  - lecture-note
status: 🌳 evergreen
created: 2026-03-06
---

# Himpunan dan Fungsi

 **Reference:** Rosen, K.H. *Discrete Mathematics and Its Applications*; Munir, R. *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
 **Source:** [[RPS-MD1]]

---

## Daftar Isi

1. [[#1. Himpunan — Fondasi Matematika]]
    - [[#1.1 Definisi dan Notasi Himpunan]]
    - [[#1.2 Cara Mendeskripsikan Himpunan]]
    - [[#1.3 Himpunan-himpunan Bilangan Penting]]
    - [[#1.4 Himpunan Kosong dan Himpunan Semesta]]
    - [[#1.5 Subhimpunan (Subset)]]
    - [[#1.6 Power Set (Himpunan Kuasa)]]
    - [[#1.7 Kardinalitas (Cardinality)]]
2. [[#2. Operasi Himpunan (Set Operations)]]
    - [[#2.1 Gabungan (Union)]]
    - [[#2.2 Irisan (Intersection)]]
    - [[#2.3 Selisih (Difference)]]
    - [[#2.4 Komplemen (Complement)]]
    - [[#2.5 Diagram Venn]]
    - [[#2.6 Hukum-hukum Aljabar Himpunan]]
    - [[#2.7 Cartesian Product (Perkalian Kartesian)]]
3. [[#3. Fungsi (Functions)]]
    - [[#3.1 Definisi Fungsi]]
    - [[#3.2 Domain, Codomain, dan Range]]
    - [[#3.3 Jenis-jenis Fungsi]]
    - [[#3.4 Komposisi Fungsi]]
    - [[#3.5 Fungsi Invers]]
4. [[#4. Deret Penjumlahan (Summation Series)]]
    - [[#4.1 Notasi Sigma]]
    - [[#4.2 Deret-deret Penting]]
5. [[#Summary — Key Concepts at a Glance]]

---

## 1. Himpunan — Fondasi Matematika

Himpunan (set) adalah konsep paling mendasar dalam seluruh matematika modern. Hampir setiap objek matematika — bilangan, fungsi, relasi, struktur data — dapat didefinisikan dalam istilah himpunan. Dalam informatika, himpunan muncul di mana-mana: dari tipe data dalam bahasa pemrograman, operasi database (SQL secara literal bekerja dengan himpunan), hingga teori bahasa formal dan automata.

### 1.1 Definisi dan Notasi Himpunan

Sebuah **himpunan** adalah kumpulan objek-objek yang terdefinisi dengan jelas (well-defined), tidak terurut, dan tanpa duplikasi. Objek-objek dalam himpunan disebut **elemen** atau **anggota**.

Notasi dasar:
- $a \in A$ berarti "$a$ adalah anggota himpunan $A$"
- $a \notin A$ berarti "$a$ bukan anggota himpunan $A$"

Dua sifat kritis himpunan yang perlu selalu diingat:
1. **Tidak berurutan** — $\{1, 2, 3\} = \{3, 1, 2\}$. Urutan penulisan tidak mempengaruhi himpunan.
2. **Tidak ada duplikasi** — $\{1, 1, 2\} = \{1, 2\}$. Elemen yang sama hanya dihitung sekali.

### 1.2 Cara Mendeskripsikan Himpunan

Ada dua cara utama untuk mendeskripsikan isi sebuah himpunan:

**Roster Method (Enumerasi/Daftar):** Menuliskan semua elemen secara eksplisit di dalam kurung kurawal.
$$A = \{1, 2, 3, 4, 5\}$$
$$\text{Vokal} = \{a, e, i, o, u\}$$

Metode ini praktis untuk himpunan kecil, tetapi tidak layak untuk himpunan besar atau tak berhingga.

**Set-Builder Notation (Notasi Pembangun):** Mendefinisikan himpunan berdasarkan sifat yang harus dipenuhi oleh anggotanya.
$$B = \{x \in \mathbb{Z} \mid x > 0 \text{ dan } x \leq 10\}$$

Dibaca: "B adalah himpunan semua bilangan bulat $x$ sedemikian sehingga $x$ lebih besar dari 0 dan $x$ kurang dari atau sama dengan 10."

Set-builder notation adalah cara yang jauh lebih powerful dan umum. Sebagian besar himpunan dalam matematika dan ilmu komputer didefinisikan dengan cara ini.

### 1.3 Himpunan-himpunan Bilangan Penting

Dalam matematika, ada beberapa himpunan bilangan standar yang memiliki simbol khusus:

| Simbol | Nama | Isi |
|---|---|---|
| $\mathbb{N}$ | Natural Numbers | $\{0, 1, 2, 3, \ldots\}$ (kadang dimulai dari 1, tergantung konvensi) |
| $\mathbb{Z}$ | Integers (Zahlen) | $\{\ldots, -2, -1, 0, 1, 2, \ldots\}$ |
| $\mathbb{Z}^+$ | Positive Integers | $\{1, 2, 3, \ldots\}$ |
| $\mathbb{Q}$ | Rational Numbers | Semua bilangan yang dapat dinyatakan sebagai $\frac{p}{q}$ dengan $p, q \in \mathbb{Z}$ dan $q \neq 0$ |
| $\mathbb{R}$ | Real Numbers | Semua bilangan pada garis bilangan (rasional dan irasional) |
| $\mathbb{C}$ | Complex Numbers | Bilangan dalam bentuk $a + bi$ dengan $a, b \in \mathbb{R}$ |

Perhatikan hierarki inklusi: $\mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$

### 1.4 Himpunan Kosong dan Himpunan Semesta

**Himpunan kosong** ($\emptyset$ atau $\{\}$): Himpunan yang tidak memiliki anggota sama sekali. Ini bukan "ketiadaan himpunan" — himpunan kosong adalah sebuah himpunan yang _ada_, hanya saja isinya kosong.

Analogi: sebuah tas kosong tetaplah sebuah tas — kamu bisa melihatnya, memegangnya. Ia hanya tidak mengandung apapun di dalamnya.

Fakta penting: $\emptyset$ adalah **subhimpunan dari setiap himpunan**. Ini mengikuti dari logika: pernyataan "$\forall x (x \in \emptyset \rightarrow x \in A)$" bernilai benar secara vakum (vacuously true) karena tidak ada $x \in \emptyset$.

**Himpunan semesta** ($U$): Himpunan yang memuat semua elemen yang relevan dalam konteks diskusi tertentu. Jika kita membicarakan bilangan, $U$ mungkin $\mathbb{R}$. Jika kita membicarakan mahasiswa di kelas, $U$ adalah himpunan seluruh mahasiswa di kelas itu.

### 1.5 Subhimpunan (Subset)

Himpunan $A$ adalah **subhimpunan** dari $B$ (ditulis $A \subseteq B$) jika setiap elemen $A$ juga merupakan elemen $B$:

$$A \subseteq B \iff \forall x (x \in A \rightarrow x \in B)$$

Jika $A \subseteq B$ tetapi $A \neq B$ (artinya ada elemen di $B$ yang tidak ada di $A$), maka $A$ disebut **proper subset** dari $B$, ditulis $A \subset B$.

Contoh:
- $\{1, 3\} \subseteq \{1, 2, 3, 4\}$ ✓
- $\{1, 2, 3\} \subseteq \{1, 2, 3\}$ ✓ (setiap himpunan adalah subhimpunan dari dirinya sendiri)
- $\{1, 5\} \subseteq \{1, 2, 3, 4\}$ ✗ (karena 5 tidak ada di himpunan kedua)

### 1.6 Power Set (Himpunan Kuasa)

**Power set** dari himpunan $A$, ditulis $\mathcal{P}(A)$, adalah himpunan dari **semua subhimpunan** $A$, termasuk $\emptyset$ dan $A$ sendiri.

Contoh: Jika $A = \{1, 2\}$, maka:
$$\mathcal{P}(A) = \{\emptyset, \{1\}, \{2\}, \{1, 2\}\}$$

Jika $|A| = n$ (himpunan $A$ memiliki $n$ elemen), maka $|\mathcal{P}(A)| = 2^n$.

Mengapa $2^n$? Karena untuk setiap elemen, kamu punya 2 pilihan: memasukkannya ke dalam subhimpunan, atau tidak. Dengan $n$ elemen, ada $2 \times 2 \times \cdots \times 2 = 2^n$ kombinasi pilihan (Product Rule dari [[DM1 - 1 - Logika dan Pencacahan#6.2 The Product Rule (Aturan Perkalian)|pencacahan]]).

### 1.7 Kardinalitas (Cardinality)

**Kardinalitas** suatu himpunan $A$, ditulis $|A|$, adalah jumlah elemen berbeda dalam himpunan tersebut.

- $|\{a, b, c\}| = 3$
- $|\emptyset| = 0$
- $|\mathbb{N}|$ = $\aleph_0$ (aleph-null — kardinalitas tak berhingga terkecil)

Untuk himpunan berhingga, kardinalitas adalah bilangan bulat non-negatif. Untuk himpunan tak berhingga, matematikawan menggunakan konsep **bilangan kardinal transfinit** — tetapi ini berada di luar cakupan MK ini.

---

## 2. Operasi Himpunan (Set Operations)

Seperti halnya bilangan dapat dijumlahkan, dikurangi, dan dikalikan, himpunan memiliki operasi-operasinya sendiri. Operasi-operasi ini menjadi fondasi bagi operasi database, query, dan manipulasi data dalam informatika.

### 2.1 Gabungan (Union)

**Gabungan** dari dua himpunan $A$ dan $B$, ditulis $A \cup B$, adalah himpunan yang memuat semua elemen yang ada di $A$, **atau** di $B$, **atau** di keduanya.

$$A \cup B = \{x \mid x \in A \lor x \in B\}$$

Contoh: $\{1, 2, 3\} \cup \{3, 4, 5\} = \{1, 2, 3, 4, 5\}$

Dalam SQL, ini setara dengan operasi `UNION`.

### 2.2 Irisan (Intersection)

**Irisan** dari dua himpunan $A$ dan $B$, ditulis $A \cap B$, adalah himpunan yang memuat semua elemen yang ada di $A$ **dan** di $B$ secara bersamaan.

$$A \cap B = \{x \mid x \in A \land x \in B\}$$

Contoh: $\{1, 2, 3\} \cap \{3, 4, 5\} = \{3\}$

Dua himpunan yang tidak memiliki elemen bersama ($A \cap B = \emptyset$) disebut **disjoint** (saling lepas).

Dalam SQL, ini setara dengan operasi `INTERSECT`.

### 2.3 Selisih (Difference)

**Selisih** dari $A$ dan $B$, ditulis $A - B$ atau $A \setminus B$, adalah himpunan elemen yang ada di $A$ tetapi **tidak** ada di $B$.

$$A - B = \{x \mid x \in A \land x \notin B\}$$

Contoh: $\{1, 2, 3, 4\} - \{3, 4, 5, 6\} = \{1, 2\}$

Perhatikan bahwa $A - B \neq B - A$ secara umum. Operasi selisih **tidak komutatif**.

Dalam SQL, ini setara dengan operasi `EXCEPT`.

### 2.4 Komplemen (Complement)

**Komplemen** dari himpunan $A$, ditulis $\overline{A}$ atau $A^c$, adalah himpunan semua elemen di himpunan semesta $U$ yang **tidak** ada di $A$.

$$\overline{A} = U - A = \{x \in U \mid x \notin A\}$$

Contoh: Jika $U = \{1, 2, 3, 4, 5\}$ dan $A = \{1, 3, 5\}$, maka $\overline{A} = \{2, 4\}$.

### 2.5 Diagram Venn

**Diagram Venn** adalah representasi visual dari himpunan dan operasi himpunan. Dalam diagram Venn:

- **Himpunan semesta** direpresentasikan oleh sebuah persegi panjang
- **Setiap himpunan** direpresentasikan oleh sebuah lingkaran di dalam persegi panjang
- **Irisan** adalah area overlap antar lingkaran
- **Gabungan** adalah total area yang tercakup oleh lingkaran-lingkaran

Diagram Venn sangat berguna untuk memvisualisasikan dan memverifikasi hubungan antara himpunan, terutama ketika melibatkan inklusi-eksklusi ([[DM1 - 1 - Logika dan Pencacahan#6.1 The Sum Rule (Aturan Penjumlahan)|Sum Rule]] dan konsepnya akan diperluas di minggu ke-14).

### 2.6 Hukum-hukum Aljabar Himpunan

Operasi himpunan mengikuti hukum-hukum yang secara struktural **identik** dengan hukum logika proposisional. Ini bukan kebetulan — himpunan dan logika terhubung secara mendalam melalui fungsi karakteristik.

| Hukum | Ekuivalensi |
|---|---|
| Identitas | $A \cup \emptyset = A$ ; $A \cap U = A$ |
| Dominasi | $A \cup U = U$ ; $A \cap \emptyset = \emptyset$ |
| Idempoten | $A \cup A = A$ ; $A \cap A = A$ |
| Komplemen | $A \cup \overline{A} = U$ ; $A \cap \overline{A} = \emptyset$ |
| Komutatif | $A \cup B = B \cup A$ ; $A \cap B = B \cap A$ |
| Asosiatif | $(A \cup B) \cup C = A \cup (B \cup C)$ |
| Distributif | $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$ |
| **De Morgan** | $\overline{A \cup B} = \overline{A} \cap \overline{B}$ ; $\overline{A \cap B} = \overline{A} \cup \overline{B}$ |

Perbandingan langsung dengan logika:

| Logika | Himpunan |
|---|---|
| $\lor$ (OR) | $\cup$ (Union) |
| $\land$ (AND) | $\cap$ (Intersection) |
| $\lnot$ (NOT) | $\overline{\phantom{A}}$ (Complement) |
| $T$ (True) | $U$ (Universe) |
| $F$ (False) | $\emptyset$ (Empty set) |

Mengetahui korespondensi ini memungkinkan kamu untuk langsung "menerjemahkan" semua hukum logika ke dalam hukum himpunan, dan sebaliknya.

### 2.7 Cartesian Product (Perkalian Kartesian)

**Perkalian Kartesian** dari dua himpunan $A$ dan $B$, ditulis $A \times B$, adalah himpunan semua **pasangan terurut** $(a, b)$ di mana $a \in A$ dan $b \in B$.

$$A \times B = \{(a, b) \mid a \in A \land b \in B\}$$

Contoh: $\{1, 2\} \times \{a, b, c\} = \{(1,a), (1,b), (1,c), (2,a), (2,b), (2,c)\}$

Perhatikan: $|A \times B| = |A| \cdot |B|$ — ini adalah Product Rule dari [[DM1 - 1 - Logika dan Pencacahan#6.2 The Product Rule (Aturan Perkalian)|pencacahan]]!

Cartesian product sangat penting karena:
- **Relasi** (yang akan dipelajari di minggu 15) didefinisikan sebagai subhimpunan dari Cartesian product
- **Fungsi** adalah jenis relasi khusus
- Dalam database relasional, **operasi JOIN** secara konseptual didasarkan pada Cartesian product

Perhatikan bahwa Cartesian product **tidak komutatif**: $A \times B \neq B \times A$ secara umum (kecuali $A = B$ atau salah satunya kosong), karena urutan dalam pasangan terurut penting: $(1, a) \neq (a, 1)$.

---

## 3. Fungsi (Functions)

### 3.1 Definisi Fungsi

Sebuah **fungsi** $f$ dari himpunan $A$ ke himpunan $B$, ditulis $f: A \rightarrow B$, adalah sebuah aturan yang menetapkan **tepat satu** elemen di $B$ untuk **setiap** elemen di $A$.

Secara formal, fungsi adalah relasi khusus: $f \subseteq A \times B$ sedemikian sehingga untuk setiap $a \in A$, terdapat **tepat satu** $b \in B$ sehingga $(a, b) \in f$.

Kata kunci: **tepat satu**. Setiap input menghasilkan satu dan hanya satu output. Ini yang membedakan fungsi dari relasi umum — dalam relasi, satu elemen bisa dipetakan ke banyak elemen.

Analogi: Bayangkan sebuah mesin (vending machine). Kamu memasukkan satu koin (input dari domain). Mesin mengeluarkan satu minuman (output dari codomain). Mesin tidak boleh mengeluarkan dua minuman untuk satu koin, dan tidak boleh menolak koin yang valid tanpa mengeluarkan apapun.

### 3.2 Domain, Codomain, dan Range

Untuk fungsi $f: A \rightarrow B$:

- **Domain** = $A$, yaitu himpunan semua input yang valid
- **Codomain** = $B$, yaitu himpunan semua output yang _mungkin_
- **Range** (atau _image_) = $\{f(a) \mid a \in A\}$, yaitu himpunan output yang _benar-benar dihasilkan_

Range selalu merupakan subhimpunan dari codomain: $\text{Range}(f) \subseteq B$, tetapi belum tentu sama.

Contoh: $f: \mathbb{R} \rightarrow \mathbb{R}$ dengan $f(x) = x^2$.
- Domain = $\mathbb{R}$
- Codomain = $\mathbb{R}$
- Range = $\{y \in \mathbb{R} \mid y \geq 0\} = [0, \infty)$ — hanya bilangan non-negatif yang benar-benar dihasilkan, meskipun codomain-nya mencakup semua bilangan real.

### 3.3 Jenis-jenis Fungsi

Fungsi diklasifikasikan berdasarkan bagaimana mereka memetakan domain ke codomain:

**Injektif (One-to-One / Injective):**

Fungsi $f$ disebut **injektif** jika elemen-elemen domain yang berbeda selalu dipetakan ke elemen codomain yang berbeda.

$$\forall a_1, a_2 \in A, \, f(a_1) = f(a_2) \rightarrow a_1 = a_2$$

Versi kontrapositif (sering lebih mudah digunakan dalam pembuktian): $a_1 \neq a_2 \rightarrow f(a_1) \neq f(a_2)$.

Contoh: $f(x) = 2x$ adalah injektif. Contoh bukan injektif: $f(x) = x^2$ (karena $f(2) = f(-2) = 4$).

**Surjektif (Onto / Surjective):**

Fungsi $f$ disebut **surjektif** jika setiap elemen di codomain $B$ memiliki setidaknya satu preimage di domain $A$.

$$\forall b \in B, \, \exists a \in A, \, f(a) = b$$

Artinya: Range $= $ Codomain. Tidak ada elemen codomain yang "terlewat."

Contoh: $f: \mathbb{R} \rightarrow \mathbb{R}^+$ dengan $f(x) = e^x$ adalah surjektif (setiap bilangan positif bisa dihasilkan). Contoh bukan surjektif: $f: \mathbb{R} \rightarrow \mathbb{R}$ dengan $f(x) = x^2$ (bilangan negatif tidak pernah dihasilkan sebagai output).

**Bijektif (Bijective):**

Fungsi yang **injektif DAN surjektif sekaligus** disebut **bijektif** (one-to-one correspondence). Setiap elemen domain dipetakan ke tepat satu elemen codomain yang unik, dan setiap elemen codomain memiliki tepat satu preimage.

Contoh: $f: \mathbb{R} \rightarrow \mathbb{R}$ dengan $f(x) = 2x + 1$ adalah bijektif.

Mengapa bijeksi penting? Karena:
1. Fungsi bijektif memiliki **fungsi invers** yang terdefinisi dengan baik
2. Bijeksi membuktikan bahwa dua himpunan memiliki **kardinalitas yang sama**
3. Dalam kriptografi, fungsi enkripsi harus bijektif agar bisa didekripsi

### 3.4 Komposisi Fungsi

Jika $f: A \rightarrow B$ dan $g: B \rightarrow C$, maka **komposisi** $g \circ f: A \rightarrow C$ didefinisikan sebagai:

$$(g \circ f)(x) = g(f(x))$$

Bacaan: "g setelah f" atau "g komposisi f." Yang dieksekusi duluan adalah $f$ (yang paling kanan/dalam).

Contoh: $f(x) = x + 1$, $g(x) = 2x$.
- $(g \circ f)(3) = g(f(3)) = g(4) = 8$
- $(f \circ g)(3) = f(g(3)) = f(6) = 7$

Perhatikan: $g \circ f \neq f \circ g$ secara umum — komposisi fungsi **tidak komutatif**.

### 3.5 Fungsi Invers

Jika $f: A \rightarrow B$ adalah **bijektif**, maka terdapat fungsi invers $f^{-1}: B \rightarrow A$ sedemikian sehingga:

$$f^{-1}(b) = a \iff f(a) = b$$

Sifat:
- $(f^{-1} \circ f)(x) = x$ untuk semua $x \in A$
- $(f \circ f^{-1})(y) = y$ untuk semua $y \in B$

Fungsi invers **hanya ada jika fungsi aslinya bijektif**. Jika fungsi tidak injektif, kamu tidak tahu input mana yang menghasilkan output tertentu. Jika fungsi tidak surjektif, ada elemen codomain yang tidak memiliki preimage — fungsi invers tidak terdefinisi di titik-titik tersebut.

Contoh: $f(x) = 3x + 2$ → $f^{-1}(y) = \frac{y - 2}{3}$

---

## 4. Deret Penjumlahan (Summation Series)

### 4.1 Notasi Sigma

**Notasi sigma** ($\sum$) adalah cara ringkas untuk menuliskan jumlah dari banyak suku yang mengikuti pola tertentu.

$$\sum_{i=m}^{n} a_i = a_m + a_{m+1} + a_{m+2} + \cdots + a_n$$

Komponen:
- $i$ = **variabel indeks** (index of summation)
- $m$ = **batas bawah** (lower bound)
- $n$ = **batas atas** (upper bound)
- $a_i$ = **suku umum** (general term)

Contoh:

$$\sum_{i=1}^{5} i^2 = 1^2 + 2^2 + 3^2 + 4^2 + 5^2 = 1 + 4 + 9 + 16 + 25 = 55$$

Notasi sigma sangat penting dalam analisis algoritma — ketika menghitung berapa banyak operasi yang dilakukan oleh sebuah loop, kamu sering menuliskannya sebagai penjumlahan sigma.

### 4.2 Deret-deret Penting

Beberapa rumus deret tertutup (closed-form) yang wajib diketahui:

**Deret Aritmatika:**
$$\sum_{i=1}^{n} i = \frac{n(n+1)}{2}$$

Ini adalah rumus jumlah bilangan asli pertama — sering muncul dalam analisis loop bersarang.

**Deret Kuadrat:**
$$\sum_{i=1}^{n} i^2 = \frac{n(n+1)(2n+1)}{6}$$

**Deret Geometri:**
$$\sum_{i=0}^{n} ar^i = a \cdot \frac{r^{n+1} - 1}{r - 1}, \quad r \neq 1$$

Deret geometri sangat penting dan akan menjadi fondasi untuk pembahasan **generating functions** di paruh kedua semester.

**Deret Geometri Tak Hingga** (untuk $|r| < 1$):
$$\sum_{i=0}^{\infty} ar^i = \frac{a}{1 - r}$$

**Sifat-sifat Penjumlahan:**

$$\sum_{i=m}^{n} (a_i + b_i) = \sum_{i=m}^{n} a_i + \sum_{i=m}^{n} b_i$$

$$\sum_{i=m}^{n} c \cdot a_i = c \cdot \sum_{i=m}^{n} a_i$$

Sifat-sifat ini analog dengan sifat integral dalam kalkulus — dan memang, penjumlahan sigma adalah "versi diskrit" dari integral.

---

## Summary — Key Concepts at a Glance

| Concept                   | Definition                                                                        |
| ------------------------- | --------------------------------------------------------------------------------- |
| Himpunan (Set)            | Kumpulan objek yang terdefinisi baik, tidak terurut, tanpa duplikasi              |
| Elemen / Anggota          | Objek individual di dalam sebuah himpunan                                         |
| Roster Method             | Mendaftar semua elemen secara eksplisit: $\{1, 2, 3\}$                           |
| Set-Builder Notation      | Mendefinisikan himpunan berdasarkan sifat: $\{x \mid P(x)\}$                     |
| Himpunan Kosong ($\emptyset$) | Himpunan tanpa elemen; subhimpunan dari setiap himpunan                       |
| Subhimpunan ($\subseteq$) | $A \subseteq B$ jika setiap elemen $A$ juga ada di $B$                           |
| Power Set ($\mathcal{P}$) | Himpunan dari semua subhimpunan; $|\mathcal{P}(A)| = 2^{|A|}$                    |
| Union ($\cup$)            | Gabungan: elemen yang ada di $A$ atau $B$                                         |
| Intersection ($\cap$)     | Irisan: elemen yang ada di $A$ dan $B$                                            |
| Difference ($-$)          | Selisih: elemen di $A$ tapi tidak di $B$                                          |
| Complement ($\overline{A}$)| Semua elemen di $U$ yang tidak ada di $A$                                        |
| Cartesian Product         | $A \times B$: semua pasangan terurut $(a,b)$                                      |
| Fungsi                    | Pemetaan yang memberikan tepat satu output untuk setiap input                     |
| Domain                    | Himpunan semua input yang valid                                                   |
| Codomain vs Range         | Codomain: output yang mungkin; Range: output yang benar-benar dihasilkan          |
| Injektif (One-to-One)     | Input berbeda → output berbeda                                                    |
| Surjektif (Onto)          | Setiap elemen codomain memiliki preimage                                          |
| Bijektif                  | Injektif dan surjektif; memiliki invers                                           |
| Komposisi ($g \circ f$)   | Menerapkan $f$ dulu, lalu $g$; tidak komutatif                                    |
| Notasi Sigma ($\sum$)     | Notasi ringkas untuk penjumlahan berurutan                                        |
| Deret Geometri            | $\sum ar^i$; fondasi generating functions                                         |

---

## Questions

1. Dalam konteks informatika, di mana tepatnya konsep **Power Set** digunakan? Apakah terkait dengan search space di algoritma?
2. Bagaimana membuktikan bahwa suatu fungsi bijektif secara formal — apakah lebih efisien membuktikan injektif dan surjektif secara terpisah, atau langsung mengkonstruksi inversnya?
3. Apa hubungan antara **Cartesian Product** di sini dengan operasi **JOIN** di SQL? Apakah SQL JOIN selalu menghasilkan Cartesian Product lengkap, atau hanya subset-nya?
4. Untuk deret geometri tak hingga, bagaimana jika $|r| \geq 1$? → Deret divergen, ini akan dibahas lebih lanjut di topik Deret Diskrit (minggu ke-9).
