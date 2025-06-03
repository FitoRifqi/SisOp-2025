
# 📚 Ringkasan Chapter 5 – CPU Scheduling (Silberschatz)

| No | Topik                           | Deskripsi                                                                 |
|----|----------------------------------|---------------------------------------------------------------------------|
| 1  | Basic Concepts                  | CPU scheduling dipakai saat lebih dari satu proses siap dieksekusi. Scheduler memilih proses dari ready queue. |
| 2  | CPU-I/O Burst Cycle             | Proses memiliki siklus CPU burst dan I/O burst. Scheduler bertujuan memaksimalkan penggunaan CPU. |
| 3  | Scheduling Criteria             | Tujuan: CPU utilization, throughput, turnaround time, waiting time, response time. |
| 4  | FCFS (First-Come First-Served)  | Proses dijalankan sesuai urutan datang. Mudah tapi bisa menyebabkan convoy effect. |
| 5  | SJF (Shortest Job First)        | Proses dengan burst time terpendek dijalankan. Ada versi preemptive (SRTF). Optimal untuk avg waiting time. |
| 6  | Priority Scheduling             | Proses dengan prioritas tertinggi dijalankan. Ada risiko starvation. |
| 7  | Round Robin (RR)                | Time-sharing: setiap proses dapat jatah waktu (quantum). Cocok untuk sistem interaktif. |
| 8  | Multilevel Queue                | Queue dibagi berdasarkan jenis proses (foreground, background). Tidak bisa pindah level. |
| 9  | Multilevel Feedback Queue       | Proses bisa berpindah antar queue berdasarkan perilaku. Lebih fleksibel. |
| 10 | Algorithm Evaluation            | Metode: deterministic modeling, queueing models, simulasi, pengukuran langsung. |
| 11 | Multiple-Processor Scheduling   | Penjadwalan pada sistem multiprosesor. Bisa asymmetric atau symmetric. |
| 12 | Real-Time CPU Scheduling        | Untuk sistem real-time. Pendekatan seperti Rate-Monotonic dan Earliest-Deadline-First digunakan. |
| 13 | Exercises                       | Latihan soal termasuk Gantt chart, perhitungan waiting/turnaround time. Fokus pada algoritma FCFS, SJF, RR, dsb. |


# 📊 Analisis CPU Scheduling: Practice Exercise 5.5 dan 5.7

## 📌 Deskripsi Tugas
Analisis algoritma penjadwalan CPU berdasarkan soal di buku _Operating System Concepts_ Chapter 5:

- Practice Exercise 5.5: Dampak dari Preemptive vs Non-Preemptive SJF.
- Practice Exercise 5.7: Pengaruh Arrival Time terhadap Preemptive SJF (SRTF).

---

## 📘 Practice Exercise 5.5

### 📋 Data Proses

| Process | Arrival Time | Burst Time |
|---------|--------------|------------|
| P1      | 0            | 8          |
| P2      | 1            | 4          |
| P3      | 2            | 9          |
| P4      | 3            | 5          |

---

### 🔁 A. Non-Preemptive SJF

**Gantt Chart:**

```
| P1 | P2 | P4 | P3 |
0    8   12  17  26
```

**Perhitungan:**

| Process | Waiting Time | Turnaround Time |
|---------|--------------|-----------------|
| P1      | 0            | 8               |
| P2      | 7            | 11              |
| P3      | 17           | 26              |
| P4      | 9            | 14              |

- **Average Waiting Time:** 8.25  
- **Average Turnaround Time:** 14.75

---

### 🔁 B. Preemptive SJF (SRTF)

**Gantt Chart:**

```
| P1 | P2 | P4 | P1 | P3 |
0    1   5   10  17  26
```

**Perhitungan:**

| Process | Waiting Time | Turnaround Time |
|---------|--------------|-----------------|
| P1      | 9            | 17              |
| P2      | 0            | 4               |
| P3      | 0            | 9               |
| P4      | 2            | 7               |

- **Average Waiting Time:** 2.75  
- **Average Turnaround Time:** 9.25

---

### ✅ Kesimpulan 5.5

Preemptive SJF (SRTF) menghasilkan rata-rata waktu tunggu dan turnaround yang lebih rendah dibandingkan Non-Preemptive SJF karena proses pendek yang datang belakangan bisa segera dieksekusi.

---

## 📘 Practice Exercise 5.7

### 📋 Data Proses

| Process | Arrival Time | Burst Time |
|---------|--------------|------------|
| P1      | 0            | 10         |
| P2      | 2            | 1          |
| P3      | 4            | 2          |

---

### 🔁 Preemptive SJF (SRTF)

**Gantt Chart:**

```
| P1 | P2 | P3 | P1 |
0    2   3   5   15
```

**Perhitungan:**

| Process | Completion | Turnaround | Waiting |
|---------|------------|------------|---------|
| P1      | 15         | 15         | 5       |
| P2      | 3          | 1          | 0       |
| P3      | 5          | 1          | 0       |

- **Average Waiting Time:** 1.67  
- **Average Turnaround Time:** 5.67

---

### ✅ Kesimpulan 5.7

Arrival time berpengaruh besar dalam penjadwalan SRTF. Proses pendek yang datang lebih lambat bisa memotong antrean proses panjang, meningkatkan efisiensi sistem.

---

## 🔧 Flow Logika Program

1. **Input proses**: PID, arrival time, burst time.
2. **Urutkan proses** sesuai waktu kedatangan.
3. **Setiap satuan waktu:**
   - Pilih proses yang sudah datang dan belum selesai.
   - Di preemptive SJF, pilih proses dengan sisa burst time terkecil.
4. **Update waktu saat ini**, hitung waktu selesai, turnaround, dan waiting.
5. **Cetak Gantt Chart dan hasil perhitungan**.

---

## 📌 Penutup

Latihan ini menunjukkan bagaimana algoritma preemptive seperti SRTF dapat mengoptimalkan waktu tunggu dan turnaround time, terutama ketika arrival time bervariasi.
