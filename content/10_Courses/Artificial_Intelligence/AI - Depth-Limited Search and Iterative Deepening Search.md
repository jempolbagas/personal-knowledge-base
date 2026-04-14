---
aliases: [DLS, IDS, Depth-Limited Search, Iterative Deepening Search]
tags: [artificial-intelligence, uninformed-search, algorithms, computer-science]
date: 2026-04-13
---

# AI - Depth-Limited Search (DLS) dan Iterative Deepening Search (IDS)

> [!abstract] Overview
> Dokumen ini adalah panduan komprehensif mengenai **Depth-Limited Search (DLS)** dan **Iterative Deepening Search (IDS)**. Kita akan membedah algoritma ini dari prinsip dasarnya (*First-Principles*), memahami mengapa mereka diciptakan untuk menutupi kelemahan algoritma pencarian sebelumnya, menganalisis kompleksitas komputasinya, dan menyimulasikan cara kerjanya secara *step-by-step*. 

---

## 1. Fondasi: Mengapa Kita Butuh DLS dan IDS? (Pendekatan *First-Principles*)

Sebelum kita masuk ke DLS dan IDS, mari kita kembali ke akar permasalahan dalam pencarian ruang keadaan (*state-space search*). Dalam **Uninformed Search** (pencarian buta), kita memiliki dua jagoan utama: **Breadth-First Search (BFS)** dan **Depth-First Search (DFS)**.

- **BFS (Pencarian Melebar):** Sangat andal karena pasti menemukan solusi (*complete*) dan jika biaya setiap langkah sama, ia pasti menemukan solusi terpendek (*optimal*). Namun, kelemahan fatal BFS adalah **memori**. BFS harus menyimpan semua simpul (*node*) pada kedalaman saat ini sebelum pindah ke kedalaman berikutnya. Kompleksitas ruangnya adalah $O(b^d)$, di mana $b$ adalah *branching factor* (cabang maksimal per node) dan $d$ adalah kedalaman solusi. Pada graf yang besar, BFS akan kehabisan RAM sebelum menemukan solusi.
- **DFS (Pencarian Mendalam):** Mengatasi masalah memori BFS. DFS hanya perlu menyimpan jalur dari *root* ke *node* saat ini. Kompleksitas ruangnya sangat kecil, yaitu $O(bm)$, di mana $m$ adalah kedalaman maksimal graf. Namun, DFS memiliki kelemahan fatal: ia bisa terjebak di jalur dengan kedalaman tak terhingga (*infinite loop*) dan melewatkan solusi yang ada di cabang lain. Oleh karena itu, DFS **tidak *complete*** dan **tidak *optimal***.

> [!question] Pertanyaan Kritis
> Bagaimana cara kita mendapatkan **efisiensi memori seperti DFS**, tetapi tetap mempertahankan **kepastian menemukan solusi (completeness) seperti BFS** dan menghindari terjebak di kedalaman tak terhingga?

Jawaban dari pertanyaan inilah yang melahirkan **DLS** dan **IDS**.

---

## 2. Depth-Limited Search (DLS)

### 2.1 Konsep Dasar
**Depth-Limited Search (DLS)** pada dasarnya adalah algoritma **DFS**, tetapi dengan sebuah "sabuk pengaman" yang disebut **Batas Kedalaman (*Depth Limit*, disimbolkan dengan $l$)**. 

Alih-alih membiarkan DFS terus turun ke kedalaman tak terhingga, DLS menginstruksikan pencarian untuk **berhenti dan memutar balik (*backtrack*)** ketika ia mencapai kedalaman $l$. Node pada kedalaman $l$ diperlakukan seolah-olah mereka tidak memiliki anak (*child*).

### 2.2 Analisis Properti DLS
Mari kita analisis karakteristik DLS berdasarkan 4 kriteria utama dalam evaluasi algoritma pencarian:

