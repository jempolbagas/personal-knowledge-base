---
title:
  - "CN - 6 - Ethernet Frame, Ethernet MAC Address, MAC Address Table, dan Address Resolution Protocol (ARP)"
type: Lecture
course:
  - Computer Networks
topic:
  - Data Link Layer
semester: 4
tags:
  - computer-networks
  - ethernet
  - mac-address
  - switch
  - arp
status: 🌿 incubating
created: 2026-04-09
---

# CN - 6 - Ethernet Frame, Ethernet MAC Address, MAC Address Table, dan Address Resolution Protocol (ARP)

**Reference:** Materi Kuliah Jaringan Komputer, Informatika UNS
**Source:** [[(CN-6) Ethernet Frame, Ethernet MAC Address, MAC Address Table, dan Address Resolution Protocol (ARP)]]
**Prasyarat:** [[CN - 5 - Physical and Data Link Layer]]

---

## Daftar Isi

1. [[#1. Ethernet Frame]]
    - [[#1.1. Peranan MAC Sublayer]]
    - [[#1.2. Tanggung Jawab Enkapsulasi Data]]
    - [[#1.3. Struktur Internal Ethernet Frame]]
2. [[#2. Ethernet MAC Address]]
    - [[#2.1. Konsep dan Representasi Heksadesimal]]
    - [[#2.2. Struktur Ethernet MAC Address]]
    - [[#2.3. Tiga Tipe MAC Address: Unicast, Broadcast, Multicast]]
3. [[#3. MAC Address Table pada Switch]]
    - [[#3.1. Dasar Operasional Layer 2 Switch]]
    - [[#3.2. Proses *Learn* (Mempelajari Source MAC)]]
    - [[#3.3. Proses *Forward* (Meneruskan berdasarkan Destination MAC)]]
    - [[#3.4. Memfilter Frame]]
4. [[#4. Address Resolution Protocol (ARP)]]
    - [[#4.1. Apa Itu ARP dan Mengapa Dibutuhkan?]]
    - [[#4.2. Cara Kerja dan Fungsi ARP]]
5. [[#Summary — Key Concepts at a Glance]]
6. [[#Active Recall Questions]]

---

## 1. Ethernet Frame

### 1.1. Peranan MAC Sublayer

**Ethernet** adalah salah satu teknologi fundamental untuk jaringan data *wired* (*kabel*) yang menghubungkan *device* satu sama lain secara fisik. Dalam model OSI, Ethernet beroperasi pada bagian bawah dari **Data Link Layer**. Data Link Layer ini dibagi lagi menjadi dua *sublayer* untuk memisahkan tanggung jawab *software* dan *hardware*:

- **Logical Link Control (LLC) sublayer**: Ini adalah perangkat lunak yang berinteraksi dengan Network layer di atasnya. LLC memiliki standar baku yaitu **IEEE 802.2**. Karena sifatnya perangkat lunak dan terstandar, ia beroperasi terlepas dari medium fisik apa pun yang digunakan di bawahnya.
- **Media Access Control (MAC) sublayer**: Ini adalah bagian *hardware* yang berinteraksi langsung dengan Physical layer bawahnya. Macam-macam standar yang ada di *sublayer* ini bergantung pada mediumnya, seperti:
  - **IEEE 802.3** untuk Ethernet kabel (LAN) 
  - **IEEE 802.11** untuk jaringan nirkabel (WLAN / Wi-Fi) 
  - **IEEE 802.15** untuk jaringan personal nirkabel (WPAN / Bluetooth) 

**Mengapa dipisah?** Pemisahan ini memungkinkan arsitektur jaringan menjadi fleksibel; lapisan LLC (Network layer) tidak perlu mempedulikan apakah medium di bawahnya berupa kabel tembaga, fiber optic, atau sinyal radio. 

*Sublayer* **MAC** sendirilah yang memiliki tanggung jawab besar atas **enkapsulasi data** dan ***media access control*.**

### 1.2. Tanggung Jawab Enkapsulasi Data

Ketika *MAC sublayer* melakukan inkubasi terhadap data (berdasarkan standar **IEEE 802.3**), ia merangkum data tersebut ke dalam struktur khusus dengan menambahkan informasi *header* dan *trailer* sebelum dikirimkan ke media fisik.

Tiga fungsi utama dari proses enkapsulasi ini adalah:
1. **Ethernet Frame internal structure**: Menentukan bagaimana *frame* disusun dan diformat menggunakan *header* dan *trailer* sehingga *receiver* bisa mengerti kapan *frame* bermula, isinya apa, dan kapan berakhir.
2. **Ethernet Addressing**: Menambahkan parameter **Source MAC Address** dan **Destination MAC Address**. **Mengapa penting?** Karena dalam *Local Area Network (LAN)* yang sama, terdapat begitu banyak *device*. *Frame* harus diarahkan dari Ethernet NIC (*Network Interface Card*) asal menuju NIC tujuan dengan presisi agar tidak terjadi salah alamat.
3. **Ethernet Error Detection**: Menempatkan *trailer* berupa **Frame Check Sequence (FCS)** di bagian paling akhir. **Bagaimana cara kerjanya?** Sang *sender* melakukan perhitungan algoritmik dari isi data (biasanya algoritma CRC). Nilai hasil tersebut disisipkan ke FCS. Sang *receiver* lantas melakukan perhitungan ulang yang sama ketika frame tiba. Jika nilainya berbeda sekecil apapun, disimpulkan bahwa *corrupt* atau data telah rusak selama transmisi kabel, lalu *frame* tersebut didrop (*error detection*).

### 1.3. Struktur Internal Ethernet Frame

Sebelum dikodekan menjadi representasi bit fisik di Physical layer, *Ethernet frame* memiliki blok fungsional yang dikenal sebagai *field*. Ukuran total *frame* Ethernet legal berkisar antara minimum **64 bytes** dan maksimum **1518 bytes**. Jika isi data membuat *frame* terlalu kecil, transmisi bakal dianggap sebagai tabrakan data "*collision fragment*". Sebaliknya jika ukuran melebihi 1518 bytes dan perangkat menolak, frame dianggap tidak valid.

Berikut tabel rincian anatomi *Ethernet Frame*:

| Field | Ukuran | Penjelasan Fungsi |
|---|---|---|
| **Preamble and SFD** | 8 bytes | Terdiri dari barisan byte *Preamble* (7 bytes) dan *Start Frame Delimiter* (SFD) (1 byte). Bagian mutlak di bagian awal frame disebut *the start of frame*, tetapi uniknya ia tidak dihitung bagian dari jumlah beban total *frame* (64-1518 ukuran legal tadi). Fungsinya adalah untuk men-**sinkronisasi** ketukan alur *timing* antara sang *sender* dan *receiver*. |
| **Destination MAC Address** | 6 bytes | MAC Address perangkat tujuan. Digunakan oleh Ethernet Switch sebagai parameter navigasi kemana *frame* diarahkan. |
| **Source MAC Address** | 6 bytes | MAC Address identitas *host* pengirim frame (berupa *unicast*). Secara cerdas akan diaudit oleh switch untuk memperbarui data rekaman *MAC address table* (Learning). |
| **Type / Length** | 2 bytes | Berisi semacam nomor jenis yang mengidentifikasi tipe dari *upper-layer protocol* (misal: penanda IPv4 kah, IPv6 kah, atau jenis paket ARP) yang sedang dibawa (*encapsulated*) dalam kolom data. |
| **Data** | 45–1500 bytes | Area inti di mana muatan aslinya diselundupkan (*packet* bermuatan dari *Network Layer*). |
| **FCS** | 4 bytes | Area paling penutup berwujud jejak pemeriksaan error. Menyimpan nilai matematis semacam *Cyclic Redundancy Check* (CRC). |

---

## 2. Ethernet MAC Address

### 2.1. Konsep dan Representasi Heksadesimal

Pada dasarnya, antarmuka jaringan dan *device* di level terasnya membaca semuanya sebagai sinyal nol dan satu binari (digital).
**Ethernet MAC Address** sendiri secara baku merupakan data berukuran statis **48-bit**, dirangkai secara seri per 8-bit.

Mengingat representasi wujud murni panjang 48 digit logika dari '01' luar biasa susah untuk kita baca dan tulis, format standarnya memangkas perpanjangannya lewat representasi angka basis-16 yaitu sistem angka **Heksadesimal**. 
- Karena tiap digit bilangan heksadesimal mampu menampung 4 bit (nilai *nibble*), maka secara ekuivalen *48-bit bernilai sejajar deretan **12 digit nilai heksadesimal***.
- Biner `00000000` setara dengan kemajemukan Hex `00`, dan *full* biner `11111111` mentok maksimal berbatas pada Hex `FF`.
- Penting: Saat merepresentasikan 8-bit (*byte*) untuk mendemonstrasikan perannya didalam MAC Address, aturan emasnya adalah tidak menyingkirkan **angka nol di awalan** (Contoh: nilai biner semisal '00001010', format Hex patennya **Wajib `0A`** bukan sekedar 'A'). 
- Penulisan Teknis: Untuk mengidentifikasinya sebagai heksadesimal, teks sering ditandai sisipan kode awalan **`0x`** (ex: `0x73`) atau akhiran khusus **`H`** (ex: `73H`).

### 2.2. Struktur Ethernet MAC Address

Mekanisme L2 Data Link Layer menjadikan *MAC Addressing* sebagai instrumen mutlak untuk mengelola **identifikasi unik pada perangkat fisik jaringan**. MAC Address senantiasa berukuran tetap **48 bit (6 byte)**.

**Mengapa wajib Unik di seluruh dunia?** Bila ada sekian dua *device* merespon terhadap identifikasi ganda dalam ranah suatu L2 subnet segmen jaringan, maka perangkat-sistem penyambung pertukaran frame seketika kebingungan lantas akan melempar macet tabrakan informasi dan *frame* hinggap di mesin yang tidak diinginkan. 

Untuk merealisasikannya, standarisasi regulasi MAC ditata sangat hati-hati oleh entitas *IEEE*, dibagi dengan format yang adil atas dua bagian komponen panjangnya:
1. Vendor / Produsen Kartu Jaringan (Network Company) yang di industri memproduksi *interface hardware* tersebut di awal wajib mendaftar untuk memperoleh *prefix* keunikan atas organisasinya dari IEEE. Terdapuk lah alokasi porsi paten di ruang **6 digit heksadesimal (3 *byte* awal)** sebagai **Organizationally Unique Identifier (OUI)**.
2. Setiap kali kelak pabrik memproduksi kepingan chip maupun komponen Ethernet device, serambi ruang kosong di sisanya bebas pabrik ini tetapkan secara independen menggunakan serial internal **6 digit heksadesimal sisa (3 *byte* buntut terakhir)** dan mereka tidak boleh mengulang angka persis kepada chip manapun berikutnya (semacam alokasi SN *serial number*).

*Contoh nyata MAC Address:* **`00-0F-66-D0-69-13`**
- OUI (Kode pendaftaran institusi / vendor): **`00-0F-66`**
- Identitas serian mandiri perangkat: **`D0-69-13`**

### 2.3. Tiga Tipe MAC Address: Unicast, Broadcast, Multicast

Frame *Ethernet* memiliki wewenang dikirim perbincangannya menyapa salah seorang saja, mendiskusikan di sebuah perkumpulan obrolan, ataupun digemakan menggunakan megaphone secara massal untuk sekampung halaman perbatasan jaringan LAN.

1. **Unicast MAC Address**
   - **Target Individu**: Adalah alamat tunggal presisi untuk mentranmisi *frame* tepat sasaran mulai letak singgah persis **satu perangkat *source*** ke eksklusif pada **satu perangkat *destination***.
   - **Bagaimana cara sang *source* tahu rahasia nama *destination* nya ini?** Ini menggunakan layanan intel tambahan, dimana apabila *Network IP* bersistem *IPv4*, kita menyerahkan perannya menelisik info MAC tersebut ke protokol **Address Resolution Protocol (ARP)**. Di era penerusnya, jika network bersistem *IPv6*, peranan pengungkapan dialihkan lewat layanan **Neighbor Discovery (ND)**.
   - Perlu diingat kolom bagian *Source MAC Address* disebuah frame haram memiliki identitas yang bukanlah sebuah unicast (Kamu tidak mungkin mengirim pakai nama alias massal).

2. **Broadcast MAC Address**
   - **Target Komunal**: Saat disebarkan dengan atribut *broadcast*, pesan terlampir diperintahkan secara implisit harus hinggap, ditangkap, dihirup utuh seraya **diproses paksa oleh seluruh setiap perangkat anggota piranti** yang berkoloni mencolok kepada *Ethernet LAN* yang sama.
   - Ditandakan dengan seluruh kolom *destination MAC Address* mencantumkan sepasang hex yang dilonjakkan habis ke tingkat paling padat: **`FF-FF-FF-FF-FF-FF`**.
   - Digandengkan tatkala paket IP beralamat *broadcast* seumpama paket `192.168.1.255` meminta DHCP pertolongan.

3. **Multicast MAC Address**
   - **Target Grup Spesifik**: Multicast merupakan format di mana bingkisan *frame Ethernet* mendarat lalu dijawab khusus hanya menuju se-*kelompok device* segelintir *subscribers* stasiun yang turut di satu jaringan ikut **multicast group**. Target yg tidak bersangkutan pun merasa tentram karena NIC L2 miliknya mem-bebas lepaskannya *frame* ini (*reject*)
   - Kode pakem inisiasi awalan Heksadesimal untuk MAC Multicast itu menuruti protokol muatan asalnya:
     - Jika dikaruniai memuat data sebuah **IPv4 multicast packet** (alamat terikat dengan limitasi renang Internet Protocol IP class `224.0.0.0` sampai `239.255.255.255`). Titik sasaran destination dari MAC dirumus mutlak sebagai **`01-00-5E` ....**  
     - Kalau menanggung tugas mengirim jenis letupan gizi berupa **IPv6 multicast packet** (alamat terikat dengan lintasan awalan logis `ff00::/8`). Destination L2 MAC Address bakal membubuhi format khusus berawalan angka hex kembar: **`33-33` ...**

---

## 3. MAC Address Table pada Switch

### 3.1. Dasar Operasional Layer 2 Switch

Sebuah Ethernet Switch bagaikan petugas pusat persimpangan rel kereta api (*Layer 2*) yang bertugas cermat meramu keputusan jalan meneruskan jalur lajur lalu-lintas jaringan (*forwarding decisions*). Namun yang unik? Ia secara total berfondasikan satu indikator semata—yaitu *Layer 2 MAC Address*.

Secara desain sistem *Layer 2 Ethernet Switch*:
1. Ia dirancang sama sekali "**tidak *aware***" atau tidak sudi berurusan mengurus membaca muatan barang logis di paket gerbong *upper-layer* *protocol* manapun disitu (dia tidak kenal istilah apa IPv4, dia tuli tentang pesan dari ARP massage atapun IPv6 ND).
2. Yang ia tilik hanya memandang tempelan stiker resi dari layer2 (Source & Destination MAC Address) untuk mengambil rute memindahkan arus gerbang (*Forwarding*).
3. Sang *Switch* meng-komparasi parameter sasaran resi tersebut melawat kedalam **MAC address table** (yang juga biasa diistilahkan sirkuit elektroniknya sebagai wujud memorinya **Content Addressable Memory - CAM table**).
4. Uniknya, di momen *booting up* dinyalakan, isi rekaman dari daftar table yang tersematkan itu keadaannya **kosong melompong zero memori**.  

### 3.2. Proses *Learn* (Mempelajari Source MAC)

Oleh karenanya, *Switch* di awal harus perlahan belajar. Intelejensi Switch bertumpu kepada menyelaraskan **Source MAC address**. Tiap detak dan kedatangan lalu lalu *frame* pada lubang *port incoming switch* mana saja, seketika di periksa lah dengan teliti *Source MAC address* tersebut. Hubungkan antara siapa MAC address tersebut dan darimana lubang *Port Interface* secara real nyolok itu berasal.

- **KONDISI A: *MAC Belum Ada*.** Kalau nilai frame *Source* MAC address terdeteksi absen belom pernah ada rekam jejak, lekas dengan tanggap disatukan info tersebut untuk **ditambahkan ke rentetan list entry table**, dibundel persis serangkai beserta *nomor port*-nya berlabuh.
- **KONDISI B: *MAC Sudah Ada (Refresh)*.** Andai didalam daftar jejak lama sudah termaktub MAC Source sedemikian rupa, memori tak diubah. Namun sang *switch* hanya memperbarui nyawa tenggat waktu atau **memperbarui timer reset *refresh* ** dari deretan rincian tabel terkait. Jika terbiar saja dan stasiun itu mendadak hening putus komunikasi hingga batas masa tertentu (*default-nya kebanyakan Switch menetapkan 5 menit menganggur tidak berkirim informasi apapun*), maka sang daftar tersebut terkelupas sirna ditelan kadaluwarsa dihapus perlahan agar RAM terjaga longgar dan tabel relevan dengan kebaruan (*Fresh*).
- **KONDISI C: *MAC Ada namun bertandang di Port Beda*.** (Skenario ini terjadi saat user usil mencabut rute LAN si pernagkat PC tersebut dan lantas memindahkannya dari dicolokkan nomor Port LAN 1 terus disusupkan pada ruang Port colokan LAN 4). Sang *Switch* terkejut? Tidak, dia berpersepsi itu merupakan pembaruan murni alias entri baru. Rincian tabel terdahulu **langsung digantikan tertimpa telak** karena mencatat hal spesifik *device* persis ini tapi pada rujukan identitas colokan **nomor port yang lebih otentik (terbaru).**

### 3.3. Proses *Forward* (Meneruskan berdasarkan Destination MAC)

Sesudah ditelaah kolom *Source* (si penyeru), tatapan switch berikutnya bergeser mereview parameter navigasi muaranya, yaitu *Destination MAC Address* memilah apa yang semustinya dijalankan dengannya: keputusan bertindak (*Forward*).

- **Situasi 1: Sudah Dipelajari (*Known Unicast*)**
  Asalkan sasaran destination *unicast* miliknya sudah diserap *switch* berwujud ada presisi terhubung nomor portnya dalam lintasan MAC Tabel. Maka sistem cukup berbisik mem-**forward frame khusus nan rahasia hanya lurus menengadah menerobos ke ruang titik lubang colokan (*port*) yang telah ditetapkan secara relevan**. Penuh senyap dan bebas hingar bingar lalu lantas di bandwitch jaringan PC lain.
- **Situasi 2: Memori Masih Kosong (*Unknown unicast*)**
  Terspesifikasi unicast (*satu tujuan*) tapi gawat—setelah di-gali menelusuri memori *MAC table*, si swtich ini *blank* nggak ketemu MAC dari *destination* ini! Inilah petualangan *Unknown unicast*. Dalam upaya menghindari di-*drop* ke lubang hitam, *switch* nekat dengan terpaksa **meneruskan menyebrang me-raungkan seluruh salinan *frame* semburatan tersebut pecah menuju kepada KE SEMUA *port switch* aktif (*Flooding*), dengan pengecualian SATU: ia enggan menularkannya menapak arus balik berlawanan pada pintu asalnya tadi (*incoming port*).** Harapan *switch* berlagak optimis: "Mesin siapapun itu, tolong lah angkat."
- **Situasi 3: Memang Bertujuan Luas (*Broadcast & Multicast*)**
  Jika *destination* MAC terindikasi bernuansa bukan ditujukan ke 1-point khusus (melainkan wujud *BroadcastFF-FF-...* atau susunan *Multicast*), cara operasinya seraut wajah disamakan secara sistematis pada mekanisme ke-2 barusan. Disebarkan sembari dibanjiri keluar mencabang lewat segala pori-pori perlintasan L2 Switch semesta (Kecuali lagi-lagi ya port dimana ia dipijakkan berakar aslinya masuk dihalau mundur).

### 3.4. Memfilter Frame

Dari pemahaman di atas dapat dinarasikan ulang, sebuah saklar sentral *Layer 2 Ethernet Switch* pada akhirnya bakal menjadi sang bijak di alam LAN yang penuh ingatan tabel. Hal paling fundamental sebagai faedah pembedanya dalam era sejarah yang menggeser *Network Hub* yang usang dan boros bandwidth: *Switch punya fitur seleksi untuk membuang kesia-siaan*.

Selama piranti-piranti asik mengoceh bertukar transmisi satu demi satu di area segmen tersebut—*MAC Address Table*-nya kian hari semakin padat dan sempurna secara dinamis beraneka warna populasi MAC terkoleksi. Kala si tabel tersebut sudah berbadan sehat menyandang referensi informasi *destination MAC address* untuk tiap *device*, pada kala itulah Switch merepresentasikan kemampuannya sanggup **mem-filter frame**. *Switch* cuma bakal menyuguhkan *forward* transmisi tersebut berhemat tenaga melintas pada satu lorong jalan raya (*port*) yang dituju, menindas penyiaran *flooding* riuh tak berguna kepada jaringan letak port sekumpulan piranti yang tak ada hak keterlibatannya.

---

## 4. Address Resolution Protocol (ARP)

### 4.1. Apa Itu ARP dan Mengapa Dibutuhkan?

Kutipan situasi: Anda *(beralamat logikal IP `192.168.1.1`)* sedang mendatangi terminal di kantor untuk mengontak rekan *(di ranah Network IP `192.168.1.5`)* pada LAN satu atap. Seperti dipelajari pada relung diskusi *layer model* komunikasi L3 dan L2, *host node* dalam jaringan tidak mengetahui secara gaib entitas hardware temannya ("Berapakah angka hex 48-biti MAC L2 physical teman saya si nomor `1.5` ini?"). Dan parahnya di sisi L2 *Layer*, si saklar jembatan Ethernet Switch menolak membaca *Destination* berbasis pengiriman IP logic. Si pengguna A butuh menyusun lengkap selusin atribut *Frame Header Header Destination MAC* sebelum menyalipkannya ke *Physical Cable*.

Bagaimana cara pernagkat PC tersebut menyingkap rahasia mengawinkan antara dimensi logic dan *Physical* ini? Jawabat mutlaknya ada di peran detektifnya utilitas sistem IP Address IPv4: Sang mediator komunikasi jaringan bernama lengkap **Address Resolution Protocol (ARP)**.

### 4.2. Cara Kerja dan Fungsi ARP

Secara ringkas misi dari layanan Address Resolution Protocol (ARP) melingkupi dua beban urusan:
1. Membantu **menerjemahkan/mengubah wujud suatu relasi IPv4 menjadi porsi format L2 MAC address**.
2. **Mengurus pengelolaan manajemen ARP table** secara cache memori.

**Runtutan Alur Kronologis Operasi ARP saat proses persiapan Enkapsulasi L2 Frame dikerjakan oleh Sender Device:**

Ketika perangkat pengirim hendak mencetuskan pelayaran paket pergerakan data... ia mutlak segera memeriksa wujud cadangan buku catatannya—yakni si repositori *ARP table*:

- **Tahap 1 - Penelusuran Area Operasi (Network Segmen):**  
  * **Skenario jika rekan IPv4 ada serumpun di *network LAN* yang sama:** Perangkat *host* cerdas bertindak seketika merunut kolom di daftarnya untuk memburu kecocokan pasangan jejak si *destination IPv4 address* di ARP table pribadinya.
  * **Skenario andai IPv4 jauh beda dimensi subnet Network kawasan berlainan:** Jika ia bermaksud mengirim bingkisan kepada situs dunia maya jauh (Contoh: web server), di ARP Tabel si device *Sender* *nggak* akan konyol menembakkan peluru *ARP ping MAC Address* IP nun jauh disana, malahan ia akan bermuara menoleh untuk menyongsong memanggil **IPv4 address letak wujud gerbang pintu masuk/keluar terpadu (IPv4 Default Gateway router)** yang dimilikinya dan menolehkan telunjuk meraba perbendaharaan *ARP table*-nya akan MAC dari Default Gateway ini!

- **Tahap 2 - Interogasi Tabel ARP Memori:**
  * **Jika Terjawap (*Found/Hit*):** Apabila kombinasi sepasang merpati IP tersebut secara memori berhasil ditemukan wujud pasangannya berformat *MAC address* menempati lapik *ARP table*  → "Bingo!", Nilai identifikasi sang target L2 perantanya akan sah direkatkan kokoh ke struktur header dalam bentuk kedudukan terhormat murni **destination MAC address**.
  * **Jika Kosong tak Bernoda (*Miss*):** Bilamana pasca dicari nihil tak jua nampak dalam lipatan *ARP table*-nya, si *device* tak bisa berlanjut. Ini teramat mendesak sehingga memicu protokol mengirimkan semburan peluru berupa pesan **ARP request**. 
    Adikodrati tabiat *ARP Request* adalah sifatnya meneriakkan Broadcast ke Ethernet (*dikirim L2 bernilai `FF-FF-FF..`*): "Halo Wahai semua pengembara Ethernet penghuni LAN ini, sekiranya diantara saksi barangsiapa bersumpah punya identitas pemegang paten IPv4 Address XXX.XXX ini? Jika berkenan berikan aku *MAC Address Hex formatmu* via balesan unicas *ARP Reply* kemari!" Lalu sang empunya IP yang disebutkan tersebut akan menuntun kembali rute identitas MAC nya dan di-input dengan syahdu masuk ke *Memory Mapping* di *ARP Table* milik inisiator *(Sender)*.

---

## Summary — Key Concepts at a Glance

| Concept | Definition |
|---|---|
| **MAC Sublayer** | Paruh terbawah dari fondasi Data Link Layer (Layer 2 OSI) bertanggung jawab eksekusi penanganan *data encapsulation* (*frame* data beserta struktur, *address*, maupun *FCS error detection*) maupun eksekusi teknikal meredam perihal *media access control*. |
| **Ethernet MAC Address** | Identifikasi eksklusif wujud piranti L2 berjumlah rentang bit 48 unit tersirat direpresentasikan selaku 12 digit *Heksadesimal*, berfungsi bak label "alamat fisik statis perangkat" (*OUI & Serial Number*) untuk pelintas dalam ekosistem *LAN*. |
| **Layer 2 Switch Operations** | Alat fasilitator sentral pemandu konektivitas perangkat dalam skala lokal yang mendasari manuver lintas mem-filter dan menerukan muatan persimpangan *forwarding frame* secara absolut murni hanya merujuk mengadili porsi rekaman *Layer 2 MAC Table*, tanpa memperdulikan wujud paket logik network *Layer-3.* |
| **Unknown Unicast** | Reaksi *flooding* ke gubahan seluruh port melainkan *incoming point port* manakala L2 *Switch* tidak menelusuri penemuan letak presisi keberadaan alamat *destination MAC* unik khusus *unicast* di rongga wacana basis data pangkalan tabel memori-nya. |
| **Address Resolution Protocol (ARP)** | Sebuah layanan fasilitas protokol translator yang menjembatani disparitas logikal layer, berfungsi melokalisasi *destination L2 MAC address* berdasarkan dari entitas pegangan sepotong klu *nomor L3 IPv4 address* lokal di *subnetwork* bersangkutan atau *Default Gateway Router*. |

---

## Active Recall Questions

> [!question]- 1. Bandingkan peran antara OUI (Organizationally Unique Identifier) dengan bagian 24-bit sisa dari sebuah Ethernet MAC Address. Mengapa pembagian tanggung jawab alokasi dari 48-bit tersebut dianggap sangat penting bagi kelangsungan model alamat jaringan di tingkat global?
> OUI merupakan 24-bit atau 3 byte dari 6 digit heksadesimal paruh pertama yang ditugaskan khusus dari pendaftaran keotoritasan *IEEE*. Ini menyiratkan cap stempel pabrikan industri vendor produsen. Sedangkan, sisa 24-bit atau 3 byte selebihnya, diwujudkan mandiri oleh perusahaan vendor NIC itu sendiri bagaikan layaknya sistem pemberian unik nomor *SerialNumber/SN* untuk perangkat-perangkat dalam jalur *assembly line* buatannya. Pembagian hierarki ini penting dikarenakan *IEEE* hanya harus menyelenggarakan pemantauan satu level di pendaftaran para *vendor*, tanpa perlu repot bersusah payah mensertifikasi satuan dari jutaan *hardware* harian individual dari seluruh perangkat perusahaan tersebut yang pastinya jauh lebih lamban nan rumit, sementara memastikan jaminan keunikan eksklusif di seluruh semesta tak akan meleset dari potensi *Clash of MAC Address*. 

> [!question]- 2. Bila seorang penganalisa jaringan mengecek paket wirehsark dan menemukan bahwa *address* yang direkam bernilai L2 destination: `FF-FF-FF-FF-FF-FF`. Secara fundamental berdasarkan konsep Address *Ethernet*, paket itu akan berefek krusial terhadap seluruh PC dalam ruangan tersebut. Benarkan pernyataan operasional transmisi ini? Jika iya sebutkan kenapa!
> Benar. Alamat bernilai Hex 100% *`FF`* mempresentasikan wujud alamat format **Broadcast MAC Address**. Sifat utama dari lalu lintas bingkai *broadcast Ethernet* menjanjikan bahwa setiap bingkisan wujud bingkainya secara pasti akan diterima (*received*), ditarik asimilasi dan dilanjutkan urusan kompuasi keprosesnya paksa serempak oleh CPU dan NIC oleh **setiap masing-masing perangkat manapun** yang terkalungkan dalam Ethernet segmen LAN tersebut yang sama persis (Terkecuali dari si port masuknya pemicu). Proses paksa untuk membuka dan menilai muatan dari bingkisan broadcast yang massal bertubi-tubi seringkali bisa melumpuhkan pemakaian persentasi resource berharga pada masing peranti di sekitar sana.

> [!question]- 3. Seorang administrator baru tak sengaja mencabut lalu menyambung memindahkan Letak kabel LAN Port Server PC Database-A dari letak asli soket `FastEthernet 0/1` ke lokasi terpencil milik soket Port LAN `FastEthernet 0/5` tatkala sebuah *L2 Ethernet Switch* dalam masa operasional *Running*. Dari sisi operasioanl mekanisme proses internal memori MAC Switch, jelaskan reaksi fenomena di memodif entri dari kondisi ini?
> Ketika ada *Frame* singgah menerobos lewat lubang `FastEthernet0/5` dikemudian harinya seraya menyedekahkan info bahwa ia diampu atas nama *Source MAC Address* milik identitas Database-A, Sang tabel dari *Switch* sebenarnya masih mengingat identitas lama bahwa MAC ini berada lekat dengan alur tempelnya port  `Fa0/1`. Fenomena pembaruan adaptif pada switch berasumsi entitas dari MAC ini masihlah perangkat serupa akan tetapi ada pergeseran letak topologi port nya. Otomatis, tak perlu bingung bimbang; ia menimpa (*overwriting*) barisan entri usangnya ini seraya menghukum pembaruan mutakhir letak lintasan navigasi port menuju alur Port Nomor Ke.`FastEthernet0/5` untuk membalas letak forward destination traffic terkininya.

> [!question]- 4. Apa tindakan protokol pemetaan sistem PC (`sender`) jika disaat mengecek pada sistem rute routing logisnya ternyata si `destination IP Address` target tersebut letaknya merentang dalam Subnet teritorial jarak jauh yang tidak berbaris pada garis *Local LAN*-nya sama persis? Terhadap siapa (*Who goes there?*) permintaan request broadcast *ARP Ping* akan meronta dari host ini? 
> Karena si *sender/host device* berdasar kepada perhitungan logika kesadaran *Netmask/Subnet* L3-nya melek bahwasanya destinasi *IPv4 address* target tak bersandar dalam satu *LAN Network* sejati nan langsung sealam, dia tidak akan mencetak kekonyolan mengambangkan pesan ping permohonan MAC dari perangkat di benua antah berantah itu. Sebagai gantinya host tersebut akan pintar bereaksi menoleh meninjau ke sistem pengawal perbatasannya; dimana si Pengirim berupaya menetapkan fokus pencarian kepada wujud keberadaan perwakilan **IP IPv4 dari Default Gateway** (IP router gerbang pintu) yang secara paten pada setting hostnya dan ia memusatkan energi ARP *request*-nya untuk menggali tahu manakah presisi L2 wujud perwakilan **MAC address dari Default Gateway** ini! Ketika ia dapat membalutnya kesana, maka di relai/forward dengan lancar lah gerbong frame menuju singgah pelabuh router itu dahulu.
