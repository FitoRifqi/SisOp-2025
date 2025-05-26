# Laporan Praktikum Sistem Operasi

## Analisis dan Visualisasi Pohon Proses

### 1. `fork01.cpp`

**Deskripsi:**

Program ini menggunakan satu kali pemanggilan `fork()`, yang menghasilkan dua proses: satu parent dan satu child.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    fork();
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child
```

**Penjelasan:**

- `fork()` membuat satu proses child dari parent.
- Kedua proses (parent dan child) akan mengeksekusi `printf("Hello World!");`, sehingga output akan tercetak dua kali.

---

### 2. `fork02.cpp`

**Deskripsi:**

Program ini memanggil `fork()` dua kali secara berurutan.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    fork();
    fork();
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child1
│   └── Child1.1
└── Child2
```

**Penjelasan:**

- Pemanggilan `fork()` pertama menghasilkan dua proses.
- Masing-masing proses kemudian memanggil `fork()` lagi, menghasilkan total empat proses.
- Setiap proses akan mencetak "Hello World!", sehingga output akan tercetak empat kali.

---

### 3. `fork03.cpp`

**Deskripsi:**

Program ini memanggil `fork()` tiga kali secara berurutan.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    fork();
    fork();
    fork();
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child1
│   ├── Child1.1
│   │   └── Child1.1.1
│   └── Child1.2
└── Child2
    ├── Child2.1
    └── Child2.2
```

**Penjelasan:**

- Setiap pemanggilan `fork()` menggandakan jumlah proses.
- Total proses yang terbentuk adalah 8 (2^3).
- Setiap proses mencetak "Hello World!", sehingga output akan tercetak delapan kali.

---

### 4. `fork04.cpp`

**Deskripsi:**

Program ini menggunakan `fork()` dalam struktur kondisional.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    if (fork() == 0) {
        fork();
    }
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child1
│   └── Child1.1
```

**Penjelasan:**

- `fork()` pertama menghasilkan satu child.
- Jika dalam child (`fork() == 0`), maka `fork()` dipanggil lagi, menghasilkan child dari child.
- Total proses: 3.
- Output "Hello World!" akan tercetak tiga kali.

---

### 5. `fork05.cpp`

**Deskripsi:**

Program ini menggunakan `fork()` dalam kombinasi dengan pernyataan kondisional.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    fork();
    if (fork() == 0) {
        fork();
    }
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child1
│   ├── Child1.1
│   └── Child1.2
└── Child2
    └── Child2.1
```

**Penjelasan:**

- Pemanggilan `fork()` pertama menghasilkan dua proses.
- Dalam setiap proses, jika `fork() == 0`, maka `fork()` dipanggil lagi.
- Total proses: 5.
- Output "Hello World!" akan tercetak lima kali.

---

### 6. `fork06.cpp`

**Deskripsi:**

Program ini menggunakan `fork()` dalam kombinasi dengan operator logika.

**Kode:**

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    fork() && fork() || fork();
    printf("Hello World!\n");
    return 0;
}
```

**Visualisasi Pohon Proses:**

```
Parent
├── Child1
│   └── Child1.1
└── Child2
```

**Penjelasan:**

- Operator `&&` dan `||` mempengaruhi urutan eksekusi `fork()`.
- Total proses yang terbentuk adalah 4.
- Output "Hello World!" akan tercetak empat kali.

---

## Kesimpulan

Melalui analisis program `fork01.cpp` hingga `fork06.cpp`, kita dapat memahami bagaimana pemanggilan `fork()` mempengaruhi pembentukan pohon proses. Visualisasi pohon proses membantu dalam memahami struktur hierarki proses yang terbentuk selama eksekusi program.
