# <h1 align="center">Laporan Praktikum Modul 5 SINGLY LINKED LIST - (BAGIAN KEDUA)  </h1>
<p align="center"> Keizya Khairunnisa - 109082500134</p>

## Dasar Teori

1. Singly Linked List

Linked list adalah struktur data yang elemen-elemennya disusun berurutan, tapi urutannya ditentukan oleh pointer di tiap elemen, bukan oleh posisi di memori seperti pada array [2]. Pada singly linked list, tiap elemen (node) punya dua bagian, yaitu info yang menyimpan data dan next yang menyimpan alamat elemen berikutnya [1][2]. Jadi satu node cuma tahu siapa yang ada setelahnya, dan penelusuran hanya bisa maju ke satu arah.

List sendiri direpresentasikan oleh satu pointer first yang menunjuk elemen pertama. Kalau first = Nil, berarti list kosong, dan elemen terakhir ditandai dengan next = Nil [1]. Setiap elemen yang ditunjuk oleh pointer P diakses lewat P->info dan P->next [1].

2. Pointer dan Alokasi Memori Dinamis

Linked list bisa dibuat karena adanya pointer, yaitu variabel yang menyimpan alamat memori variabel lain. Operator & dipakai untuk mengambil alamat, dan operator * (atau -> untuk struct) dipakai untuk mengakses isi dari alamat itu [3]. Elemen list dibuat saat program berjalan dengan new dan dikembalikan ke sistem dengan delete, sehingga ukuran list bisa bertambah atau berkurang sesuai kebutuhan [3]. Hal ini yang jadi dasar fungsi alokasi dan dealokasi di ADT yang dibuat pada latihan.

3. Abstract Data Type (ADT)

Menurut modul, semua operasi dasar linked list merupakan bagian dari ADT singly linked list. Penerapannya dipisah menjadi dua file, yaitu file header (.h) yang berisi deklarasi tipe dan prototype fungsi, dan file implementasi (.cpp) yang berisi isi fungsinya [1]. Dengan cara ini, program utama (main.cpp) cukup memanggil fungsi tanpa perlu tahu cara kerja di dalamnya.

4. Operasi Dasar yang Dipakai pada Latihan
CreateList. Membentuk list kosong dengan mengisi first dengan Nil [1].
alokasi dan dealokasi. alokasi membuat elemen baru berisi nilai tertentu, sedangkan dealokasi mengembalikan memori elemen ke sistem [1].
insertFirst. Menaruh elemen baru di awal list. Elemen baru diarahkan ke elemen yang tadinya pertama, lalu first dipindahkan ke elemen baru [1]. Operasi ini cepat karena tidak perlu menelusuri list, yaitu O(1) [2]. Karena penyisipan selalu di depan, elemen yang dimasukkan paling akhir akan berada paling depan.
printInfo. Menampilkan semua isi list dengan menelusuri (traversal) dari elemen pertama sampai Nil [1].
5. Searching

Searching adalah operasi mencari node tertentu dengan mengunjungi setiap node dan berhenti setelah node yang dicari ketemu [1]. Menurut modul, operasi ini juga mempermudah operasi lain seperti insert after, delete after, dan update [1]. Fungsi findElm mengembalikan alamat elemen yang info-nya sama dengan nilai yang dicari, atau Nil kalau tidak ada [1]. Karena pencariannya berurutan (linear search), kasus terburuknya harus melewati seluruh elemen sehingga kompleksitasnya O(n) [2].

6. Penjumlahan Seluruh Elemen

Menjumlahkan semua info pada list memakai prinsip traversal yang sama dengan printInfo. Bedanya, tiap elemen yang dikunjungi tidak dicetak, tapi nilainya ditambahkan ke sebuah variabel penampung. Hasil akhirnya didapat setelah seluruh elemen dikunjungi, dan sama seperti searching, kompleksitasnya O(n) karena tiap elemen dikunjungi satu kali [2].


## Guided

