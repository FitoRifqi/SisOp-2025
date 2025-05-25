# 📝Chapter 5 Exercises

## 📍Soal 5.17

**Pertimbangkan mekanisme RPC. Jelaskan konsekuensi tidak diinginkan yang dapat timbul jika tidak menerapkan semantik "at most once" atau "exactly once". Jelaskan juga kemungkinan penggunaan semantik "at least once".**

### ✅ Jawaban:

![image](https://github.com/user-attachments/assets/cfbf30e2-ba7c-48ea-9028-5709dc01c4be)


## ✅ Proses yang Diberikan:

| Proses | Waktu Burst | Prioritas |
|--------|-------------|-----------|
| P1     | 5           | 4         |
| P2     | 3           | 1         |
| P3     | 1           | 2         |
| P4     | 7           | 2         |
| P5     | 4           | 3         |

> Semua proses tiba pada waktu 0.

---

### a. Gantt Chart

#### 1️⃣FCFS (First-Come-First-Serve / Datang Pertama Dilayani Pertama)

Urutan: P1 → P2 → P3 → P4 → P5

**📦Gantt Chart:**

```
| P₁ | P₂ | P₃ | P₄ | P₅ |
0    5    8   9   16   20
```

#### 2️⃣SJF (Shortest Job First, Non-preemptive / Pekerjaan Terpendek Dulu)

Urutan: P3 (1) → P2 (3) → P5 (4) → P1 (5) → P4 (7)

**📦Gantt Chart**

```
| P₃ | P₂ | P₅ | P₁ | P₄ |
0    1    4    8   13   20
```

#### 3️⃣Prioritas Non-Preemptive (Angka lebih besar = prioritas lebih tinggi)

Urutan: P1 (4) → P5 (3) → P3 (2) → P4 (2) → P2 (1)  
*Semua tiba di waktu 0, maka urut berdasarkan prioritas lalu FCFS.*

**📦Gantt Chart**

```
| P₁ | P₅ | P₃ | P₄ | P₂ |
0    5    9   10  17   20
```

#### 4️⃣Round Robin (Quantum = 2)

**📦Gantt Chart**

```
| P₁ | P₂ | P₃ | P₄ | P₅ | P₁ | P₄ | P₅ | P₁ | P₄ | P₄ |
0    2    4    5    7    9   11   13  15  16   18  20
```

---

### b. 🧮 Turnaround Time (TAT = Waktu Selesai - Waktu Kedatangan)

| Proses | FCFS | SJF | Prioritas | RR  |
|--------|------|-----|-----------|-----|
| P1     | 12   | 13  | 9         | 17  |
| P2     | 8    | 3   | 18        | 11  |
| P3     | 9    | 1   | 17        | 5   |
| P4     | 16   | 19  | 17        | 18  |
| P5     | 20   | 7   | 12        | 16  |

---

### c. ⌛ Waktu Tunggu (WT = Turnaround Time - Burst Time)

| Proses | FCFS | SJF | Prioritas | RR  |
|--------|------|-----|-----------|-----|
| P1     | 7    | 8   | 5         | 12  |
| P2     | 5    | 0   | 15        | 8   |
| P3     | 8    | 0   | 16        | 4   |
| P4     | 9    | 12  | 15        | 11  |
| P5     | 16   | 3   | 8         | 12  |

---

### d. ⌛ Rata-Rata Waktu Tunggu

| Algoritma | Rata-Rata Waktu Tunggu     |
|-----------|-----------------------------|
| FCFS      | (7+5+8+9+16)/5 = **9.0 ms**     |
| SJF       | (8+0+0+12+3)/5 = **4.6 ms** ✅ (*paling optimal*) |
| Prioritas | (5+15+16+15+8)/5 = **11.8 ms**  |
| RR        | (12+8+4+11+12)/5 = **9.4 ms**   |


Jika semantik "at most once" atau "exactly once" tidak diterapkan, permintaan RPC dari klien bisa dijalankan lebih dari satu kali di server akibat kegagalan komunikasi. Misalnya, jika klien tidak menerima respons, ia mungkin akan mengulangi permintaan, sehingga operasi dijalankan dua kali.

**Konsekuensinya:**
- Jika operasi bukan idempotent (misalnya: transaksi keuangan), maka dapat terjadi eksekusi ganda yang menyebabkan kerugian atau ketidakkonsistenan data.
- Sulit memastikan apakah permintaan benar-benar telah dieksekusi atau tidak.

**Semantik "at least once"** dapat digunakan ketika operasi bersifat **idempotent**, seperti: menetapkan variabel ke nilai tertentu atau menulis isi file tetap. Dalam kasus ini, eksekusi ganda tidak akan menyebabkan perubahan hasil.

---

## 📍Soal 5.18

**Apakah memungkinkan sebuah aplikasi memiliki semantik konsistensi berbeda pada berbagai bagian dari ruang alamatnya? Jelaskan.**

### ✅ Jawaban:

![image](https://github.com/user-attachments/assets/b1636a11-3d85-47e8-ac90-9f3371485171)


## ✅ Proses yang Diberikan:

| Proses | Prioritas | Burst | Kedatangan |
|--------|-----------|-------|------------|
| P1     | 8         | 15    | 0          |
| P2     | 3         | 20    | 0          |
| P3     | 4         | 20    | 20         |
| P4     | 4         | 20    | 25         |
| P5     | 5         | 5     | 45         |
| P6     | 5         | 15    | 55         |

**Jenis Penjadwalan:** *Preemptive* berbasis **prioritas**, dengan **round-robin** di dalam grup prioritas yang sama.  
**Quantum Waktu:** 10 unit  
**Aturan Preemption:** Proses dengan prioritas lebih tinggi yang datang akan *menghentikan* proses yang sedang berjalan. Proses yang dihentikan akan masuk ke akhir antrian dengan prioritas yang sama.

---

### a. 📊 Gantt Chart

```
| P1 | P1 | P2 | P3 | P4 | P3 | P5 | P6 | P6 | P4 | P2 |
0   10  15  20  30  40  50  55  65  70  80  90
```

---

### b. 🧮 Turnaround Time (TAT = Waktu Selesai - Waktu Kedatangan)

| Proses | Waktu Selesai | Waktu Datang | Turnaround Time |
|--------|----------------|--------------|-----------------|
| P1     | 15             | 0            | 15              |
| P2     | 90             | 0            | 90              |
| P3     | 50             | 20           | 30              |
| P4     | 80             | 25           | 55              |
| P5     | 55             | 45           | 10              |
| P6     | 70             | 55           | 15              |

---

### c. ⏳ Waktu Tunggu (WT = Turnaround Time - Burst Time)

| Proses | Turnaround Time | Burst Time | Waktu Tunggu |
|--------|------------------|------------|---------------|
| P1     | 15               | 15         | 0             |
| P2     | 90               | 20         | 70            |
| P3     | 30               | 20         | 10            |
| P4     | 55               | 20         | 35            |
| P5     | 10               | 5          | 5             |
| P6     | 15               | 15         | 0             |

---

### ✨Ringkasan:

- **Gantt Chart:**
```
| P1 | P1 | P2 | P3 | P4 | P3 | P5 | P6 | P6 | P4 | P2 |
0   10  15  20  30  40  50  55  65  70  80  90
```
- **Turnaround Terbaik:** P1 dan P5 (15 & 10)
- **Waktu Tunggu Terlama:** P2 (**70 ms**)


Ya, hal tersebut **memungkinkan**. Sistem operasi atau pengelola memori dapat mengizinkan aplikasi untuk menggunakan kebijakan konsistensi berbeda pada setiap bagian memori.

Contohnya, dalam sistem memori bersama terdistribusi (*Distributed Shared Memory*), suatu bagian memori dapat menggunakan **sequential consistency** untuk data kritis, sementara bagian lain menggunakan **causal consistency** untuk performa lebih baik.

Dengan membagi semantik konsistensi, aplikasi dapat menyeimbangkan **kebutuhan konsistensi** dan **efisiensi performa**.

---
