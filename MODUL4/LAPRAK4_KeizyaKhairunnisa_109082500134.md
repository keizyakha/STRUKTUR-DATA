# <h1 align="center">Laporan Praktikum Modul 4 - SINGLY LINKED LIST (BAGIAN PERTAMA) </h1>
<p align="center"> Keizya Khairunnisa - 109082500134</p>

## Dasar Teori
1. Singly Linked List

Singly linked list merupakan struktur data yang terdiri dari beberapa node yang saling terhubung menggunakan pointer. Setiap node memiliki dua bagian, yaitu info untuk menyimpan data dan next untuk menunjuk ke node berikutnya. Node pertama ditunjuk oleh first, sedangkan node terakhir menunjuk ke NULL.

2. Pointer

Pointer adalah variabel yang menyimpan alamat memori. Dalam singly linked list, pointer digunakan untuk menghubungkan setiap node. Pada C++, operator digunakan untuk mengakses anggota struktur melalui pointer.

3. Operasi Singly Linked List

Operasi dasar singly linked list meliputi insert untuk menambahkan data, delete untuk menghapus data, view untuk menampilkan data, dan update untuk mengubah data. Selain itu, terdapat searching untuk mencari data tertentu.

4. Alokasi Memori

Alokasi memori digunakan untuk menyediakan ruang bagi node baru menggunakan operator new. Sementara itu, operator delete digunakan untuk membebaskan memori ketika node sudah tidak digunakan.



## Guided 1 list.h

source code guided 1
```C++

#ifndef LIST_H
#define LIST_H
#define Nil NULL

#include <iostream>
#include <string>
using namespace std;

// deklarasi isi data struct mahasiswa
struct mahasiswa {
    string nama;
    string nim;
    int umur;
};

// alias dataMahasiswa untuk struct mahasiswa
typedef mahasiswa dataMahasiswa;

// alias address sebagai pointer ke struct node
typedef struct node *address;

// node untuk isi linked list: data & pointer next
struct node {
    dataMahasiswa isidata;
    address next;
};

// linked list-nya
struct LinkedList {
    address first;
};

// semua function & prosedur yang dipakai
bool isEmpty(LinkedList List);
void createList(LinkedList &List);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &nodeHapus);
void printList(LinkedList List);
void insertFirst(LinkedList &List, address nodeBaru);
void insertAfter(LinkedList &List, address nodeBaru, address Prev);
void insertLast(LinkedList &List, address nodeBaru);

void delFirst(LinkedList &List);
void delLast(LinkedList &List);
void delAfter(LinkedList &List, address nodeHapus, address nodePrev);
int nbList(LinkedList List);
void deleteList(LinkedList &List);

#endif
```
penjelasan guided 1

Program ini digunakan untuk mendeklarasikan struktur data Singly Linked List untuk menyimpan data mahasiswa yang terdiri dari nama, NIM, dan umur. Program ini mendefinisikan struktur node yang berisi data mahasiswa dan pointer `next` untuk menghubungkan node satu dengan lainnya. Selain itu, terdapat deklarasi berbagai fungsi untuk membuat list, menambahkan dan menghapus data, menampilkan isi list, serta menghitung jumlah node.


## Guided 2 list.cpp