### Guided 1 listBuah.h

source code guided 1
```C++
#ifndef LISTBUAH_H
#define LISTBUAH_H
#define Nil NULL

#include<iostream>
using namespace std;

struct buah{
    string nama;
    int jumlah; 
    float harga;
};

typedef buah dataBuah;  

typedef struct node *address; 

struct node{ 
    dataBuah isidata;
    address next;
};

struct linkedlist{ 
    address first;
};

bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, int jumlah, float harga);
void dealokasi(address &node);
void printList(linkedlist List);
void insertFirst(linkedlist &List, address nodeBaru);
void insertAfter(linkedlist &List, address nodeBaru, address prev);
void insertLast(linkedlist &List, address nodeBaru);
void delFirst(linkedlist &List);
void delLast(linkedlist &List);
void delAfter(linkedlist &List, address nodeHapus, address nodePrev);
int nbList(linkedlist List);
void deleteList(linkedlist &List);

void updateFirst(linkedlist List);
void updateLast(linkedlist List);
void updateAfter(linkedlist List, address prev);

void FindNodeByData(linkedlist list, string data);
void FindNodeByAddress(linkedlist list, address node);
void FindNodeByRange(linkedlist list, float hargaAwal, float HargaAkhir);

#endif
```
penjelasan guided 1

Program ini digunakan untuk mendefinisikan struktur data linked list untuk menyimpan data buah berupa nama, jumlah, dan harga. File ini juga berisi deklarasi fungsi untuk membuat list, menambah, menghapus, memperbarui, mencari, dan menghitung jumlah node. Deklarasi ini nantinya digunakan oleh file program lain yang menjalankan fungsi-fungsi tersebut.

### Guided 2 listBuah.cpp

source code guided 2
```C++  
#include "listBuah.h"
#include <iostream>
using namespace std;

//fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedlist List) {
    if(List.first == Nil){
        return true; 
    } else {
        return false;
    }
}

//pembuatan linked list kosong
void createList(linkedlist &List) {
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, int jumlah, float harga) { 
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.jumlah = jumlah; 
    nodeBaru->isidata.harga = harga;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru) {
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
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

//prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(linkedlist &List){
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
        cout << "Node pertama berhasil terhapus!" << endl;
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List){
    address nodeHapus, nodePrev;
    if(isEmpty(List) == false){
        nodeHapus = List.first;
        if(nodeHapus->next == Nil){
            List.first->next = Nil;
            dealokasi(nodeHapus);
        } else { 
            while(nodeHapus->next != Nil){
                nodePrev = nodeHapus; 
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil; 
            dealokasi(nodeHapus);
        }
        cout << "Node terakhir berhasil terhapus!" << endl;
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) { 
            nodeHapus = nodePrev->next;       
            nodePrev->next = nodeHapus->next;  
            nodeHapus->next = Nil;         
            dealokasi(nodeHapus);
            cout << "Node setelah node " << nodePrev->isidata.nama << " berhasil terhapus!" << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

//prosedur untuk menampilkan isi list
void printList(linkedlist List) {
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List) {
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next; 
    }
    return count;
}

//prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedlist &List){
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus); 
    }
    List.first = Nil; 
    cout << "List berhasil terhapus!" << endl;
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - UPDATE -----*/
//prosedur-prosedur untuk melakukan update data node
void updateFirst(linkedlist List){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        cout << "Masukkan update data node pertama : " << endl;
        cout << "Nama buah : ";
        cin >> List.first->isidata.nama;
        cout << "Jumlah : ";
        cin >> List.first->isidata.jumlah;
        cout << "Harga : ";
        cin >> List.first->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateLast(linkedlist List){
    if (isEmpty(List) == true) {
        cout << "List Kosong!" << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        cout << "masukkan update data node terakhir : " << endl;
        cout << "Nama buah : ";
        cin >> nodeBantu->isidata.nama;
        cout << "Jumlah : ";
        cin >> nodeBantu->isidata.jumlah;
        cout << "Harga : ";
        cin >> nodeBantu->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateAfter(linkedlist List, address nodePrev){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        if (nodePrev != Nil && nodePrev->next != Nil){
            address nodeBantu = nodePrev->next;
            cout << "masukkan update data node setelah node " << nodePrev->isidata.nama << " : " << endl;
            cout << "Nama buah : ";
            cin >> nodeBantu->isidata.nama;
            cout << "Jumlah : ";
            cin >> nodeBantu->isidata.jumlah;
            cout << "Harga : ";
            cin >> nodeBantu->isidata.harga;
            cout << "Data Berhasil Diupdate!" << endl;
            cout << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - SEARCHING -----*/
//prosedur-prosedur untuk searching data
//prosedur untuk mencari node berdasarkan data
void FindNodeByData(linkedlist list, string data){
    if(isEmpty(list) == true){
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while(nodeBantu != Nil){
            posisi++;
            if(nodeBantu->isidata.nama == data){
                cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false){
            cout << "Node dengan data " << data << " tidak ditemukan!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan alamat node
void FindNodeByAddress(linkedlist list, address node) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while (nodeBantu != Nil) {
            posisi++;
            if(nodeBantu == node) {
                cout << "Node ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Alamat node : " << nodeBantu << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Node dengan alamat " << node << " tidak ditemukan dalam list!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan range data (range harga)
void FindNodeByRange(linkedlist list, float hargaAwal, float hargaAkhir) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        cout << "--- Buah dalam range harga " << hargaAwal << " - " << hargaAkhir << " ---" << endl;
        cout << "-------------------------------------------" << endl;
        while (nodeBantu != Nil) {
            posisi++;
            float harga = nodeBantu->isidata.harga;
            if(harga >= hargaAwal && harga <= hargaAkhir) {
                cout << "Data ditemukan pada posisi ke-" << posisi << " :" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                cout << "-------------------------------------------" << endl;
                found = true;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Tidak ada data buah dalam range harga tersebut!" << endl;
            cout << "-------------------------------------------" << endl;
        }
    }
    cout << endl;
}
```
penjelasan guided 2

