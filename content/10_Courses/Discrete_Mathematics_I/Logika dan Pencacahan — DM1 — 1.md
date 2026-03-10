---
title:
  - Logika dan Pencacahan
type: Lecture
course:
  - Discrete Mathematics I
topic:
  - Mathematical Logic
  - Counting Basics
semester: 4
tags:
  - discrete-mathematics
  - logic
  - counting
  - college
  - lecture-note
created: 2026-03-06
---

# Logika dan Pencacahan

 **Reference:** Rosen, K.H. *Discrete Mathematics and Its Applications*; Munir, R. *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
 **Source:** [[RPS-MD1]]

---

## Daftar Isi

1. [[#1. Apa itu Matematika Diskrit?]]
2. [[#2. Proposisi dan Logika Proposisional]]
    - [[#2.1 Definisi Proposisi]]
    - [[#2.2 Operator Logika (Logical Connectives)]]
    - [[#2.3 Tabel Kebenaran (Truth Tables)]]
    - [[#2.4 Ekuivalensi Logis (Logical Equivalences)]]
3. [[#3. Logika Predikat (Predicate Logic)]]
    - [[#3.1 Dari Proposisi ke Predikat]]
    - [[#3.2 Quantifiers — Kuantor Universal dan Eksistensial]]
4. [[#4. Rules of Inference — Aturan Penarikan Kesimpulan]]
    - [[#4.1 Mengapa Rules of Inference Penting?]]
    - [[#4.2 Aturan-aturan Dasar Inferensi]]
    - [[#4.3 Fallacy — Kesalahan Penalaran]]
5. [[#5. Paradoks dalam Logika]]
    - [[#5.1 Paradoks Klasik]]
    - [[#5.2 Mengapa Paradoks Penting dalam Matematika Diskrit?]]
6. [[#6. Pengantar Pencacahan (Introduction to Counting)]]
    - [[#6.1 The Sum Rule (Aturan Penjumlahan)]]
    - [[#6.2 The Product Rule (Aturan Perkalian)]]
    - [[#6.3 Menggabungkan Sum Rule dan Product Rule]]
7. [[#Summary — Key Concepts at a Glance]]

---

## 1. Apa itu Matematika Diskrit?

Matematika diskrit adalah cabang matematika yang mempelajari objek-objek **diskrit** — yaitu objek yang bisa dihitung satu per satu, berbeda dari objek **kontinu** yang mengalir tanpa batas di antara dua nilai.

Analogi paling sederhana: bayangkan tangga versus ramp. Jika kamu menaiki tangga, kamu berada di anak tangga ke-1, ke-2, ke-3 — tidak ada "anak tangga ke-1,5". Itulah diskrit. Jika kamu berjalan naik di sebuah ramp, kamu bisa berada di ketinggian _mana pun_ — 1,0 meter, 1,0001 meter, 1,00015 meter. Itulah kontinu.

Dalam ilmu komputer, hampir semua yang kita kerjakan bersifat diskrit. Komputer bekerja dengan **bit** — 0 dan 1 — bukan bilangan yang mengalir kontinu. Algoritma bekerja dalam **langkah-langkah** yang bisa dihitung. Data disimpan dalam **byte** yang berhingga. Oleh karena itu, matematika diskrit menjadi fondasi paling penting bagi informatika.

Mata kuliah Matematika Diskrit I membahas logika, [[himpunan]], pembuktian, induksi, prinsip pencacahan, [[fungsi]], relasi, dan relasi rekursi — semua ini adalah alat-alat dasar yang akan digunakan di hampir setiap mata kuliah informatika lanjutan.

---

## 2. Proposisi dan Logika Proposisional

### 2.1 Definisi Proposisi

Sebuah **[[proposisi]]** (proposition) adalah pernyataan deklaratif yang bernilai **benar (True)** atau **salah (False)** — tidak pernah keduanya, dan tidak pernah "tidak tentu". Ini disebut **prinsip bivalen** (principle of bivalence).

Contoh proposisi:
- "2 + 3 = 5" → **True**
- "Jakarta adalah ibu kota Thailand" → **False**
- "Setiap bilangan genap lebih besar dari 2 adalah jumlah dua bilangan prima" (Konjektur Goldbach) → Belum dibuktikan benar atau salah secara final, tapi tetaplah proposisi karena secara prinsip harus bernilai benar atau salah.

Contoh yang **bukan** proposisi:
- "Tutup pintu!" → Ini perintah, bukan pernyataan.
- "Berapa umurmu?" → Ini pertanyaan.
- "x + 1 = 2" → Ini bukan proposisi _sampai_ kita tahu nilai x. Ini disebut **fungsi proposisional** (propositional function), yang akan dibahas di bagian [[logika predikat]].

Proposisi biasanya dilambangkan dengan huruf kecil: $p$, $q$, $r$, dsb.

### 2.2 Operator Logika (Logical Connectives)

Proposisi-proposisi sederhana dapat digabungkan menggunakan [[Operator Logika|operator logika]] untuk membentuk proposisi yang lebih kompleks. Inilah bahasa formal dari penalaran — dan menjadi fondasi desain rangkaian digital, basis data, hingga kecerdasan buatan.

| Operator | Nama | Simbol | Dibaca |
|---|---|---|---|
| Negasi | NOT | $\lnot p$ | "bukan p" / "not p" |
| Konjungsi | AND | $p \land q$ | "p dan q" |
| Disjungsi | OR | $p \lor q$ | "p atau q" (inklusif) |
| Disjungsi Eksklusif | XOR | $p \oplus q$ | "p atau q, tapi tidak keduanya" |
| Implikasi | IF...THEN | $p \rightarrow q$ | "jika p maka q" |
| Biimplikasi | IF AND ONLY IF | $p \leftrightarrow q$ | "p jika dan hanya jika q" |

**Implikasi** ($p \rightarrow q$) layak mendapat perhatian khusus karena sering membingungkan. Dalam implikasi, $p$ disebut **hipotesis** (antecedent) dan $q$ disebut **kesimpulan** (consequent). Hal yang paling kontra-intuitif: **jika $p$ salah, maka $p \rightarrow q$ selalu bernilai benar**, apapun nilai $q$. Ini disebut **vacuous truth** — sebuah janji yang tidak dilanggar karena kondisinya tidak pernah terpenuhi.

Analogi: "Jika hujan, saya bawa payung." Jika hari ini tidak hujan, kamu tidak bisa menilai saya melanggar janji — janji itu otomatis "terpenuhi" karena kondisinya tidak terjadi.

### 2.3 Tabel Kebenaran (Truth Tables)

Tabel kebenaran (truth table) adalah alat untuk secara sistematis mengevaluasi semua kemungkinan kombinasi nilai kebenaran dari proposisi-proposisi yang terlibat. Untuk $n$ variabel proposisi, tabel kebenaran memiliki $2^n$ baris.

**Contoh:** Tabel kebenaran untuk implikasi $p \rightarrow q$:

| $p$ | $q$ | $p \rightarrow q$ |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | T |

Perhatikan baris ketiga dan keempat — ketika $p$ bernilai False, implikasi selalu bernilai True. Inilah vacuous truth yang sudah dibahas.

Tabel kebenaran menjadi semakin besar seiring bertambahnya variabel. Untuk 3 variabel memiliki 8 baris, 4 variabel memiliki 16 baris, dan seterusnya. Di sinilah kita mulai merasakan pertumbuhan **eksponensial** — tema yang akan muncul berulang kali dalam informatika.

### 2.4 Ekuivalensi Logis (Logical Equivalences)

Dua proposisi majemuk disebut **logically equivalent** (ekuivalen secara logis) jika mereka memiliki nilai kebenaran yang sama untuk _setiap_ kombinasi nilai kebenaran variabel-variabel penyusunnya. Ditulis: $p \equiv q$.

Beberapa ekuivalensi logis yang paling penting dan sering digunakan:

**[[Hukum De Morgan]]:**
$$\lnot(p \land q) \equiv (\lnot p) \lor (\lnot q)$$
$$\lnot(p \lor q) \equiv (\lnot p) \land (\lnot q)$$

Analogi De Morgan: "Bukan benar bahwa kamu pintar **dan** rajin" sama artinya dengan "Kamu tidak pintar **atau** kamu tidak rajin." Negasi mengubah AND menjadi OR, dan sebaliknya.

**Hukum-hukum lain yang penting:**

| Nama Hukum | Ekuivalensi |
|---|---|
| Hukum Identitas | $p \land T \equiv p$ ; $p \lor F \equiv p$ |
| Hukum Dominasi | $p \lor T \equiv T$ ; $p \land F \equiv F$ |
| Hukum Idempoten | $p \land p \equiv p$ ; $p \lor p \equiv p$ |
| Hukum Negasi Ganda | $\lnot(\lnot p) \equiv p$ |
| Hukum Komutatif | $p \land q \equiv q \land p$ ; $p \lor q \equiv q \lor p$ |
| Hukum Asosiatif | $(p \land q) \land r \equiv p \land (q \land r)$ |
| Hukum Distributif | $p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$ |
| Hukum Kontrapositif | $p \rightarrow q \equiv \lnot q \rightarrow \lnot p$ |

**Kontrapositif** sangat berguna dalam pembuktian. Daripada membuktikan "jika p maka q" secara langsung, kadang lebih mudah membuktikan "jika bukan q maka bukan p" — dan keduanya ekuivalen.

---

## 3. Logika Predikat (Predicate Logic)

### 3.1 Dari Proposisi ke Predikat

Logika proposisional memiliki keterbatasan: ia tidak bisa mengekspresikan pernyataan tentang **variabel**. Pernyataan "x > 3" bukan proposisi karena kebenarannya tergantung pada nilai $x$. Di sinilah **logika predikat** mengambil alih.

Sebuah **predikat** adalah pernyataan yang mengandung satu atau lebih variabel. Notasi: $P(x)$ berarti "pernyataan $P$ tentang $x$." Predikat menjadi proposisi ketika variabelnya diberikan nilai tertentu, atau ketika variabelnya diikat oleh sebuah **kuantor** (quantifier).

Contoh:
- $P(x)$: "$x$ adalah bilangan prima"
- $P(7)$: "7 adalah bilangan prima" → **True** (sekarang ini proposisi)
- $P(4)$: "4 adalah bilangan prima" → **False** (ini juga proposisi)

### 3.2 Quantifiers — Kuantor Universal dan Eksistensial

**Kuantor** mengikat variabel dalam predikat sehingga menghasilkan proposisi.

**Kuantor Universal** ($\forall$): "Untuk semua" / "Untuk setiap"
$$\forall x \, P(x)$$
Artinya: "$P(x)$ benar untuk **setiap** nilai $x$ dalam domain."

Contoh: $\forall x \in \mathbb{Z}^+, \, x + 1 > x$ — "Untuk setiap bilangan bulat positif $x$, $x+1$ lebih besar dari $x$." → **True**

Untuk membantah pernyataan universal, cukup temukan **satu counterexample** (contoh penyangkal).

**Kuantor Eksistensial** ($\exists$): "Ada" / "Terdapat setidaknya satu"
$$\exists x \, P(x)$$
Artinya: "Terdapat setidaknya satu nilai $x$ dalam domain sehingga $P(x)$ benar."

Contoh: $\exists x \in \mathbb{R}, \, x^2 = 2$ — "Terdapat bilangan real $x$ sehingga $x^2 = 2$." → **True** ($x = \sqrt{2}$)

**Negasi Kuantor** (sangat penting untuk pembuktian):
$$\lnot(\forall x \, P(x)) \equiv \exists x \, \lnot P(x)$$
$$\lnot(\exists x \, P(x)) \equiv \forall x \, \lnot P(x)$$

Analogi: "Tidak benar bahwa **semua** mahasiswa lulus ujian" sama artinya dengan "**Ada** setidaknya satu mahasiswa yang tidak lulus ujian."

---

## 4. Rules of Inference — Aturan Penarikan Kesimpulan

### 4.1 Mengapa Rules of Inference Penting?

Setiap pembuktian matematika, setiap argumen logis, setiap deduksi — semuanya dibangun dari langkah-langkah kecil yang masing-masing mengikuti suatu **aturan inferensi** (rule of inference). [[Rules of inference]] adalah _alat_ yang memungkinkan kita berpindah dari premis-premis yang diketahui ke kesimpulan yang valid secara logis.

Jika logika proposisional adalah _bahasanya_, maka *rules of inference* adalah _tata bahasa_-nya — aturan yang menentukan mana kalimat yang valid dan mana yang tidak.

### 4.2 Aturan-aturan Dasar Inferensi

| Aturan | Bentuk Formal | Penjelasan |
|---|---|---|
| **Modus Ponens** | $p, \, p \rightarrow q \, \therefore q$ | Jika $p$ benar dan $p$ mengimplikasikan $q$, maka $q$ benar. |
| **Modus Tollens** | $\lnot q, \, p \rightarrow q \, \therefore \lnot p$ | Jika $q$ salah dan $p$ mengimplikasikan $q$, maka $p$ salah. |
| **Hypothetical Syllogism** | $p \rightarrow q, \, q \rightarrow r \, \therefore p \rightarrow r$ | Rantai implikasi: jika $p$ menyebabkan $q$ dan $q$ menyebabkan $r$, maka $p$ menyebabkan $r$. |
| **Disjunctive Syllogism** | $p \lor q, \, \lnot p \, \therefore q$ | Jika salah satu dari $p$ atau $q$ benar, dan $p$ salah, maka $q$ pasti benar. |
| **Addition** | $p \, \therefore p \lor q$ | Dari sesuatu yang benar, kita boleh menambahkan apapun dengan OR. |
| **Simplification** | $p \land q \, \therefore p$ | Dari konjungsi, kita bisa mengambil salah satu bagiannya. |
| **Conjunction** | $p, \, q \, \therefore p \land q$ | Jika dua hal masing-masing benar, maka konjungsinya benar. |
| **Resolution** | $p \lor q, \, \lnot p \lor r \, \therefore q \lor r$ | Aturan ini sangat penting dalam pembuktian otomatis dan AI. |

**Modus Ponens** dan **Modus Tollens** adalah dua aturan yang paling sering digunakan. Modus Ponens bekerja "maju" — dari hipotesis ke kesimpulan. Modus Tollens bekerja "mundur" — dari negasi kesimpulan ke negasi hipotesis (ini terkait erat dengan kontrapositif).

Contoh Modus Ponens dalam kehidupan sehari-hari:
- Premis 1: "Jika hujan, jalanan basah." ($p \rightarrow q$)
- Premis 2: "Hujan." ($p$)
- Kesimpulan: "Jalanan basah." ($q$) ✓

### 4.3 Fallacy — Kesalahan Penalaran

Sebuah **fallacy** (kekeliruan logis) terjadi ketika argumen _tampak_ valid tetapi sebenarnya melanggar aturan inferensi. Dua fallacy paling umum:

**Affirming the Consequent** (Mengafirmasi Konsekuen):
- $p \rightarrow q, \, q \, \therefore p$ ← **INVALID!**
- Contoh: "Jika hujan, jalanan basah. Jalanan basah. Maka pasti hujan." — Salah! Jalanan bisa basah karena penyiraman.

**Denying the Antecedent** (Menyangkal Anteseden):
- $p \rightarrow q, \, \lnot p \, \therefore \lnot q$ ← **INVALID!**
- Contoh: "Jika hujan, jalanan basah. Tidak hujan. Maka jalanan tidak basah." — Salah! Jalanan bisa basah karena alasan lain.

Mengenali fallacy adalah keterampilan yang sangat penting — tidak hanya dalam matematika, tetapi juga dalam pemrograman (debugging logical errors), keamanan sistem, dan kehidupan sehari-hari.

---

## 5. Paradoks dalam Logika

### 5.1 Paradoks Klasik

Paradoks adalah pernyataan yang tampaknya menghasilkan kontradiksi — pernyataan yang tidak bisa bernilai benar maupun salah tanpa menimbulkan masalah. Paradoks penting dalam sejarah logika karena mendorong para matematikawan untuk memperjelas fondasi penalaran.

**Paradoks Tukang Cukur (Barber Paradox):**
"Di sebuah desa, ada seorang tukang cukur yang mencukur semua orang yang _tidak_ mencukur dirinya sendiri, dan hanya orang-orang itu. Siapa yang mencukur tukang cukur?"

- Jika tukang cukur mencukur dirinya sendiri → maka dia termasuk orang yang mencukur dirinya sendiri → maka seharusnya dia _tidak_ dicukur oleh tukang cukur (yaitu dirinya sendiri). Kontradiksi.
- Jika tukang cukur _tidak_ mencukur dirinya sendiri → maka dia termasuk orang yang tidak mencukur dirinya sendiri → maka seharusnya dia _dicukur_ oleh tukang cukur. Kontradiksi lagi.

**Paradoks Pembohong (Liar Paradox):**
"Kalimat ini salah."

- Jika kalimat itu benar → maka isinya benar bahwa kalimat itu salah → kontradiksi.
- Jika kalimat itu salah → maka isinya salah, artinya kalimat itu benar → kontradiksi.

**Paradoks Russell:**
Perhatikan himpunan $S = \{x \mid x \notin x\}$ — himpunan dari semua himpunan yang tidak mengandung dirinya sendiri. Apakah $S \in S$?

- Jika $S \in S$, maka berdasarkan definisi, $S \notin S$. Kontradiksi.
- Jika $S \notin S$, maka berdasarkan definisi, $S \in S$. Kontradiksi.

Paradoks Russell memiliki dampak besar pada fondasi matematika — ia menunjukkan bahwa definisi himpunan yang terlalu longgar bisa menghasilkan kontradiksi. Hal ini mendorong lahirnya teori himpunan aksiomatik (seperti Zermelo-Fraenkel).

### 5.2 Mengapa Paradoks Penting dalam Matematika Diskrit?

Paradoks bukan sekadar teka-teki menarik. Mereka mengilustrasikan batas-batas dari sistem logika dan mengajarkan kita untuk berhati-hati dalam mendefinisikan konsep secara formal. Dalam konteks informatika, paradoks-paradoks ini terkait erat dengan:

- **Halting Problem** — tidak ada program yang bisa menentukan apakah program lain akan berhenti atau berjalan selamanya (Alan Turing membuktikan ini dengan argumen yang mirip dengan paradoks).
- **Self-reference** dalam pemrograman — rekursi tanpa base case yang benar mirip dengan paradoks pembohong.
- **Design constraint** — ketika merancang database atau sistem tipe, kita harus menghindari definisi self-referential yang bisa menyebabkan inkonsistensi.

---

## 6. Pengantar Pencacahan (Introduction to Counting)

Pencacahan (counting) adalah salah satu kemampuan paling fundamental dalam matematika diskrit. Pertanyaan dasarnya sederhana: **"Ada berapa cara?"** — berapa cara memilih, menyusun, atau mengkombinasikan objek-objek dalam kondisi tertentu.

Pada tingkat dasar, pencacahan dibangun dari dua prinsip fundamental.

### 6.1 The Sum Rule (Aturan Penjumlahan)

**Aturan Penjumlahan** digunakan ketika ada beberapa **pilihan yang saling eksklusif** — kamu harus memilih salah satu dari beberapa opsi, dan memilih satu opsi berarti kamu _tidak_ memilih opsi lainnya.

Secara formal: Jika tugas bisa dilakukan dengan cara pertama sebanyak $n_1$ cara **ATAU** cara kedua sebanyak $n_2$ cara, dan kedua cara ini saling eksklusif (tidak bisa dilakukan bersamaan), maka total cara untuk melakukan tugas tersebut adalah:

$$n_1 + n_2$$

Contoh: Kamu ingin memilih satu mata kuliah pilihan. Dari departemen A ada 5 pilihan, dari departemen B ada 3 pilihan. Kamu hanya boleh memilih satu. Maka total pilihan = $5 + 3 = 8$.

Generalisasi: Jika ada $k$ cara yang saling eksklusif dengan masing-masing $n_1, n_2, \ldots, n_k$ pilihan, total cara = $n_1 + n_2 + \cdots + n_k$.

### 6.2 The Product Rule (Aturan Perkalian)

**Aturan Perkalian** digunakan ketika ada beberapa **langkah berurutan** yang harus _semua_ dilakukan — kamu harus membuat pilihan di langkah pertama **DAN** langkah kedua **DAN** langkah ketiga, dan seterusnya.

Secara formal: Jika prosedur terdiri dari langkah pertama dengan $n_1$ cara **DAN** langkah kedua dengan $n_2$ cara, maka total cara melakukan seluruh prosedur adalah:

$$n_1 \times n_2$$

Contoh: Kamu membuat password yang terdiri dari 1 huruf kapital diikuti 1 angka. Ada 26 huruf kapital dan 10 angka. Total password yang mungkin = $26 \times 10 = 260$.

Generalisasi: Jika prosedur terdiri dari $k$ langkah berurutan dengan masing-masing $n_1, n_2, \ldots, n_k$ pilihan, total cara = $n_1 \times n_2 \times \cdots \times n_k$.

### 6.3 Menggabungkan Sum Rule dan Product Rule

Dalam soal nyata, kamu perlu menggabungkan kedua aturan ini. Kunci untuk menentukan aturan mana yang digunakan:

- Lihat kata kunci **"ATAU"** → Sum Rule
- Lihat kata kunci **"DAN"** → Product Rule

Contoh gabungan: "Berapa banyak string biner (string yang hanya terdiri dari 0 dan 1) dengan panjang **tepat 3** ATAU **tepat 4**?"
- String panjang 3: setiap posisi punya 2 pilihan → $2 \times 2 \times 2 = 8$ (Product Rule)
- String panjang 4: $2 \times 2 \times 2 \times 2 = 16$ (Product Rule)
- Total: $8 + 16 = 24$ (Sum Rule, karena panjang 3 dan panjang 4 saling eksklusif)

---

## Summary — Key Concepts at a Glance

| Concept                        | Definition                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------------- |
| Matematika Diskrit             | Cabang matematika yang mempelajari objek-objek yang bisa dihitung (diskrit, bukan kontinu)    |
| Proposisi                      | Pernyataan deklaratif yang bernilai benar atau salah                                          |
| Operator Logika                | Simbol penghubung proposisi: $\lnot$, $\land$, $\lor$, $\rightarrow$, $\leftrightarrow$      |
| Tabel Kebenaran                | Tabel yang mengevaluasi semua kemungkinan nilai kebenaran dari ekspresi logis                  |
| Ekuivalensi Logis              | Dua ekspresi dengan nilai kebenaran yang identik di semua kasus                               |
| Hukum De Morgan                | $\lnot(p \land q) \equiv \lnot p \lor \lnot q$ dan sebaliknya                                |
| Predikat                       | Pernyataan dengan variabel; menjadi proposisi setelah variabel diikat                         |
| Kuantor Universal ($\forall$)  | "Untuk semua" — pernyataan berlaku bagi setiap elemen dalam domain                           |
| Kuantor Eksistensial ($\exists$)| "Terdapat" — pernyataan berlaku bagi setidaknya satu elemen                                  |
| Rules of Inference             | Aturan formal untuk menarik kesimpulan valid dari premis                                      |
| Modus Ponens                   | $p, \, p \rightarrow q \, \therefore q$                                                      |
| Modus Tollens                  | $\lnot q, \, p \rightarrow q \, \therefore \lnot p$                                          |
| Fallacy                        | Argumen yang tampak valid namun melanggar aturan inferensi                                     |
| Paradoks                       | Pernyataan yang menghasilkan kontradiksi logis                                                |
| Sum Rule                       | Total cara = jumlah cara dari pilihan-pilihan yang saling eksklusif                           |
| Product Rule                   | Total cara = hasil kali cara dari langkah-langkah berurutan                                   |

---

## Questions

1. Bagaimana De Morgan's Laws diterapkan dalam simplifikasi query di database (SQL)?
2. Apakah ada batasan jumlah variabel di mana tabel kebenaran masih bisa dipahami secara efektif, sebelum kita perlu beralih ke metode lain (misalnya Karnaugh Map)?
3. Bagaimana **Resolution** rule digunakan dalam automated theorem proving?
4. Dalam konteks pencacahan, bagaimana jika pilihannya **tidak** saling eksklusif (overlap)? → Ini akan terkait dengan Prinsip Inklusi-Eksklusi di minggu ke-14.
