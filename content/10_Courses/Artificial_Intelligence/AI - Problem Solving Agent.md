---
title:
  - Problem Solving Agent
type: Lecture
course:
  - Artificial Intelligence
topic:
  - Problem Solving Agent
semester: 4
tags:
  - artificial-intelligence
status: 🌳 evergreen
created: 2026-04-13
week: 3
---

# Problem Solving Agent: Sebuah Panduan Komprehensif

> [!abstract] Ringkasan Eksekutif
> Materi ini membahas secara mendalam tentang **Problem Solving Agent** dalam Kecerdasan Buatan (AI), dibangun dari prinsip-prinsip dasar (*first-principles*). Kita akan membedah mekanismenya mulai dari perumusan tujuan hingga eksekusi, lengkap dengan analogi dan simulasi kasus dunia nyata.

---

## 1. Fondasi: Apa itu Problem Solving Agent?

Dalam paradigma Kecerdasan Buatan, agen adalah entitas yang mengamati lingkungannya (melalui sensor) dan bertindak atas lingkungan tersebut (melalui aktuator). 

**Problem Solving Agent (Agen Pemecah Masalah)** adalah jenis agen spesifik yang menggunakan teknik pencarian (*search techniques*) untuk menyelesaikan masalah dalam upaya mencapai tujuan tertentu.

### Mengapa Termasuk *Goal-Based Agent*?

> [!info] Definisi: Goal-Based Agent
> Agen yang tidak hanya bereaksi terhadap kondisi lingkungan saat ini, tetapi juga memiliki informasi tentang keadaan yang diinginkan (tujuan/goal) dan memilih tindakan yang membawanya lebih dekat ke tujuan tersebut.

Problem Solving Agent secara inheren adalah **Goal-Based Agent** (Agen Berbasis Tujuan) karena:
1. **Fokus pada Hasil Akhir:** Agen ini tidak memiliki sekumpulan aturan kondisi-aksi (seperti *reflex agent*). Ia diberikan *state* (keadaan) akhir yang harus dicapai, dan tugasnya adalah mencari tahu *bagaimana* mencapainya.
2. **Perencanaan (Planning):** Ia mempertimbangkan dampak dari urutan tindakan di masa depan sebelum mengambil langkah pertama. Tindakannya tidak instan, melainkan hasil kalkulasi kognitif untuk mencocokkan *current state* (keadaan saat ini) dengan *goal state* (keadaan tujuan).

---

## 2. Analogi Intuitif: Perjalanan ke Kota yang Belum Pernah Dikunjungi

Mari gunakan pemikiran *first-principles* melalui sebuah analogi sederhana.

Bayangkan Anda berada di Jakarta dan ingin pergi ke sebuah desa terpencil di Jawa Tengah (Selo), tetapi Anda **tidak tahu jalannya** dan tidak ada GPS aktif yang memberi instruksi *turn-by-turn*. Anda hanya memiliki sebuah peta kertas.

1. **Perumusan Tujuan (Goal Formulation):** Anda memutuskan, "Saya ingin berada di Desa Selo." Ini adalah tujuan yang mengarahkan semua tindakan selanjutnya. Tanpa ini, Anda hanya akan mengemudi tanpa arah.
2. **Perumusan Masalah (Problem Formulation):** Anda melihat peta kertas Anda. Anda mengidentifikasi:
   - *Keadaan awal (Initial State):* Saya di Jakarta.
   - *Tindakan yang mungkin (Actions):* Saya bisa mengambil Tol Cipali, Tol Cipularang, atau jalur Pantura.
   - *Keadaan Transisi (Transition Model):* Jika saya di Jakarta dan mengambil Tol Cipali, saya akan sampai di Cirebon.
   - *Biaya (Path Cost):* Jarak tempuh, waktu, atau biaya tol.
3. **Pencarian (Searching):** Anda duduk di mobil, belum menyalakan mesin. Anda menelusuri rute di peta dengan jari Anda. "Jika lewat Pantura, macet. Jika lewat Cipali, sampai Semarang, lalu belok ke Boyolali... Ah, ini rute terpendek!" Anda menyimulasikan perjalanan di kepala Anda sebelum benar-benar bergerak.
4. **Eksekusi (Execution):** Setelah rute lengkap (solusi) ditemukan di kepala/peta, Anda menyalakan mobil dan mulai menyetir mengikuti urutan langkah yang sudah Anda temukan tadi.

