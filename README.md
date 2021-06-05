# soal-shift-sisop-modul-4-C05-2021

Repository Praktikum Sisop Modul 4
- 05111940000073_Aji Wahyu Admaja Utama
- 05111940000084_Aldo Yaputra Hartono
- 05111940000204_Muhammad Subhan

## Penyelesaian Soal No.1
Di suatu jurusan, terdapat admin lab baru yang super duper gabut, ia bernama Sin. Sin baru menjadi admin di lab tersebut selama 1 bulan. Selama sebulan tersebut ia bertemu orang-orang hebat di lab tersebut, salah satunya yaitu Sei. Sei dan Sin akhirnya berteman baik. Karena belakangan ini sedang ramai tentang kasus keamanan data, mereka berniat membuat filesystem dengan metode encode yang mutakhir. Berikut adalah filesystem rancangan Sin dan Sei :

```txt
NOTE :
Semua file yang berada pada direktori harus ter-encode menggunakan Atbash cipher(mirror).
Misalkan terdapat file bernama kucinglucu123.jpg pada direktori DATA_PENTING
"AtoZ_folder/DATA_PENTING/kucinglucu123.jpg" → "AtoZ_folder/WZGZ_KVMGRMT/pfxrmtofxf123.jpg"

Note : filesystem berfungsi normal layaknya linux pada umumnya, Mount source (root) filesystem adalah directory
/home/[USER]/Downloads, dalam penamaan file '/' diabaikan, dan ekstensi tidak perlu di-encode.

Referensi : https://www.dcode.fr/atbash-cipher
```

a. Jika sebuah direktori dibuat dengan awalan `AtoZ_`, maka direktori tersebut akan menjadi direktori ter-encode.

b. Jika sebuah direktori di-rename dengan awalan `AtoZ_`, maka direktori tersebut akan menjadi direktori ter-encode.

c. Apabila direktori yang terenkripsi di-rename menjadi tidak ter-encode, maka isi direktori tersebut akan terdecode.

d. Setiap pembuatan direktori ter-encode (mkdir atau rename) akan tercatat ke sebuah log. Format : **/home/[USER]/Downloads/[Nama Direktori] → /home/[USER]/Downloads/AtoZ_[Nama Direktori]**

e. Metode encode pada suatu direktori juga berlaku terhadap direktori yang ada di dalamnya.(rekursif)

#
### Jawab 1
jawab 1

#
### Kendala
1. Kendala

#
## Penyelesaian Soal No.2
Selain itu Sei mengusulkan untuk membuat metode enkripsi tambahan agar data pada komputer mereka semakin aman. Berikut rancangan metode enkripsi tambahan yang dirancang oleh Sei

a. Jika sebuah direktori dibuat dengan awalan `RX_[Nama]`, maka direktori tersebut akan menjadi direktori terencode beserta isinya dengan perubahan nama isi sesuai kasus nomor 1 dengan algoritma tambahan ROT13 (Atbash + ROT13).

b. Jika sebuah direktori di-rename dengan awalan `RX_[Nama]`, maka direktori tersebut akan menjadi direktori terencode beserta isinya dengan perubahan nama isi sesuai dengan kasus nomor 1 dengan algoritma tambahan Vigenere Cipher dengan key `SISOP` (Case-sensitive, Atbash + Vigenere).

c. Apabila direktori yang terencode di-rename (Dihilangkan `RX_` nya), maka folder menjadi tidak terencode dan isi direktori tersebut akan terdecode berdasar nama aslinya.

d. Setiap pembuatan direktori terencode (mkdir atau rename) akan tercatat ke sebuah log file beserta methodnya (apakah itu mkdir atau rename).

e. Pada metode enkripsi ini, file-file pada direktori asli akan menjadi terpecah menjadi file-file kecil sebesar 1024 bytes, sementara jika diakses melalui filesystem rancangan Sin dan Sei akan menjadi normal. Sebagai contoh, Suatu_File.txt berukuran 3 kiloBytes pada directory asli akan menjadi 3 file kecil yakni:

