# Peer-to-Peer (P2P)

> Mata Kuliah: Jaringan Komputer
> Topik: Arsitektur Jaringan P2P

---

## 1. Definisi dan Konsep Dasar P2P

Dalam model jaringan **Peer-to-Peer (P2P)**, setiap perangkat (sering disebut *node* atau *host*) dalam jaringan bertindak sebagai **client** (peminta layanan) **sekaligus server** (penyedia layanan) pada saat yang bersamaan. Berbeda dengan model tradisional yang tersentralisasi, P2P tidak memiliki hierarki atau kontrol terpusat. Setiap perangkat memiliki kedudukan yang setara (*peer*).

## 2. Karakteristik Jaringan P2P

- **Terdesentralisasi:** Tidak ada administrator terpusat yang mengatur seluruh jaringan. Setiap pengguna memiliki kebebasan penuh atas perangkatnya sendiri.
- **Kesetaraan Peran:** Setiap komputer dapat membagikan sumber daya yang dimilikinya (seperti file, printer, atau pemrosesan komputasi) sekaligus menggunakan sumber daya dari komputer lain secara langsung.
- **Skala Kecil:** Dalam implementasi jaringan lokal, P2P umumnya membangun jaringan dalam bentuk **Workgroup**. Karena kerumitan pengelolaannya, P2P tradisional via LAN sangat direkomendasikan untuk jaringan berskala kecil (paling banyak 10 host).

## 3. Kelebihan dan Kekurangan

### Kelebihan
- **Biaya Sangat Murah:** Tidak membutuhkan pembelian dan pemeliharaan *dedicated server* yang mahal karena komputer manapun bisa saling melayani.
- **Implementasi Mudah:** Sangat mudah untuk dikonfigurasi. Sistem operasi standar seperti Windows, macOS, atau Linux sudah memiliki fitur bawaan untuk membuat jaringan P2P (misalnya fitur *File and Printer Sharing*).
- **Tidak Butuh Administrator Khusus:** Pengguna biasa dapat mengatur komputernya sendiri tanpa perlu merekrut tenaga administrator jaringan profesional.

### Kekurangan
- **Tidak Scalable:** Jaringan akan menjadi lambat dan terjadi kekacauan manajemen data jika jumlah komputer pada jaringan P2P terus bertambah. Kinerja koneksi jaringan dapat menurun drastis.
- **Tingkat Keamanan Rendah:** Karena kontrol keamanan dilakukan di masing-masing perangkat, sulit untuk menerapkan kebijakan keamanan yang terpusat dan konsisten secara sistem. Setiap pengguna harus menjaga keamanan datanya sendiri.
- **Manajemen Data Tersebar:** Tidak adanya *server* pusat berarti bahwa file dan data tersebar di berbagai komputer berbeda. Tidak ada sistem cadangan (backup) otomatis secara tersentralisasi, sehingga bila satu host rusak/mati, maka data dan layanan yang ada pada host tersebut menjadi tidak dapat diakses host lain.

## 4. Perbandingan P2P vs Client-Server

| Aspek | Peer-to-Peer (P2P) | Client-Server |
| :--- | :--- | :--- |
| **Arsitektur** | Terdesentralisasi, semua *host* setara | Tersentralisasi, server menyediakan layanan, client memintanya |
| **Biaya Implementasi** | Rendah (tidak butuh *dedicated server* dan OS khusus) | Tinggi (butuh *dedicated server*, OS *Server*, dan perangkat keras level enterprise) |
| **Keamanan** | Rendah, diatur masing-masing *host* | Tinggi, dikendalikan terpusat oleh Server dan administrator |
| **Manajemen Jaringan** | Dikelola individu pengguna, tidak butuh administrator jaringan khusus | Membutuhkan tenaga ahli administrator IT/Jaringan yang handal |
| **Skalabilitas** | **Sangat terbatas**, direkomendasikan maksimal 10 komputer | **Sangat Scalable**, mampu menangani pengembangan skala besar |
| **Penyimpanan Data** | Tersebar di masing-masing *host*, rentan hilang | Terpusat di *server* penyimpanan, mudah dibackup |

## 5. Implementasi & Aplikasi P2P di Dunia Nyata

Meskipun model tradisionalnya terbatas untuk LAN kecil, arsitektur dasar P2P sangat berpengaruh dan berevolusi menjadi teknologi internet skala masif saat ini, di antaranya:

- **Local File & Printer Sharing (Workgroup):** Menggunakan fitur sistem operasi bawaan seperti Workgroup pada Windows untuk berbagi folder atau printer secara kolektif dengan PC lain di ruangan yang sama.
- **Aplikasi File-Sharing (BitTorrent):** P2P memungkinkan pendistribusian file ukuran besar secara luas tanpa membebani satu server. Pengunduh (*leecher*) secara bersamaan bertindak sebagai pengunggah (*seeder*) dari potongan-potongan file tersebut ke pengguna lain.
- **Cryptocurrency & Blockchain (Bitcoin, Ethereum):** Memanfaatkan desentralisasi ekstrem P2P agar tidak ada satu bank/entitas terpusat yang memiliki, meregulasi, atau mengontrol pencatatan seluruh jaringan transaksi buku besar (*ledger*).
- **VoIP & Komunikasi (Skype awal):** Secara historis, protokol awal aplikasi komunikasi video seperti Skype memanfaatkan skema P2P untuk mengalirkan paket jaringan telepon dan video antar penggunanya secara langsung guna mentransfer beban bandwidth dari server sentral pengembang.