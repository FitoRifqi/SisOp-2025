# Analisis Algoritma Penjadwalan CPU

## Repository Referensi

> Repository yang digunakan sebagai referensi: [ferryastika/Scheduling-Algorithms](https://github.com/ferryastika/Scheduling-Algorithms)

---

## 🔹 1. Shortest Job First (SJF) Non-Preemptive - Tanpa Arrival Time

```cpp
#include<stdio.h>
struct proc
{
    int no,bt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    struct proc p[10],tmp;
    float avgtat=0,avgwt=0;
    int n,ct=0;
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].bt>p[j+1].bt)
            {
				tmp=p[j];
				p[j]=p[j+1];
				p[j+1]=tmp;
            }
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        ct+=p[i].bt;
		p[i].ct=p[i].tat=ct;
		avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

### Deskripsi

Algoritma SJF Non-Preemptive tanpa arrival time mengeksekusi proses dengan burst time terkecil terlebih dahulu. Tidak mempertimbangkan waktu kedatangan karena semua proses dianggap datang bersamaan.

### Contoh Kasus

| Proses | Burst Time |
| ------ | ---------- |
| P1     | 6          |
| P2     | 8          |
| P3     | 7          |
| P4     | 3          |

### Gantt Chart

```
| P4 | P1 | P3 | P2 |
0    3    9   16  24
```

### Hasil Perhitungan

| Proses | BT | CT | TAT | WT |
| ------ | -- | -- | --- | -- |
| P4     | 3  | 3  | 3   | 0  |
| P1     | 6  | 9  | 9   | 3  |
| P3     | 7  | 16 | 16  | 9  |
| P2     | 8  | 24 | 24  | 16 |

**Rata-rata TAT** = 13.0
**Rata-rata WT** = 7.0

### Analisis Kode (`SJF Scheduling Algorithm Without Arrival Time.c`)

#### 🧱 Struktur Data

```c
struct proc {
    int no, bt, ct, tat, wt;
};
```

Struktur `proc` menyimpan informasi tiap proses:

* `no` → Nomor proses
* `bt` → Burst Time (durasi eksekusi)
* `ct` → Completion Time (waktu selesai eksekusi)
* `tat` → Turnaround Time (`ct - 0` karena tidak ada arrival time)
* `wt` → Waiting Time (`tat - bt`)

#### 🔍 Fungsi Input

```c
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```

Fungsi `read()` menerima input burst time dari pengguna untuk proses ke-i, lalu mengembalikan struct `proc` yang sudah terisi.

#### 🧠 Proses Utama (`main`)

```c
int n, ct = 0;
float avgtat = 0, avgwt = 0;
```

* `n` → jumlah proses
* `ct` → waktu total berjalan untuk mencatat `completion time`
* `avgtat`, `avgwt` → akumulasi untuk menghitung rata-rata

##### 1. Input Proses

```c
for (int i = 0; i < n; i++)
    p[i] = read(i + 1);
```

Membaca semua proses dan menyimpannya ke array `p[]`.

##### 2. Pengurutan Berdasarkan Burst Time

```c
for (int i = 0; i < n - 1; i++)
    for (int j = 0; j < n - i - 1; j++)
        if (p[j].bt > p[j + 1].bt) {
            tmp = p[j];
            p[j] = p[j + 1];
            p[j + 1] = tmp;
        }
```

Menggunakan **bubble sort** untuk mengurutkan proses berdasarkan burst time terkecil ke terbesar, karena arrival time tidak dipertimbangkan (semua dianggap tiba bersamaan).

##### 3. Perhitungan dan Output

```c
for (int i = 0; i < n; i++) {
    ct += p[i].bt;
    p[i].ct = p[i].tat = ct;
    p[i].wt = p[i].tat - p[i].bt;
    avgtat += p[i].tat;
    avgwt += p[i].wt;
    printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
}
```

* `ct` dijumlahkan dari proses sebelumnya (karena tidak ada arrival time).
* `ct` digunakan untuk menghitung:

  * `TAT = CT - AT` (AT = 0)
  * `WT = TAT - BT`
* Data ditampilkan untuk masing-masing proses.

##### 4. Rata-Rata

```c
avgtat /= n;
avgwt /= n;
printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
```

Menghitung rata-rata turnaround time dan waiting time seluruh proses.

#### 🔚 Ringkasan Alur

* Pengguna memasukkan jumlah dan burst time setiap proses.
* Proses diurutkan berdasarkan burst time (terpendek dahulu).
* Proses dieksekusi satu per satu sesuai urutan.
* Turnaround time dan waiting time dihitung serta ditampilkan.
* Rata-rata ditampilkan di akhir.

---

## 🔹 2. Shortest Job First (SJF) Non-Preemptive - Dengan Arrival Time

```cpp
#include<stdio.h>
struct proc
{
    int no,at,bt,it,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    int  n,j,min=0;
    float avgtat=0,avgwt=0;
    struct proc p[10],temp;
    printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    for(j=1;j<n&&p[j].at==p[0].at;j++)
        if(p[j].bt<p[min].bt)
            min=j;
    temp=p[0];
    p[0]=p[min];
    p[min]=temp;
    p[0].it=p[0].at;
    p[0].ct=p[0].it+p[0].bt;
    for(int i=1;i<n;i++)
    {
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
        if(p[i].at<=p[i-1].ct)
            p[i].it=p[i-1].ct;
        else
            p[i].it=p[i].at;
        p[i].ct=p[i].it+p[i].bt;
    }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

### Deskripsi

Proses dengan burst time terpendek akan dipilih dari kumpulan proses yang sudah tiba pada waktu tertentu. Proses tidak dapat di-preempt.

### Contoh Kasus

| Proses | AT | BT |
| ------ | -- | -- |
| P1     | 0  | 7  |
| P2     | 2  | 4  |
| P3     | 4  | 1  |
| P4     | 5  | 4  |
| P5     | 6  | 3  |

### Gantt Chart

```
| P1 | P3 | P2 | P5 | P4 |
0    7    8   12  15  19
```

### Hasil Perhitungan

| Proses | AT | BT | CT | TAT | WT |
| ------ | -- | -- | -- | --- | -- |
| P1     | 0  | 7  | 7  | 7   | 0  |
| P2     | 2  | 4  | 12 | 10  | 6  |
| P3     | 4  | 1  | 8  | 4   | 3  |
| P4     | 5  | 4  | 19 | 14  | 10 |
| P5     | 6  | 3  | 15 | 9   | 6  |

**Rata-rata TAT** = 8.8
**Rata-rata WT** = 5.0

### Analisis Kode (`SJF Scheduling Algorithm.c`)

#### 🧱 Struktur Data

```c
struct proc {
    int no, at, bt, it, ct, tat, wt;
};
```

Struktur ini mencatat:

* `no` → Nomor proses
* `at` → Arrival Time (waktu kedatangan)
* `bt` → Burst Time
* `it` → waktu mulai eksekusi (idle time)
* `ct` → Completion Time
* `tat` → Turnaround Time = `ct - at`
* `wt` → Waiting Time = `tat - bt`

#### 🔍 Fungsi Input

```c
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```

Digunakan untuk membaca arrival time dan burst time setiap proses.

#### 🧠 Proses Utama (`main`)

1. Proses diurutkan berdasarkan waktu kedatangan (`arrival time`).
2. Jika ada beberapa proses datang bersamaan, dipilih yang burst time-nya paling kecil.
3. Iterasi akan memilih proses berikutnya dari yang sudah tiba (arrival time <= current time).
4. Waktu idle (`it`) ditentukan berdasarkan apakah CPU sedang menunggu proses berikutnya.

#### 📤 Output dan Perhitungan

```c
p[i].tat = p[i].ct - p[i].at;
p[i].wt = p[i].tat - p[i].bt;
```

Digunakan untuk menghitung turnaround time dan waiting time masing-masing proses. Average-nya dihitung dari total dibagi jumlah proses.

#### 🔚 Ringkasan Alur

* Pengguna memasukkan arrival time dan burst time.
* Proses diurutkan sesuai arrival time.
* Pada setiap waktu, proses dengan burst terkecil yang telah tiba dieksekusi.
* Jika tidak ada proses tersedia, sistem menunggu.
* Perhitungan CT, TAT, dan WT dilakukan, lalu dirata-rata.

---

## 🔹 3. Shortest Remaining Time First (SRTF) - Preemptive SJF

```cpp
#include<stdio.h>
#define MAX 9999
struct proc
{
    int no,at,bt,rt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    p.rt=p.bt;
    return p;
}
int main()
{
    struct proc p[10],temp;
    float avgtat=0,avgwt=0;
    int n,s,remain=0,time;
    printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt=MAX;
    for(time=0;remain!=n;time++)
    {
        s=9;
        for(int i=0;i<n;i++)
            if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                s=i;
        p[s].rt--;
        if(p[s].rt==0)
        {
            remain++;
            p[s].ct=time+1;
            p[s].tat=p[s].ct-p[s].at;
            avgtat+=p[s].tat;
            p[s].wt=p[s].tat-p[s].bt;
            avgwt+=p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
        }
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

### Deskripsi

Merupakan versi preemptive dari SJF. Proses dengan remaining time terkecil akan dieksekusi. Proses yang sedang berjalan dapat dihentikan jika proses baru yang lebih singkat datang.

### Contoh Kasus

| Proses | AT | BT |
| ------ | -- | -- |
| P1     | 0  | 8  |
| P2     | 1  | 4  |
| P3     | 2  | 9  |
| P4     | 3  | 5  |

### Gantt Chart

```
| P1 | P2 | P4 | P1 | P3 |
0    1    5   10  17  26
```

*Catatan: Perubahan konteks terjadi saat proses baru dengan burst time lebih pendek datang. Misalnya, P2 menggantikan P1 di waktu 1 karena burst time P2 < sisa waktu P1.*

### Hasil Perhitungan

| Proses | AT | BT | CT | TAT | WT |
| ------ | -- | -- | -- | --- | -- |
| P1     | 0  | 8  | 17 | 17  | 9  |
| P2     | 1  | 4  | 5  | 4   | 0  |
| P3     | 2  | 9  | 26 | 24  | 15 |
| P4     | 3  | 5  | 10 | 7   | 2  |

**Rata-rata TAT** = 13.0
**Rata-rata WT** = 6.5

### Analisis Kode (`SRTF Scheduling Algorithm.c`)

#### 🧱 Struktur Data

```c
struct proc {
    int no, at, bt, rt, ct, tat, wt;
};
```

* `no` → Nomor proses
* `at` → Arrival Time
* `bt` → Burst Time
* `rt` → Remaining Time
* `ct` → Completion Time
* `tat` → Turnaround Time (`ct - at`)
* `wt` → Waiting Time (`tat - bt`)

#### 🧠 Proses Utama (`main`)

```c
p[9].rt = MAX;
for (time = 0; remain != n; time++) {
    s = 9;
    for (int i = 0; i < n; i++)
        if (p[i].at <= time && p[i].rt < p[s].rt && p[i].rt > 0)
            s = i;
    p[s].rt--;
    if (p[s].rt == 0) {
        remain++;
        p[s].ct = time + 1;
        p[s].tat = p[s].ct - p[s].at;
        p[s].wt = p[s].tat - p[s].bt;
        avgtat += p[s].tat;
        avgwt += p[s].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[s].no, p[s].at, p[s].bt, p[s].ct, p[s].tat, p[s].wt);
    }
}
```

* `MAX` sebagai sentinel nilai tertinggi remaining time (dummy process P9)
* Loop berjalan per satuan waktu (`time++`) dan mencari proses `p[i]` yang sudah datang (`at <= time`) dan memiliki `remaining time` terkecil
* Jika proses selesai (`rt == 0`), catat CT, TAT, dan WT, lalu tambahkan ke total

#### 🔚 Ringkasan Alur

* Setiap waktu, proses yang sedang berjalan bisa diganti jika ada proses baru dengan sisa waktu lebih pendek
* Proses dihentikan jika ada yang lebih pendek
* Digunakan teknik preemptive (berbasis waktu)
* Perhitungan dilakukan saat proses selesai
* Rata-rata TAT dan WT dihitung di akhir

---

## 🔹 Perbandingan Singkat

| Algoritma             | Preemptive | Arrival Time | Starvation | Kompleksitas | Rata-rata WT |
| --------------------- | ---------- | ------------ | ---------- | ------------ | ------------ |
| SJF Tanpa Arrival     | Tidak      | Tidak        | Ya         | Rendah       | 7.0          |
| SJF Dengan Arrival    | Tidak      | Ya           | Ya         | Sedang       | 5.0          |
| SRTF (Preemptive SJF) | Ya         | Ya           | Ya         | Tinggi       | 6.5          |

---

## 📄 Kesimpulan

Pemilihan algoritma penjadwalan CPU bergantung pada kebutuhan sistem:

* Jika kesederhanaan penting, bisa gunakan SJF Non-Preemptive.
* Untuk sistem real-time yang membutuhkan respons cepat, SRTF lebih sesuai.
* Starvation tetap menjadi masalah utama untuk algoritma berbasis burst time.

> Disusun berdasarkan studi kode dari: [ferryastika/Scheduling-Algorithms](https://github.com/ferryastika/Scheduling-Algorithms)

---