```txt
Suatu_File.txt.0000
Suatu_File.txt.0001
Suatu_File.txt.0002
```

Ketika diakses melalui filesystem hanya akan muncul Suatu_File.txt

#
### Jawab 2
jawab 2

#
### Kendala
1. Kendala

#
## Penyelesaian Soal No.3
Karena Sin masih super duper gabut akhirnya dia menambahkan sebuah fitur lagi pada filesystem mereka.

a. Jika sebuah direktori dibuat dengan awalan `A_is_a_`, maka direktori tersebut akan menjadi sebuah direktori spesial.

b. Jika sebuah direktori di-rename dengan memberi awalan `A_is_a_`, maka direktori tersebut akan menjadi sebuah direktori spesial.

c. Apabila direktori yang terenkripsi di-rename dengan menghapus `A_is_a_` pada bagian awal nama folder maka direktori tersebut menjadi direktori normal.

d. Direktori spesial adalah direktori yang mengembalikan enkripsi/encoding pada direktori `AtoZ_` maupun `RX_` namun masing-masing aturan mereka tetap berjalan pada direktori di dalamnya (sifat recursive  `AtoZ_` dan `RX_` tetap berjalan pada subdirektori).

e. Pada direktori spesial semua nama file (tidak termasuk ekstensi) pada fuse akan berubah menjadi lowercase insensitive dan diberi ekstensi baru berupa nilai desimal dari binner perbedaan namanya.

Contohnya jika pada direktori asli nama filenya adalah `FiLe_CoNtoH.txt` maka pada fuse akan menjadi `file_contoh.txt.1321`. 1321 berasal dari biner 10100101001.

#
### Jawab 3
jawab 3

#
### Kendala
1. Kendala

#
## Penyelesaian Soal No.4
Untuk memudahkan dalam memonitor kegiatan pada filesystem mereka Sin dan Sei membuat sebuah log system dengan spesifikasi sebagai berikut.

a. Log system yang akan terbentuk bernama `SinSeiFS.log` pada direktori home pengguna (/home/[user]/SinSeiFS.log). Log system ini akan menyimpan daftar perintah system call yang telah dijalankan pada filesystem.

b. Karena Sin dan Sei suka kerapian maka log yang dibuat akan dibagi menjadi dua level, yaitu INFO dan WARNING.

c. Untuk log level WARNING, digunakan untuk mencatat syscall rmdir dan unlink.

d. Sisanya, akan dicatat pada level INFO.

e. Format untuk logging yaitu:

```txt
[Level]::[dd][mm][yyyy]-[HH]:[MM]:[SS]:[CMD]::[DESC :: DESC]

Level : Level logging, dd : 2 digit tanggal, mm : 2 digit bulan, yyyy : 4 digit tahun, HH : 2 digit jam (format 24 Jam),
MM : 2 digit menit, SS : 2 digit detik, CMD : System Call yang terpanggil, DESC : informasi dan parameter tambahan

INFO::28052021-10:00:00:CREATE::/test.txt
INFO::28052021-10:01:00:RENAME::/test.txt::/rename.txt
```