Program listBuah.cpp ini berisi implementasi fungsi-fungsi linked list, mulai dari mengecek list kosong, membuat node, menambah dan menghapus node, sampai menampilkan serta menghitung jumlah node. Selain itu, terdapat fungsi untuk memperbarui data buah pada node pertama, terakhir, atau setelah node tertentu. Program juga menyediakan fitur pencarian buah berdasarkan nama, alamat node, dan rentang harga. Setiap fungsi dibuat agar data buah dapat dikelola sesuai kebutuhan.


### Guided 3 main.cpp

source code guided 3
```C++
#include "listBuah.h"

  #include<iostream>
  using namespace std;

  int main(){
      linkedlist List;
      address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
      createList(List);

      dataBuah dtBuah;

      nodeA = alokasi("Jeruk", 100, 3000);
      nodeB = alokasi("Apel", 75, 4000);
      nodeC = alokasi("Pir", 87, 5000);
      nodeD = alokasi("Semangka", 43, 11500);
      nodeE = alokasi("Durian", 15, 31450);

      insertFirst(List, nodeA);
      insertLast(List, nodeB);
      insertAfter(List, nodeC, nodeA);
      insertAfter(List, nodeD, nodeC);
      insertLast(List, nodeE);

      cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      updateFirst(List);
      printList(List);
      updateLast(List);
      printList(List);
      updateAfter(List, nodeD);
      printList(List);

      cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      FindNodeByData(List, "kelapa");
      FindNodeByAddress(List, nodeC);
      FindNodeByRange(List, 5000, 10000);

      delFirst(List);
      printList(List);
      delLast(List);
      printList(List);
      delAfter(List, nodeD, nodeC);
      printList(List);

      cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      deleteList(List);
      cout << "--- ISI LIST SETELAH DILAKUKAN HAPUS LIST ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      return 0;
  }
```
penjelasan guided 3

