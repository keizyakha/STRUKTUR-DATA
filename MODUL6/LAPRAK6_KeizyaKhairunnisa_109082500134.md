# <h1 align="center">Laporan Praktikum Modul 6 - DOUBLY LINKED LIST (BAGIAN PERTAMA) </h1>
<p align="center"> Keizya Khairunnisa - 109082500134</p>

## Dasar Teori

1. Doubly Linked List

Doubly linked list adalah linked list yang tiap elemennya punya dua pointer: prev yang nunjuk ke elemen sebelumnya, dan next yang nunjuk ke elemen sesudahnya [1]. Karena ada dua arah, list bisa ditelusuri maju maupun mundur. Beda dengan single linked list yang tiap elemennya cuma punya satu pointer, jadi cuma bisa jalan satu arah [2].

Komponen utamanya [1]:

First: pointer list yang nunjuk elemen pertama.
Last: pointer list yang nunjuk elemen terakhir.
Next: pointer elemen yang nunjuk elemen berikutnya.
Prev: pointer elemen yang nunjuk elemen sebelumnya.

List dianggap kosong kalau First = Nil (NULL) [1].

2. Struktur Data (ADT)

Satu elemen (ElmList) isinya info (data), next, dan prev. List-nya (List) isinya First dan Last. Operasi dasarnya: CreateList (bikin list kosong), alokasi (bikin elemen baru), dealokasi (hapus elemen dari memori), dan printInfo (tampilin isi list) [1].

3. Operasi pada Doubly Linked List

Insert [1][2]

Insert First: elemen baru ditaruh paling depan, lalu First pindah ke elemen itu.
Insert Last: elemen baru ditaruh paling belakang, lalu Last pindah ke elemen itu.
Insert After: elemen baru disisipin setelah elemen tertentu (Prec). Pointer next dan prev elemen di sekitarnya ikut disambungin ulang.
Insert Before: kebalikan insert after, bedanya cuma di cara nyari elemennya [1].

Delete [1][2]

Delete First: elemen paling depan dilepas, First pindah ke elemen berikutnya.
Delete Last: elemen paling belakang dilepas, Last pindah ke elemen sebelumnya.
Delete After: elemen setelah Prec dilepas, lalu pointer Prec dan elemen berikutnya disambungin lagi.
Delete Before: kebalikan delete after [1].

Searching, update, dan view
Prosesnya pada dasarnya sama kayak single linked list. Bedanya, di doubly linked list lebih gampang karena bisa iterasi maju dan mundur [1].

4. Kelebihan dan Kekurangan

Kelebihannya, penelusuran bisa dua arah, dan insert serta delete jadi lebih mudah karena tiap elemen tahu posisi sebelum dan sesudahnya [2]. Kekurangannya, tiap elemen butuh satu pointer tambahan, jadi pemakaian memori lebih besar dibanding single linked list. Dibanding array, linked list lebih fleksibel buat memori dinamis, tapi akses datanya lebih lambat [4].


## Guided 1 doublylist.h

source code guided 1
```C++
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>

#define Nil NULL

// Latihan 1
struct infotype {
    std::string nopol; 
    std::string warna; 
    int thnBuat;      
};
typedef struct elmlist *address;
struct elmlist {
    infotype info;  
    address next;   
    address prev;   
};
struct List {
    address First; 
    address Last;  
};


// Latihan 1
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

// Latihan 2

address findElm(List L, std::string nopol);

// Latihan 3
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteElm(List &L, std::string nopol, bool &status);

#endif  
```
penjelasan guided 1

Program ini berisi deklarasi struktur data dan daftar fungsi untuk doubly linked list data kendaraan. Satu elemen menyimpan data kendaraan (nomor polisi, warna, tahun) serta pointer next dan prev. List-nya sendiri punya pointer First dan Last yang menunjuk elemen pertama dan terakhir. Di bawahnya ada deklarasi fungsi untuk tiga latihan: membuat dan menampilkan list, mencari data, dan menghapus data.


## Guided 2 doublylist.cpp

