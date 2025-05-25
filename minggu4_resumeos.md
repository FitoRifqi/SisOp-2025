## Transisi dari Mode Pengguna ke Mode Kernel

## Mode Pengguna (User Mode)
Mode user itu ialah mode di mana aplikasi pengguna biasa berjalan yang dimana aplikasi memiliki akses terbatas ke sumber daya system dan ditandai dengan **"mode bit = 1"**.  
Sementara mode kernel itu sendiri adalah mode di mana sistem operasi berjalan dengan akses penuh ke semua sumber daya system dan ditandai dengan **"mode bit = 0"**.

---

## Berikut Proses-Prosesnya

1. **Proses Pengguna (User Process):**  
   Aplikasi pengguna berjalan dalam mode pengguna lalu ketika aplikasi perlu mengakses fungsi sistem operasi (misalnya, membaca file), ia akan membuat **"system call"**.

2. **Panggilan Sistem (System Call):**  
   Lalu system call akan memicu **"trap"**, yang menyebabkan peralihan ke mode kernel yang membuat **"mode bit" berubah menjadi 0**.

3. **Mode Kernel:**  
   Ketika sistem operasi mengeksekusi panggilan sistem di mode kernel disaat setelah selesai, sistem operasi mengembalikan kontrol ke aplikasi pengguna.

4. **Kembali ke Mode Pengguna:**  
   **"Return"** mengembalikan eksekusi ke aplikasi pengguna dengan **"mode bit" kembali menjadi 1**.

---

## Timer dan Pencegahan Infinite Loop
Gambar ini juga menjelaskan bagaimana timer digunakan untuk mencegah aplikasi pengguna mendominasi sumber daya sistem:

- **Timer:**  
  - Timer diatur untuk menginterupsi komputer setelah periode waktu tertentu.  
  - Penghitung (**counter**) dikelola dan dikurangi oleh jam fisik.  
  - Sistem operasi mengatur penghitung (instruksi istimewa).  
  - Ketika penghitung mencapai nol, interupsi dihasilkan.  
  - Ini digunakan untuk mengambil kembali kendali dari proses yang melebihi waktu yang dialokasikan atau untuk menghentikan program yang mengalami **"infinite loop"** (loop tak terbatas).

--- 

## Process Management & Process Management

### Proses sebagai Unit Kerja
Proses sebagai Unit Kerja adalah program yang sedang berjalan yang aktif dan menggunakan sumber daya sistem. Program, di sisi lain juga adalah entitas pasif, seperti berkas yang berisi instruksi.

- **Kebutuhan Sumber Daya:**  
  - Setiap proses membutuhkan sumber daya seperti **CPU**, **memori**, **perangkat I/O**, dan **berkas** untuk menjalankan tugasnya termasuk data inisialisasi juga diperlukan saat proses dimulai.

- **Siklus Hidup Proses:**  
  - Ketika proses selesai, sumber daya yang digunakan harus dikembalikan agar bisa dipakai oleh proses lain.

- **Jenis Proses:**  
  - **Proses Berulir Tunggal:**  
    - Hanya memiliki satu alur eksekusi.  
    - Instruksi dijalankan berurutan.  
    - Memiliki satu program counter (penghitung program) yang menunjukkan instruksi berikutnya.
  - **Proses Berulir Ganda:**  
    - Memiliki beberapa alur eksekusi yang bisa berjalan bersamaan.  
    - Memiliki program counter untuk setiap alur.

- **Manajemen Proses dalam Sistem Operasi:**  
  - Sistem operasi menjalankan banyak proses secara bersamaan dengan cara membagi waktu penggunaan CPU.  
  - Ini disebut konkurensi, yang dicapai dengan multiplexing.

### Aktivitas Manajemen Proses oleh Sistem Operasi
- **Pembuatan dan Penghapusan Proses:**  
  Sistem operasi bertanggung jawab untuk membuat dan menghapus proses, baik proses pengguna maupun proses sistem.

- **Penangguhan dan Pengaktifan Kembali Proses:**  
  Sistem operasi dapat menangguhkan sementara proses dan mengaktifkannya kembali nanti.

- **Sinkronisasi Proses:**  
  Sistem operasi menyediakan mekanisme agar proses-proses dapat bekerja sama dan berbagi sumber daya tanpa konflik.

- **Komunikasi Antarproses:**  
  Sistem operasi memfasilitasi komunikasi antarproses, memungkinkan mereka bertukar data dan informasi.

- **Penanganan Deadlock:**  
  Sistem operasi menangani situasi deadlock, di mana dua atau lebih proses saling menunggu sumber daya yang dipegang oleh proses lain.

---

## Memory Management

