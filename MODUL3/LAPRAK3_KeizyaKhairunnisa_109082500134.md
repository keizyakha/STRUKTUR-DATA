# <h1 align="center">Laporan Praktikum Modul 3 - Abstract Data Type (ADT)</h1>
<p align="center"> Keizya Khairunnisa - 109082500134</p>

## Dasar Teori
Abstract Data Type (ADT) adalah konsep yang mengatur data dan operasi yang dapat dilakukan pada data tersebut. ADT membantu program menjadi lebih teratur karena data dan fungsi yang digunakan memiliki tugas masing-masing [1].

Struct adalah tipe data dalam C++ yang digunakan untuk menggabungkan beberapa variabel dengan tipe data berbeda dalam satu kelompok. Pada program ini, struct digunakan untuk menyimpan nama dan kode mata pelajaran.

Array adalah kumpulan data dengan tipe yang sama yang disimpan dalam satu variabel dan diakses menggunakan indeks. Array dapat digunakan untuk menyimpan beberapa data dengan lebih mudah [2].

Fungsi adalah bagian program yang digunakan untuk menjalankan tugas tertentu. Pada program ini, fungsi digunakan untuk membuat dan menampilkan data mata pelajaran.



## Guided 1 pelajaran.cpp

source code unguided 1
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string namapel, string kodepel){
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel){
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}

```
penjelasan unguided 1

Program ini digunakan untuk membuat dan menampilkan data mata pelajaran. Fungsi `create_pelajaran()` digunakan untuk mengisi nama dan kode mata pelajaran, sedangkan fungsi `tampil_pelajaran()` digunakan untuk menampilkan nama dan kode mata pelajaran ke layar.

## Guided 2 pelajaran.h

source code unguided 2
```C++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct pelajaran{
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran pel);

#endif 

```
penjelasan guided 2

Program ini digunakan untuk menyimpan data mata pelajaran, yaitu nama dan kode mata pelajaran. Di dalamnya juga terdapat fungsi untuk membuat dan menampilkan data mata pelajaran.

## Guided 3 main.cpp

source code unguided 3
```C++
#include <iostream>
#include "mahasiswa.h"

using namespace std;

int main(){
  mahasiswa mhs;
  inputMHS (mhs) ;
  cout << "rata rata = " << rata2 (mhs);
  return 0;
}

```
penjelasan guided 3

Program ini digunakan untuk menghitung rata-rata nilai mahasiswa. Data mahasiswa disimpan dalam variabel `mhs`. Fungsi `inputMHS()` digunakan untuk memasukkan data mahasiswa, sedangkan fungsi `rata2()` digunakan untuk menghitung dan menampilkan nilai rata-ratanya.



## Unguided 

### 1. Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3 * uts + 0.4 * uas + 0.3 * tugas.

source code unguided 1
```C++
#include <iostream>
#include <string>
using namespace std;

struct mahasiswa {
    string nama;
    string nim;
    float uts, uas, tugas;
    float nilaiAkhir;
};

int main() {
    mahasiswa mhs[10];
    int n;

    cout << "Jumlah mahasiswa (max 10): ";
    cin >> n;
    while (n < 1 || n > 10) {
        cout << "Jumlah harus 1 - 10, input lagi: ";
        cin >> n;
    }

    for (int i = 0; i < n; i++) {
        cout << "\nData mahasiswa ke-" << i + 1 << endl;
        cout << "Nama   : ";
        cin >> mhs[i].nama;
        cout << "NIM    : ";
        cin >> mhs[i].nim;
        cout << "UTS    : ";
        cin >> mhs[i].uts;
        cout << "UAS    : ";
        cin >> mhs[i].uas;
        cout << "Tugas  : ";
        cin >> mhs[i].tugas;

        mhs[i].nilaiAkhir = 0.3 * mhs[i].uts + 0.4 * mhs[i].uas + 0.3 * mhs[i].tugas;
    }

    cout << "\n=== Data Mahasiswa ===" << endl;
    for (int i = 0; i < n; i++) {
        cout << "Mahasiswa ke-" << i + 1 << endl;
        cout << "Nama        : " << mhs[i].nama << endl;
        cout << "NIM         : " << mhs[i].nim << endl;
        cout << "UTS         : " << mhs[i].uts << endl;
        cout << "UAS         : " << mhs[i].uas << endl;
        cout << "Tugas       : " << mhs[i].tugas << endl;
        cout << "Nilai Akhir : " << mhs[i].nilaiAkhir << endl;
        cout << endl;
    }

    return 0;
}
```
### Output Unguided 1 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL3/Screenshot_Output_soal1.png)


penjelasan unguided 1 

Program ini digunakan untuk memasukkan dan menampilkan data mahasiswa, seperti nama, NIM, nilai UTS, UAS, dan tugas. Jumlah mahasiswa yang bisa dimasukkan maksimal 10 orang. Program akan menghitung nilai akhir setiap mahasiswa dengan bobot UTS 30%, UAS 40%, dan tugas 30%. Setelah semua data dimasukkan, program akan menampilkan kembali data mahasiswa beserta nilai akhirnya.

### 2. Berdasarkan guided pointer dan reference sebelumnya, buatlah keduanya dapat menukar nilai dari 3 variabel.

source code unguided 2
#### pelajaran.h
```C++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran pel);