source code guided 2
```C++  
#include "Doublylist.h"

// Latihan 1
void CreateList(List &L) {
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x) {
    address P = new elmlist;
    P->info = x;
    P->next = Nil;
    P->prev = Nil; 
    return P;
}

void dealokasi(address &P) {
    delete P;
}

void printInfo(List L) {
    address P = L.Last;
    if (P == Nil) {
        std::cout << "List kosong." << std::endl;
        return;
    }
    while (P != Nil) {
        std::cout << "no polisi : " << P->info.nopol << std::endl;   
        std::cout << "warna     : " << P->info.warna << std::endl;   
        std::cout << "tahun     : " << P->info.thnBuat << std::endl; 
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == Nil) { 
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;         
        (L.Last)->next = P;     
        L.Last = P;               
    }
}

// Latihan 2
address findElm(List L, std::string nopol) {
    address P = L.First;
    while (P != Nil) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return Nil;
}

// Latihan 3
void deleteFirst(List &L, address &P) {
    if (L.First == Nil) return;

    P = L.First; 
    if (L.First == L.Last) { 
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.First = P->next;     
        (L.First)->prev = Nil; 
        P->next = Nil;         
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == Nil) return;

    P = L.Last; 
    if (L.First == L.Last) { 
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.Last = P->prev;      
        (L.Last)->next = Nil; 
        P->prev = Nil;         
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec == Nil || Prec->next == Nil) return;

    P = Prec->next;
    if (P == L.Last) {
        deleteLast(L, P);
    } else {
        Prec->next = P->next;     
        (P->next)->prev = Prec; 
        P->next = Nil;            
        P->prev = Nil;           
    }
}

void deleteElm(List &L, std::string nopol, bool &status) {
    address P = findElm(L, nopol);
    status = false;

    if (P != Nil) {
        if (P == L.First) {
            deleteFirst(L, P);
        } else if (P == L.Last) {
            deleteLast(L, P);
        } else {
            address Prec = P->prev;
            deleteAfter(L, Prec, P);
        }
        dealokasi(P); 
        status = true;
    }
}
```
penjelasan guided 2

Program ini berisi implementasi fungsi yang dideklarasikan di `doublylist.h`. Pada latihan 1, `CreateList` membuat list kosong, `alokasi` membuat elemen baru, `dealokasi` menghapus elemen dari memori, `printInfo` menampilkan isi list dari belakang ke depan, dan `insertLast` menambahkan elemen di akhir list. Pada latihan 2, `findElm` mencari elemen berdasarkan nomor polisi dan mengembalikan alamat elemen jika ditemukan atau `Nil` jika tidak. Pada latihan 3, `deleteFirst`, `deleteLast`, dan `deleteAfter` menghapus elemen di awal, akhir, dan setelah elemen tertentu, sedangkan `deleteElm` menghapus elemen sesuai posisinya.


## Guided 3 main.cpp

source code guided 3
```C++
#include <iostream>
#include "Doublylist.h"
using namespace std;

void inputData(List &L) {
    infotype data;
    address P;

    cout << "masukkan nomor polisi: "; cin >> data.nopol;
    cout << "masukkan warna kendaraan: "; cin >> data.warna;
    cout << "masukkan tahun kendaraan: "; cin >> data.thnBuat;
    if (findElm(L, data.nopol) == Nil) {
        P = alokasi(data); 
        insertLast(L, P);  
    } else {
        cout << "nomor polisi sudah terdaftar" << endl; 
    }
}

int main() {
    List L;
    CreateList(L); 
    address P;

    // Latihan 1
    inputData(L); 
    inputData(L); 
    inputData(L); 
    inputData(L); 

    cout << "\nDATA LIST 1" << endl; 
    printInfo(L); 

    // Latihan 2
    string nopolCari;
    cout << "\nMasukkan Nomor Polisi yang dicari : "; 
    cin >> nopolCari; 
    
    P = findElm(L, nopolCari); 
    if (P != Nil) {
        cout << "Nomor Polisi : " << P->info.nopol << endl; 
        cout << "Warna        : " << P->info.warna << endl; 
        cout << "Tahun        : " << P->info.thnBuat << endl; 
    } else {
        cout << "Data dengan nomor polisi " << nopolCari << " tidak ditemukan." << endl;
    }

    // Latihan 3
    string nopolHapus;
    bool hapusBerhasil;
    cout << "\nMasukkan Nomor Polisi yang akan dihapus : ";
    cin >> nopolHapus;

    deleteElm(L, nopolHapus, hapusBerhasil); 

    if (hapusBerhasil) {
        cout << "Data dengan nomor polisi " << nopolHapus << " berhasil dihapus." << endl; 
    } else {
        cout << "Data dengan nomor polisi " << nopolHapus << " tidak ditemukan." << endl;
    }
    cout << "\nDATA LIST 1" << endl; 
    printInfo(L); 

    return 0;
}
```
penjelasan guided 3

