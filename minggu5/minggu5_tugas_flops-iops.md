# Laporan Sistem Operasi

## Tugas FLOPS-IOPS

## Tujuan Pembelajaran FLOPS & IOPS

Dalam dunia komputasi, **FLOPS (Floating Point Operations Per Second)** dan **IOPS (Input/Output Operations Per Second)** adalah dua metrik penting yang digunakan untuk mengukur kinerja sistem komputer, terutama dalam pemrosesan data dan penyimpanan. Berikut adalah tujuan pembelajaran terkait kedua konsep ini:

### 1. Memahami Konsep Dasar FLOPS dan IOPS
- Menjelaskan apa itu **FLOPS**, bagaimana ia mengukur kemampuan komputasi numerik, dan mengapa penting dalam aplikasi seperti simulasi ilmiah, kecerdasan buatan, dan grafik komputer.
- Menjelaskan apa itu **IOPS**, bagaimana ia mengukur kecepatan operasi baca/tulis penyimpanan, serta perbedaannya dengan throughput dan latency.

### 2. Menganalisis Perbedaan antara FLOPS dan IOPS
- Memahami bahwa **FLOPS digunakan untuk mengukur kecepatan pemrosesan matematika**, sedangkan **IOPS mengukur kecepatan akses dan pemrosesan data di perangkat penyimpanan**.
- Mengidentifikasi hubungan antara FLOPS dan IOPS dalam berbagai skenario komputasi, seperti dalam **superkomputer, server database, dan sistem cloud computing**.

### 3. Menerapkan Konsep FLOPS dan IOPS dalam Dunia Nyata
- Menganalisis spesifikasi hardware komputer dan server berdasarkan FLOPS dan IOPS untuk menentukan kinerja terbaik sesuai kebutuhan aplikasi.
- Membandingkan teknologi penyimpanan (HDD, SSD, NVMe) berdasarkan **IOPS** dan memahami bagaimana berbagai faktor seperti **queue depth, latency, dan block size** mempengaruhi performa I/O.
- Mengevaluasi arsitektur **GPU dan CPU** yang digunakan dalam komputasi tinggi dengan metrik FLOPS untuk memahami efisiensinya dalam menangani tugas-tugas spesifik seperti **deep learning** dan **simulasi ilmiah**.

### 4. Mengoptimalkan Kinerja FLOPS dan IOPS dalam Sistem Komputasi
- Menggunakan teknik **parallel computing** dan **vectorization** untuk meningkatkan efisiensi pemrosesan berbasis FLOPS.
- Mengimplementasikan strategi **RAID (Redundant Array of Independent Disks)** dan caching untuk meningkatkan kinerja IOPS dalam sistem penyimpanan data.
- Mengevaluasi dampak **bottleneck hardware** yang dapat mempengaruhi performa FLOPS dan IOPS serta cara mengatasinya.

## Dasar Teori FLOPS & IOPS

### 1. Teori Komputasi Numerik dan Arsitektur CPU/GPU (FLOPS)
Komputasi numerik melibatkan operasi matematika yang dilakukan oleh prosesor dalam bentuk bilangan floating-point. FLOPS digunakan untuk mengukur seberapa cepat sebuah prosesor dapat melakukan operasi ini dalam satu detik.

- **Bilangan Floating-Point**: Representasi angka desimal dalam sistem biner yang digunakan untuk perhitungan ilmiah dan teknik.
- **Arsitektur CPU vs. GPU**: CPU memiliki beberapa inti (cores) yang dioptimalkan untuk tugas serial, sedangkan GPU memiliki ribuan inti kecil yang dapat melakukan operasi floating-point secara paralel.
- **Faktor yang Mempengaruhi FLOPS**: Kecepatan clock (GHz), jumlah inti, dan kemampuan SIMD (Single Instruction Multiple Data).

Contoh aplikasi: **Machine learning, simulasi fisika, dan pemodelan cuaca**.