#
### Jawab 4
Untuk soal ini kita diminta untuk membuat log system yang bertujuan untuk memudahkan dalam memonitor kegiatan pada file system. Disini kita membuat dua fungsi dalam pembuatan log system ini yaitu fungsi `tulisLog` dan `tulisLog2` perbedaannya terdapat pada DESC (informasi dan parameter tambahan) yang perlu dicantumkan dalam format untuk loggingnya. Dalam menuliskan log system sesuai format yang ada kita perlu mencari waktu sekarang untuk nanti dicantumkan dalam log systemnya. Dalam fungsi `tulisLog` kita juga memasukkan parameter `char *nama` yang mana adalah System Call dan `char *fpath` adalah deskripsi mengenai file yang ada.
```
void tulisLog(char *nama, char *fpath)
{
	time_t rawtime;
	struct tm *timeinfo;
	time(&rawtime);
	timeinfo = localtime(&rawtime);
  ...
```
Selanjutnya kita inisialisasi sebuah array of char atau string `char haha[1000];` untuk nanti menyimpan perintah system call yang telah dijalankan pada filesystem dan mencatatnya dalam file `SinSeiFS.log`. Lalu kita perlu membuka file `SinSeiFS.log` pada direktori home pengguna dengan mode `a` agar nanti bisa dituliskan log yang baru dan jika file belum ada maka akan dibuat file yang baru. 
```
FILE *file;
file = fopen("/home/aldo/SinSeiFS.log", "a");
```
Selanjutnya kita bisa melakukan pengecekan pada syscall yang ada pada parameter. Jika syscall adalah `RMDIR` atau `UNLINK` maka log levelnya akan dicatat `WARNING` namun jika tidak maka log levelnya akan dicatat `INFO`. Dan akan dicatat juga waktu sekarang beserta keterangan lainnya.
```
if (strcmp(nama, "RMDIR") == 0 || strcmp(nama, "UNLINK") == 0)
		sprintf(haha, "WARNING::%.2d%.2d%d-%.2d:%.2d:%.2d::%s::%s\n", timeinfo->tm_mday, timeinfo->tm_mon + 1, timeinfo->tm_year + 1900, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, nama, fpath);
	else
		sprintf(haha, "INFO::%.2d%.2d%d-%.2d:%.2d:%.2d::%s::%s\n", timeinfo->tm_mday, timeinfo->tm_mon + 1, timeinfo->tm_year + 1900, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, nama, fpath);
```
Langkah terakhir kita tuliskan log yang ada kedalam file `SinSeiFS.log` dan kita tutup filenya.
```
  fputs(haha, file);
	fclose(file);
	return;
}
```
Untuk fungsi yang kedua `tulisLog2` sebenarnya kurang lebih sama dengan fungsi `tulisLog` yang sudah dijelaskan sebelumnya, namun terdapat perbedaan pada parameter yang diberikan dan pada pencatatannya. Untuk parameternya ada `char *nama` yang merupakan syscall, `const char *from` adalah keterangan file sebelum dilakukannya perintah system call yang dijalankan oleh file system dan `const char *to` keterangan file setelah dilakukannya perintah system call yang dijalankan oleh file system. Lalu pada pencatatannya kurang lebih sama dengan yang sebelumnya namun ditambahkan keterangan sesuai dengan parameter yang diberikan.
```
void tulisLog2(char *nama, const char *from, const char *to)
{
	time_t rawtime;
	struct tm *timeinfo;
	time(&rawtime);
	timeinfo = localtime(&rawtime);

	char haha[1000];

	FILE *file;
	file = fopen("/home/aldo/SinSeiFS.log", "a");

	if (strcmp(nama, "RMDIR") == 0 || strcmp(nama, "UNLINK") == 0)
		sprintf(haha, "WARNING::%.2d%.2d%d-%.2d:%.2d:%.2d::%s::%s::%s\n", timeinfo->tm_mday, timeinfo->tm_mon + 1, timeinfo->tm_year + 1900, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, nama, from, to);
	else
		sprintf(haha, "INFO::%.2d%.2d%d-%.2d:%.2d:%.2d::%s::%s::%s\n", timeinfo->tm_mday, timeinfo->tm_mon + 1, timeinfo->tm_year + 1900, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, nama, from, to);

	fputs(haha, file);
	fclose(file);
	return;
}
```
Lalu untuk implementasinya kita masukkan fungsi-fungsi ini kedalam setiap fungsi system call yang ada.

#
### Kendala
1. Kendala