---

## 3. Mekanisme Kognitif: Empat Langkah Problem Solving

Secara formal, Problem Solving Agent beroperasi dalam siklus empat fase yang ketat. Asumsi dasarnya adalah lingkungan bersifat *observable* (dapat diamati sepenuhnya), *discrete* (langkah-langkahnya jelas), *deterministic* (hasil dari suatu tindakan dapat dipastikan), dan *static* (lingkungan tidak berubah saat agen sedang berpikir).

### A. Perumusan Tujuan (Goal Formulation)

Ini adalah langkah pertama dan paling krusial. Tujuan membatasi ruang lingkup apa yang harus dipikirkan oleh agen.
- **Definisi:** Proses menetapkan keadaan (state) atau sekumpulan keadaan yang ingin dicapai oleh agen.
- **Fungsi:** Mengorganisir perilaku agen dengan menyaring bagian-bagian lingkungan dan tindakan yang tidak relevan dengan tujuan.
- *Contoh:* Dalam catur, tujuannya adalah *checkmate* (skakmat) raja lawan, bukan memakan pion sebanyak-banyaknya.

### B. Perumusan Masalah (Problem Formulation)

Setelah tujuan ditetapkan, agen harus mendefinisikan masalah secara matematis agar bisa diselesaikan oleh algoritma komputer. Sebuah masalah secara formal didefinisikan oleh 5 komponen:

