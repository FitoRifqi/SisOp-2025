# PRAKTIKUM: Penerapan Thread di Berbagai Platform

## Deskripsi Praktikum

Praktikum ini membahas implementasi threading pada tiga platform berbeda: Java, Linux, dan Windows. Setiap platform memiliki pendekatan dan API yang unik untuk mengelola eksekusi paralel dalam aplikasi.

---

## 1. Implementasi Thread di Java (`SumTask.java`)

### Overview
Program Java menggunakan **Fork/Join Framework** untuk mendistribusikan beban kerja computational ke multiple threads. Pendekatan ini sangat efektif untuk tugas yang dapat dipecah secara rekursif.

### Arsitektur Program

#### Deklarasi Kelas
```java
public class SumTask extends RecursiveTask<Integer>
```

Kelas `SumTask` mengextend `RecursiveTask<Integer>` yang merupakan bagian dari Fork/Join Framework, memungkinkan task untuk dibagi secara rekursif dan mengembalikan hasil bertipe Integer.

#### Algoritma Divide and Conquer
```java
if (end - begin < THRESHOLD) {
    // Pemrosesan sekuensial untuk data kecil
} else {
    // Pembagian menjadi dua subtask untuk pemrosesan paralel
}
```

Program menggunakan threshold untuk menentukan kapan harus memproses data secara langsung atau membaginya lagi. Strategi ini mengoptimalkan performa dengan menghindari overhead thread creation untuk dataset kecil.

#### Eksekusi Paralel
```java
leftTask.fork();
rightTask.fork();
return rightTask.join() + leftTask.join();
```

- `fork()`: Memulai eksekusi task secara asinkron
- `join()`: Menunggu completion dan mengambil hasil
- Hasil dari kedua subtask digabungkan untuk mendapatkan total final

#### Penggunaan ForkJoinPool
```java
ForkJoinPool pool = new ForkJoinPool();
int sum = pool.invoke(task);
```

`ForkJoinPool` secara otomatis mengelola thread pool dan mengoptimalkan penggunaan CPU cores yang tersedia.

### Keunggulan
- Automatic load balancing
- Work-stealing algorithm untuk efisiensi maksimal
- Scalable dengan jumlah CPU cores
- High-level abstraction yang mudah digunakan

---

## 2. Implementasi Thread di Linux (`thrd-posix.c`)

### Overview
Program Linux menggunakan **POSIX Threads (pthreads)** yang merupakan standar threading pada sistem Unix-like. Implementasi ini memberikan kontrol level rendah terhadap thread management.

### Komponen Utama

#### Thread Creation
```c
pthread_t tid;
pthread_create(&tid, NULL, runner, argv[1]);
```

- `pthread_t`: Identifier untuk thread
- `pthread_create()`: Fungsi untuk membuat thread baru
- Parameter terakhir berisi argumen yang akan diteruskan ke thread function

#### Thread Function Implementation
```c
void *runner(void *param) {
    int i, upper = atoi(param);
    sum = 0;
    for (i = 1; i <= upper; i++)
        sum += i;
    pthread_exit(0);
}
```

Thread function harus memiliki signature yang spesifik:
- Return type: `void *`
- Parameter: `void *` (generic pointer)
- Menggunakan `pthread_exit()` untuk terminasi

#### Thread Synchronization
```c
pthread_join(tid, NULL);
```

Main thread menunggu completion dari worker thread sebelum mengakses hasil perhitungan, mencegah race condition.

### Karakteristik
- Low-level control over thread lifecycle
- Minimal overhead
- Portable across POSIX-compliant systems
- Manual memory management required

---

## 3. Implementasi Thread di Windows (`thrd-win32.c`)

### Overview
Program Windows menggunakan **Win32 Threading API** yang terintegrasi dengan Windows kernel. Pendekatan ini menggunakan Windows-specific data types dan calling conventions.

### Komponen Implementasi

#### Thread Creation dengan CreateThread
```c
DWORD ThreadId;
HANDLE ThreadHandle;
ThreadHandle = CreateThread(NULL, 0, Summation, argv[1], 0, &ThreadId);
```

Parameter CreateThread:
- Security attributes (NULL untuk default)
- Stack size (0 untuk default)
- Thread function pointer
- Parameter untuk thread function
- Creation flags
- Output thread ID

#### Thread Function Declaration
```c
DWORD WINAPI Summation(LPVOID Param) {
    int upper = atoi(Param);
    Sum = 0;
    for (int i = 1; i <= upper; i++)
        Sum += i;
    return 0;
}
```

Windows thread function requirements:
- Return type: `DWORD`
- Calling convention: `WINAPI`
- Parameter: `LPVOID` (long pointer to void)

#### Thread Synchronization
```c
WaitForSingleObject(ThreadHandle, INFINITE);
```

- `WaitForSingleObject()`: Menunggu thread completion
- `INFINITE`: Timeout infinite (menunggu sampai selesai)
- Alternatif: timeout value dalam milliseconds

### Windows-Specific Features
- `HANDLE`: Universal object identifier untuk thread
- `DWORD`: 32-bit unsigned integer untuk thread ID
- Rich set of synchronization objects (Events, Mutexes, Semaphores)
- Integration dengan Windows scheduler

---

## Perbandingan Platform

### Kompleksitas Development
| Platform | Difficulty | Learning Curve | Abstraction Level |
|----------|------------|----------------|-------------------|
| Java     | Rendah     | Mudah          | Tinggi            |
| Linux    | Sedang     | Menengah       | Rendah            |
| Windows  | Sedang     | Menengah       | Rendah            |

### Performance Characteristics
- **Java**: Overhead JVM, namun optimized work-stealing
- **Linux**: Minimal overhead, direct system calls
- **Windows**: Platform-optimized dengan scheduler integration

### Portability
- **Java**: Cross-platform dengan JVM
- **Linux**: Portable di sistem POSIX-compliant
- **Windows**: Spesifik Windows platform

### Use Cases
- **Java**: Enterprise applications, complex parallel algorithms
- **Linux**: System programming, server applications
- **Windows**: Windows-specific applications, desktop software

---

## Kesimpulan

Setiap platform menawarkan pendekatan threading yang berbeda dengan trade-offs tersendiri:

1. **Java Fork/Join**: Ideal untuk divide-and-conquer algorithms dengan automatic optimization
2. **POSIX Threads**: Memberikan kontrol maksimal dengan minimal overhead
3. **Win32 Threads**: Terintegrasi penuh dengan Windows ecosystem

Pemilihan platform harus mempertimbangkan faktor target deployment, performance requirements, dan kompleksitas development yang dapat ditoleransi oleh tim pengembang.
