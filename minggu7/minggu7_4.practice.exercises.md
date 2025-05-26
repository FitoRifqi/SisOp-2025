# 📋 Latihan Soal Bab 4 (Jawaban dalam Bahasa Indonesia)

---

## 📝Soal 4.1

Berikan 3 contoh pemrograman ***Multithreading*** yang memberikan performa lebih baik dibandingkan dengan solusi menggunakan ***Single-Threaded***.

## 📤Jawaban:

Tiga implementasi ***Multithreading*** yang menunjukkan keunggulan signifikan terhadap ***Single-Threading***:

- **Server Database**
Database server seperti **MySQL** atau **PostgreSQL** harus menangani query dari banyak klien secara simultan. Dengan ***Multithreading***, setiap koneksi klien dapat diproses oleh **thread** terpisah, memungkinkan eksekusi query paralel tanpa menunggu satu sama lain.

- **Aplikasi Pengolahan Gambar**
Software seperti **Photoshop** menggunakan ***Multithreading*** untuk operasi berat seperti rendering filter atau efek visual. Satu **thread** menangani antarmuka pengguna, **thread** lain memproses transformasi gambar, dan **thread** tambahan mengelola preview real-time.

- **Browser Modern**
Browser seperti **Chrome** memanfaatkan ***Multithreading*** untuk memisahkan proses rendering halaman web, eksekusi JavaScript, dan pengelolaan tab. Hal ini memastikan jika satu tab mengalami masalah, tab lainnya tetap responsif.

---

## 📝Soal 4.2

Gunakan **Hukum Amdahl**, kemudian hitung kalkulasi peningkatan kecepatan (*speedup*) dari sebuah aplikasi yang memiliki 60% bagian paralel pada:

**a.** Dua core pemrosesan
**b.** Empat core pemrosesan

## 📤Jawaban:

#### 🔍Informasi yang Diberikan:

- Bagian yang dapat diparalelkan \( P = 60\% = 0.6 \)
- Jumlah core untuk kasus **(a.)** adalah \( N = 2 \)
- Jumlah core untuk kasus **(b.)** adalah \( N = 4 \)
- Formula Hukum Amdahl:

$$
\text{Speedup} = \frac{1}{(1 - P) + \frac{P}{N}}
$$

---

#### ✏️Perhitungan

**Kasus (a.) dengan 2 core:**

$$
\text{Speedup} = \frac{1}{(1 - 0.6) + \frac{0.6}{2}} = \frac{1}{0.4 + 0.3} = \frac{1}{0.7} \approx 1.43
$$

**Hasil:** Menggunakan 2 core menghasilkan peningkatan performa **<ins>1,43 kali lipat</ins>**.

**Kasus (b.) dengan 4 core:**

$$
\text{Speedup} = \frac{1}{(1 - 0.6) + \frac{0.6}{4}} = \frac{1}{0.4 + 0.15} = \frac{1}{0.55} \approx 1.82
$$

**Hasil:** Menggunakan 4 core menghasilkan peningkatan performa **<ins>1,82 kali lipat</ins>**.

---

## 📝Soal 4.4

Apa dua perbedaan antara thread tingkat pengguna (**user-level threads**) dan thread tingkat kernel (**kernel-level threads**)? Pada kondisi apa, yang membuat salah satu tipe lebih baik daripada yang lain?

## 📤Jawaban:

Dua perbedaan mendasar antara kedua jenis thread:

| User-Level Threads                     | Kernel-Level Threads                 |
|:---------------------------------------------:|:-------------------------------------------:|
| Pengelolaan dilakukan oleh **runtime library** aplikasi tanpa intervensi sistem operasi. | Pengelolaan dilakukan **secara penuh oleh sistem operasi**. |
| Perpindahan antar thread sangat **efisien** karena tidak memerlukan system call. | Perpindahan antar thread **memerlukan waktu lebih lama** karena melibatkan kernel mode switching. |

**Kondisi optimal untuk masing-masing:**

- **User-Level Threads unggul ketika:**
  - Aplikasi memerlukan **performa tinggi** dalam thread switching
  - Aplikasi lebih fokus pada **komputasi intensif** dengan minimal I/O blocking

- **Kernel-Level Threads unggul ketika:**
  - Aplikasi sering melakukan **operasi I/O** yang dapat menyebabkan blocking
  - Dibutuhkan **paralelisme sejati** pada sistem multicore

---

## 📝Soal 4.5

Jelaskan tindakan yang dilakukan oleh kernel saat akan melakukan pergantian konteks (**context-switch**) antara **thread tingkat kernel**?

## 📤Jawaban:

Langkah-langkah yang dilakukan kernel dalam context switching:

1. **Penyimpanan State Thread Aktif:**
   - Kernel menyimpan seluruh kondisi CPU (register, program counter, stack pointer) dari thread yang sedang berjalan ke dalam Thread Control Block (TCB).

2. **Seleksi Thread Berikutnya:**
   - Scheduler kernel memilih thread yang siap dieksekusi berdasarkan kebijakan penjadwalan yang diterapkan (misalnya *first-come-first-served* atau *shortest-job-first*).

3. **Restore State Thread Baru:**
   - Kernel mengembalikan kondisi CPU dari TCB thread yang akan dijalankan, termasuk semua register dan pointer.

4. **Transfer Kontrol Eksekusi:**
   - CPU memulai eksekusi thread baru dari titik terakhir thread tersebut dihentikan.

---

## 📝Soal 4.6

Sumber daya apa saja yang digunakan saat sebuah **thread** dibuat? Apa perbedaannya dengan sumber daya yang digunakan pada saat pembuatan proses?

## 📤Jawaban:

#### 🧵Resource yang Dialokasikan untuk Thread Baru:
- Program Counter individual
- Stack area terpisah untuk local variables
- Set register CPU khusus
- **Thread Control Block** (*TCB*) untuk metadata thread
- Akses bersama ke resource utama:
  - Virtual memory space
  - File descriptors
  - Network connections

#### 🔄Perbandingan Resource <ins>Thread Creation</ins> vs <ins>Process Creation</ins>

| Thread Creation              | Process Creation                 |
|:---------------------------------------------:|:-------------------------------------------:|
| **Lightweight** - hanya memerlukan resource minimal karena berbagi dengan parent process. | **Heavyweight** - memerlukan alokasi resource lengkap dan terpisah. |
| Menggunakan address space yang sudah ada. | Membuat address space baru secara independen. |
| **Overhead rendah** dan eksekusi cepat. | **Overhead tinggi** dengan waktu inisialisasi lebih lama. |

---

## 📝Soal 4.7

Misalkan sebuah sistem operasi melakukan pemetaan ***user-level threads*** ke kernel menggunakan model ***many-to-many*** dan pemetaan tersebut dilakukan melalui **LWP** (*Lightweight process*). Kemudian, sistem memungkinkan pengembang untuk membuat ***real-time threads*** untuk digunakan pada ***real-time systems***. Apakah diperlukan untuk mengikat (***bind***) ***real-time threads*** ke sebuah **LWP**? Jelaskan!

## 📤Jawaban:

**Binding** ***real-time threads*** ke **LWP** adalah **wajib** untuk sistem real-time. Alasannya:

Tanpa **binding** khusus, real-time thread dapat terjebak dalam antrian user-level scheduler dan kehilangan karakteristik deterministiknya. Dengan **binding** langsung ke LWP, thread mendapat akses prioritas kernel dan dapat dijadwalkan dengan jaminan temporal yang ketat, sesuai dengan persyaratan sistem real-time yang memerlukan respon dalam batas waktu yang telah ditentukan.

---
