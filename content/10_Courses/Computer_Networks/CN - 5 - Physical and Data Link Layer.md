---
title:
  - Physical and Data Link Layer
type: Lecture
course:
  - Computer Networks
topic:
  - Physical Layer
  - Data Link Layer
semester: 4
tags:
  - college
  - computer-networks
  - osi-model
status: 🌿 incubating
created: 2026-04-02
---

# CN - 5 - Physical and Data Link Layer

%% **Reference:** Informatika UNS – Jaringan Komputer Genap 2025/2026 by Herdito Ibnu Dewangkoro %%
**Source:** [[(CN-5) Physical Layer dan Data Link Layer.pdf]]
%% **Prasyarat:** [[CN - 4 - Network Protocol Suite, Standard Organization, and Reference Model]] %%

---

## Daftar Isi

1. [[#1. Pengantar Physical Layer]]
2. [[#2. Karakteristik Operasional Physical Layer]]
3. [[#3. Media Transmisi Fisik]]
    - [[#3.1 Kabel Tembaga (Copper Cables)]]
    - [[#3.2 Kabel Fiber Optik]]
    - [[#3.3 Media Nirkabel (Wireless)]]
4. [[#4. Pengantar Data Link Layer]]
5. [[#5. Topologi Jaringan]]
6. [[#6. Struktur Data Link Frame]]
7. [[#Summary — Key Concepts at a Glance]]
8. [[#Active Recall Questions]]

---

## 1. Pengantar Physical Layer

**Physical Layer** (Layer 1 pada OSI Model) memiliki satu peran fundamental: menyediakan sarana fisik untuk mentransportasikan representasi bit informasi (0 dan 1) lintas jaringan dari *source* ke *destination*. Lapisan ini berada di paling bawah dari *network stack*.

### Mengapa Kita Membutuhkan Physical Connection?
Sebelum data logis apa pun dapat dikirim (seperti membuka halaman web atau mengirim pesan chat), host harus terhubung secara fisik (atau melalui konversi gelombang nirkabel) ke *local network*. Koneksi fisik ini bisa berupa kabel (misalnya *Ethernet cable*) atau koneksi *wireless* melalui **Network Interface Card (NIC)**. NIC inilah yang bertindak sebagai jembatan yang menghubungkan device ke network. Tergantung pada device, bisa terdapat multiple NIC—misalnya, satu NIC untuk koneksi jaringan kabel LAN dan satu lagi untuk koneksi *wireless* (Wi-Fi).

### Bagaimana Proses Komunikasi di Layer Ini? (Proses Enkapsulasi)
Physical Layer tidak peduli dengan alamat IP atau isi dari pesan. Fungsinya sangat mekanis:
1. Lapisan ini menerima sebuah **complete frame** dari Data Link Layer (Layer 2).
2. Lapisan ini kemudian melakukan **encoding** (pengkodean) frame tersebut ke dalam bentuk serangkaian sinyal. Sinyal ini dapat berupa variasi **voltage** (sinyal listrik pada kabel tembaga), **cahaya** (pulsa optik pada kabel *fiber*), atau gelombang **radio** (pada koneksi nirkabel).
3. Setelah di-*encode*, sinyal-sinyal ini ditransmisikan **satu per satu** melalui media fisik secara serial.
4. Pada sisi *destination node* dari aliran koneksi jaringan, Physical Layer menangkap sinyal-sinyal fisik tersebut dari media, memulihkannya kembali ke representasi *bit streams*, dan kemudian meneruskannya ke atas (ke Layer 2) sebagai sebuah *complete frame* kembali secara utuh.

---

## 2. Karakteristik Operasional Physical Layer

Agar transmisi *bit streams* berjalan dengan sukses, Physical Layer mengandalkan tiga area fungsional utama secara berurutan: **Physical Component**, **Encoding**, dan **Signaling**.

### Area Fungsional
1. **Physical Component**: Ini melibatkan objek *hardware* perantara komunikasi yang nyata (*Hardware device* seperti NIC, *interfaces*, konektor fisik, dan *cabling materials*). Desain tipe media/kabel, tipe isolasi tembaga materialnya, spesifikasi transmisi listrik semuanya diregulasi standarnya secara internasional terkait *physical layer component*.
2. **Encoding**: Jika komputer asal mengeluarkan 0 dan 1, bagaimana data akan mengenali bahwa transmisi tidak cacat? **Encoding** (atau *line encoding*) adalah metode operasional mengkonversi rentetan aliran data *bits* menjadi pola arus suatu "kode" format yang dapat diramal (*predictable*). Pola yang *predictable* ini membuat device penerima mampu menterjemahkan bitnya. Analoginya seperti *kode morse* menggunakan perpaduan tanda bunyi peluit "." dan "_". Sebagai contoh, dalam terminologi **Manchester Encoding**: representasi sinyal listrik yang berpindah/transisi dari tegangan (*voltage*) yang *high* ditarik turun menuju *low voltage* maka mesin akan mencatatnya sebagai representasi bit "**0**". Sebaliknya, transisi mendaki *low* ditarik menuju *high voltage* dibaca bit "**1**".
3. **Signaling**: Ini adalah metode wujud fisik sinyal mempresentasikan media tersebut. Lapisan ini mem-*generate* pancaran fisis nyata *wireless, electric, atau optical*. Metode *Signaling* memodulasi gelombang ke berbagai metode, di antaranya transmisi **Digital Signal**, **Amplitude Modulation (AM)**, **Frequency Modulation (FM)**, atau **Phase Modulation (PM)**.

### Konsep Bandwidth Terminology
Selain area di atas, ada sebuah terminologi limitasi daya tampung dari spesialis perangkat fisis yang terangkum:
- **Bandwidth**: Kapasitas teoretis penuh suatu media perantara dalam mengangkut aliran membawa data. Ia mengukur seberapa banyak volume laju *bits* yang direpresentasikan maksimal dapat dipancarkan ditransmisikan dalam durasi satu detik (contoh: Mbps, Gbps, dll.). Sifat media fisik, teknologi perangkat rilis kekinian, dan hukum fisika konduktor berperan membetuk seberapa ukuran dasar kapastitas bandwidth aslinya. Jika arus penguna melebihi batas, maka lalu lintas padat ini berubah fenomena tersendat **congestion** (kemacetan paket).
- **Latency**: Jumlah waktu keterlambatan riil yang berjalan (termasuk friksi waktu gesekan, hambatan *delay*, panjang rute jalan tarikan kabel) agar paket data dapat berpindah selesai berjalan dari *Satu Titik* sampai masuk sempurna ke stasiun pelabuhan *Titik yang lain*.
- **Throughput**: Jika *Bandwidth* adalah teori mulus idealnya, *Throughput* adalah rasio **Aktual** *transfer rate bits* melalui jalur tersebut. Seberapa mulus lalu lintas menyaingi jalan aslinya per sekon durasi riil.
- **Goodput**: Ini merepresentasikan parameter ukuran hasil transmisi nyata *bersih* pemindahan kumpulan serbuk bongkisan informasi utuh ke aplikasi antarmuka. *The strictly usable data*. Di dalam sistem komputer jaringan aslinya banyak sekali terisi tumpangan data penumpang sisipan "Pajak Jalan" overhead—semacam konfirmasi sesi *(acknowledgment)*, proses muat balik pengiriman yang rusak *resend packet*, maupun tag panjang header paket enkapsulasi itu sendiri, semua ini tidak terhitung bagian dari isi *Application message data*. Maka hitungannya: **Goodput = throughput – traffic overhead**. 

---

## 3. Media Transmisi Fisik

Fisik jaringan terdiri dari tembaga konduksi kelistrikan, kaca transmisi optikal laser pantulan, dan gelombang radiasi tanpa batas kawat di udara cerah. *Let's see deeply into their characteristics differences!*.

### 3.1 Kabel Tembaga (Copper Cables)

Ini adalah materi kawan lawas konvensional terpopuler sepanjang masa operasional masa kini. Inti kabel tembaga (*copper cables*) mengandalkan arus listrik dan sirkuit. Tembaga dipakai luas lantaran paling ramah di kantong rupiah, proses *skilled installation*-nya sangat membumi praktis, dibalut nilai keperuntukan hambatan *electrical resistance* / resistensi yang sangat baik di frekuensi kawat kabel ini mendistribusikan pulsa listrik.

Namun dia mendapati kelemahan fundamental:
- **Attenuation Limitasi**: Semakin renggang lintasan jauh sinyal *voltage* ini tersalurkan bergerak, gelombang setrumannya akan makin merosot layu melemah, alias menipis degradasi hilangnya voltase power sirkuit sinyal di kawat panjang.
- Sinyal tembaga luar biasa rentan sekali tercemar *corrupted polutan* kebisingan cuaca dari *External Interference*. Efek mendistorsi induksi gelombang menembus medan pembungkus merusak struktur sinyal transmisi aslinya dari bahaya kontaminasi **Electromagnetic Interference (EMI)** maupun frekuensi kebisingan tak terlihat dari gelombang silangan **Radio Frequency Interference (RFI)** perangkat kabel radio sekeliling area kawat.

**Tiga Jenis Variasi Desain Copper Data-Links:**
1. **Unshielded Twisted-Pair (UTP) Cable**: Mengawali kasta LAN, kabel jenis ini didesain termurah, ringkas dan universal sebagai punggung menyambungkan rakitan antar terminal komputer end-device ke *switching intermedietary/router*. UTP ini polos tanpa selimut pelindung *noise besi* sama sekali (*Unshielded*). Ia cerdas menetralisir efek kerugian bahaya *Crosstalk interference* dan radiasi pasif EMI internal ini menggunakan solusi jenius murahan: **"menjalin kawat berpelukan di dalam memilin" (Twisting)**. Pola lilit-pilin setiap kabel pasangannya yang beraliran warna spesifik didesain khusus agar gelombang magnetis yang keluar dari tiap pasang induksi saling membunuh arah (*Self Cancelling Effect)* menahan gelombang bocor. Kabel UTP lazimnya disokong ke lubang colokan *RJ-45 Connector.* Pada penyusunan soket warna susunan kabel bisa digunakan **Straight-Through Cable** *(device dari layer strata berbeda: misal Switch & PC)*, tapi di keadaan tipe mesin sesama kasta setara *peers device* (keduanya identik sama Router vs Router, maupun end-to-end laptop kawan peer) harus menyilangkan rute kabel khusus ke sambungan **Crossover Cable**.
2. **Shielded Twisted-Pair (STP) Cable**: Masih bersenjatakan kabel tembaga dipilin namun *upgrade* versi ekstra solid pelindung kebal (*Shielded*). Setiap kawat jalinan *twisted wires* dirangkap dan dibungkus selubung aluminium/lempengan metalik plat *(Foil lapisan baja tipis).* Menjadikannya tebal ganda pelindung khusus mereduksi total intrusi bahaya dari spektrum gangguan ekstrim EMI/RFI, jauh di atas tingkatan model *murahan* yang sebelumnya. Sayangnya ini sangat menguras ongkos pembahanan (Mahal), diameternya terlampau gendut rigid berat dikarenakan lapisan bajanya, serta harus memegang *careful termination process* ketika instalasi agar grounding sistem lapisan alumunium ini bekerja utuh.
3. **Coaxial Cable**: Adalah kakek leluhur teknologi konektivitas, kawatnya tersusun dengan sumbu melintang tembaga di pusat konduktor inti. Tetapi, tembaga di pusat konduktor diisolasi karet pelapis serta diselumbungi dengan lapisan cangkang luar berbentuk semacam "tabung anyaman berselubung tembaga *(Mesh metalic foil)* kawat". *Shielding layer* sirkuit ke-dua menutupi sekeliling melingkarkan selimut perisai memutar inti transmisi sinyal tembaga tersebut menjamin bebas polusi EMI/RFI, menjauhkan pantulan radiasi *outer space environment*. Berperan besar dipakai industri infrastruktur *TV Kabel/ Antena parabola nirkabel* di bubungan atap rumah pelanggan ISP *(Internet Service Providers)* model tipe Colokan BNC *type*.

### 3.2 Kabel Fiber Optik

Kabel *Fiber-Optic* ini adalah rahasia tulang punggung (backbone internet transkontinental bumi) karena arsitekturnya yang berlawanan alam dengan tembaga *copper elektrik*: ia membuang setrum dan bertransformasi sepenuhnya membawa sinyal biner dari merambat kedipan pendaran "Cahaya optik/Fotonik" murni. Gelombang melaju terpusat di perambatan kepingan silinder *core* benang silika di dalam tabung pantulan (*WaveGuide*) tabung cermin yang mulus jernih di dalam urat instalasinya sepanjang puluhan kilometer *panjang jarak ekstrem* tanpa menderita cacat kelesuan sinyal (super rendah ancaman hilangnya sinyal / *Attenuation* minim).
- Ia menawarkan fitur **Bandwidth yang mematikan dan tercepat ektrim**.
- Fiber tidak bekerja memancarkan *resistansi electrical hazard* alias tidak dialiri arus elektron setrum tegang, artinya fiber optik ini **Sepenuhnya kebal alias Secara total dan menyeluruh aman tanpa hembusan cacat akan "EMI & RFI" sekeras apapun induksi**. Kecepatan bisa berlari hingga melampaui rentan 100Gbps, menjadikannya de-facto dipakai titik pusat penghantar konektivitas antar-kampus (*distribution facilities*) maupun pelari kelautan internasional. Konsekuensinya ongkos pembengkakan yang meroket mahal dan dibutuhkan kesabaran merakit koneksi laser (*Skill instalasinya sangat kaku rumit dan rapuh*).

Variasi Fiber didesain kedalam mode dua wujud:
- **Single-Mode Fiber (SMF)**: Digunakan rentang jarak sangat epik berjuta meter transmisi konektivitas tanpa *repetisi ampli*, inti inti-tabung rongga pancarannya memuat *dimensi diameter nano micron yang sangat amat sempit padat.*  *Laser* mahal sebagai mesin pembuat sumber cahaya optik biner langsung dipancarkan menempuh lorong lurus linear tak berpendar. Jaketku selalu *Pembungkus Kuning.*
- **Multimode Fiber (MMF)**: Digunakan jangkauan sekitar 500meter (lingkungan perusahaan/internal kampus area LAN berkapasitas besar), Rongga inti ukurannya dilebarkan agar berkas cahaya murah meriah dari jenis *Lampu LED* biasa bisa dimasukan berpendar, membiarkan cahayanya di-dribble, menyebarkan tembakan sudut yang bergerak memantul tak seragam dari pinggiran tembok sirkulasi pantulannya lintasan ber-"Multi jalur zigzag". Dibungkus selimut ciri identik warna Orange / Aqua.

### 3.3 Media Nirkabel (Wireless)

Meskipun Fiber Optik kencang layaknya meteor bersinar di laut malam, dan tembaga UTP sangat merakyat, revolusi digital menuntut *mobility* manusia yang anti-kabel-statis. Wireless merambatkan *sinyal Electromagnetic pancaran frekuensi* / sinyal gelombang radio microwave tanpa harus direntang di tanah bumi, mentransformasikan sinyal terbang di belantara atmosfer.
Namun di balik merdekanya infrastruktur *deploy*, batasan *Limitation* Wireless memunculkan cacat bawaan:
- **Rentabilitas Area Jangkauan (Coverage Rate)**: Radius jangkauan udara sinyal gelombang ini fluktuatif akan pudar diintervensi oleh gundukan rintangan batasan ruang fisik di alam.
- **Rentan Crosstalk & Noise Radio Interference (Interferensi)**: Menggunakan frekuensi udara membebaskan udara ini direbut semua pihak. Rentan distorsi oleh pantauan radiasi perabot dapur microwave, *overlap bluetooth* sebelah bilik kantor, hingga pancaran alat gelombang yang bertetangga meracuni gelombang anda (*Corrupted Data*).
- **Zero Privacy *(Keamanan Security Riskan)***: Tanpa membutuhkan merobek colokan kabel dinding, entitas tetangga luar tembok area dengan alat penyadap *antenna packet analizer router sniffer* sudah bisa merenggut *Intercept stream paket wireless* ke ruang privat anda jika tidak digembok dengan perisai enkripsi password wpa2.
- **Batasan Bandwidth secara "Shared Medium & Half-Duplex"**: *Wireless* ibarat bicara ke publik perihal pembagian antrian jatah makan di ruangan aula terbatas. Perangkat keras *Wireless* (Access point / AP) menderita pola operasional arsitektur **Half Duplex**: (Antara bicara melempar *send* / Diam menyedot mendengar *Receive* bergantian ritmenya dan *satu device* hanya boleh bicara per selang giliran waktu sekon tanpa boleh membombardir serempak bersamaan). Saat Anda terikat menumpuk di konektivitas ruang rapat aula massal hotspot padat serentak ke satu router wifi ini (Banyak kawan kampus mengakses *WLAN / Wireless LAN segment Access Point yang sama* secara simultan), maka antrian gerbong ini berbenturan, dan Jatah Kuota kue Bandwidth koneksi melambat diperas dibagikan rata merosot turun tajam performa kecepatannya.

Berdasarkan variasi Standar peruntukan Wireless komite Industri (IEEE), mereka tertuang di reguler pembacaan L1/L2:
- *Wi-Fi (IEEE 802.11)*: Wireless lokal *WLAN / Wireless Access Point (AP)* dan *Wireless NIC Host adapter*.
- *Bluetooth (IEEE 802.15)*: *WPAN / Wireless Personal* area jarak sentuh personal radius mini meter.
- *WiMAX (IEEE 802.16)*: Konektivitas makro broadband *point-to-multipoint* di daratan.
- *Zigbee (IEEE 802.15.4)*: Ekosistem transmisi *bandwitdh redah lambat-data / irit tegangan batre terendah* (Internet of Things sensor paut di perabotan rumah lampu pintar / kulkas IOT).

---

## 4. Pengantar Data Link Layer

Perancangan internet tidak serta-merta melontarkan aliran IP mentah langsung jatuh menghujam aspal kabel tembaga begitu saja. *Data Link Layer* (Layer 2) ini merekayasa komunikasi khusus murni di level kartu jaringan. Pekerjaannya spesifik yakni: Mengatasi arus manajemen pergerakan antrean komunikasi dan identifikasi kontrol perlintasan hardware transmisi pertukaran di antar kepingan chip antarmuka permesinan **NIC (*Network Interface Card*)** yang bertetangga sejajar link langsung, mengepak bungkusan "Layer 3 *IP Packet*" ke dalam karung peti logistik brankas di layer miliknya yaitu wujud entitas **Layer 2 Frame** agar lolos meluncur disapu Physical Layer membasahi kabel, serta melengkapi fungsi pendeteksi mutlak pembongkaran penolakan barang "corrupt error" (Sistem *Deteksi Kesalahan bingkai/bingkaian data* merusak sisa *cacat frame* yang patah di aspal).

IEEE 802 mengklasifikasinya dari spesifikasi perangkat kaku ke otak arsitektur pembelahan Dua bagian *Data Link SubLayer* utama pendukung LAN:
- **LLC (Logical Link Control) Sublayer / IEEE 802.2**. Manajer penengah perangkat lunak (*Networking Software di L3*) ke perangkat keras *(di Driver hardware L1 / L2 Mac SubLayer)*.
- **MAC (Media Access Control) Sublayer**. Ini lapisan jendral lapangan yang bersinggungan ekstrim erat di wewenang lapisan perambatan konektor fisik Layer satu. Arsitek komando mengatur antrean etika kesepakatan media per-komunikasiannya (*Ethernet, WLAN Radio, dll*) agar giliran antrian frame transmisi menyeberangi sirkulasi Media Accessnya mulus.  

**Simfoni Perjalanan Data Router antar Media Fisik (The Node Hop)**
Ketika sebuah perjalanan paket jaringan merayapi area lintas benua interkoneksi benua router persilangan. *Format amplop Media fisikal perjalanannya* tidak seragam sejalan! (Kadang *Packet IPv4 Router Gateway lokal* ini dikirim lewat UTP kabel LAN di lantai 1; Namun, ketika ia merembet naik menembus dinding masuk *Switch lantai 2 gedung kampus* itu harus diubah *format spesifik enkapsulasi data amplop radikal* beralih berganti wahana melewati menara tiang transmisi selancar udara *Wireless Mac SubLayer WiMAX broadband*, masuk lagi tenggelam lewat trans samudera benua menaiki amplop karung enkapsulasi baru *Fiber Optic*) Perputaran wahana amplop sublayer MAC pengiriman ini berganti-ganti kemasan menyesuaikan media transport lokal yg spesifik pada etape "lompatan *Hops*" nya. Router di tengah estafet ini menunaikan tugas mutlak ritme 4 gerak:
1. Menangkap Frame kiriman bit gelombang asal yg menerjangnya tadi dari mulut kabel media jaringan pertama masuk ke pelukannya.
2. Membelah, Merobek, dan mende-konstruksi *De-enkapsulasi Header asalnya* membongkar wujud pelindung perantara luarnya memuntahkan perhiasan isinya memunculkan bentuk bongkahan kargo di dada hatinya yaitu: Inti dari *Layer 3 Encapsulated packet routing logis abstrak.*
3. *Inti Layer 3 Paket* ini ditelanjangi lantas **kembali dirakit ulang menanggalkan pakaian baru** ke dalam tubuh spesifikasi bungkus *Layer 2 MAC Frame baru* mematuhi regulasi kabel lingkungan perlintasan estafet sebelahnya yang bertolak berbeda spesifikasi model fisik jenis baru.
4. "Kargo amplop New Frame" disodorkan ke gerbang *Segment Media perlintasan Fisik ke dua berikutnya* (Siklus Forwarding transmisi). Estafet bergulir hinga menembus tujuan *destination receiver* sejati IP Address di Layer 3. 

---

## 5. Topologi Jaringan

Bagaimana sebidang kerangka tulang perangkat infrastruktur ditata di sepetak gedung arsitektural maupun dirunut jalan-raya abstrak? Hal ini didalami lewat pemetaan Topologi jaringan dua dimensi konsep persepektif ini:
- **Topologi Logis (*Logical Topology*)**: Cetak biru ini buta aksara soal kondisi ruang realita lokasi *server di gedung bertingkat lantai berapa* disingkirkan ke tempat sampah; Aliran Map pemetaannya lebih menganalisa rute maya virtual di dalam layar "Logis IP Addressing skema" penempatan rutenya. Ia memodelkan secara abstraksi cara lintasan paket data informasi pergerakan jalan virtual port alokasi IP Address antar jaringan host mesin. (*Murni untuk pemetaan sistem dan IP flow*).
- **Topologi Fisik (*Physical Topology*)**: Denah mandor konstruksional penempatan instalasi paku baut dan tata letak per-kabelan ke rak-rak lemari port soket perangkat rill di mata nyata. Mengidentifikasikan bagaimana piringan gulungan tarikan per-soket media kabel saling mengawinkan komputer dan perangkat persimpangan perangkat *Switching/router Intermediary port interface* mengokang susunannya yang nyata. Susunan instalasi real ini umumnya berkisar di model: Titik Terpusat persilangan hub kabel model ***Star*** dan bercabang menjadi ***Extended Star***. Maupun merangkul simpul menyusur membelah sepanjang aspal tulang punggung tiang kawat pusat di seberang pinggir aspal rel kabel ***Bus*** network, diterminasi matinya kedua ujung tali simpul kawatnya, hingga jalur putaran tertutup tetangga berpegangan sirkuler putaran roda tak bertepi model tipe ***Ring***.

---

## 6. Struktur Data Link Frame

Frame layer dua itu bukanlah tumpukan bit ampas di ujung kabel tak berbentuk, ia memiliki pakan anatomi konstruksi kargo kompartemen sasis kontainer kotak surat khusus yg menopang tubuhnya utuh saat di transmisikan. Proses enkapsulasi melilit kargo paket ditengahnya ini menambahkan dua blok pembungkus pengaman sayap tempel (*Bahu Kepala & Ekor Bawah Trailer Data Link*).

Anatomi Tiga bagian *Frame Segment Layer 2 Data-Link*:

| Komponen Frame | Fungsi Data Segmen L2 *Frame* |
|---|---|
| **Header** | **Frame Start** (Bendera tanda permulaan identifikasi *Start of frame bit streams* akan segera dikirimkan mendarat bersambung menyusul sinkronisasi datang). <br>  **Addressing** (Label tujuan perangko mesin antarmuka lokal: Berisi tanda arah MAC address dari Perangkat Host sumber NIC pengirim awal berikatan menarget terminal piranti ujung ke MAC *destination terminal* media jaringan tetangga terdekat link). <br>  **Type** (Label petunjuk jenis *Protokol muatan Payload L3 Network IP Header* apa yang diangkut menopang didalam rahimnya). <br> **Control** (Sinyal komando kendali kecepatan mengontrol *flow control services transimisi*). |
| **Data** | Muatan brankas harta bendanya, muara wadah intil *Payload L3 Encapsulated packet routing logis* bersandar didalam. |
| **Trailer (Ekor Bawah)** | **Error Detection** (Sistem penghakiman perlengkapan tameng asuransi proteksi hitung matematis korupsi kabel. Mesin pernerima Router ujung *mengadili verifikasi cek FCS kalkulasi matematis*. Bila sinyalnya *corrupted-mismatch/patah sumbang angka* oleh distorsi cuaca kawat, Layer dua tanpa sungkan mendelet me-reject/membuang eksistensi mematikan frame kiriman malapetaka errornya (*Error Detection Filter* perusak frame sampah). <br> **Frame Stop** (Titik purnawaktu garis finish / pertanda ekor akhiran gerbong penutup pemberhentian bit). |

---

## Summary — Key Concepts at a Glance

| Concept | Definition |
|---|---|
| **Physical Layer** | Layer yang fungsinya murni mensarangi bit di medium fisik; mengubah rentetan representasi keping bit *encode logis komputer* ke realita asimilasi konversi fluktuatif bising listrik/optik cahaya mekanis/radio udara *Signal Transmission Modulator*. |
| **Throughput & Goodput Rate** | *Throughput* adalah ukuran rasio hitungan metrik laju lintasan *bit stream rate* nyata yang bisa berhasil dipuntir pada kabel per rentang saat itu. Namun *Goodput* murni rasio logis kecekatan jumlah *transfer file murni usablenya aplikatif end-user*, (*Throughput Total murni* sesaat dipajaki dipotong dikurangi overhead *data control* adminitrasi perjalanannya per keping). |
| **Media Kabel LAN Layer Fisik** | Menawarkan kawat murah setrum berbasis tembaga ber-konsep lilit memilin menetralisasi badai bocornya induksi (*UTP & STP Kabel pelindung Crosstalk EMI twist*); Atau investasi infrastruktur dewa *Fiber Optik kaca tabung inti serabut pantul cahaya* laser berfrekuensi bandwidth tercepat mahakarya peradapan terhebat, sama sekali imun mustahil disetrum polusi EMI lingkungan sekitarnya. |
| **Data Link Layer / Media Access** | Sublayer 2 OSI penyedia arsitektur komando etika komutatif persetujuan hak pakai frekuensi kabel *(MAC Media Access control)* yg meverifikasi *error transmisi checksum hardware drop filter* di antara hardware *NIC Local Nodes Link* saat frame tersebut bersandar di masing masing titik hop perambatan segmen stasiun port. |
| **Logical & Physical Topology Map** | Pandangan pemetaan yang kontras fungsi: *Logical topology blueprint* menampakkan abstraksi wujud pengalamatan aliran perpindahan virtual map IP *(Aliran abstraks IP di udara software)* VS *Physical Topology* menampilah rupa baut rancang sketsa gambar rakit paku rentang jarak fisik colokan letak geografis antar alat piranti. |

---

## Active Recall Questions

> [!question]- 1. Saat menonton video di jaringan Wireless Kafe kampus (*WLAN*), video anda sering terhenti merespon jeda lambat dibandingkan saat dicolok kabel LAN. Bandingkan karakteristik media *Wireless WLAN* vs Kabel Tembaga dalam mempengaruhi kejadian ini berdasarkan spesifikasi Physical layer (Ingat: sifat propagasi *Shared medium* dan konsep *Goodput*)!
> Ketika sebuah data video di *streamingkan* melewati WLAN / Jaringan wifi Media nirkabel frekuensi radio, gelombang sinyal ini rawan menemui tabrakan kontaminasi pantulan redaman dari interferensi medan gelombang Microwave / penghalang partisi arsitektural beton di koridor kampus (menyerap dan mencincang gelombang signal propagasi).
Selain korupsi karena polusi udara sekeliling, koneksi Radio transmisi ini memiliki sifat limitasi **Shared Medium yang mutlak menggunakan arsitektur aliran operasional transmisi alat berat beralur "Half-Duplex"**. *(Hal ini adalah biang masalahnya)*. Transmisi ini mengindikasikan setiap entitas satu komputer dengan entitas HP mahasiswa kolega-kolega anda hanya boleh berteriak bersuara di jalur frekuensi wifi yang sempit membusa antri dan tidak boleh serentak me-request pertukaran packet data secara bersamaan (*Satu berbicara, selusin lainnya wajib menahan antrian delay berdiam diam jeda waktu*). Antrian hiruk pikuk "Sharing the space channel bandwidth access" kepada ratusan rekan kampus pengguna WLAN secara massal di ruang kafe berjejal parah akan secara ekstrem menyayat-nyayat porsi Bandwith utuh anda—Dan ini berdampak merusak tingkat kalkulasi kecepatan bersih aplikasi (*Merosotnya Nilai Rasio The GOODPUT Rate*) karena besarnya *Delay jeda antrian radio overhead* dibanding ketika anda memakai *full-duplex private track personal UTP Copper Kabel LAN* tanpa gangguan rekan kolega.

> [!question]- 2. Media kawat tembaga kabel LAN seperti "UTP Unshielded Twisted-Pair" sama sekali telanjang tidak memiliki *selimut pelindung foil tameng logam (*Unshielded*).* Namun kabel tembaga ini sangat murah padahal kabel tembaga disekitar rak server harusnya rawan didera korupsi kebisingan medan silang *Electromagnetic Interference (EMI).* Bagaimana sebuah kabel murah UTP bisa menetralisasi serangan korupsi data *Crosstalk & Induksi gelombang medan Magnetik?*
> Kabel murah *UTP* melawan bahaya pencemaran frekuensi kebisingan *EMI RFI / Electromagnetic Crosstalk* bukan dengan mengadalkan protektor mahal tameng baja zirah *seperti STP Shielded Twist platting*, melainkan mengakali fisika kelistrikan dengan merancang *desain anyaman kepang menyilang* "**Twisting / Memilin kawat kawat tersebut sangat spesifik secara berpelukan berpasang pasang (*Twisted-Pair*)**". Putaran derajat silangan memilin antar tembaga sepasang inti tersebut menipu memanfaat efek fisis di mana dua utas sejajar ini akan me-*cancel* dan mengeliminasi secara drastis (*Self-cancelling effect induksi magnet berlawanan arah*). Desain putaran spesifik *twisting rate* berbanding ini dengan mulus membunuh kebocoran silang dan membungkam riak induktivitas transmisi antar pasang kabel murahnya.

> [!question]- 3. Data Link Layer (L2) itu dipecah kembali kompartemennya di standar IEEE arsitektur 802 LAN/MAN, sub-layer apakah itu pengontrol antrian laju ke sirkulasi tembaga port antarmuka kabel (Media fisik)? Dan dalam skenario komunikasi *Hop-To-Hop Router Segmen beda jenis Media kabel fisik*, mengapa Frame L2 terus menerus digunting *"De-Enkapsulasi"* dibongkar dan disusun ulang *"Re-Enkapsulasi Header barunya"* di setiap stasiun pos halte *router*? 
> Sub-layer perantara komando lapangan pengatur antrean akses kabel itu ialah **MAC Sublayer / Media Access Control** (mengontrol laju hardware, *siapa* mendapat giliran memakai antrian media link *channel* perlintasan tersebut sesuai model transmisinya misal: standard MAC WLAN wireless 802.11 yang di udara VS Ethernet 802.3 LAN dlsnya).
Paket Data (L3) harus menempuh perjalanan etape persimpangan stasiun *Intermediary Hops* Router melintasi medium perangkat fisik benua pelintas konektor (*Segment Network*) yang senantiasa **Sangat berbeda bentuk Hardware transmisi fisiknya (*Berbeda bahasa Medium Link layer MAC Access controlnya*)**.
Misal: L3 Packet tiba di antrean terminal di pelabuhan pintu stasiun Router C melalui kawat tembaga jenis *Ethernet*. Tetapi selanjutnya router ini berkewajiban merutekan melempar L3 Packet ini meluncur meloncat masuk berpindah jenis ke terowongan pipa laju *Kabel Fiber Optik benua bawah laut*. Karena bahasa standar spesifik Layer Dua dari koneksi pipa *Tembaga UTP* itu amat *Incompatible* bermusuhan format enkapsulasinya dengan rancang arsitektur antarmuka di mulut *Kabel Fiber optik kaca,* Maka sebelum data logis menyebrang melompat dilempar kedalam pintu corong lintasan media medium segmen selanjutnya: *Network Router di Layer dua akan secara radikal mende-konstruksi membongkar merobek bungkus pelindung baju seragam (Lapis Header De-enkapsulasi Data-link) dari frame paket media jaringan Tembaga yg mengangkutnya pada staisun awal tadi. Mengisolasikan Paket L3 yang ditelanjangi; kemudian Router mencetak bungkus label stiker ulang merakit men-packging bungkusan paket kedalam rahim cetakan mesin stempel* **Re-enkapsulasi MAC Address Header Frame yang spesifik baru** *Yang dirancang dikawinkan bahasa medium fisiknya mematuhi kompatibilitas jenis lintasan spesifikasi terowongan Media Optik Fiber yang selanjutnya akan membawanya masuk menelusuri hop antrean ke depan.* Segmen transmisi berlanjut dengan frame baru estafet berjalan melompat node-node stasiun persimpangan per media dengan terus mengonta ganti membongkar paketnya bergantian lapis *selimut* frame.