1. **Completeness (Apakah pasti menemukan solusi?):** 
   - **TIDAK**, kecuali jika kita tahu persis bahwa kedalaman solusi $d$ lebih kecil atau sama dengan batas $l$ ($d \le l$). Jika solusi berada di kedalaman $d = 5$, tetapi kita menyetel batas $l = 3$, DLS tidak akan pernah menemukan solusi tersebut.
2. **Optimality (Apakah pasti menemukan solusi terbaik/terpendek?):** 
   - **TIDAK**. DLS tidak optimal jika $l > d$. Ia bisa saja menemukan solusi yang lebih panjang di cabang pertama yang ia telusuri sebelum menemukan solusi yang lebih pendek di cabang lain.
3. **Time Complexity (Kompleksitas Waktu):** $O(b^l)$
   - Dalam kasus terburuk, DLS akan menelusuri seluruh pohon hingga kedalaman $l$.
4. **Space Complexity (Kompleksitas Ruang / Memori):** $O(bl)$
   - Seperti DFS, ia hanya menyimpan jalur saat ini. Karena dibatasi hingga $l$, memorinya berbanding lurus dengan batas tersebut. Ini sangat efisien dibandingkan $O(b^l)$ milik BFS jika BFS berjalan hingga kedalaman $l$.

> [!info] Istilah Teknis: *Branching Factor* ($b$)
> Rata-rata atau jumlah maksimum anak (*children*) yang dapat dihasilkan dari setiap state/node.

### 2.3 Simulasi Kasus DLS (Worked Example)

Bayangkan kita memiliki pohon pencarian berikut. Tujuan (Goal) kita adalah menemukan simpul **G**.
*Node Root (A) berada di kedalaman 0.*

```text
Level 0:          A
                /   \
Level 1:       B     C
              / \   / \
Level 2:     D   E F   G
            /
Level 3:   H 
```

**Kasus: Kita menjalankan DLS dengan Limit $l = 1$**
1. Mulai dari **A** (Level 0). Periksa: Apakah A = G? Tidak. Kedalaman saat ini (0) < limit (1). Ekspansi A.
2. Ke **B** (Level 1). Periksa: Apakah B = G? Tidak. Kedalaman saat ini (1) == limit (1). **DLS tidak mengekspansi B**. Balik arah (*backtrack*).
3. Ke **C** (Level 1). Periksa: Apakah C = G? Tidak. Kedalaman saat ini (1) == limit (1). **DLS tidak mengekspansi C**.
4. Pencarian selesai. **Status: Gagal (Cutoff).** DLS gagal karena solusi (G) ada di kedalaman 2, sedangkan limit kita hanya 1.

**Kasus: Kita menjalankan DLS dengan Limit $l = 2$**
1. Mulai dari **A** (Level 0). Ekspansi.
2. Turun ke **B** (Level 1). Ekspansi.
3. Turun ke **D** (Level 2). Periksa: Apakah D = G? Tidak. Kedalaman (2) == limit (2). Tidak diekspansi (meskipun ada H). *Backtrack* ke B.
4. Turun ke **E** (Level 2). Periksa: Apakah E = G? Tidak. Kedalaman (2) == limit (2). *Backtrack* ke B, lalu ke A.
5. Turun ke **C** (Level 1). Ekspansi.
6. Turun ke **F** (Level 2). Periksa: Apakah F = G? Tidak. Kedalaman (2) == limit (2). *Backtrack* ke C.
7. Turun ke **G** (Level 2). Periksa: Apakah G = G? **YA! Solusi ditemukan.**

> [!warning] Kelemahan DLS
> Masalah terbesar DLS adalah kita harus mengetahui (atau menebak dengan akurat) nilai $l$. Di dunia nyata, seringkali kita tidak tahu seberapa dalam solusi berada. Jika kita salah menebak $l$ terlalu kecil, kita gagal. Jika kita menebak $l$ terlalu besar, kita membuang-buang waktu menelusuri cabang yang dalam namun tidak relevan.

---

## 3. Iterative Deepening Search (IDS)

### 3.1 Konsep Dasar: Menemukan "Sweet Spot"
Bagaimana jika kita **tidak tahu** limit yang tepat? Jawaban brilian dari Computer Science adalah: **Coba saja satu per satu!**