#endif

```

#### pelajaran.cpp
```C++
#include "pelajaran.h"

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```

#### main.cpp
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```

### Output Unguided 2 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL3/Screenshot_Output_soal2.png)


penjelasan unguided 2

Program ini digunakan untuk menyimpan dan menampilkan data mata pelajaran menggunakan struct. Program mengisi nama mata pelajaran dengan “Struktur Data” dan kode mata pelajaran dengan “STD”. Setelah itu, data dibuat menggunakan fungsi `create_pelajaran()` dan ditampilkan ke layar menggunakan fungsi `tampil_pelajaran()`.

### 3. Buatlah program dengan ketentuan:
### - 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
### - fungsi/prosedur yang menampilkan isi sebuah array integer 2D
### - fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
### - fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer

source code unguided 3

```C++
#include <iostream>
using namespace std;

void tampil(int a[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << a[i][j] << " ";
        }
        cout << endl;
    }
}

void tukarArr(int a[3][3], int b[3][3], int x, int y) {
    int tmp = a[x][y];
    a[x][y] = b[x][y];
    b[x][y] = tmp;
}

void tukarPtr(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

int main() {
    int arr1[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
    int arr2[3][3] = {{9,8,7},{6,5,4},{3,2,1}};
    int n1 = 10, n2 = 20;
    int *p1 = &n1;
    int *p2 = &n2;
    int baris, kolom;

    cout << "Array 1 :" << endl;
    tampil(arr1);
    cout << "Array 2 :" << endl;
    tampil(arr2);

    cout << "Masukkan baris (0-2) : ";
    cin >> baris;
    cout << "Masukkan kolom (0-2) : ";
    cin >> kolom;

    tukarArr(arr1, arr2, baris, kolom);

    cout << endl << "Setelah ditukar" << endl;
    cout << "Array 1 :" << endl;
    tampil(arr1);
    cout << "Array 2 :" << endl;
    tampil(arr2);

    cout << endl << "Pointer sebelum ditukar : " << *p1 << " " << *p2 << endl;
    tukarPtr(p1, p2);
    cout << "Pointer setelah ditukar : " << *p1 << " " << *p2 << endl;

    return 0;
}
```

### Output Unguided 3 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL3/Screenshot_Output_soal3.png)

penjelasan unguided 3

Program ini digunakan untuk menampilkan dua array berukuran 3×3 dan menukar nilai di posisi baris dan kolom yang dipilih. Program meminta pengguna memasukkan nomor baris dan kolom, lalu nilai pada kedua array di posisi tersebut akan ditukar. Selain itu, program juga menggunakan pointer untuk menukar nilai dua variabel, yaitu dari 10 dan 20 menjadi 20 dan 10.

## Kesimpulan
Dari beberapa program yang dibuat, dapat disimpulkan bahwa array, pointer, reference, struct, dan fungsi memiliki kegunaan masing-masing dalam program C++. Array digunakan untuk menyimpan beberapa data, pointer dan reference dapat digunakan untuk menukar nilai variabel, sedangkan struct dan fungsi membantu mengatur serta mengolah data dalam program.

## Referensi
[1] University of Toronto, “Data Types, Abstract and Concrete.” [Online]. Available: https://www.teach.cs.toronto.edu/~csc110y/fall/notes/10-abstraction/04-abstract-data-types.html

[2] cppreference.com, “Array declaration.” [Online]. Available: https://en.cppreference.com/w/cpp/language/array
