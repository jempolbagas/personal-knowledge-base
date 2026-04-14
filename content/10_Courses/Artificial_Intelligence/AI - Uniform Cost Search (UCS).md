---
title:
  - Uniform Cost Search
type: Lecture
course:
  - Artificial Intelligence
topic:
  - Uninformed Search
semester: 4
tags:
  - Search_Algorithms
  - Uninformed_Search
  - artificial-intelligence
status: 🌳 evergreen
created: 2026-03-10
week: 4
aliases:
  - UCS
---

# Uniform Cost Search (UCS)

> [!info] Definisi
> **Uniform Cost Search (UCS)** adalah algoritma pencarian tidak terinformasi (*uninformed search*) yang digunakan untuk melintasi atau mencari pada struktur data graf dan pohon. Tujuan utama UCS adalah menemukan jalur dari node awal (start node) ke node tujuan (goal node) dengan **biaya kumulatif total paling rendah (least-cost path)**, bukan sekadar jalur terpendek dalam hal jumlah langkah.

Dalam pendekatan *First-Principles*, bayangkan Anda berada di sebuah labirin di mana setiap lorong memiliki "panjang" atau "usaha" yang berbeda-beda untuk dilewati. Algoritma biasa mungkin hanya menghitung "berapa belokan" untuk sampai ke pintu keluar, tanpa peduli bahwa satu belokan mengharuskan Anda memanjat tebing. UCS memecahkan masalah ini dengan memastikan bahwa kita selalu memprioritaskan jalan yang membutuhkan **usaha total paling sedikit** sejak dari titik awal.

---

## 1. UCS vs Breadth-First Search (BFS)

Sangat penting untuk memahami bagaimana UCS berevolusi dari *Breadth-First Search* (BFS).

> [!abstract] Perbedaan Paradigma: Level vs Biaya
> - **BFS (Breadth-First Search):** Memperluas node berdasarkan kedalaman/level (*depth*). BFS berasumsi bahwa **setiap transisi memiliki biaya yang sama** (cost = 1). BFS akan menemukan jalur terpendek dalam hal *jumlah tepi (edges)*.
> - **UCS (Uniform Cost Search):** Memperluas node berdasarkan **biaya kumulatif**. UCS dirancang untuk graf yang memiliki bobot/biaya yang bervariasi pada setiap tepinya (*weighted graph*).

**Mengapa kita tidak bisa selalu menggunakan BFS?**
Misalkan Anda ingin pergi dari Kota A ke Kota C.
- Rute 1: $A \rightarrow B \rightarrow C$ (A ke B jaraknya 10 km, B ke C jaraknya 10 km. Total: 20 km. Jumlah langkah: 2)
- Rute 2: $A \rightarrow C$ (A ke C ada jalan tol berbayar mahal dengan jarak 100 km. Total: 100 km. Jumlah langkah: 1)

BFS akan memilih Rute 2 ($A \rightarrow C$) karena hanya membutuhkan 1 langkah (berada di level/kedalaman 1 dari A). Namun, dalam dunia nyata, Rute 1 jauh lebih optimal berdasarkan jarak/biaya. Di sinilah UCS masuk untuk memperbaiki kelemahan BFS.

*(Catatan: Jika semua edge pada graf memiliki bobot/cost yang identik, maka UCS beroperasi persis sama seperti BFS.)*

---

## 2. Mekanisme Inti: Biaya Kumulatif $g(n)$

Inti dari Uniform Cost Search terletak pada sebuah fungsi biaya yang sederhana namun fundamental:

$$g(n)$$

> [!note] Definisi $g(n)$
> $g(n)$ merepresentasikan **biaya kumulatif aktual (actual cumulative cost)** dari node awal (start node) untuk mencapai node $n$.