**Iterative Deepening Search (IDS)** adalah strategi elegan yang menggunakan DLS berulang kali secara inkremental. Algoritmanya bekerja secara iteratif:
1. Jalankan DLS dengan limit $l = 0$. Jika solusi ditemukan, selesai. Jika tidak, lanjut.
2. Jalankan DLS dengan limit $l = 1$. Jika solusi ditemukan, selesai. Jika tidak, lanjut.
3. Jalankan DLS dengan limit $l = 2$.
4. Dan seterusnya, dengan limit $l = 3, 4, 5...$ hingga solusi ditemukan.

> [!quote] Definisi Konseptual IDS
> IDS pada dasarnya mensimulasikan pencarian melebar (BFS) dengan menjalankan pencarian mendalam (DFS/DLS) berulang-ulang, setiap kali dengan batas yang lebih dalam sedikit.

### 3.2 Analisis Properti IDS: The Best of Both Worlds
Mengapa IDS sering disebut sebagai algoritma pencarian buta (uninformed) terbaik ketika ruang pencarian sangat besar dan kedalaman solusi tidak diketahui?

1. **Completeness:** **YA**. Karena IDS secara bertahap meningkatkan batas kedalaman, ia *pasti* akan pada akhirnya mencapai kedalaman $d$ tempat solusi berada, layaknya BFS.
2. **Optimality:** **YA** (asalkan biaya semua langkah sama). IDS akan selalu menemukan solusi pada kedalaman paling dangkal terlebih dahulu, karena ia memeriksa level 0, lalu 1, lalu 2, dst.
3. **Space Complexity:** $O(bd)$. 
   - Ini adalah kekuatan utama IDS. Karena pada intinya ia menjalankan DLS (yang merupakan varian DFS), ia hanya menyimpan satu jalur pada satu waktu dalam memori. Memorinya linier, persis seperti DFS.
4. **Time Complexity:** $O(b^d)$.
   - Pertanyaannya: *"Bukankah IDS sangat lambat karena harus memeriksa node dari awal (root) berulang-ulang setiap kali batas dinaikkan?"*
   - Jawaban: **Secara mengejutkan, TIDAK signifikan.** 

#### 3.2.1 Intuisi Matematis: Mengapa Redundansi di IDS Bukan Masalah Besar
Pohon pencarian tumbuh secara eksponensial. Jumlah node pada kedalaman paling bawah jauh lebih banyak daripada total *semua* node di atasnya.

Mari kita hitung node yang dibangkitkan pada IDS. Node pada level $d$ dihasilkan sekali. Node pada level $d-1$ dihasilkan 2 kali. Node pada root (level 0) dihasilkan $d+1$ kali.
Total node yang dihasilkan:
$N(IDS) = (d+1)b^0 + d b^1 + (d-1)b^2 + \dots + 1 \cdot b^d$

Bandingkan dengan BFS (yang membangkitkan semua node hingga level $d$ sekaligus):
$N(BFS) = b^0 + b^1 + b^2 + \dots + b^d = O(b^d)$

Secara asimtotik (Big-O notation), $O(b^d)$ milik IDS sama persis dengan $O(b^d)$ milik BFS. Biaya tambahan dari mengulang level atas ternyata memudar dibandingkan biaya mengekspansi level terbawah yang ukurannya masif. Redundansinya sekitar $\frac{b}{b-1}$ saja. (Contoh jika $b=10$, IDS hanya butuh 11% iterasi lebih banyak dari BFS).

### 3.3 Simulasi Kasus IDS (Worked Example)

Menggunakan pohon yang sama:
```text
Level 0:          A
                /   \
Level 1:       B     C
              / \   / \
Level 2:     D   E F   G
```
Tujuan: **G** (Level 2).

**Iterasi 1: Limit l = 0**
- Mulai (DLS). Kunjungi A. Batas limit tercapai. A bukan G. Selesai (Cutoff).
- Node dikunjungi: {A}