Program ini adalah program utama yang menjalankan semua fungsi tadi. Pertama, pengguna memasukkan 4 data kendaraan lewat inputData, dan nomor polisi yang sudah terdaftar ditolak. Setelah itu list ditampilkan. Lalu pengguna memasukkan nomor polisi yang ingin dicari, dan programnya menampilkan datanya atau pesan tidak ditemukan. Terakhir, pengguna memasukkan nomor polisi yang ingin dihapus, programnya menampilkan pesan berhasil atau tidak, lalu list ditampilkan lagi.


## Unguided 

### 1. Pembuatan ADT Dasar dan Insert Data

Buatlah ADT Doubly Linked List sebagai berikut di dalam file “Buku.h”:

```Text
Type infotype : buku <
    kodeBuku : string
    judul     : string
    thnTerbit : integer
>

Type address : pointer to ElmList
Type ElmList <
    info : infotype
    next : address
    prev : address
>

Type List <
    First : address
    Last : address
>

procedure CreateList( input/output L : List )
function alokasi( x : infotype ) -> address
procedure dealokasi( input/output P : address )
procedure printInfo( input L : List )
procedure insertLast( input/output L : List, input P : address )
```
Buatlah implementasi ADT Doubly Linked List pada file “Buku.cpp” dan cobalah hasil implementasi ADT tersebut pada file “main.cpp”. Pastikan sistem melakukan pengecekan duplikasi kodeBuku sebelum memasukkan data baru ke dalam list.
  
source code unguided soal 1

#### buku.h
```C++
#ifndef BUKU_H
#define BUKU_H

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};

typedef buku infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

// buat ngecek duplikasi kodeBuku
bool sudahAda(List L, string kode);

#endif
```

#### buku.cpp
```C++
#include "Buku.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

// dicetak dari belakang (Last -> First) sesuai contoh output
void printInfo(List L) {
    address P = L.Last;
    cout << "DATA LIST 1" << endl;
    while (P != NULL) {
        cout << "kode buku : " << P->info.kodeBuku << endl;
        cout << "judul     : " << P->info.judul << endl;
        cout << "tahun     : " << P->info.thnTerbit << endl;
        cout << endl; 
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        // list masih kosong
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

// true kalau kode udah ada di list
bool sudahAda(List L, string kode) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == kode) {
            return true;
        }
        P = P->next;
    }
    return false;
}
```

#### main.cpp
```C++
#include "Buku.h"

int main() {
    List L;
    CreateList(L);

    infotype x;
    address P;

    for (int i = 0; i < 4; i++) {
        cout << endl;
        cout << "masukkan kode buku: ";
        cin >> x.kodeBuku;
        cout << "masukkan judul buku: ";
        cin >> x.judul;
        cout << "masukkan tahun terbit: ";
        cin >> x.thnTerbit;

        if (sudahAda(L, x.kodeBuku)) {
            // kode udah ada, ga jadi dimasukin
            cout << "kode buku sudah terdaftar" << endl; 
        } else {
            P = alokasi(x);
            insertLast(L, P);
        }
    }
    cout << endl;
    printInfo(L);

    return 0;
}
```

### Output Unguided soal 1 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL6/Screenshot_Output_soal1.png)


