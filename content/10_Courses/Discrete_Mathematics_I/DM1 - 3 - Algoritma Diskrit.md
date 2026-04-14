---
title:
  - Algoritma Diskrit dan Analisis Waktu Komputasi
type: Lecture
course:
  - Discrete Mathematics I
topic:
  - Discrete Algorithms
  - Computational Time Complexity
semester: 4
tags:
  - discrete-mathematics
  - algorithm
  - time-complexity
  - college
  - lecture-note
status: 🌳 evergreen
created: 2026-04-02
---

# Algoritma Diskrit dan Analisis Waktu Komputasi

**Reference:** Rosen, K.H. *Discrete Mathematics and Its Applications*; Munir, R. *Matematika Diskrit dan Aplikasinya pada Ilmu Komputer*
**Source:** [[RPS-MD1]]

---

## Daftar Isi

1. [[#1. Pengantar Algoritma Diskrit]]
2. [[#2. Contoh Algoritma Dasar]]
    - [[#2.1 Linear Search (Pencarian Sekuensial)]]
    - [[#2.2 Binary Search (Pencarian Biner)]]
3. [[#3. Analisis Waktu Komputasi (Computational Time Complexity)]]
    - [[#3.1 Mengapa Kita Membutuhkan Analisis Kompleksitas?]]
    - [[#3.2 Worst-case, Best-case, dan Average-case Analysis]]
4. [[#4. Notasi Asimptotik (Asymptotic Notations)]]
    - [[#4.1 Big-O Notation ($O$) - Upper Bound]]
    - [[#4.2 Big-Omega Notation ($\Omega$) - Lower Bound]]
    - [[#4.3 Big-Theta Notation ($\Theta$) - Tight Bound]]
5. [[#5. Kompleksitas Algoritma Sorting (Contoh Kasus)]]
    - [[#5.1 Bubble Sort]]
    - [[#5.2 Insertion Sort]]
6. [[#Summary — Key Concepts at a Glance]]
7. [[#Active Recall Questions]]

---

## 1. Pengantar Algoritma Diskrit

Sebuah **algoritma** adalah urutan langkah-langkah presisi (*finite set of instructions*) yang digunakan untuk memecahkan sebuah permasalahan atau melakukan proses komputasi. Dalam konteks Matematika Diskrit, algoritma banyak menangani struktur diskrit seperti graf, *integer*, *string*, dan himpunan.

Agar sebuah set instruksi dapat disebut algoritma yang valid, ia harus memenuhi **lima karakteristik mutlak**, yaitu:

1. **Input:** Harus memiliki nol atau lebih variabel *input* dari sebuah spesifik *set*.
2. **Output:** Menghasilkan satu atau lebih nilai *output* yang berkorelasi dengan *input*.
3. **Definiteness (Kepastian):** Setiap langkah didefinisikan secara presisi dan tak mengandung *ambiguity* (ambigu).
4. **Correctness (Kebenaran):** Mampu menghasilkan *output* yang benar untuk setiap himpunan *input* valid.
5. **Finiteness (Keterbatasan):** Algoritma *wajib* berhenti (*halt*) setelah memproses sejumlah langkah (*finite steps*). Sebuah algoritma tidak boleh terjebak dalam *infinite loop* (rekursi tak terhingga).
6. **Effectiveness (Keefektifan):** Setiap operasi logis yang diminta harus cukup mendasar agar dapat dijalankan dan diselesaikan manusia menggunakan kertas dan pensil (murni dasar hitungan matematis).
7. **Generality:** Algoritma harus berlaku tidak hanya untuk spesifik himpunan data awal, tapi ke masalah abstrak secara keseluruhan.

> [!note] Pseudocode
> Untuk mendeskripsikan logika tanpa terikat bahasa pemrograman spesifik (seperti Java, Python, atau C++), kita menggunakan **Pseudocode**, yaitu struktur bahasa Inggris-matematika campuran yang menekankan *logical structure*.

---

## 2. Contoh Algoritma Dasar

Mari kita lihat beberapa algoritma fundamental yang banyak digunakan dan dipelajari dalam Matematika Diskrit.

### 2.1 Linear Search (Pencarian Sekuensial)

**Tujuan:** Mencari sebuah elemen $x$ dalam *list* (array) $A$. Algoritma akan mencari dari elemen pertama sampai elemen terakhir satu per satu.

```pascal
procedure linear_search(x: integer, a1, a2, ..., an: distinct integers)
i := 1
while (i ≤ n and x ≠ ai)
    i := i + 1
if i ≤ n then location := i
else location := 0
return location
```

> [!tip] Pendekatan Linear Search
> Sangat *brute-force* karena mencoba semua probabilitas skema tanpa pra-syarat susunan data. Algoritma ini berjalan aman walau data tersebut *unsorted* (acak).

### 2.2 Binary Search (Pencarian Biner)

**Tujuan:** Mencari *integer* $x$ di dalam sebuah *list* yang **sudah terurut** (misal *sorted in ascending order*).

```pascal
procedure binary_search(x: integer, a1, a2, ..., an: increasing integers)
i := 1 {i is left endpoint of search interval}
j := n {j is right endpoint of search interval}
while i < j
    m := ⌊(i + j)/2⌋
    if x > am then i := m + 1
    else j := m
if x = ai then location := i
else location := 0
return location
```

> [!info] Mengapa Binary Search Jauh Lebih Cepat?
> Dengan memotong ukuran interval menjadi 2 di tiap langkah, interval observasi merosot drastis sehingga komputasi yang dihasilkan bersifat logaritmik ($O(\log n)$), alih-alih mencoba semua input (linear). Ini butuh prasyarat *"Sorted Array"*.

---

## 3. Analisis Waktu Komputasi (Computational Time Complexity)

### 3.1 Mengapa Kita Membutuhkan Analisis Kompleksitas?

Jika kita ingin melihat performa kecepatan sebuah algoritma program, mengapa tidak sekadar merekam kecepatannya dalam **detik** saja? 

**Jawabannya:** Pengukuran dalam *detik* membuat performa program menjadi tidak objektif, karena kecepatannya akan bergantung (*dependent*) pada tipe *hardware* (CPU clock), sistem operasi yang berbeda, jenis bahasa, dan kualitas kompiler yang mendelegasikan tugas komputasi mesin. 

Maka dari itu, untuk mengukur kecepatan konseptual, kita menggunakan **Time Complexity Analysis**. Kita tidak menghitung detik, melainkan kita **menghitung tingkat pertumbuhan jumlah operasi fundamental** (*counting fundamental operations*) saat volume input (*size* $n$) meningkat.

### 3.2 Worst-case, Best-case, dan Average-case Analysis

Terdapat 3 sudut pandang utama dalam memperkirakan seberapa efisien sebuah algoritma berjalan berdasarkan variasi *input*-nya. Mari kita amati menggunakan contoh **Linear Search** untuk memperjelas konsepnya:

- **Worst-case Analysis (Kasus Terburuk):**
  Menghitung *maximum number of operations* seandainya algoritma mendapatkan pasokan input skenario yang paling memakan waktu ("sial"). 
  Kebanyakan ilmuwan komputer dan *software engineer* paling peduli dengan parameter ini untuk menjamin performa aplikasinya tidak pernah *crash* karena melebihi limitasi *resource*.
  > [!example] Contoh Linear Search (Worst-Case)
  > Anda mencari nilai $x$, namun anomali terjadi: ternyata $x$ terletak di indeks paling belakang, atau secara mengecewakan **tidak ada sama sekali** di dalam *array*!
  > Algoritma dipaksa keras menelusuri dan mencocokkan setiap elemen satu per satu hingga letak batas data $n$. Operasi pun tereksekusi sebanyak $n$-kali. Kompleksitasnya adalah **$O(n)$**.

- **Best-case Analysis (Kasus Terbaik):**
  Mengukur *minimum number of operations* atau skema eksekusi yang paling singkat (*optimal*).
  Meskipun tampak bagus, matriks ini cenderung diabaikan / jarang diserap sebagai jaminan performa operasional murni karena asumsi mendadak beruntung ini amat rapuh bila berhadapan dengan data serba sembarang.
  > [!example] Contoh Linear Search (Best-Case)
  > Jackpot beruntung! Elemen $x$ yang sedang Anda cari rupanya bertengger manis secara natural persis bertempat di kotak indeks pertama (elemen pada jejak iterasi `A[1]`). 
  > Alur program sukses menemukan referensinya seketika pada siklus perulangan terawal saja dan spontan *halt* (putus terminasi). Kompleksitasnya seketika meroket konstan mandiri: **$\Omega(1)$**.

- **Average-case Analysis (Kasus Rata-rata):**
  Ini mengusung perkiraan *number of operations* rata-rata berdasarkan analisis statistik dari *probability distribution* (distribusi probabilitas) kumpulan masukan data program. Analisis ini bersifat amat *math-intensive* (padat aritmatika).
  > [!example] Contoh Linear Search (Average-Case)
  > Sekiranya dipastikan elemen $x$ wajib wujud entah letak berapapun secara sempang *uniform*, maka nilai kecocokannya memiliki kesempatan kemunculan yang *equal/fair* murni di tiap posisi.
  > Probabilitas statistiknya menggambarkan bahwa mayoritas kecocokan *querying* ini ditangkap tepat saat menempuh pertengahan penapisan, melahirkan hitungan operasi komputasi di kurva $\frac{n}{2}$. Setelah penindakan simplifikasi aturan asimtot (membuang beban operator fraksional konstanta 1/2), maka ia kembali bertransformasi menggapai proporsinya erat sebagai kompleksitas **$\Theta(n)$**. 

---

## 4. Notasi Asimptotik (Asymptotic Notations)

Di dalam Matematika Diskrit, kita meletakkan analisis kerumitan ke sebuah skala standardisasi yang disebut **Notasi Asimptotik**. Gunanya untuk menggambarkan perilaku limit dari sebuah fungsi seiring variabel bebas tumbuh menuju tak hingga.

### 4.1 Big-O Notation ($O$) - Upper Bound

Menyatakan **batas atas konstan** (*upper bound*).
> [!abstract] Definisi Big-O
> Fungsional $f(x)$ dibilang $O(g(x))$ jikalau terdapat *constants* rill $C$ dan variabel acuan $k$ di mana:
> $|f(x)| \le C|g(x)|$, kapan saja $x > k$.

*Analogi:* Big-O memberikan jaminan/pelindung absolut bahwa algoritma ini "**tumbuhnya tidak lebih buruk / melampaui kurva $g(x)$**" di waktu krusial seiring bertambahnya ukuran data.

### 4.2 Big-Omega Notation ($\Omega$) - Lower Bound

Menyatakan **batas bawah konstan** (*lower bound*). 
> [!abstract] Definisi Big-Omega
> Fungsional $f(x)$ dibilang $\Omega(g(x))$ jikalau terdapat *constants* rill $C$ dan variabel acuan $k$ di mana:
> $|f(x)| \ge C|g(x)|$, kapan saja $x > k$.

*Analogi:* Ini menunjukkan *best-case scenario*, algoritma "**paling cepat eksekusi menempuh minimum operasi $g(x)$**", setidaknya waktu berjalannya selalu lebih lambat dari kurva tersebut.

### 4.3 Big-Theta Notation ($\Theta$) - Tight Bound

Menyatakan **batas presisi (tepat)** (*tight bound*). 
Fungsional $f(x)$ dibilang $\Theta(g(x))$ jika pada dasarnya algoritmanya di waktu bersamaan $O(g(x))$ DAN $\Omega(g(x))$.

Artinya, waktu komputasi fungsional terbatasi ketat dari atas dan bawah (algoritma berjalan proporsional persis dengan $g(x)$ tanpa penyimpangan besar).

> [!important] Aturan Penting "Asymptotic":
> 1. **Drop Constants (Abaikan Konstanta):** Jika rumusnya $f(n) = 3n^2 + 5$, maka *time complexity*-nya adalah $O(n^2)$. Angka 3 dan 5 tidak berpengaruh tajam ketika *n* menuju triliunan.
> 2. **Drop Non-Dominant Terms (Abaikan Term Terlemah):** Jika $f(n) = n^3 + n^2 + n$, karena eksponen 3 akan membengkak jauh lebih cepat dan masif melampaui $n^2$ ketika n membesar, kita sederhanakan ini jadi $O(n^3)$.

---

## 5. Kompleksitas Algoritma Sorting (Contoh Kasus)

Banyak varian algoritma digunakan untuk melakukan *sorting* data (Mengurutkan bilangan kecil ke besar dll).

### 5.1 Bubble Sort

**Metode:** Algoritma paling *naive*, dia akan merotasi ulang dan melirik indeks angka dari 2 bilangan terdekat untuk diganti saling *swap* jika bilangan pertama melebihi kedua. *Heavy looping!*

```pascal
procedure bubblesort(a1,...,an: real numbers with n ≥ 2)
for i := 1 to n − 1
    for j := 1 to n − i
        if aj > aj+1 then interchange aj and aj+1
```

**Analisis Kompetensi Waktu ($O$):**
Terdapat **nested loop** (perulangan dalam perulangan).
Total rotasi $\rightarrow (n-1) + (n-2) + \dots + 1 = \frac{n(n-1)}{2} = O(n^2)$.
Baik secara *worst case* maupun rutinitas biasa tanpa validasi, ini berjalan memakan beban kuadratik $O(n^2)$. Sangat buruk untuk set besar.

### 5.2 Insertion Sort

**Metode:** Konsep ini meniru perilaku cara manusia mengambil dan mengurutkan dan menempatkan kumpulan kartu dari tangan dek pertama, menggeser seluruh elemen tersisa untuk memastikan per sisipan aman di ranahnya.

```pascal
procedure insertion_sort(a1, a2, ..., an: real numbers with n ≥ 2)
for j := 2 to n
    i := 1
    while aj > ai
        i := i + 1
    m := aj
    for k := 0 to j − i − 1
        aj−k := aj−k−1
    ai := m
```

**Analisis Kompleksitas Waktu ($O$):**
Jika datanya dalam keadaan ekstrem *reverse sorted* (Terbalik seutuhnya), tiap sisipan kartu dari ke 2 sampai N membutuhkan total $\sum_{j=2}^n j$ rotasi loop dan evaluasi paksa, yang mendongkrak algoritma tetap ke limit konstan asimtotik teratasnya: $O(n^2)$. 

Walaupun Insertion sort berlabel parah $O(n^2)$ pada worst-case scenario, dia sangat efisien $O(n)$ di **best-case** apabila data sudah *nearly sorted*.

---

## Summary — Key Concepts at a Glance

| Konsep | Definisi / Penjelasan |
|---|---|
| Algoritma Diskrit | Kumpulan langkah instruksi murni deterministik logis terpresisi (*input-output-finiteness*). |
| *Time Complexity* | Tingkat pertumbuhan fungsional performa waktu ditinjau dari fundamental analisis jumlah prosesnya.  |
| *Worst-case Analysis* | Pendekatan perlindungan komputasi algoritma dengan simulasi kondisi "tersulit". |
| $O$ (Big-O) | *Asymptotic Upper Bound.* Limit performa paling maksimal algoritma. (Jangan melampaui ini). |
| $\Omega$ (Big-Omega) | *Asymptotic Lower Bound.* Limit kecepatan komputasi minimum. Paling cepat sebatas kurva ini. |
| $\Theta$ (Big-Theta) | *Asymptotic Tight Bound*. Operasional proporsional tetap algoritma. |
| Operasi Dasar Konstan | Penyederhanaan notasi asimtot. Mengabaikan penambahan parameter konseptual dominan terkecil, misal 5n dicatat sebagai $O(n)$. |
| Bubble & Insertion Sort | Keduanya bernilai *worst-case complexity* ekuivalen: $O(n^2)$. |

---

## External Resources & Further Reading

Untuk memperdalam pemahaman tentang algoritma diskrit, kompleksitas waktu, dan memvisualisasikan cara kerja algoritma, Anda bisa mengunjungi referensi eksternal berikut:

- **[Big-O Cheat Sheet](https://www.bigocheatsheet.com/)** — Referensi definitif dan ringkas untuk membandingkan kompleksitas waktu dan ruang dari berbagai struktur data dan algoritma *sorting*. Sangat berguna sebagai contekan!
- **[VisuAlgo - Sorting](https://visualgo.net/en/sorting)** — Alat visualisasi interaktif dari National University of Singapore (NUS) yang sangat brilian. Memungkinkan Anda melihat *step-by-step* animasi bagaimana *Bubble Sort*, *Insertion Sort*, dan algoritma lain bekerja murni di memori.
- **[GeeksforGeeks: Understanding Time Complexity](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)** — Artikel komprehensif dengan contoh kasus implementasi matematis yang mengkoneksikan logika diskrit ke dalam *real-world programming*.

---

## Active Recall Questions

> [!question]- 1. Mengapa para ilmuwan komputer mengevaluasi kinerja algoritma dengan metode asimtotik (Big-O) daripada menghitung total durasi waktu yang dibutuhkan program berjalan (Execution Time / Stopwatch)?
> Menghitung menggunakan *stopwatch / execution time* sangat bergantung pada tipe spesifikasi hardware, variasi kompiler sistem (C++ vs Java vs V8 engine), operasi latar belakang os (multitasking). 
> Notasi asimtotik menghilangkan beban anomali independen hardware tsb, dan memfokuskan hanya pada metrik terobjektifnya: *"Bagaimana percepatan jumlah total komputasi perulangan skala kode ini selagi *input-size (n)* nya dinaikkan ke miliaran angka terburuk?"*

> [!question]- 2. Andaikan kode kamu menghasilkan model komputasi matematis $C(n) = 7n^4 + 32n^2 + 8n \log n + 10$. Apa Big-O *time complexity*-nya pascasimplifikasi mendasar batas atas?
> Kita mengabaikan semua faktor konstanta dan **drop the non-dominant term**. Term yang memiliki beban *scaling factor* terbesar dan eksponensial di fungsi tsb adalah n^4. Sisanya memilik pengaruh sangat kerdil di saat n menuju "Miliaran takhingga". Dengan demikian, maka kompleksitasnya adalah **$O(n^4)$**.

> [!question]- 3. Terangkan persis mengapa $O(\log n)$ (Logaritmik Time, yang digunakan pada Binary Search) diyakinkan jauh lebih efisien pada himpunan masif daripada performa pencarian yang bersifat linear $O(n)$ !
> Pencarian logaritmik ($O(\log n)$), layaknya strategi *Binary Search*, memangkas / menebas jarak pencariannya sendiri menjadi dua iteratur (dibelah) setiap perulangan berurutan. Ini mendegradasi rotasi. Menangani pencarian $n=1,000,000$ baris elemen *linear* butuh hingga $1 juta$ langkah di *worst case*. Dengan $O(\log_2(1000000))$, binary search hanya butuh *worst case scenario* sekitar **20 proses komputasi iteratif**. Terdapat defisit komparasi besar yang amat mencolok.

> [!question]- 4. Apa parameter fatal *Bubble Sort* mengapa bisa ia digolongkan secara *worst-case* menjadi kelas yang payah dan terkurung di komputasi $O(n^2)$ (Kuadratik)?
> Karena bubble sort mempunyai format sistem `nested for loops` (perulangan di dalam kurungan perulangan utama). Di *worst-scenario* elemen terburuk datanya sama sekali belum terfaktorkan untuk rotasi per langkah nya: ia akan membandingkan setiap elemen $n$. Dan untuk setiap 1 elemen di outer-loop, program ditugaskan mengevaluasi sisanya yang $n-1$, $n-2$... dst. Total akumulasi ini mendasari operasi Gauss Sum yang merekonstruksinya menjadi beban operasi Kuadratik.