### Kenapa Manajemen Memori Penting?
- **Menjalankan Program:**  
  - Komputer perlu menyimpan instruksi dan data program di memori agar bisa menjalankannya.  
  - Jika tidak ada cukup ruang, program tidak bisa berjalan.
- **Efisiensi:**  
  - Manajemen memori yang baik membuat komputer bekerja lebih cepat dan responsif.  
  - Ini mencegah program saling berebut memori dan memperlambat sistem.

### Bagaimana Manajemen Memori Bekerja?
- **Pelacakan:**  
  Komputer mencatat bagian memori mana yang sedang digunakan dan oleh program apa.
- **Pemindahan:**  
  Komputer bisa memindahkan program atau data dari memori ke penyimpanan lain (seperti hard drive) jika memori penuh.  
  Ini disebut **"swapping"**.
- **Alokasi dan Dealokasi:**  
  Komputer memberikan ruang memori kepada program saat dibutuhkan.  
  Setelah program selesai, ruang memori tersebut dikembalikan agar bisa digunakan oleh program lain.

#### Contoh Sederhana:
Bayangkan memori komputer seperti tempat parkir mobil:  
- Setiap program yang berjalan membutuhkan tempat parkir.  
- Manajemen memori adalah seperti petugas parkir yang mengatur mobil masuk dan keluar.  
- Petugas parkir memastikan bahwa setiap mobil mendapat tempat parkir, dan tidak ada mobil yang parkir di tempat yang salah.  
- Jika tempat parkir penuh, maka ada mobil yang harus keluar untuk sementara waktu, agar mobil lain bisa masuk.

---

## File-system Management

Bayangkan komputer Anda sebagai perpustakaan besar. Di perpustakaan ini, buku-buku adalah data, dan rak-rak buku adalah penyimpanan.

- **Tugas Sistem Operasi:**  
  - Sistem operasi bertugas sebagai pustakawan yang rapi.  
  - Ia menciptakan sistem agar kita mudah menemukan dan mengatur buku (berkas).  
  - Ia menyederhanakan cara kita melihat data.  
  - Kita tidak perlu tahu detail rumit tentang bagaimana data disimpan secara fisik.  
  - Kita hanya melihatnya sebagai "berkas" yang rapi.  
  - Sistem operasi juga mengatur siapa saja yang boleh meminjam atau mengubah buku (mengatur hak akses).

- **Kegiatan Pustakawan (Sistem Operasi):**  
  - Membuat rak-rak baru (direktori/folder).  
  - Menyusun buku-buku di rak (mengatur berkas dalam direktori).  
  - Mencatat lokasi setiap buku di katalog (memetakan berkas ke penyimpanan fisik).  
  - Membuat salinan cadangan buku-buku penting (mencadangkan data).

---

## Mass-Storage Management

Jika perpustakaan memiliki gudang besar untuk menyimpan buku-buku lama atau buku-buku yang jarang dipinjam, itulah yang disebut penyimpanan massal.

- **Pentingnya Gudang (Penyimpanan Massal):**  
  - Komputer menggunakan disk (seperti hard disk) sebagai gudang untuk menyimpan data yang terlalu besar untuk memori utama atau data yang perlu disimpan lama.  
  - Kinerja komputer sangat bergantung pada seberapa cepat dan efisien gudang ini dikelola.

- **Tugas Pengelola Gudang (Sistem Operasi):**  
  - Mengatur pemasukan dan pengeluaran barang dari gudang (mounting dan unmounting).  
  - Mencatat ruang kosong di gudang (manajemen ruang kosong).  
  - Menentukan lokasi penyimpanan barang baru (alokasi penyimpanan).  
  - Mengatur jadwal pengiriman barang (penjadwalan disk).  
  - Membagi gudang menjadi beberapa bagian (partisi).  
  - Melindungi barang-barang berharga (perlindungan data).

- **Penyimpanan Tambahan (Penyimpanan Tersier):**  
  - Ada juga gudang-gudang lain yang lebih lambat, seperti penyimpanan optik atau pita magnetik, untuk menyimpan data yang jarang diakses.  
  - Meskipun lambat, gudang-gudang ini tetap perlu dikelola.

#### Intinya:
- Manajemen sistem berkas mengatur bagaimana kita melihat dan mengelola data sebagai berkas dan direktori.
- Manajemen penyimpanan massal mengatur bagaimana data disimpan secara fisik di perangkat penyimpanan sekunder.

---

## caching

**Caching** adalah penyimpanan sementara data yang sering digunakan di tempat yang lebih cepat diakses yang bertujuan untuk mempercepat akses data.

### Cara Kerja:
- Data disalin dari penyimpanan lambat ke penyimpanan cepat (**cache**).  
- Sistem memeriksa cache terlebih dahulu sebelum mengakses penyimpanan utama.
