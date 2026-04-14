---
title:
  - Intelligent Agent
type: Lecture
course:
  - Artificial Intelligence
topic:
  - Intelligent Agent
semester: 4
tags:
  - intelligent-agent
  - rational-agent
  - PEAS
  - agent-types
  - environment
  - artificial-intelligence
status: 🌳 evergreen
created: 2026-03-10
week: 2
---

# Intelligent Agent

**Reference:** S. Russell & P. Norvig, *Artificial Intelligence: A Modern Approach*
**Source:** [[(AI-3) Intelligent Agent.pdf]]

---

## Daftar Isi

1. [[#1. Konsep Dasar Agen]]
   - [[#1.1 Definisi Agen]]
   - [[#1.2 Komponen Agen]]
   - [[#1.3 Rational Agent]]
2. [[#2. Lingkungan Agen (Task Environment — PEAS)]]
   - [[#2.1 Jenis-Jenis Lingkungan]]
3. [[#3. Merancang Agen Cerdas]]
   - [[#3.1 Agent Function dan Agent Program]]
   - [[#3.2 Contoh: VacuumCleaner World]]
4. [[#4. Karakteristik Agen]]
5. [[#5. Arsitektur dan Tipe Agen]]
   - [[#5.1 Arsitektur Agen]]
   - [[#5.2 Tipe Agen]]
6. [[#Summary — Key Concepts at a Glance]]

---

## 1. Konsep Dasar Agen

### 1.1 Definisi Agen

> [!abstract] Definisi Agen
> Menurut **Russell dan Norvig**, agen adalah segala sesuatu yang dapat mempersepsikan (*perceiving*) lingkungannya melalui sejumlah **sensor**, lalu bertindak (*action*) terhadap lingkungan tersebut menggunakan **aktuator**.
> 
> Menurut **Wooldridge**, agen adalah sebuah sistem komputer yang berada dalam suatu lingkungan dan mampu bertindak secara *autonomous* sesuai dengan sasaran yang dirancang.

Sebuah **[[Intelligent Agent]]** secara khusus adalah perangkat lunak yang bekerja tanpa campur tangan langsung manusia untuk melaksanakan tugas, mengambil tindakan tertentu, atau membuat keputusan — berdasarkan pengetahuan bawaan (*built-in*) dan data dari lingkungannya.

> [!example] Contoh Nyata Agen Cerdas
> - Filter spam di Gmail
> - Filter harga termurah di situs belanja / tiket
> - Antivirus SmadAV yang mendeteksi virus dan menyarankan *scan* secara otomatis

### 1.2 Komponen Agen

Setiap agen memiliki empat komponen inti yang saling berinteraksi dengan lingkungan:

| Komponen | Penjelasan | Contoh (Manusia) | Contoh (Robot) |
|---|---|---|---|
| **Sensor** | Alat untuk mempersepsikan lingkungan | Mata, telinga, hidung | Kamera, infrared |
| **Percept** | Input yang ditangkap dari sensor pada satu waktu tertentu | Melihat mobil di depan | Frame video |
| **Percept Sequence** | Sejarah seluruh input yang pernah diterima agen | Semua pengalaman hidup | Log sensor |
| **Actuator** | Alat untuk melakukan tindakan | Tangan, kaki, mulut | Lengan robot, motor |
| **Action** | Tindakan yang dikeluarkan melalui aktuator | Mengerem, bicara | Menggerakkan lengan |

> **Pertanyaan kunci:** Komponen di atas belum cukup — kita harus mendefinisikan **tujuan** (goal) dari si agen. *"Si agent ini mau ngapain sih?"*

### 1.3 Rational Agent

> [!info] Rational ≠ Sempurna (Omniscient)
> **Rasional** berarti melakukan hal yang *terbaik* berdasarkan informasi yang dimilikinya saat itu — bukan berarti ia maha tahu atau sempurna, karena ada batasan persepsi atau aspek lingkungan yang di luar kendali.

Sebuah **[[Intelligent Agent#Explanation|Rational Agent]]** adalah agen yang selalu memilih tindakan yang diharapkan dapat **memaksimalkan ukuran kinerjanya** (*performance measure*), dengan mempertimbangkan semua pola *percept sequence* dan pengetahuan yang dimilikinya.

**Goal** (tujuan) harus diukur secara kuantitatif melalui matriks ***performance measure***. Contoh:

| Goal | Performance Measure |
|---|---|
| Lulus kuliah | IPK / Nilai Ujian |
| Cepat kaya | Saldo di rekening bulanan |
| Juara liga | Poin kemenangan klasemen |

Agen dikatakan **autonomous** jika interaksi dan perilakunya juga bergantung dan ditentukan oleh *pengalaman pembelajarannya sendiri*, bukan murni pada pengetahuan program bawaan pembuatnya.

---

## 2. Lingkungan Agen (Task Environment — PEAS)

Sebelum merancang agen, kita harus mendefinisikan **Task Environment** lingkungan agen tersebut menggunakan terminologi kerangka **PEAS**:

> [!abstract] Kerangka PEAS
> - **P**erformance measure — metrik kriteria keberhasilan agen
> - **E**nvironment — lokasi dan kondisi batasan di sekitar agen
> - **A**ctuators — apa saja medium agen untuk mengubah lingkungan
> - **S**ensors — apa saja yang menjadi indra input agen

> [!example] Contoh PEAS: Taksi Otomatis
> 
> | PEAS | Isi |
> |---|---|
> | Performance | Tiba di tujuan, tidak tabrakan/melanggar lalu lintas, penumpang nyaman, waktu cepat |
> | Environment | Jalan raya, persimpangan, pejalan kaki, kondisi cuaca |
> | Actuators | Sistem kemudi, pedal gas, rem, klakson, indikator sein |
> | Sensors | Kamera video, detektor jarak (lidar/sonar), GPS, accelerometer |

> [!example] Contoh PEAS: Medical Diagnosis System
> 
> | PEAS | Isi |
> |---|---|
> | Performance | Pasien berhasil sembuh, meminimalisir biaya, mitigasi tuntutan hukum pasien |
> | Environment | RS/Klinik, catatan kesehatan pasien, ketersediaan dokter/suster |
> | Actuators | Tampilan layar dengan instruksi (diagnosa resep, observasi lanjutan) |
> | Sensors | Input sentuh form gejala dari pengguna (jawaban observasi pasien) |

### 2.1 Jenis-Jenis Lingkungan

Ada 6 dimensi yang digunakan untuk mengklasifikasikan lingkungan agen:

**1. Fully Observable vs. Partially Observable**
Lingkungan *fully observable* jika sensor agen dapat mengakses **keseluruhan keadaan** lingkungan yang relevan dengan pemilihan aksi — sehingga agen tidak perlu menyimpan state internal. Sebaliknya, *partially observable* terjadi akibat gangguan/ketidakakurasian sensor atau bagian lingkungan yang tidak terdeteksi.

**2. Deterministic vs. Stochastic**
*Deterministic*: keadaan selanjutnya **sepenuhnya ditentukan** oleh keadaan sekarang dan aksi agen. *Stochastic*: kebalikannya — ada unsur ketidakpastian. Catatan khusus: jika lingkungan deterministic kecuali untuk aksi agen lain, disebut *strategic*.

**3. Episodic vs. Sequential**
*Episodic*: setiap episode (perceive → aksi) berdiri **sendiri**, tidak bergantung episode sebelumnya — lebih sederhana karena tidak perlu perencanaan ke depan. *Sequential*: tindakan sekarang **mempengaruhi** tindakan selanjutnya.

**4. Static vs. Dynamic**
*Static*: lingkungan **tidak berubah** saat agen berpikir/memilih aksi. *Dynamic*: lingkungan bisa berubah sewaktu agen sedang mengambil keputusan. Ada juga *semidynamic*: lingkungan tidak berubah, tapi skor/kemampuan agen berubah seiring waktu.

**5. Discrete vs. Continuous**
*Discrete*: persepsi dan aksi **terbatas dan terdefinisi jelas** (contoh: catur, Reversi). *Continuous*: nilai state dan aksi berubah secara terus-menerus (contoh: taksi, mobil otonom).

**6. Single Agent vs. Multi Agent**
*Single agent*: hanya ada satu agen (contoh: solver teka-teki silang). *Multi agent*: lebih dari satu agen berinteraksi, bisa kooperatif atau kompetitif (contoh: catur, permainan Reversi).

**Tabel klasifikasi contoh task environments:**

| Task Env. | Observable | Agent | Deterministic | Episodic | Static | Discrete |
|---|---|---|---|---|---|---|
| Chess with clock | Fully | Multi | Deterministic | Sequential | Semi | Discrete |
| Image analysis | Fully | Single | Deterministic | Episodic | Semi | Continuous |
| Taxi driving | Partially | Multi | Stochastic | Sequential | Dynamic | Continuous |
| Medical diagnosis | Partially | Single | Stochastic | Sequential | Dynamic | Continuous |
| English Tutor | Partially | Multi | Stochastic | Sequential | Dynamic | Discrete |

---

## 3. Merancang Agen Cerdas

Sebelum membuat agen, perlu diketahui dengan baik:
1. Semua kemungkinan **percept dan aksi** yang dapat diterima/dilakukan agen
2. **Tujuan atau performance measure** yang ingin dicapai
3. **Lingkungan** di mana agen akan dioperasikan

Tindakan yang tepat adalah tindakan yang akan menyebabkan agen **paling sukses** — diukur secara kuantitatif.

### 3.1 Agent Function dan Agent Program

> [!abstract] Definisi Fungsi Sistem
> **Agent function** adalah fungsi abstrak matematis yang memetakan histori komulatif percept (*percept sequence* $\mathcal{P}^*$) ke dalam sebuah keputusan/aksi ($\mathcal{A}$):
> $$f: \mathcal{P}^* \rightarrow \mathcal{A}$$
> 
> **Agent program** adalah implementasi kode riil dari fungsi tersebut yang dijalankan di atas sebuah komputasi fisik atau substrat perangkat lunak (*Architecture*):
> $$\text{Agent} = \text{Architecture} + \text{Program}$$

### 3.2 Contoh: VacuumCleaner World

Task environment vacuum cleaner dengan dua ruangan (A dan B):

| PEAS | Isi |
|---|---|
| Performance | Menjaga kebersihan |
| Environment | Ruangan A dan B beserta debunya |
| Actuators | DoKeKiri, DoKeKanan, DoSedot, DoSantai |
| Sensors | Lokasi dan status, contoh: [A, Kotor] |

**Agent function (AgenRajin™):**
```
function AgenRajin(status, lokasi) return action
  if status = kotor then return DoSedot
  else if lokasi = A then return DoKeKanan
  else return DoKeKiri
```

**Agent function (AgenMalas™):**
```
function AgenMalas(status, lokasi) return action
  if status = kotor then return DoSedot
  else if random(1.0) >= 0.8 then return DoSantai
  else if lokasi = A then return DoKeKanan
  else return DoKeKiri
```

> **Mana yang lebih rasional?** Tergantung pada definisi goal "menjaga kebersihan" dan sifat lingkungan — apakah ruangan yang sudah bersih bisa kotor lagi? Seberapa cepat? Apakah ada syarat hemat energi?

---

## 4. Karakteristik Agen

Agen cerdas memiliki 8 karakteristik utama:

| # | Karakteristik | Penjelasan |
|---|---|---|
| 1 | **Autonomous** | Bertindak dan memutuskan secara mandiri tanpa intervensi luar |
| 2 | **Reaktif** | Cepat beradaptasi terhadap perubahan informasi di lingkungan |
| 3 | **Proaktif** | Berorientasi tujuan; selalu mengambil inisiatif untuk mencapai goal |
| 4 | **Fleksibel** | Memiliki banyak cara untuk mencapai tujuannya |
| 5 | **Robust** | Dapat kembali ke kondisi semula setelah mengalami kegagalan |
| 6 | **Rasional** | Bertindak sesuai tugas dan pengetahuan, menghindari konflik tindakan |
| 7 | **Social** | Mampu berkomunikasi dan berkoordinasi dengan manusia atau agen lain |
| 8 | **Situated** | Harus berada dan berjalan di lingkungan tertentu |

---

## 5. Arsitektur dan Tipe Agen

### 5.1 Arsitektur Agen

**1. Black Box**
Agen menerima percept dari luar → memproses → menghasilkan aksi. Model Brenner mencakup tahapan: *interaction → information fusion → information processing → action*.

**2. BDI (Belief-Desire-Intention)**
Model arsitektur yang lebih kaya secara kognitif:
- **Belief**: pengetahuan/informasi yang dimiliki agen tentang lingkungannya
- **Desire**: tujuan atau tugas yang ingin dicapai
- **Intention**: rencana-rencana konkret untuk mencapai desire

### 5.2 Tipe Agen

Ada 5 tipe agen yang menggambarkan tingkat kecerdasan dari paling sederhana ke paling kompleks:

**1. Simple Reflex Agent**
Tipe paling sederhana — hanya menerapkan aturan *kondisi-aksi* (if-then). Agen mecocokkan percept dengan aturan statik, lalu mengeksekusinya tanpa memori historis.
> [!example] Contoh Taksi Otomatis
> "Jika kamera melihat lampu merah di *frame* sekarang (percept) $\rightarrow$ injak rem purna (aksi)."

**2. Model-Based Reflex Agent**
Menambahkan **model internal** keadaan (state) tentang cara dunia nyata beroperasi. Agen menjaga *memory log* berdasarkan input untuk terus memperbarui apa yang kini tak lagi nampak sehingga tangguh di lingkungan *partially observable*.
> [!example] Contoh Taksi Otomatis
> Kamera terhalang truk pickup, tapi taksi *mengingat* ada pengendara motor di depan sisi truk tersebut dari 3 detik lalu, sehingga ia tidak menyalip.

**3. Goal-Based Agent**
Mengadopsi informasi deskriptor tujuan (goal). Agen merencanakan rentetan urutan tindakan *future oriented*. Melibatkan model pencarian rute (*search*) dan strategi (*planning*).
> [!example] Contoh Taksi Otomatis
> Taksi memikirkan urutan gerensi simulasi rute (belok kiri, lurus 2km, belok simpang layang) agar tiba di bandara titik X.

**4. Utility-Based Agent**
Mencapai tujuan tak lantas membuat aksi ini "paling" optimal. Agen mengevaluasi **utility factor** (kuantitatif nilai profit vs risk) demi opsi absolut *terbaik* di antara rentetan iterasi alternatif tujuan.
> [!example] Contoh Taksi Otomatis
> Ada 3 probabilitas jalur layang menuju bandara. Taksi menempuh rute tol B—meski lebih jauh putaran km-nya, statistik historisnya lengang/mulus, sehingga rasio estimasi efisiensi waktu vs *wear and tear* (utility) maksimal tinggi.

**5. Learning Agent**
Agen bertransisi mempelajari probabilitias **pengalaman di lapangan** dan menyesuaikan parameter sistemnya. Terkomposisi akan *learning element*, *performance element*, modul *critic*, dan abstraksi *problem generator*.
> [!example] Contoh Taksi Otomatis
> Taksi melaju lambat di salju basah namun memicu rem ABS terselip *(error feedback/critic)*. Ia berevolusi *(learning elemen)* memodifikasi standar rasio akselerator-rem jika sistem hidrologi radar mendeteksi cuaca bersalju esok harisnya.

**Hierarki tipe agen (dari paling sederhana ke paling cerdas):**
Simple Reflex → Model-Based → Goal-Based → Utility-Based → Learning → Multi-Agent Systems

---

## Summary — Key Concepts at a Glance

| Konsep | Definisi |
|---|---|
| Agent | Entitas yang mempersepsikan lingkungan via sensor dan bertindak via aktuator |
| Percept | Input yang ditangkap sensor pada satu waktu |
| Percept Sequence | Sejarah seluruh input agen |
| Rational Agent | Agen yang memaksimalkan performance measure berdasarkan percept dan pengetahuannya |
| PEAS | Kerangka mendefinisikan task environment: Performance, Environment, Actuators, Sensors |
| Fully Observable | Sensor dapat mengakses seluruh keadaan lingkungan yang relevan |
| Deterministic | Keadaan selanjutnya sepenuhnya ditentukan keadaan sekarang + aksi agen |
| Episodic | Setiap episode berdiri sendiri, tidak mempengaruhi episode berikutnya |
| Simple Reflex Agent | Agen yang hanya menggunakan aturan kondisi-aksi (if-then) |
| Model-Based Agent | Agen yang menjaga model internal dari lingkungan |
| Goal-Based Agent | Agen yang merencanakan aksi untuk mencapai tujuan tertentu |
| Utility-Based Agent | Agen yang memilih aksi terbaik berdasarkan nilai utility kuantitatif |
| Learning Agent | Agen yang belajar dari pengalaman untuk meningkatkan kinerjanya |
| BDI | Arsitektur agen: Belief (pengetahuan), Desire (tujuan), Intention (rencana) |
| Autonomous | Perilaku agen ditentukan pengalaman sendiri, bukan hanya instruksi pembuatnya |

---

## Questions (Active Recall)

> [!question]- 1. Apa perbedaan mendasar antara *goal-based agent* dan *utility-based agent* jika keduanya sama-sama memiliki tujuan?
> *Goal-based* hanya peduli memastikan sebuah kondisi tujuan **tercapai** (berhasil vs gagal murni). *Utility-based* memedulikan optimisasi **kualitas** pencapaian proses tersebut (seberapa besar untung/efisiennya jika tujuan digapai rute A dibanding rute B).

> [!question]- 2. Bagaimana cara merancang matriks *performance measure* yang presisi mengukur tujuan kita, bukan menduplikasi proxy nilainya?
> Metrik ukuran murni semestinya mendata dan mengevaluasi apa hal **aktual/objektif yang dimodifikasi pada lingkungan nyata**, *bukan aktivitas internal/frekuensi pergerakan* dari agen itu. (Cth: Performa diukur lewat persentase lantai bersih dari kotoran mikroba. Bukan metrik debu internal yang ditelan tangki, karena agen *bisa saja meludah sampah demi menghisapnya berulang-ulang*).

> [!question]- 3. Dalam agen di dimensi lingkungan eksternal gabungan *partially observable* dan *stochastic*, strategi hybrid fungsional apa yang ideal diimplantasikan?
> Konfigurasi hierarki internal harus menyusun implementasi *minimal* **Model-Based** (untuk merotasi log state observasi lingkungan tertutup radar) sekaligus terjalin model fungsi **Utility-Based Atau Probabilistik** (mengevaluasi pohon rentetan probabilitas aksi tertinggi di tengah respons semesta dunia yang belum 100% absolut taksirannya).

> [!question]- 4. Mungkinkah heuristik AgenMalas™ secara teori lebih merengkuh aspek ekuilibrium rasionalitas daripada AgenRajin™ ? Korelasi lingkungan seperti apakah parameternya?
> Mutlak berlaku. Semisal kalkulasi ekuasi fungsi agen dikenakan penalti/biaya setiap meter ia bermanuver (kuras baterai dsb), dan siklus emisi distribusi kotoran terlampau minimal—aksi stagnan pasif ritme (`DoSantai`) memastikan akumulasi matriks *Performance Measure* mengunggulkan robot agen vakum yang beristirahat mayoritas temporal disbanding bermanuver mengelilingi lantai *clean room*.

> [!question]- 5. Model arsitektur abstrak BDI berpisah landasan teknis dibanding arsitektur taksonomi tipe agen lain lewat diferensiasi apa?
> Skema taksonomi model rasional *BDI* lebih mencerminkan replikasi komparatif dari komputasi antropologi/psikologi sistem kognitif perancangan manusia dalam memetakan model tak kasat: **Belief** (Realita peta apa yg diketahui sistem mengenai alam realitas yang memagarinya), **Desire** (Daftar *Objective State* hierarki yang melingkupinya), serta **Intention** (Modul urutan langkah pragmatis absolut konkret yang tereksekusi komitmennya hingga garis akhir komputasi).