source code guided 2
```C++
#include "list.h"
#include <iostream>
using namespace std;

// I.S = Initial State / kondisi awal
// F.S = Final State / kondisi akhir

// fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(LinkedList List) {
    return List.first == Nil;
}

// pembuatan linked list kosong
void createList(LinkedList &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) {
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata
       sesuai parameter dan next = Nil */
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

// penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &nodeHapus) {
    /* I.S. terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    nodeHapus->next = Nil;
    delete nodeHapus;
    nodeHapus = Nil;
}

// prosedur-prosedur untuk insert / menambahkan node baru ke dalam list
void insertFirst(LinkedList &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(LinkedList &List, address nodeBaru, address Prev) {
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(LinkedList &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen baru pada akhir list */
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

// prosedur-prosedur untuk delete / menghapus node yang ada di dalam list
void delFirst(LinkedList &List) {
    /* I.S. list tidak kosong
       F.S. node pertama di list terhapus */
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(LinkedList &List) {
    /* I.S. list tidak kosong
       F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev = Nil;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        if (nodeHapus->next == Nil) {
            List.first = Nil;
            dealokasi(nodeHapus);
        } else {
            while (nodeHapus->next != Nil) {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    } else {
        cout << "List kosong!" << endl;
    }
}

void delAfter(LinkedList &List, address nodeHapus, address nodePrev) {
    /* I.S. list tidak kosong, nodePrev alamat salah satu elemen list
       F.S. node setelah nodePrev dihapus dari list */
    if (isEmpty(List) == true) {
        cout << "List kosong!" << endl;
    } else {
        if (nodePrev != Nil && nodePrev->next != Nil) {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

// prosedur untuk menampilkan isi list
void printList(LinkedList List) {
    /* I.S. mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) {
            cout << "Nama : " << nodeBantu->isidata.nama
                 << ", NIM : " << nodeBantu->isidata.nim
                 << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

// function untuk menghitung jumlah node di dalam list
int nbList(LinkedList List) {
    /* I.S. list sudah ada
       F.S. mengembalikan jumlah node di dalam list */
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

// prosedur untuk menghapus list (menghapus semua node di dalam list)
void deleteList(LinkedList &List) {
    /* I.S. list sudah ada
       F.S. menghapus semua node di dalam list */
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while (nodeBantu != Nil) {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}
```
penjelasan guided 2

Program ini digunakan untuk mengelola data mahasiswa menggunakan struktur data Singly Linked List. Program ini memiliki beberapa fungsi untuk menambahkan, menghapus, menampilkan, dan menghitung jumlah data mahasiswa yang tersimpan dalam list. Data mahasiswa terdiri dari nama, NIM, dan umur. Selain itu, program juga dapat menghapus seluruh data yang ada di dalam list.

## Guided 3 main.cpp

source code guided 3
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

Program ini digunakan sebagai program utama untuk menjalankan pengolahan data mahasiswa. Fungsi `inputMHS(mhs)` digunakan untuk memasukkan data mahasiswa, sedangkan `rata2(mhs)` digunakan untuk menghitung rata-rata dari data yang diolah. Hasil perhitungan kemudian ditampilkan menggunakan `cout`. Fungsi `main()` menjadi bagian awal program dijalankan.

## Unguided 

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h” 

Type infotype : int
Type address : pointer to ElmList

Type ElmList <
    info : infotype
    next : address
>

Type List : < First : address >

procedure CreateList( input/output L : List )

function alokasi( x : infotype ) → address

procedure dealokasi(input/output P : address )

procedure printInfo( input L : List )

procedure insertFirst(input/output L : List, input P :address)

Kemudian buatlah implementasi dari procedure-procedure yang digunakan didalam file “Singlylist.cpp”

Kemudian buat program utama didalam file “main.cpp” dengan implementasi sebagai berikut:

int main() {
    List L;
    address P1, P2, P3, P4, P5 = Nil;
    createList(L);
    P1 = alokasi(2);
    insertFirst(L, P1);
    P2 = alokasi(0);
    insertFirst(L, P2);
    P3 = alokasi(8);
    insertFirst(L, P3);
    P4 = alokasi(12);
    insertFirst(L, P4);
    P5 = alokasi(9);
    insertFirst(L, P5);
    printInfo(L)
    return 0;
}

Sehingga linkedlist yang dibuat akan seperti ini:

First → [9] → [12] → [8] → [0] → [2] → Nil

Output yang diharapkan:
9 12 8 0 2


source code unguided 1
#### singlylist.h
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif // SINGLYLIST_H_INCLUDED
```

#### singlylist.cpp
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.First = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}
```

#### main.cpp
```C++
#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5 = Nil;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);   // 9 12 8 0 2

    return 0;
}
```

### Output Unguided 1 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL4/Screenshot_Output_soal1.png)


penjelasan unguided 1