> [!note] Komponen Masalah Formal
> 1. **Initial State ($S_0$):** Keadaan agen saat masalah dimulai.
> 2. **Actions($s$):** Fungsi yang mengembalikan himpunan tindakan yang dapat dilakukan pada keadaan $s$.
> 3. **Transition Model / Result($s, a$):** Fungsi yang mengembalikan keadaan baru yang dihasilkan dari melakukan tindakan $a$ pada keadaan $s$.
> 4. **Goal Test:** Kondisi yang menentukan apakah keadaan saat ini adalah keadaan tujuan.
> 5. **Path Cost / Action Cost ($c(s, a, s')$):** Fungsi yang memberikan biaya numerik untuk melakukan tindakan $a$ dari state $s$ ke state $s'$.

Ruang dari semua state yang mungkin dikunjungi disebut **State Space**.

### C. Pencarian (Searching)

Ini adalah fase "berpikir". Agen menggunakan algoritma pencarian untuk mengeksplorasi *state space* berdasarkan *problem formulation* di atas.
- **Proses:** Agen membangun **Search Tree** (pohon pencarian). Akar pohon adalah *Initial State*. Cabang-cabangnya diciptakan dengan mengaplikasikan *Actions* pada state (proses ini disebut *expanding* a node).
- **Output:** Sebuah urutan tindakan (sequence of actions) dari *Initial State* ke *Goal State*. Urutan ini disebut **Solusi**. Jika solusi meminimalkan *Path Cost*, itu disebut **Solusi Optimal**.
- **Kompleksitas:** Pencarian sering diukur kinerjanya menggunakan notasi Big-O. Sebagai contoh, Breadth-First Search (BFS) memiliki kompleksitas waktu dan ruang sebesar $O(b^d)$, di mana $b$ adalah *branching factor* (jumlah maksimum penerus/cabang dari sebuah node) dan $d$ adalah kedalaman (*depth*) dari solusi yang paling dangkal.

### D. Eksekusi (Execution)

Setelah algoritma pencarian mengembalikan sebuah urutan solusi (array tindakan), agen berhenti berpikir dan mulai bertindak.
- Agen mengeksekusi tindakan pertama dalam urutan solusi.
- Kemudian melanjutkan ke tindakan kedua, dan seterusnya, tanpa perlu mengevaluasi lingkungan lagi (karena asumsi lingkungan *static* dan *deterministic*).

---

## 4. Simulasi Kasus: "The Vacuum World" (Langkah-demi-Langkah)

Mari kita lihat bagaimana logika ini bekerja secara *real-time* menggunakan permasalahan klasik AI: **Dunia Penghisap Debu (Vacuum World)**.

**Konteks Lingkungan:**
- Hanya ada 2 kotak berdekatan: Kotak A (kiri) dan Kotak B (kanan).
- Setiap kotak bisa dalam keadaan Bersih (Clean) atau Kotor (Dirty).
- Robot *vacuum* bisa berada di A atau B.

### Langkah 1: Goal Formulation
**Tujuan:** Semua kotak harus dalam keadaan bersih (Clean). Tidak peduli robot akhirnya berada di kotak mana.

### Langkah 2: Problem Formulation
- **Initial State:** Robot berada di Kotak A. Kotak A Kotor, Kotak B Kotor. Representasi: `[In:A, A:Dirty, B:Dirty]`
- **Actions:** Ada tiga tindakan yang mungkin:
  1. `Left` (Pindah ke kiri)
  2. `Right` (Pindah ke kanan)
  3. `Suck` (Menghisap debu di kotak saat ini)
- **Transition Model (Result):**
  - Jika `Result([In:A, A:Dirty, B:Dirty], Suck)` $\rightarrow$ `[In:A, A:Clean, B:Dirty]`
  - Jika `Result([In:A, A:Clean, B:Dirty], Right)` $\rightarrow$ `[In:B, A:Clean, B:Dirty]`
- **Goal Test:** Apakah `A == Clean` DAN `B == Clean`?
- **Path Cost:** Setiap tindakan (Left, Right, Suck) memiliki biaya = 1. Kita ingin meminimalkan total langkah yang diambil.

### Langkah 3: Searching (Membangun Search Tree)

Agen tidak bergerak secara fisik. Ia melakukan simulasi di dalam "otaknya".

> [!example] Iterasi Search Tree
> **Node Root (Awal):** `Node0: [In:A, A:Dirty, B:Dirty]`
> *Apakah Node0 adalah Goal? Tidak.*
> 
> **Expand Node0 (Terapkan semua Action yang mungkin):**
> - *Action 'Left':* Tabrak tembok, state tidak berubah $\rightarrow$ `[In:A, A:Dirty, B:Dirty]` (Abaikan, karena menyebabkan looping)
> - *Action 'Right':* Pindah ke B $\rightarrow$ `Node1: [In:B, A:Dirty, B:Dirty]`
> - *Action 'Suck':* Bersihkan A $\rightarrow$ `Node2: [In:A, A:Clean, B:Dirty]`
> 
> *Algoritma pencarian akan memeriksa Node1 dan Node2.*
> *Apakah Node1 atau Node2 Goal? Tidak.*
> 
> **Expand Node2 (Fokus pada jalur yang paling menjanjikan/logis):**
> - *Action 'Right':* Pindah ke B $\rightarrow$ `Node3: [In:B, A:Clean, B:Dirty]`
> - *Action 'Suck':* A sudah bersih $\rightarrow$ (Abaikan, biaya terbuang percuma)
> 
> *Apakah Node3 adalah Goal? Tidak.*
> 
> **Expand Node3:**
> - *Action 'Left':* Kembali ke A $\rightarrow$ (Abaikan, mundur)
> - *Action 'Suck':* Bersihkan B $\rightarrow$ `Node4: [In:B, A:Clean, B:Clean]`
> 
> **Evaluasi Node4:**
> *Apakah Node4 adalah Goal Test?* Ya! `A:Clean` dan `B:Clean`.

**Solusi Ditemukan:** Algoritma menelusuri balik jalan dari Node4 ke Node Root.
- **Urutan Tindakan (Solusi):** `[Suck, Right, Suck]`
- **Total Path Cost:** 3 langkah.

### Langkah 4: Execution

Sekarang, setelah "berpikir" selesai, barulah robot secara fisik bergerak di dunia nyata:
1. Mengaktifkan mesin penghisap di Kotak A (`Suck`).
2. Menggerakkan roda ke kanan menuju Kotak B (`Right`).
3. Mengaktifkan mesin penghisap di Kotak B (`Suck`).

> [!success] Kesimpulan
> Problem Solving Agent mengubah masalah kognitif abstrak menjadi urutan operasi matematis yang terstruktur. Dengan memisahkan fase *Searching* (berpikir secara proaktif dalam *state space*) dari *Execution* (bertindak secara reaktif di dunia nyata), agen ini dapat menjamin menemukan solusi optimal tanpa perlu melakukan metode *trial-and-error* yang mungkin sangat mahal atau berbahaya jika dilakukan secara fisik.