penjelasan unguided 1

Program ini dipakai buat nyimpen data buku (kode, judul, tahun terbit) di sebuah doubly linked list. Tiap data punya pointer next dan prev, jadi bisa jalan maju maupun mundur. Data dimasukin lewat insertLast, jadi buku baru selalu nyambung di belakang list. Sebelum dimasukin, program ngecek dulu kode bukunya udah ada atau belum. Kalau udah ada, muncul tulisan “kode buku sudah terdaftar” dan datanya ga disimpen. Waktu ditampilin, printInfo jalan dari Last mundur ke First, makanya urutannya B004, B003, B001.


### 2. Pencarian Elemen (Searching)

Carilah elemen dengan kode buku B001 dengan membuat fungsi baru:
fungsi findElm( L : List, x : infotype ) : address

Contoh Output Pencarian:
```Text
Masukkan Kode Buku yang dicari : B001

Kode Buku    : B001
Judul        : Algoritma
Tahun Terbit : 2020
```

source code unguided 2

#### buku.h
```C++
#ifndef BUKU_H
#define BUKU_H

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};

typedef buku infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

// HAPUS (punya soal 1, diganti findElm)
// bool sudahAda(List L, string kode);

// tambah sesuai perintah soal
address findElm(List L, infotype x);

#endif
```

#### buku.cpp
```C++
#include "Buku.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.Last;
    cout << "DATA LIST 1" << endl;
    while (P != NULL) {
        cout << "kode buku : " << P->info.kodeBuku << endl;
        cout << "judul     : " << P->info.judul << endl;
        cout << "tahun     : " << P->info.thnTerbit << endl;
        cout << endl;  
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        // list masih kosong
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

// HAPUS (fungsi sudahAda punya soal 1, diganti findElm di bawah)
// bool sudahAda(List L, string kode) {
//     address P = L.First;
//     while (P != NULL) {
//         if (P->info.kodeBuku == kode) {
//             return true;
//         }
//         P = P->next;
//     }
//     return false;
// }

// tambah sesuai perintah soal (seluruh fungsi findElm)
address findElm(List L, infotype x) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == x.kodeBuku) {
            return P;
        }
        P = P->next;
    }
    return NULL;
} 
```

#### main.cpp
```C++
#include "Buku.h"

int main() {
    List L;
    CreateList(L);

    infotype x;
    address P;

    for (int i = 0; i < 4; i++) {
        cout << endl;   
        cout << "masukkan kode buku: ";
        cin >> x.kodeBuku;
        cout << "masukkan judul buku: ";
        cin >> x.judul;
        cout << "masukkan tahun terbit: ";
        cin >> x.thnTerbit;

        // HAPUS: if (sudahAda(L, x.kodeBuku)) {
        // UBAH (pakai findElm): sesuai perintah soal
        if (findElm(L, x) != NULL) {
            // kode udah ada, ga jadi dimasukin
            cout << "kode buku sudah terdaftar" << endl; 
        } else {
            P = alokasi(x);
            insertLast(L, P);
        }
    }
    cout << endl;
    printInfo(L);

    // TAMBAH (searching, sampai tanda "selesai")
    cout << endl;
    cout << "Masukkan Kode Buku yang dicari : ";
    cin >> x.kodeBuku;
    P = findElm(L, x);
    if (P != NULL) {
        cout << "Kode Buku    : " << P->info.kodeBuku << endl;
        cout << "Judul        : " << P->info.judul << endl;
        cout << "Tahun Terbit : " << P->info.thnTerbit << endl;
    } else {
        cout << "Buku tidak ditemukan." << endl;
    }
    // TAMBAH selesai

    return 0;
}
```

### Output Unguided 2 :

![Screenshot Output 1](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL6/Screenshot_Output_soal2(1).png)

![Screenshot Output 2](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL6/Screenshot_Output_soal2(2).png)

penjelasan unguided 2