Program ini digunakan untuk membuat singly linked list yang berisi beberapa angka. Data dimasukkan menggunakan ``fungsi alokasi()` dan `insertFirst()`, sehingga setiap angka baru ditambahkan ke bagian paling depan list. Fungsi  `printInfo()` digunakan untuk menampilkan semua data dari awal sampai akhir. Karena data dimasukkan dari depan, hasil akhirnya adalah 9 12 8 0 2.

### 2. Dari soal Latihan pertama, lakukan penghapusan node 9 menggunakan deleteFirst(), node 2 menggunakan deleteLast(), dan node 8 menggunakan deleteAfter(). Kemudian tampilkan jumlah node yang tersimpan menggunakan nbList() dan lakukan penghapusan seluruh node menggunakan deleteList().
Output yang diharapkan:

12 0

Jumlah node : 2

- List Berhasil Terhapus -
  
Jumlah node : 0


source code unguided 2
#### singlylist.h
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

// dari soal 1
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

// tambahan soal 2
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);
int nbList(List L);
void deleteList(List &L);

#endif // SINGLYLIST_H_INCLUDED
```

#### singlylist.cpp
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.First = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    // next nya P disambung ke First yg lama, abis itu First pindah ke P
    P->next = L.First;
    L.First = P;
}

// ----- tambahan soal 2 -----

void deleteFirst(List &L, address &P) {
    if (L.First != Nil) {
        P = L.First;
        L.First = P->next;
        P->next = Nil;
    } else {
        P = Nil; // listnya kosong, gaada yg dihapus
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == Nil) {
        // kosong
        P = Nil;
    } else if (L.First->next == Nil) {
        // elemennya cuma 1
        P = L.First;
        L.First = Nil;
    } else {
        // cari elemen sebelum yg terakhir
        address Q = L.First;
        while (Q->next->next != Nil) {
            Q = Q->next;
        }
        P = Q->next;
        Q->next = Nil;
    }
}

void deleteAfter(address Prec, address &P) {
    // hapus node yg ada setelah Prec
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    } else {
        P = Nil;
    }
}

int nbList(List L) {
    int jumlah = 0;
    address P = L.First;
    while (P != Nil) {
        jumlah++;
        P = P->next;
    }
    return jumlah;
}

void deleteList(List &L) {
    address P;
    // hapus dari depan terus sampe abis
    while (L.First != Nil) {
        deleteFirst(L, P);
        dealokasi(P);
    }
}
```
#### main.cpp
```C++
#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5 = Nil;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    address P;

    // hapus node 9
    deleteFirst(L, P);
    dealokasi(P);

    // hapus node 2
    deleteLast(L, P);
    dealokasi(P);

    // hapus node 8, sebelumnya node 12 (yg skrg jadi First)
    deleteAfter(L.First, P);
    dealokasi(P);

    printInfo(L);   // 12 0
    cout << "Jumlah node : " << nbList(L) << endl;

    // hapus semua
    deleteList(L);
    cout << endl << "- List Berhasil Terhapus -" << endl;
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}
```

### Output Unguided 2 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL4/Screenshot_Output_soal2.png)

penjelasan unguided 2

Program ini menggunakan struktur data singly linked list untuk menyimpan dan mengelola data berupa angka. Pertama, program membuat list dan memasukkan lima data, yaitu 2, 0, 8, 12, dan 9 menggunakan fungsi `insertFirst`. Selanjutnya, program menghapus node pertama, node terakhir, dan node setelah node pertama. Hasil akhirnya adalah data 12 dan 0 dengan jumlah 2 node. Setelah itu, fungsi `deleteList` digunakan untuk menghapus seluruh node sehingga list menjadi kosong.


## Kesimpulan
Berdasarkan praktikum yang telah dilakukan, singly linked list merupakan struktur data yang setiap node-nya menyimpan data dan pointer ke node berikutnya. Penambahan dan penghapusan node dilakukan dengan mengatur pointer sesuai posisi yang diinginkan. Selain itu, perlu memperhatikan kondisi list kosong atau hanya memiliki satu node, serta membebaskan memori yang sudah tidak digunakan agar program berjalan dengan baik.

## Referensi
[2]Tim Penyusun. (t.t.). *Modul 4: Singly Linked List (Bagian Pertama).* Praktikum Struktur Data, hlm. 36–46.

[2] GeeksforGeeks. (t.t.). *Singly Linked List Tutorial.* https://www.geeksforgeeks.org/dsa/singly-linked-list-tutorial/
