---
title:
  - Teknik Induksi & Rekursi
type: Lecture
course:
  - Discrete Mathematics I
topic:
  - Algoritma Diskrit
semester: 2
tags:
status: 🌿 incubating
created: 2026-04-02
---
 
# Teknik Induksi & Rekursi

**Reference:** RPS-MD1.md, Discrete Mathematics and Its Applications (Kenneth H. Rosen)
**Source:** [[RPS-MD1]]
**Prasyarat:** [[DM1 - 3 - Algoritma Diskrit]]
**Praktikum/Tugas Terkait:** N/A

---

## Daftar Isi

1. [[#1. Introduction to Strong Induction]]
2. [[#2. Pembuktian dengan Strong Induction]]
3. [[#3. Recursive Algorithms]]
4. [[#4. Contoh Algoritma Rekursi dan Analisisnya]]
5. [[#Summary — Key Concepts at a Glance]]
6. [[#Active Recall Questions]]
7. [[#External Resources]]

---

## 1. Introduction to Strong Induction

Dalam matematika diskrit, **Mathematical Induction** (induksi matematika biasa atau *weak induction*) adalah teknik fundamental untuk membuktikan bahwa suatu properti $P(n)$ berlaku untuk seluruh bilangan bulat positif $n$. Namun, terkadang asumsi bahwa $P(k)$ benar tidak cukup kuat untuk membuktikan $P(k+1)$. Di sinilah kita menggunakan **Strong Induction** (Induksi Kuat).

Perbedaan utama antara *Weak Induction* dan *Strong Induction* terletak pada **Inductive Hypothesis**:
- **Weak Induction:** Kita mengasumsikan properti tersebut benar untuk satu elemen sebelumnya, yaitu asumsi $P(k)$ bernilai *True*, untuk membuktikan $P(k+1)$.
- **Strong Induction:** Kita mengasumsikan properti tersebut benar untuk **semua** elemen dari *Base Case* sampai ke $k$. Artinya, kita berasumsi $P(1), P(2), \dots, P(k)$ semuanya bernilai *True*, untuk membuktikan $P(k+1)$.

Kapan kita menggunakan *Strong Induction*? Teknik ini sangat berguna ketika nilai atau *state* dari tahap ke-$(k+1)$ bergantung pada lebih dari satu *state* sebelumnya, atau bahkan semua *state* sebelumnya (misalnya dalam barisan bilangan rekursif yang kompleks seperti Fibonacci).

---

## 2. Pembuktian dengan Strong Induction

Untuk melakukan pembuktian menggunakan **Strong Induction**, kita mengikuti kerangka terstruktur dengan dua tahap utama:

1. **Basis Step (Base Case):** 
   Kita mem-verifikasi bahwa proposisi $P(n)$ benar untuk nilai awal (biasanya $n=1$, namun terkadang dibuktikan untuk beberapa nilai awal sekaligus seperti $n=1, n=2$, tergantung kebutuhan relasi rekurensinya).
2. **Inductive Step:**
   - **Inductive Hypothesis:** Asumsikan bahwa $P(i)$ adalah benar untuk semua himpunan bilangan bulat $i$ sedemikian rupa sehingga $\text{base\_case} \leq i \leq k$.
   - **Goal:** Gunakan keseluruhan hipotesis tersebut untuk membuktikan secara logis bahwa $P(k+1)$ juga benar.

### Contoh Pembuktian: Fundamental Theorem of Arithmetic
**Proposisi:** Setiap bilangan bulat $n \ge 2$ dapat dituliskan sebagai hasil kali bilangan prima (atau bilangan itu sendiri sudah prima).

**Proof:**
- **Basis Step:** Untuk $n=2$. Karena 2 adalah bilangan prima, maka proposisi bernilai *True*.
- **Inductive Step:** Asumsikan bahwa proposisi $P(i)$ bernilai *True* untuk seluruh bilangan bulat $i$ dimana $2 \le i \le k$. Kita harus membuktikan bahwa $P(k+1)$ benar.
  Terdapat dua kasus untuk bilangan $(k+1)$:
  1. Jika $(k+1)$ adalah bilangan prima, maka proposisi langsung terbukti *True*.
  2. Jika $(k+1)$ adalah bilangan komposit, maka bilangan tersebut dapat dibagi menjadi dua faktor, sebut saja $a$ dan $b$, sehingga $(k+1) = a \times b$, dengan $2 \le a \le k$ dan $2 \le b \le k$. 
  
  Berdasarkan **Inductive Hypothesis** dari *Strong Induction*, karena $a$ dan $b$ berada di rentang $2$ hingga $k$, maka $a$ dan $b$ pasti dapat direpresentasikan sebagai perkalian dari bilangan prima. Akibatnya, $(k+1)$ yang merupakan hasil perkalian $(a \times b)$ juga merupakan perkalian dari bilangan-bilangan prima.

Proposisi terbukti!

---

## 3. Recursive Algorithms

Dalam ranah *Computer Science*, **Recursion** adalah sebuah teknik di mana sebuah fungsi memanggil dirinya sendiri (*self-invocation*) sebagai bagian dari eksekusinya. Sebuah algoritma dikatakan merupakan **Recursive Algorithm** jika algoritma tersebut menyelesaikan suatu permasalahan berukuran besar dengan mereduksi (membagi) permasalahan tersebut ke dalam *instances* berskala lebih kecil dari permasalahan yang sama.

Setiap fungsi rekursif yang dapat berjalan dengan benar (tanpa mengalami *infinite loop*) harus memiliki 2 komponen krusial:
1. **Base Case(s):** Kondisi spesifik di mana fungsi menghentikan pemanggilan dirinya sendiri (*recursive call*) dan langsung mengembalikan suatu nilai deterministik. *Base Case* berfungsi sebagai terminal poin agar eksekusi memori tak *overflow* (menghindari *StackOverflow*).
2. **Recursive Step:** Bagian fungsional di mana fungsi mengeksekusi operasi (jika perlu) dan memanggil dirinya sendiri dengan *input* parameter yang telah dimodifikasi, sehingga secara bertahap menuju ke *Base Case*.

---

## 4. Contoh Algoritma Rekursi dan Analisisnya

Mari kita bedah dua contoh algoritma rekursif klasik:

### 4.1 Perhitungan Faktorial
Penghitungan $n! = n \times (n-1) \times \dots \times 1$ bisa disederhanakan dalam formula rekursif $n! = n \times (n-1)!$.

```python
def factorial(n):
    # Base Case
    if n == 0:
        return 1
    # Recursive Step
    return n * factorial(n - 1)
```
- **Base Case:** Saat $n = 0$, fungsi langsung evaluasi menjadi 1.
- **Recursive Step:** Fungsi memanggil `factorial(n-1)`. Setiap langkah, ukuran input akan berkurang 1 hingga menyentuh *Base Case*.

### 4.2 Deret Fibonacci
Suku ke-$n$ pada deret Fibonacci didefinisikan sebagai jumlah dari dua suku secara berurutan sebelumnya: $F(n) = F(n-1) + F(n-2)$.

```python
def fibonacci(n):
    # Base Case (ada 2 terminal)
    if n == 0:
        return 0
    if n == 1:
        return 1
    # Recursive Step
    return fibonacci(n - 1) + fibonacci(n - 2)
```
Untuk membuktikan bahwa pemanggilan rekursif seperti `fibonacci` dieksekusi dengan benar sepanjang $n$, metode pembuktian yang paling komprehensif adalah **Strong Induction**, karena kita perlu mengacu pada dua *state* ke belakang ($n-1$ dan $n-2$) bukan cuma satu *state*.

---

## Summary — Key Concepts at a Glance

| Concept | Definition |
|---|---|
| **Strong Induction** | Teknik pembuktian matematis yang menggunakan asumsi bahwa proposisi yang diuji benar untuk **seluruh** nilai sebelumnya (sejak *base case* hingga $k$) guna membuktikan instansiasi $k+1$. |
| **Recursion** | Metode problem-solving dalam *Computer Science* di mana sebuah fungsi menyelesaikan *problem* dengan cara memanggil dirinya sendiri menggunakan *input* berukuran lebih kecil. |
| **Base Case** | Kondisi terminasi dalam fungsi rekursi untuk mencegah *infinite recursive call* (jebakan eksekusi tanpa henti). |
| **Recursive Step** | Reduksi ukuran masalah, pemanggilan ulang fungsi (*self-invocation*), dan operasi bertahap hingga menuju *Base Case*. |

---

## Active Recall Questions

> [!question]- 1. Apa perbedaan utama pada perumusan *Inductive Hypothesis* antara *Weak Induction* dan *Strong Induction*? Mengapa perbedaan ini krusial untuk kasus fungsi yang lebih kompleks?
> Pada *Weak Induction*, kita hanya berasumsi bahwa observasi pada langkah tepat sebelum observasi saat ini ($n=k$) adalah bernilai *True* untuk membuktikan kebenaran pada langkah $n=k+1$. Di sisi lain, *Strong Induction* mengasumsikan bahwa **keseluruhan observasi** dari titik mulai (seperti $n=1$ atau $n=0$) hingga tepat pada $n=k$ adalah *True*.
> Ini sangat krusial pada kasus komputasi struktural yang dependensinya tidak hanya bergantung pada $1$ *state* sebelum ini, melainkan merujuk pada banyak *state* lampau (seperti deret *Fibonacci* yang bergantung pada *state* $k-1$ dan $k-2$).

> [!question]- 2. Andaikan seorang *engineer* menciptakan *Recursive Algorithm* tanpa mencantumkan komponen *Base Case*. Apa konsekuensi pada *running system* ketika fungsi tersebut dieksekusi?
> Konsekuensinya adalah aplikasi akan menemui kesalahan eksekusi ekstrim: *Infinite Recursion*. Karena tidak memiliki kondisi terminasi (*Base Case*), fungsi akan terus memanggil dirinya sendiri selamanya, mengokupasi ruang dari *Call Stack* di RAM hingga menyebabkan *system crash* (biasanya kita kenal dengan pesan *error*: `StackOverflowError` atau `RecursionError`).

> [!question]- 3. Mengapa pembuktian analitis *algoritma faktorial* cocok memakai *Mathematical Induction* biasa, sedangkan pembuktian *Fibonacci* mengharuskan pemakaian *Strong Induction*?
> Karena dalam algoritma Faktorial ($n! = n \times (n-1)!$), kita hanya bergantung pada tepat **satu** argumen di tahap sebelumnya ($(n-1)!$). Sedangkan pada fungsi Fibonacci ($F(n) = F(n-1) + F(n-2)$), kelayakan nilainya tidak bisa sekadar bergantung pada $F(n-1)$ saja, namun secara inheren ia juga memerlukan informasi tentang properti bernilai benar di iterasi berjarak 2 langkah: $F(n-2)$. Maka, diperlukan *Strong Induction*.

---

## External Resources

Berikut adalah referensi eksternal dari *website* dan *YouTube* untuk memperkuat pemahaman mengenai *Strong Induction* dan aplikasinya pada *Discrete Mathematics*:
- **[YouTube]** [Strong Induction Examples - TrevTutor](https://www.youtube.com/results?search_query=Strong+Induction+discrete+mathematics)
- **[Article]** [TutorialsPoint - Strong Mathematical Induction](https://www.tutorialspoint.com/strong-induction)
- **[Article]** [Cornell CS2800 - Strong Induction](https://courses.cs.cornell.edu/cs2800/wiki/index.php/Strong_induction)