Program ini nambahin fitur nyari buku berdasarkan kode bukunya. Fungsi findElm ngecek satu-satu dari elemen pertama pakai pointer next, sampai ketemu kode yang sama. Kalau ketemu, fungsinya ngasih alamat elemen itu, terus datanya ditampilin. Kalau sampai ujung list ga ketemu, fungsinya ngasih NULL dan program nampilin “Buku tidak ditemukan”. Fungsi ini juga dipakai buat ngecek duplikat pas insert, jadi sudahAda dari soal 1 udah ga kepake.




### 3. Penghapusan Elemen (Delete)
Hapus elemen dengan kode buku B003 dengan membuat prosedur delete berikut:
```Text
procedure deleteFirst( input/output L : List, input/output P : address )
procedure deleteLast( input/output L : List, input/output P : address )
procedure deleteAfter( input Prec : address, input/output P : address )
```

Contoh Output Penghapusan:
```Text
Masukkan Kode Buku yang akan dihapus : B003
Data dengan kode buku B003 berhasil dihapus.

DATA LIST 1
Kode Buku    : B004
Judul        : Jaringan_Komputer
Tahun Terbit : 2022
Kode Buku    : B001
Judul        : Algoritma
Tahun Terbit : 2020
```

source code unguided 3

#### buku.h
```C++
#ifndef BUKU_H
#define BUKU_H

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};

typedef buku infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

// dari soal 2, tetap dipakai buat nyari elemen yang mau dihapus
address findElm(List L, infotype x);

// TAMBAH (sesuai perintah soal)
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);

#endif

```

#### buku.cpp
```C++
#include "Buku.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

// dicetak dari belakang (Last -> First) sesuai contoh output
void printInfo(List L) {
    address P = L.Last;
    cout << "DATA LIST 1" << endl;
    while (P != NULL) {
        // HAPUS: cout << "kode buku : " << P->info.kodeBuku << endl;
        // HAPUS: cout << "judul     : " << P->info.judul << endl;
        // HAPUS: cout << "tahun     : " << P->info.thnTerbit << endl;

        // UBAH (label disesuaikan sama output soal 3)
        cout << "Kode Buku    : " << P->info.kodeBuku << endl;
        cout << "Judul        : " << P->info.judul << endl;
        cout << "Tahun Terbit : " << P->info.thnTerbit << endl;
        cout << endl;   
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        // list masih kosong
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

// dari soal 2, ga ada yang diubah
address findElm(List L, infotype x) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == x.kodeBuku) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

// TAMBAH (3 procedure delete, sampai tanda "selesai")
void deleteFirst(List &L, address &P) {
    if (L.First == NULL) {
        P = NULL;
    } else if (L.First == L.Last) {
        // cuma 1 elemen
        P = L.First;
        L.First = NULL;
        L.Last = NULL;
    } else {
        P = L.First;
        L.First = P->next;
        L.First->prev = NULL;
        P->next = NULL;
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == NULL) {
        P = NULL;
    } else if (L.First == L.Last) {
        P = L.Last;
        L.First = NULL;
        L.Last = NULL;
    } else {
        P = L.Last;
        L.Last = P->prev;
        L.Last->next = NULL;
        P->prev = NULL;
    }
}

// hapus elemen setelah Prec
void deleteAfter(address Prec, address &P) {
    P = Prec->next;
    if (P != NULL) {
        Prec->next = P->next;
        if (P->next != NULL) {
            P->next->prev = Prec;
        }
        P->next = NULL;
        P->prev = NULL;
    }
}
// TAMBAH selesai
```