Program ini digunakan untuk membuat linked list yang berisi data buah, seperti nama, jumlah, dan harga. Data dimasukkan ke dalam list menggunakan beberapa fungsi insert, lalu ditampilkan dan dihitung jumlah nodenya. Setelah itu, program melakukan update data dan pencarian buah berdasarkan nama, alamat node, serta rentang harga. Selanjutnya, beberapa node dihapus satu per satu, kemudian seluruh list dihapus menggunakan `deleteList()`. Di setiap tahap, isi list dan jumlah nodenya ditampilkan untuk melihat perubahan data.


## Unguided 

### 2. Buatlah ADT Singly Linked List sebagai berikut di dalam file “Singlylist.h”:

Type infotype : int
Type address : pointer to ElmList
Type ElmList < info : infotype, next : address >
Type List : < First : address >
procedure CreateList(input/output L : List)
function alokasi(x : infotype) → address
procedure dealokasi(input/output P : address)
procedure printInfo(input L : List)
procedure insertFirst(input/output L : List, input P : address)

Kemudian buat implementasi ADT Singly Linked List pada file “Singlylist.cpp”. Cobalah hasil implementasi ADT pada file “main.cpp”.

  
source code unguided soal 2
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
    address first;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif
```

#### singlylist.cpp
```C++
#include "Singlylist.h"

void CreateList(List &L) {
    L.first = Nil;
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
    address P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.first;
    L.first = P;
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

    CreateList(L);

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

    printInfo(L);
    return 0;
}
```

### Output Unguided soal 2 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL5/Screenshot_Output_soal2.png)


penjelasan unguided soal 2

Program ini digunakan untuk membuat singly linked list dengan memasukkan lima data, yaitu 2, 0, 8, 12, dan 9. Pertama, program membuat list kosong menggunakan `CreateList(L)`. Setelah itu, setiap data dibuat menjadi node baru menggunakan fungsi `alokasi()`, lalu dimasukkan ke bagian awal list menggunakan `insertFirst()`. Setiap node menyimpan nilai data dan alamat node berikutnya. Karena data selalu dimasukkan dari bagian awal, urutan datanya menjadi terbalik, yaitu 9, 12, 8, 0, dan 2. Terakhir, fungsi `printInfo()` digunakan untuk menampilkan seluruh data dalam linked list.

### 3. Carilah elemen dengan info 8 dengan membuat fungsi baru.
`function findElm(L : List, x : infotype) : address`

source code unguided 3
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
    address first;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);
address findElm(List L, infotype x);

#endif
```
kode singlylist.h sama dengan soal 2, tapi sesuai perintah soal 3, tambahkan kode berikut:

sebelum #endif
```C++
   address findElm(List L, infotype x);
```

#### singlylist.cpp
```C++
#include "Singlylist.h"

void CreateList(List &L) {
    L.first = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

address findElm(List L, infotype x) {
    address P = L.first;
    while (P != Nil) {
        if (P->info == x) {
            return P;
        }
        P = P->next;
    }
    return Nil;
}
void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.first;
    L.first = P;
}
```
kode singlylist.cpp sama seperti soal 2 tetapi sesuai perintah soal 3, tambahkan kode berikut:

```C++
address findElm(List L, infotype x) {
    address P = L.first;
    while (P != Nil) {
        if (P->info == x) {
            return P;
        }
        P = P->next;
    }
    return Nil;
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

    CreateList(L);

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

    printInfo(L);
    address hasil = findElm(L, 8);
if (hasil != Nil) {
    cout << hasil->info << " ditemukan dalam list" << endl;
} else {
    cout << "8 tidak ditemukan dalam list" << endl;
}
    return 0;
}
```

sesuai perintah soal, tambahkan kode yg sesuai tepat setelah printInfo(L);