### Bagaimana $g(n)$ dihitung?
Jika node $n'$ adalah anak (*child*) dari node $n$, dan biaya transisi (edge cost) dari node $n$ ke $n'$ dilambangkan sebagai $c(n, n')$, maka biaya kumulatif untuk mencapai $n'$ adalah:

$$g(n') = g(n) + c(n, n')$$

**Struktur Data yang Digunakan:**
Untuk mengelola mana node yang harus diekspansi selanjutnya, UCS menggunakan **Priority Queue** (biasanya diimplementasikan dengan struktur data *Min-Heap*). Antrean ini diurutkan murni berdasarkan nilai $g(n)$. Node dengan nilai $g(n)$ terendah akan selalu berada di posisi paling depan untuk diekspansi (dikeluarkan dari antrean).

---

## 3. Simulasi Studi Kasus (Worked Example)

Mari kita bedah cara kerja algoritma ini langkah-demi-langkah agar logikanya terlihat bekerja secara *real-time*.

### Konfigurasi Graf
Misalkan kita memiliki graf berbobot sebagai berikut:
- **Start Node:** $S$
- **Goal Node:** $G$

**Daftar Edge (Tepi) dan Biaya (Cost):**
- $S \rightarrow A$ (Cost: 2)
- $S \rightarrow B$ (Cost: 5)
- $A \rightarrow C$ (Cost: 2)
- $A \rightarrow D$ (Cost: 4)
- $B \rightarrow D$ (Cost: 1)
- $B \rightarrow G$ (Cost: 6)
- $C \rightarrow G$ (Cost: 5)
- $D \rightarrow G$ (Cost: 2)

### Eksekusi Algoritma (Step-by-Step)

Kita akan melacak status **Priority Queue (Frontier)** dan **Node yang Diekspansi (Explored Set)**. Format di Queue: `[Node, g(n)]`.

**Langkah 0: Inisialisasi**
- **Frontier:** `[S, 0]`
- **Explored:** `{}`

**Langkah 1: Ekspansi S**
- Keluarkan `S` dari antrean karena memiliki cost terendah (0). Apakah `S` adalah Goal? Bukan.
- Masukkan tetangga `S` ke dalam Frontier dan hitung $g(n)$ mereka.
    - $g(A) = g(S) + c(S, A) = 0 + 2 = 2$
    - $g(B) = g(S) + c(S, B) = 0 + 5 = 5$
- **Frontier:** `[A, 2], [B, 5]` *(Diurutkan dari terkecil)*
- **Explored:** `{S}`

**Langkah 2: Ekspansi A**
- Keluarkan `A` (cost terendah: 2). Apakah `A` adalah Goal? Bukan.
- Masukkan tetangga `A` ke dalam Frontier:
    - $g(C) = g(A) + c(A, C) = 2 + 2 = 4$
    - $g(D) = g(A) + c(A, D) = 2 + 4 = 6$
- **Frontier:** `[C, 4], [B, 5], [D, 6]` *(Diurutkan)*
- **Explored:** `{S, A}`

**Langkah 3: Ekspansi C**
- Keluarkan `C` (cost terendah: 4). Apakah `C` Goal? Bukan.
- Masukkan tetangga `C` (yaitu `G`):
    - $g(G) = g(C) + c(C, G) = 4 + 5 = 9$
- **Frontier:** `[B, 5], [D, 6], [G, 9]`
- **Explored:** `{S, A, C}`

**Langkah 4: Ekspansi B**
- Keluarkan `B` (cost terendah: 5). Apakah `B` Goal? Bukan.
- Masukkan tetangga `B` (`D` dan `G`):
    - $g(D_{baru}) = g(B) + c(B, D) = 5 + 1 = 6$. Karena di antrean sudah ada `[D, 6]`, tidak ada pembaruan biaya menjadi lebih murah. Tetap `[D, 6]`.
    - $g(G_{baru}) = g(B) + c(B, G) = 5 + 6 = 11$. Karena di antrean sudah ada `[G, 9]`, kita abaikan jalur ini karena lebih mahal.
- **Frontier:** `[D, 6], [G, 9]`
- **Explored:** `{S, A, C, B}`

**Langkah 5: Ekspansi D**
- Keluarkan `D` (cost terendah: 6). Apakah `D` Goal? Bukan.
- Masukkan tetangga `D` (`G`):
    - $g(G_{baru}) = g(D) + c(D, G) = 6 + 2 = 8$.
- > [!warning] Perhatian! Update Frontier
  > Kita menemukan rute baru ke $G$ dengan cost 8, yang mana **lebih murah** dibandingkan rute sebelumnya yang ada di Frontier (`[G, 9]`). Maka, kita **memperbarui** node $G$ di dalam Priority Queue.
- **Frontier:** `[G, 8]`
- **Explored:** `{S, A, C, B, D}`

**Langkah 6: Ekspansi G (Goal Node Terdeteksi)**
- Keluarkan `G` (cost terendah: 8). Apakah `G` Goal? **YA!**
- **Pencarian Selesai.**

> [!success] Hasil Akhir
> - **Total Cost:** 8
> - **Jalur Optimal:** $S \rightarrow A \rightarrow D \rightarrow G$
> *(Bisa dilacak balik dengan menyimpan pointer 'parent' pada setiap node saat dimasukkan ke dalam antrean)*

---

## 4. Mengapa UCS Dianggap Optimal?

Uniform Cost Search menjamin sebuah properti penting dalam kecerdasan buatan: **Optimality (Optimalitas)**.

Sebuah algoritma pencarian dikatakan **Optimal** jika algoritma tersebut *selalu* menemukan solusi dengan biaya terendah di antara semua solusi yang mungkin, asalkan solusi tersebut ada.

**Syarat Mutlak Optimalitas UCS:**
UCS dijamin optimal **hanya jika** seluruh edge (biaya langkah) memiliki nilai positif ($\epsilon > 0$). Artinya, tidak ada biaya negatif. Jika ada biaya negatif, UCS bisa masuk ke dalam jebakan *infinite loop* (terus memutar di siklus berbiaya negatif untuk membuat $g(n)$ semakin kecil), dan algoritma tidak bisa lagi menjamin solusi terpendek. (Untuk graf dengan bobot negatif, *Bellman-Ford algorithm* adalah pendekatannya).

**Bukti Logika (First-Principles) mengapa Optimal:**
UCS selalu mengekspansi node $n$ yang memiliki nilai $g(n)$ terkecil di seluruh *frontier*. Saat UCS mengeluarkan Goal Node dari Priority Queue, itu berarti tidak ada lagi node lain di *frontier* yang memiliki $g(n)$ lebih kecil dari cost Goal Node tersebut. Karena semua biaya edge bernilai positif, memperluas node lain mana pun yang tersisa di *frontier* tidak mungkin menghasilkan jalur ke Goal dengan biaya yang lebih kecil daripada yang baru saja kita temukan.

---

## 5. Kompleksitas Waktu dan Ruang (Time & Space Complexity)

Untuk menganalisis seberapa efisien UCS secara komputasional, kita menggunakan tiga variabel utama:
- $b$: *Branching factor* (rata-rata jumlah anak/cabang dari sebuah node).
- $C^*$: Biaya (cost) dari jalur optimal menuju Goal.
- $\epsilon$: Batas bawah (lower bound) dari biaya setiap edge. Asumsinya $\epsilon > 0$ agar algoritma konvergen (misal minimum biaya langkah adalah $\epsilon$).

### Kompleksitas Waktu (Time Complexity)
Berapa lama algoritma ini berjalan (jumlah node yang dihasilkan)?
Alih-alih bergantung pada kedalaman (seperti $O(b^d)$ pada BFS), kompleksitas UCS diatur oleh "seberapa dalam" algoritma bisa menembus graf dengan mempertimbangkan biayanya. Kedalaman maksimum (atau efektif) yang dieksplorasi oleh UCS kira-kira adalah $\lfloor C^* / \epsilon \rfloor$.

Oleh karena itu, pada skenario terburuk (*worst-case*), UCS akan mengekspansi setiap level hingga biaya melebihi $C^*$.
Kompleksitas waktunya adalah:
$$O\left(b^{1 + \left\lfloor \frac{C^*}{\epsilon} \right\rfloor}\right)$$

### Kompleksitas Ruang (Space Complexity)
Karena UCS menyimpan semua node yang dihasilkan di dalam memori (di dalam Priority Queue / Frontier dan tabel Explored), kompleksitas ruangnya identik dengan kompleksitas waktunya.
Kompleksitas ruang:
$$O\left(b^{1 + \left\lfloor \frac{C^*}{\epsilon} \right\rfloor}\right)$$

> [!warning] Kelemahan Terbesar UCS
> Meskipun Optimal dan *Complete* (pasti menemukan solusi jika ada), **kompleksitas memori** adalah musuh utama UCS. Sama halnya seperti BFS, UCS bisa dengan cepat menghabiskan RAM pada graf berukuran masif (seperti masalah peta dunia nyata dengan jutaan persimpangan). Untuk kasus seperti ini, variasi heuristik seperti **A* Search (A-Star)** jauh lebih disukai. A* menggabungkan $g(n)$ dari UCS dengan fungsi perkiraan heuristik $h(n)$ untuk mengarahkan pencarian lebih cepat.

---

## 6. Referensi Pendukung
Jika Anda ingin melihat implementasi visual dan penjelasan alternatif, berikut beberapa referensi otoritatif:
- [Artificial Intelligence: A Modern Approach by Stuart Russell and Peter Norvig](http://aima.cs.berkeley.edu/) (Buku Teks Standar Industri AI).
- [YouTube: Gate Smashers - Uniform Cost Search](https://www.youtube.com/watch?v=dRMvK76xQJI) (Untuk pemahaman konseptual yang cepat).
- Dalam ilmu komputer tradisional (bukan konteks pencarian state-space AI), Uniform Cost Search pada dasarnya merupakan varian dari **Dijkstra's Algorithm** di mana pencarian berhenti segera setelah satu titik tujuan khusus ditemukan.