#### main.cpp
```C++
#include "Buku.h"

int main() {
    List L;
    CreateList(L);

    infotype x;
    address P;

    for (int i = 0; i < 4; i++) {
        cout << endl;  
        cout << "masukkan kode buku: ";
        cin >> x.kodeBuku;
        cout << "masukkan judul buku: ";
        cin >> x.judul;
        cout << "masukkan tahun terbit: ";
        cin >> x.thnTerbit;

        if (findElm(L, x) != NULL) {
            // kode udah ada, ga jadi dimasukin
            cout << "kode buku sudah terdaftar" << endl;   
        } else {
            P = alokasi(x);
            insertLast(L, P);
        }
    }
    cout << endl;
    printInfo(L);

    // HAPUS (blok searching dari soal 2, ga dipakai di soal 3)
    // cout << endl;
    // cout << "Masukkan Kode Buku yang dicari : ";
    // cin >> x.kodeBuku;
    // P = findElm(L, x);
    // if (P != NULL) {
    //     cout << "Kode Buku    : " << P->info.kodeBuku << endl;
    //     cout << "Judul        : " << P->info.judul << endl;
    //     cout << "Tahun Terbit : " << P->info.thnTerbit << endl;
    // } else {
    //     cout << "Buku tidak ditemukan." << endl;
    // }

    // TAMBAH (penghapusan, sampai tanda "selesai")
    cout << endl;
    cout << "Masukkan Kode Buku yang akan dihapus : ";
    cin >> x.kodeBuku;
    P = findElm(L, x);
    if (P == NULL) {
        cout << "Data tidak ditemukan." << endl;
    } else {
        address hapus;
        if (P == L.First) {
            deleteFirst(L, hapus);
        } else if (P == L.Last) {
            deleteLast(L, hapus);
        } else {
            deleteAfter(P->prev, hapus);
        }
        dealokasi(hapus);
        cout << "Data dengan kode buku " << x.kodeBuku << " berhasil dihapus." << endl;
        printInfo(L);
    }
    // TAMBAH selesai

    return 0;
}
```

### Output Unguided 3 :

![Screenshot Output 1](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL6/Screenshot_Output_soal3(1).png)

![Screenshot Output 2](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL6/Screenshot_Output_soal3(2).png)


penjelasan unguided 3

Program ini dipakai buat ngehapus buku dari list berdasarkan kode bukunya. Pertama kodenya dicari dulu pakai findElm. Kalau ketemu, cara hapusnya tergantung posisi elemennya. Kalau di paling depan dipakai deleteFirst, kalau di paling belakang dipakai deleteLast, dan kalau di tengah dipakai deleteAfter dengan Prec berupa elemen sebelumnya. Di contoh, B003 ada di tengah, jadi kena deleteAfter. Setelah dilepas dari list, elemennya di-dealokasi biar memorinya kebebasin, terus list ditampilin lagi tanpa B003.

## Kesimpulan

Dari praktikum ini saya belajar cara membuat dan memakai doubly linked list di C++. Setiap elemennya punya pointer next dan prev, jadi list bisa dijelajahi dari depan maupun dari belakang.

Di soal 1, data buku dimasukkan ke list dengan insertLast, dan kode buku dicek dulu supaya tidak ada yang kembar. Di soal 2, fungsi findElm dipakai untuk mencari buku berdasarkan kode bukunya. Di soal 3, buku dihapus dengan deleteFirst, deleteLast, atau deleteAfter, tergantung posisinya di list.

Hasilnya, doubly linked list membuat penambahan, pencarian, dan penghapusan data lebih mudah karena setiap elemen terhubung ke elemen sebelum dan sesudahnya. Tapi pointer-nya harus diatur dengan teliti supaya list tidak putus.

## Referensi

[1] Modul Praktikum Struktur Data, “Modul 6: Doubly Linked List,” hlm. 51–58.

[2] A. Wijoyo dkk., “Penggunaan Algoritma Doubly Linked List Untuk Insertion Dan Deletion,” JRIIN, vol. 1, no. 12, hlm. 1329–1331, 2024. https://jurnalmahasiswa.com/index.php/jriin/article/view/1282

[3] M. T. Mbejo dkk., “Analisis Struktur Data Linked List dalam Pengolahan Data Mahasiswa,” JSIT, vol. 2, no. 2, hlm. 441–444, 2025. https://rcf-indonesia.org/jurnal/index.php/jsit/article/download/591/418

[4] A. Wijoyo dkk., “Perbandingan struktur linked list dan array dalam manajemen memori,” JRIIN, vol. 1, no. 12, hlm. 1290–1293, 2024. https://www.jurnalmahasiswa.com/index.php/jriin/article/view/957 