```C++
address hasil = findElm(L, 8);
if (hasil != Nil) {
    cout << hasil->info << " ditemukan dalam list" << endl;
} else {
    cout << "8 tidak ditemukan dalam list" << endl;
}
```

### Output Unguided soal 3 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL5/Screenshot_Output_soal3.png)

penjelasan unguided soal 3

Fungsi findElm mencari elemen yang isinya sama dengan angka yang dicari. Caranya, ia mulai dari elemen pertama lalu pindah ke elemen berikutnya satu per satu. Tiap elemen dicek, kalau info-nya sama dengan x, alamat elemen itu langsung dikembalikan. Kalau sudah sampai ujung list dan tidak ada yang cocok, fungsi mengembalikan Nil. Di main, hasilnya dicek: kalau tidak Nil berarti angka 8 ada dan ditampilkan “8 ditemukan dalam list”, kalau Nil berarti tidak ada.

### 4. Hitunglah jumlah total info seluruh elemen (9+12+8+0+2=31).

source code unguided soal 4
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
    address first;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);
int sumInfo(List L);   // <-- TAMBAHAN SESUAI PERINTAH SOAL

#endif
```

#### singlylist.cpp
```C++
#include "Singlylist.h"

void CreateList(List &L) {
    L.first = Nil;
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
    address P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.first;
    L.first = P;
}

// <-- TAMBAHAN  SESUAI PERINTAH SOAL (seluruh fungsi ini)
int sumInfo(List L) {
    int total = 0;
    address P = L.first;
    while (P != Nil) {
        total = total + P->info;
        P = P->next;
    }
    return total;
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
    CreateList(L);

    P1 = alokasi(2);  insertFirst(L, P1);
    P2 = alokasi(0);  insertFirst(L, P2);
    P3 = alokasi(8);  insertFirst(L, P3);
    P4 = alokasi(12); insertFirst(L, P4);
    P5 = alokasi(9);  insertFirst(L, P5);

    printInfo(L);

    // <-- TAMBAHAN SESUAI PERINTAH SOAL
    cout << "Total info dari kelima elemen adalah " << sumInfo(L) << endl;

    return 0;
}
```

### Output Unguided soal 4 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/MODUL5/Screenshot_Output_soal4.png)

penjelasan unguided soal 4

Fungsi sumInfo menjumlahkan semua isi elemen di list. Variabel total mulai dari 0, lalu list ditelusuri dari elemen pertama sampai habis, dan info tiap elemen ditambahkan ke total. Setelah semua elemen terlewati, nilai total dikembalikan. Untuk data di soal, hitungannya 9 + 12 + 8 + 0 + 2 sehingga hasilnya 31, dan angka itu yang dicetak di main.


## Kesimpulan

Singly linked list menyimpan data dalam node yang terhubung lewat pointer `next`, sehingga ukurannya bisa berubah saat program berjalan. Lewat ADT yang dibuat pada latihan ini, operasi `insertFirst` dan `printInfo` berjalan dengan benar, dan data yang dimasukkan 2, 0, 8, 12, 9 tampil terbalik menjadi 9 12 8 0 2 karena penyisipan selalu dilakukan di depan list. Fungsi `findElm` berhasil menemukan elemen dengan info 8, dan fungsi `sumInfo` menghasilkan total 31 sesuai hitungan di soal. Keduanya bekerja dengan menelusuri elemen satu per satu, jadi waktunya bergantung pada jumlah elemen dalam list.


## Referensi

[1] Laboratorium Struktur Data, Modul 5: Singly Linked List (Bagian Kedua), Praktikum Struktur Data.

[2] T. H. Cormen, C. E. Leiserson, R. L. Rivest, dan C. Stein, Introduction to Algorithms, 3rd ed. Cambridge, MA: MIT Press, 2009, Bab 10.2 “Linked lists”.

[3] T. Donaldson, “Linked Lists,” CMPT 225, Simon Fraser University. https://www2.cs.sfu.ca/CourseCentral/225/tjd/linked_lists.html