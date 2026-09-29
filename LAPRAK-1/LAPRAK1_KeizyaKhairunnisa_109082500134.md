# <h1 align="center">Laporan Praktikum Modul 1 - Codeblocks IDE & Pengenalan Bahasa C++ (Bagian Pertama)</h1>
<p align="center"> Keizya Khairunnisa - 109082500134</p>

## Dasar Teori
Tipe data adalah bentuk pengelompokan data berdasarkan jenis nilai yang dapat ditampung, seperti integer untuk bilangan bulat dan float untuk bilangan pecahan, di mana bahasa C++ menerapkan konsep strongly typed sehingga setiap variabel harus dideklarasikan dengan tipe data yang jelas. Operator aritmatika digunakan untuk melakukan operasi matematika dasar seperti penjumlahan (+), pengurangan (-), perkalian (*), dan pembagian (/) terhadap dua buah operand[1].

Percabangan (branching) merupakan struktur kontrol program yang digunakan untuk menjalankan blok kode tertentu berdasarkan suatu kondisi. Struktur if-else akan menjalankan satu blok kode jika kondisi bernilai benar, dan menjalankan blok kode lain jika kondisi bernilai salah, sehingga cocok digunakan untuk memilih hasil keluaran berdasarkan nilai input yang diterima program[2].

Perulangan (looping) adalah struktur kontrol program yang digunakan untuk mengeksekusi suatu blok kode secara berulang selama kondisi tertentu masih terpenuhi. Struktur for umum digunakan ketika jumlah perulangan sudah diketahui sejak awal, dan dapat disusun bertingkat (nested loop) untuk menghasilkan pola keluaran tertentu, seperti pada pembuatan pola atau tabel di layar.



## Unguided 

### 1. Buatlah program yang menerima input-an dua buah bilangan bertipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian dan pembagian dari dua bilangan tersebut.

source code unguided 1

#include <iostream>
using namespace std;

int main() {
    float a, b;

    cout << "masukkan bilangan pertama : ";
    cin >> a;
    cout << "masukkan bilangan kedua : ";
    cin >> b;

    float tambah = a + b;
    float kurang = a - b;
    float kali = a * b;
    float bagi = a / b;

    cout << "hasil tambah = " << tambah << endl;
    cout << "hasil kurang = " << kurang << endl;
    cout << "hasil kali = " << kali << endl;
    cout << "hasil bagi = " << bagi << endl;

    return 0;
}
### Output Unguided 1 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/LAPRAK-1/Screenshot_Output_soal1.png)


penjelasan unguided 1 
Program ini digunakan untuk menghitung dua bilangan yang dimasukkan oleh pengguna. Program akan menghitung hasil tambah, kurang, kali, dan bagi dari kedua bilangan tersebut, lalu menampilkan hasilnya.

### 2. Buatlah sebuah program yang menerima masukan angka dan mengeluarkan ouput nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-inputkan user adalah bilangan bulat positif muali dari 0 s.d 10.

source code unguided 2

#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "masukkan angka (0-100) : ";
    cin >> n;

    string kata[20] = {"nol", "satu", "dua", "tiga", "empat", "lima", "enam",
                        "tujuh", "delapan", "sembilan", "sepuluh", "sebelas",
                        "dua belas", "tiga belas", "empat belas", "lima belas",
                        "enam belas", "tujuh belas", "delapan belas", "sembilan belas"};

    string puluh[10] = {"", "", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};

    if (n == 100) {
        cout << n << " : seratus" << endl;
    } else if (n < 20) {
        cout << n << " : " << kata[n] << endl;
    } else {
        int depan = n / 10;
        int belakang = n % 10;

        if (belakang == 0) {
            cout << n << " : " << puluh[depan] << " puluh" << endl;
        } else {
            cout << n << " : " << puluh[depan] << " puluh " << kata[belakang] << endl;
        }
    }

    return 0;
}
### Output Unguided 2 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/LAPRAK-1/Screenshot_Output_soal2.png)


penjelasan unguided 2
Program ini digunakan untuk mengubah angka dari 0 sampai 100 menjadi tulisan dalam bahasa Indonesia. Pengguna memasukkan angka, lalu program akan mengecek angka tersebut dan menampilkan bentuk tulisannya, seperti 25 menjadi “dua puluh lima”.

### 3. Buatlah program yang dapat menerima input dan output sbb. (digambar)

source code unguided 3

#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "input: ";
    cin >> n;

    cout << "output:" << endl;

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j < i; j++) {
            cout << " ";
        }

        for (int k = n - i; k >= 1; k--) {
            cout << k << " ";
        }

        cout << "*";

        for (int k = 1; k <= n - i; k++) {
            cout << " " << k;
        }

        cout << endl;
    }

    return 0;
}
### Output Unguided 3 :

![Screenshot Output Unguided](https://github.com/keizyakha/STRUKTUR-DATA/blob/main/LAPRAK-1/Screenshot_Output_soal3.png)

penjelasan unguided 3
Program ini digunakan untuk membuat pola angka dan tanda * berdasarkan angka yang dimasukkan. Program menggunakan perulangan untuk mengatur jarak, angka di sebelah kiri dan kanan, serta tanda * di tengah sampai membentuk pola tertentu.

## Kesimpulan
Dari program tersebut, saya mulai belajar cara menggunakan C++, seperti memasukkan input, melakukan perhitungan, menggunakan if, dan membuat perulangan. Saya masih belajar dan belum terlalu paham, tapi dari program ini saya jadi lebih tahu dasar-dasar cara kerja C++.

## Referensi
[1] G. Fathonia dan Yahfizham, "Analisis Studi Literatur Penyelesaian Operator Aritmatika Serta Bilangan Bulat Dengan Code Sederhana Pada Bahasa Pemrograman C++," *SABER: Jurnal Teknik Informatika, Sains dan Ilmu Komunikasi*, vol. 2, no. 1, hal. 9–16, 2023. doi: 10.59841/saber.v2i1.604
[2] L. J. E. Dewi, "Media Pembelajaran Bahasa Pemrograman C++," *Jurnal Pendidikan Teknologi dan Kejuruan*, vol. 7, no. 1, hal. 63–72, 2010. doi: 10.23887/jptk-undiksha.v7i1.31