### 2. Teori Sistem Penyimpanan dan Manajemen I/O (IOPS)
IOPS digunakan untuk mengukur kecepatan akses data dalam perangkat penyimpanan seperti HDD, SSD, dan NVMe.

- **Operasi I/O**: Setiap kali sistem membaca atau menulis data ke perangkat penyimpanan, itu dihitung sebagai satu operasi I/O.
- **Jenis Penyimpanan**:  
  - **HDD (Hard Disk Drive)**: Kecepatan terbatas karena bagian mekanis yang bergerak.  
  - **SSD (Solid State Drive)**: Lebih cepat dari HDD karena menggunakan memori flash tanpa komponen bergerak.  
  - **NVMe (Non-Volatile Memory Express)**: Teknologi SSD terbaru dengan performa sangat tinggi dan latensi rendah.  
- **Faktor yang Mempengaruhi IOPS**: Ukuran blok data, queue depth, latensi, dan throughput sistem penyimpanan.

Contoh aplikasi: **Database, cloud computing, dan server berbasis penyimpanan**.

### 3. Teori Bottleneck dan Optimasi Kinerja FLOPS & IOPS
Kinerja sistem sering kali dibatasi oleh **bottleneck**, yaitu komponen yang memperlambat seluruh sistem.

- **CPU Bottleneck**: Jika prosesor terlalu lambat dalam melakukan operasi floating-point, meskipun penyimpanan cepat, sistem tetap tidak optimal.
- **Storage Bottleneck**: Jika sistem memiliki CPU yang cepat tetapi penyimpanan lambat, maka kecepatan akses data menjadi hambatan utama.
- **Teknik Optimasi**:  
  - **Parallel Processing**: Menggunakan banyak inti CPU/GPU untuk meningkatkan FLOPS.  
  - **RAID (Redundant Array of Independent Disks)**: Meningkatkan IOPS dengan menggabungkan beberapa perangkat penyimpanan untuk akses lebih cepat.  
  - **Caching**: Menyimpan data yang sering diakses dalam memori lebih cepat untuk mengurangi beban I/O.  

## Langkah-langkah Pengujian FLOPS & IOPS

1. Buka terminal Linux dan lakukan clone repository flops-iops:
   ```sh
   git clone https://github.com/ferryastika/flops-iops.git
   ```
2. Masuk ke direktori flops-iops:
   ```sh
   cd flops-iops
   ```
3. Build program benchmark:
   ```sh
   make
   ```
![Contoh Gambar](https://github.com/user-attachments/assets/2b30ef95-acd3-467b-aaf0-8a8e1705c47a)

   
4. Jalankan pengujian FLOPS dan IOPS:
   ```sh
   ./iops32 $(nproc)
   ./iops64 $(nproc)
   ./flops32 $(nproc)
   ./flops64 $(nproc)
   ```

## Hasil Pengujian

**Spesifikasi CPU:** Intel Core i9-11900H

- **IOPS 32-bit:**
  ```sh
  ./iops32 $(nproc)
  ```
![Contoh Gambar](https://github.com/user-attachments/assets/626c9bda-65d7-4e10-8722-f91a1ad9200e)

  
- **IOPS 64-bit:**
  ```sh
  ./iops64 $(nproc)
  ```
![Contoh Gambar](https://github.com/user-attachments/assets/9a984b68-285f-46ce-a9e4-c4017f18bb1e)

  
- **FLOPS 32-bit:**
  ```sh
  ./flops32 $(nproc)
  ```
![Contoh Gambar](https://github.com/user-attachments/assets/d90d46b3-23b6-4cd2-a402-6a3bac767102)

  
- **FLOPS 64-bit:**
  ```sh
  ./flops64 $(nproc)
![Contoh Gambae1](https://github.com/user-attachments/assets/c9f9989a-e5fe-48ca-8b90-d056fb3ea86d)

  