**Iterasi 2: Limit l = 1**
- Mulai baru. Kunjungi A. Ekspansi ke B dan C.
- Kunjungi B. Batas tercapai. Balik.
- Kunjungi C. Batas tercapai.
- C bukan G. Selesai (Cutoff).
- Node dikunjungi: {A, B, C}

**Iterasi 3: Limit l = 2**
- Mulai baru. Kunjungi A. Ekspansi.
- Kunjungi B. Ekspansi.
- Kunjungi D. Batas tercapai. Balik.
- Kunjungi E. Batas tercapai. Balik ke B, balik ke A.
- Kunjungi C. Ekspansi.
- Kunjungi F. Batas tercapai. Balik.
- Kunjungi G. **Kondisi Goal Tercapai! Solusi Ditemukan.**
- Node dikunjungi secara spesifik pada tahap ini: {A, B, D, E, C, F, G}

> [!check] Kesimpulan IDS
> Meskipun terlihat membuang-buang waktu karena memeriksa `A` 3 kali, `B` dan `C` 2 kali, IDS memberi kita jaminan menemukan `G` (seperti BFS) tanpa pernah menyimpan seluruh barisan `B, C, D, E, F, G` dalam RAM secara bersamaan.

---

## 4. Perbandingan Performa Komprehensif

Tabel berikut merangkum posisi DLS dan IDS di antara algoritma pencarian lainnya:

| Algoritma | Lengkap (Complete)? | Optimal? | Waktu | Ruang (Memori) | Keunggulan Utama |
| :--- | :---: | :---: | :--- | :--- | :--- |
| **Breadth-First (BFS)** | Ya | Ya | $O(b^d)$ | $O(b^d)$ | Menemukan solusi terpendek pasti |
| **Depth-First (DFS)** | Tidak | Tidak | $O(b^m)$ | $O(bm)$ | Hemat memori |
| **Depth-Limited (DLS)** | Tidak | Tidak | $O(b^l)$ | $O(bl)$ | DFS tanpa jebakan *infinite loop* |
| **Iterative Deepening (IDS)** | **Ya** | **Ya** | **$O(b^d)$** | **$O(bd)$** | **Hemat memori (spt DFS) + Pasti & Optimal (spt BFS)** |

*Keterangan:*
- $b$: Branching factor
- $d$: Kedalaman di mana solusi ditemukan
- $m$: Kedalaman maksimal ruang keadaan (*state space*)
- $l$: Batas kedalaman (*limit*)

---

## 5. Ringkasan & Takeaways

1. **DLS** adalah "perban" untuk kelemahan DFS. Dengan memberikan limit $l$, DLS mencegah program mencari solusi ke dasar jurang yang tidak berujung. DLS digunakan saat kita (melalui pengetahuan masalah/domain) mengetahui batas maksimal solusi yang masuk akal.
2. **IDS** adalah mahakarya algoritma pencarian buta. Jika Anda disuruh merancang program pencarian di lingkungan di mana solusi tidak jelas kedalamannya dan memori sangat terbatas, **selalu gunakan IDS**.
3. **Mitos Terbesar IDS** adalah ia tidak efisien karena redundansi. Fakta matematis membuktikan biaya perulangan level atas sangat marjinal (kecil) jika dibandingkan dengan manfaat penghematan memori eksponensial.

---

## 6. Referensi & Pembelajaran Lanjutan

Untuk memperdalam visualisasi dan teori, Anda dapat merujuk ke sumber daya berikut:
- **Video Pembelajaran (YouTube):**
  - [Artificial Intelligence - Iterative Deepening Search (IDS) Explained](https://www.youtube.com/results?search_query=iterative+deepening+search+artificial+intelligence) *(Cari video dari kanal pendidikan CS terkemuka seperti Neso Academy atau Udacity).*
- **Buku Teks Akademik Primer:**
  - *Artificial Intelligence: A Modern Approach (AIMA)* oleh Stuart Russell dan Peter Norvig. (Bab 3: Solving Problems by Searching). Di buku ini dibuktikan secara ketat mengapa IDS direkomendasikan secara universal.
