## Pendahuluan

Apa itu shell ? shell adalah program (penterjemah perintah) yang menjembatani user dengan sistem operasi dalam hal ini kernel (inti sistem operasi), umumnya shell menyediakan prompt sebagai user interface, tempat dimana user mengetikkan perintah-perintah yang diinginkan baik berupa perintah internal shell (internal command), ataupun perintah eksekusi suatu file progam (eksternal command), selain itu shell memungkinkan user menyusun sekumpulan perintah pada sebuah atau beberapa file untuk dieksekusi sebagai program. 

## Macam - macam shell

Tidak seperti sistem operasi lain yang hanya menyediakan satu atau 2 shell, sistem operasi dari keluarga unix misalnya linux sampai saat ini dilengkapi oleh banyak shell dengan kumpulan perintah yang sangat banyak, sehingga memungkinkan pemakai memilih shell mana yang paling baik untuk membantu menyelesaikan pekerjaannya, atau dapat pula berpindah-pindah dari shell yang satu ke shell yang lain dengan mudah, beberapa shell yang ada di linux antara lain: 
- Bourne shell(sh),
- C shell(csh),
- Korn shell(ksh),
- Bourne again shell(bash),
- dsb.

Masing - masing shell mempunyai kelebihan dan kekurangan yang mungkin lebih didasarkan pada kebutuhan pemakai yang makin hari makin meningkat, untuk dokumentasi ini shell yang digunakan adalah bash shell dari GNU, yang merupakan pengembangan dari Bourne shell dan mengambil beberapa feature (keistimewaan) dari C shell serta Korn shell, Bash shell merupakan shell yang cukup banyak digunakan pemakai linux karena kemudahan serta banyaknya fasilitas perintah yang disediakan.

```bash
[aikom@linux$]echo $BASH_VERSION
bash 2.04.12(1)-release
```

Mungkin saat anda membaca dokumentasi ini versi terbaru dari bash sudah dirilis dengan penambahan feature yang lain. 

## Pemrograman Shell

Yaitu menyusun atau mengelompokkan beberapa perintah shell (internal atupun eksternal command) menjadi kumpulan perintah yang melakukan tugas tertentu sesuai tujuan penyusunnya. Kelebihan shell di linux dibanding sistem operasi lain adalah bahwa shell di linux memungkinkan kita untuk menyusun serangkaian perintah seperti halnya bahasa pemrograman (interpreter language), melakukan proses I/O, menyeleksi kondisi, looping, membuat fungsi, dsb. adalah proses - proses yang umumnya dilakukan oleh suatu bahasa pemrograman, jadi dengan shell di linux kita dapat membuat program seperti halnya bahasa pemrograman, untuk pemrograman shell pemakai unix atau linux menyebutnya sebagai script shell. 

## Kebutuhan Dasar

Sebelum mempelajari pemrograman Bash shell di linux sebaiknya anda telah mengetahui dan menggunakan perintah - perintah dasar shell baik itu internal command yang telah disediakan shell maupun eksternal command atau utility, seperti 

- cd, pwd, times, alias, umask, exit, logout, fg, bg, ls, mkdir, rmdir, mv, cp, rm, clear, ...
- utilitas seperti cat, cut, paste, chmod, lpr,...
- redirection (cara mengirim output ke file atau menerima input dari file), menggunakan operator redirect >, >>, <, <<, 

contohnya:

```bash
ls > data
hasil ls dikirim ke file data, jika file belum ada akan dibuat tetapi jika sudah ada isinya akan ditimpa.
```

```bash
ls >> data
hampir sama, bedanya jika file sudah ada maka isinya akan ditambah di akhir file.
```

```bash
cat < data
file data dijadikan input oleh perintah cat
```

- pipa (output suatu perintah menjadi input perintah lain), operatornya : | , contoh:

```bash 
ls -l | sort -s
ouput perintah ls -l (long) menjadi input perintah sort -s (urutkan secara descending), mending pake ls -l -r saja :-)
```

```bash 
ls -l | sort -s | more
```

```bash 
cat  databaru
```

- Wildcard dengan karakter *, ?, [ ], contohnya:

```bash 
ls i*
tampilkan semua file yang dimulai dengan i
```

```bash
ls i?i
tampilkan file yang dimulai dengan i, kemudian sembarang karakter tunggal, dan diakhiri dengan i
```

```bash
ls [ab]*
tampilkan file yang dimulai dengan salah satu karakter a atau b
```

## Simple Bash Script

Langkah awal sebaiknya periksa dulu shell aktif anda, gunakan perintah ps (report process status) 

```bash
aikom@linux$]ps
 PID TTY          TIME CMD
  219 tty1     00:00:00 bash
  301 tty1     00:00:00 ps
```

bash adalah shell aktif di system saya, jika disystem anda berbeda misalnya csh atau ksh ubahlah dengan perintah change shell 

```bash
[aikom@linux$]chsh
Password:
New shell [/bin/csh]:/bin/bash
Shell changed
```

tau dengan mengetikkan bash 

```bash
[aikom@linux$]bash
```
sekarang coba anda ketikkan perintah dibawah ini pada prompt shell 

```bash
echo "Script shell aikom di linux"
```

```bash
[fajar@linux$]echo "Script shell aikom di linux"
Script shell aikom di linux
```

string yang diapit tanda kutip ganda (double quoted) akan ditampilkan pada layar anda, echo adalah statement (perintah) built-in bash yang berfungsi menampilkan informasi ke standard output yang defaultnya adalah layar. jika diinginkan mengulangi proses tersebut, anda akan mengetikkan kembali perintah tadi, tapi dengan fasilitas history cukup menggunakan tombol panah kita sudah dapat mengulangi perintah tersebut, bagaimana jika berupa kumpulan perintah yang cukup banyak, tentunya dengan fasilitas hirtory kita akan kerepotan juga mengulangi perintah yang diinginkan apalagi jika selang beberapa waktu mungkin perintah-perintah tadi sudah tertimpa oleh perintah lain karena history mempunyai kapasitas penyimpanan yang ditentukan. untuk itulah sebaiknya perintah-perintah tsb disimpan ke sebuah file yang dapat kita panggil kapanpun diinginkan. 

coba ikuti langkah - langkah berikut: 
- Masuk ke editor anda, apakah memakai vim,nano,dsb...
- ketikkan perintah berikut

```bash
#!/bin/bash
echo "Hello, nama kamu"
```
**simpan dengan nama file aikom**
**ubah permission file tes menggunakan chmod**

```bash
[aikom@linux$]chmod 755 aikom
```
**jalankan**

```bash
[aikom@linux$]./aikom
```

kapan saja anda mau mengeksekusinya tinggal memanggil file aikom tersebut, jika diinginkan mengeset direktory kerja anda sehingga terdaftar pada search path ketikkan perintah berikut 

```bash
PATH=$PATH:.
```
setelah itu script diatas dapat dijalankan dengan cara 

```bash
[aikom@linux$]aikom
Hello, nama kamu
```

tanda #! pada /bin/bash dalam script aikom adalah perintah yang diterjemahkan ke kernel linux untuk mengeksekusi path yang disertakan dalam hal ini program bash pada direktory /bin, sebenarnya tanpa mengikutkan baris tersebut anda tetap dapat mengeksekusi script bash, dengan catatan bash adalah shell aktif. atau dengan mengetikkan bash pada prompt shell. 

```bash
[aikom@linux$]bash aikom
```

tentunya cara ini kurang efisien, menyertakan path program bash diawal script kemudian merubah permission file sehingga dapat anda execusi merupakan cara yang paling efisien.
Sekarang coba kita membuat script shell yang menampilkan informasi berikut: 

- Waktu system
- Info tentang anda
- jumlah pemakai yang sedang login di system

contoh scriptnya: 

```bash
#!/bin/bash
#aikom

#membersihkan tampilan layar
clear           

#menampilkan informasi
echo -n "Waktu system   :"; date
echo -n "Anda           :"; whoami
echo -n "Banyak pemakai :"; who | wc -l
```

sebelum dijalankan jangan lupa untuk merubah permission file aikom sehingga dapat dieksekusi oleh anda 

```bash
[aikom@linux$]chmod 755 aikom
[aikom@linux$]./aikom
Waktu system   : Kam okt 14  09:00:15 BORT 2021
Anda           : aikom
Banyak pemakai : 2
```

tentunya layout diatas akan disesuaikan dengan system yang anda gunakan statement echo dengan opsi -n akan membuat posisi kursor untuk tidak berpindah ke baris baru karena secara default statement echo akan mengakhiri proses pencetakan ke standar output dengan karakter baris baru (newline), anda boleh mencoba tanpa menggunakan opsi -n, dan lihat perbedaannya. opsi lain yang dapat digunakan adalah -e (enable), memungkinkan penggunaan backslash karakter atau karakter sekuen seperti pada bahasa C atau perl, misalkan : 

```bash
echo -e "\abunyikan bell"
```
jika dijalankan akan mengeluarkan bunyi bell, informasi opsi pada statement echo dan backslash karakter selengkapnya dapat dilihat via man di prompt shell. 

```bash
[aikom@linux$]man echo
```

## Pemakaian Variabel

Secara sederhana variabel adalah pengenal (identifier) berupa satuan dasar penyimpanan yang isi atau nilainya sewaktu-waktu dapat berubah baik oleh eksekusi program (runtime program) ataupun proses lain yang dilakukan sistem operasi. dalam dokumentasi ini saya membagi variabel menjadi 3 kategori: 

- Environment Variable
- Positional Parameter
- User Defined Variable

### Environment Variable

atau variabel lingkungan yang digunakan khusus oleh **shell atau **system linux** kita untuk proses kerja system seperti variabel **PS1**, **PS2**, **HOME**, **PATH**, **USER**, **SHELL**,dsb...jika digunakan akan berdampak pada system, misalkan **variabel PS1** yang digunakan untuk mengeset prompt shell pertama yaitu prompt tempat anda mengetikkan perintah - perintah shell (**defaultnya "\s-\v\$"**), **PS2** untuk prompt pelengkap perintah, **prompt** ini akan ditampilkan jika perintah yang dimasukkan dianggap belum lengkap oleh **shell** (**defaultnya ">"**). anda dapat mengeset **PS1** dan **PS2** seperti berikut.
simpan dahulu isi **PS1** asli system anda, sehingga nanti dapat dengan mudah dikembalikan 

```bash
[aikom@linux$]PS1LAMA=$PS1
```
sekarang masukkan string yang diinginkan pada variabel **PS1**

```bash
[fajar@linux$]PS1="Hi aikom ini Promptku!"
Hi aikom ini Promptku!PS2="Lengkapi dong ? "
```

maka prompt pertama dan kedua akan berubah, untuk mengembalikan **PS1** anda ke prompt semula ketikkan perintah 

```bash
[aikom@linux$]PS1=$PS1LAMA
```

Jika anda ingin mengkonfigurasi prompt shell, bash telah menyediakan beberapa backslash karakter diantaranya adalah: 

```bash
\a 	ASCII bell character (07)
\d 	date dengan format "Weekday Month Date" (misalnya "Tue May 26")
\e 	ASCII escape character (033)
\H 	hostname (namahost)
\n 	newline (karakter baru)
\w 	Direktory aktif
\t 	time dalam 24 jam dengan format HH:MM:SS
dll 	man bash:-)
```

contoh pemakaiannya: 

```bash
[aikom@linux$]PS1="[\t][\u@\h:\w]\$"
```

agar prompt shell hasil konfigurasi anda dapat tetap berlaku (permanen) sisipkan pada file **.bashrc** atau **.profile**


### Positional Parameter

atau parameter posisi yaitu variabel yang digunakan shell untuk menampung argumen yang diberikan terhadap shell baik berupa argumen waktu sebuah file dijalankan atau argumen yang dikirim ke subrutin. variabel yang dimaksud adalah 1,2,3,dst..lebih jelasnya lihat contoh script berikut : 

```bash
#!/bin/bash
#argumen1

echo $1 adalah salah satu $2 populer di $3
```

Hasilnya 

```bash
[fajar@linux$]./argumen1 bash shell linux
bash adalah salah satu shell populer di linux
```

ada 3 argumen yang disertakan pada script argumen1 yaitu bash, shell, linux, masing2 argumen akan disimpan pada variabel 1,2,3 sesuai posisinya. variabel spesial lain yang dapat digunakan diperlihatkan pada script berikut: 

```bash
#!/bin/bash
#argumen2

clear
echo "Nama script anda : $0";
echo "Banyak argumen   : $#";
echo "Argumennya adalah: $*";
```

Hasilnya: 

```bash
[fajar@linux$]./argumen 1 2 3 empat
Nama script anda  : ./argumen
Banyak argumen    : 4
Argumennya adalah : 1 2 3 empat
```

### User Defined Variable

atau variabel yang didefinisikan sendiri oleh pembuat script sesuai dengan kebutuhannya, beberapa hal yang perlu diperhatikan dalam mendefenisikan variabel adalah: 

- dimulai dengan huruf atau underscore
- hindari pemakaian spesial karakter seperti *,$,#,dll...
- bash bersifat case sensitive, maksudnya membedakan huruf besar dan kecil, a berbeda dengan A, nama berbeda dengan Nama,NaMa,dsb..

untuk mengeset nilai variabel gunakan operator assignment (pemberi nilai)"=", contohnya : 

```bash
myos="linux"        #double-quoted
nama='pinguin'      #single-quoted 
hasil=`ls -l`;      #back-quoted
angka=12
```

kalau anda perhatikan ada 3 tanda kutip yang kita gunakan untuk memberikan nilai string ke suatu variabel, adapun perbedaannya adalah:
**dengan kutip ganda (double-quoted), bash mengizinkan kita untuk menyisipkan variabel di dalamnya. contohnya:**

```bash
#!/bin/bash

nama="aikom"
kata="Hi $nama, selamat pagi"    #menyisipkan variabel nama
echo $kata;
```
Hasillnya:

```bash
Hi aikom, selamat pagi
```

**dengan kutip tunggal (single-quoted), akan ditampilkan apa adanya. contohnya:**

```bash
#!/bin/bash
 
nama="aikom"
kata='Hi $nama, selamat pagi'    #menyisipkan variabel nama
echo $kata;
```

Hasilnya: 

```bash
Hi $nama, selamat pag
```

**dengan kutip terbalik (double-quoted), bash menerjemahkan sebagai perintah yang akan dieksekusi, contohnya:**

```bash
#!/bin/bash

hapus=`clear`;
isi=`ls -l`;        #hasil dari perintah ls -l disimpan di variabel isi

#hapus layar
echo $hapus

#ls -l
echo $isi;  
```

**Hasilnya: silahkan dicoba sendiri  :D**

Untuk lebih jelasnya lihat contoh berikut: 

```bash
#!/bin/bash
#aikom

nama="aikom"
OS='linux'
distro="macam-macam, bisa slackware,redhat,mandrake,debian,suse,dll"
pc=1
hasil=`ls -l $0`

clear
echo -e "Hi $nama,\npake $OS\nDistribusi, $distro\nkomputernya, $pc buah"
echo "Hasil ls -l $0 adalah =$hasil"
```

Hasilnya:

```bash
[aikom@linux$]./aikom
Hi aikom,
pake linux Distribusi, macam-macam, bisa slackware,redhat,mandrake,debian,suse,dll
komputernya, 1 buah
Hasil ls -l ./aikom adalah -rwxr-xr-x 1 aikom users 299 Okt 14 09:24 ./aikom
```

untuk operasi matematika ada 3 cara yang dapat anda gunakan, dengan statement builtin let atau expr atau perintah subtitusi seperti contoh berikut: 

```bash
#mat1

a=10
b=5
#memakai let
jumlah=$(($a+$b))
kurang=$(($a-$b))
kali=$(($a*$b))

#memakai expr
bagi=`expr $a / $b`

#memakai perintah subtitusi $((ekspresi))
modul=$(($a%$b))  #sisa pembagian

echo "$a+$b=$jumlah"
echo "$a-$b=$kurang"
echo "$a*$b=$kali"
echo "$a/$b=$bagi"
echo "$a%$b=$modul"
```

Hasilnya:

```bash
[aikom@linux$]./mat1
10+5=15
10-5=5
10*5=50
10/5=2
10%5=0
```

fungsi **expr** begitu berdaya guna baik untuk operasi matematika ataupun **string** contohnya: 

```bash
[aikom@linux$]mystr="linux"
[aikom@linux$]expr length $mystr
5
```

Mungkin anda bertanya - tanya, apakah bisa variabel yang akan digunakan dideklarasikan secara eksplisit dengan tipe data tertentu?, mungkin seperti C atau pascal, untuk hal ini oleh Bash disediakan statement declare dengan opsi -i hanya untuk data integer (bilangan bulat). Contohnya: 

```bash
#!/bin/bash

declare -i angka
angka=100;
echo $angka;
```

apabila variabel yang dideklarasikan menggunakan declare -i ternyata anda beri nilai string (karakter), maka Bash akan mengubahnya ke nilai 0, tetapi jika anda tidak menggunakannya maka dianggap sebagai string. 


## Simple I/O

I/O merupakan hal yang mendasar dari kerja komputer karena kapasitas inilah yang membuat komputer begitu berdayaguna. I/O yang dimaksud adalah device yang menangani masukan dan keluaran, baik itu berupa keyboard, floppy, layar monitor,dsb. sebenarnya kita telah menggunakan proses I/O ini pada contoh -contoh diatas seperti statement echo yang menampilkan teks atau informasi ke layar, atau operasi redirect ke ke file. selain echo, bash menyediakan perintah builtin printf untuk mengalihkan keluaran ke output standard, baik ke layar ataupun ke file dengan format tertentu, mirip statement printf kepunyaan bahasa C atau perl. berikut contohnya: 

### Output dengan printf

```bash
#!/bin/bash
#pr1

url="aikomternate.ac.id";
angka=32;

printf "Hi, Pake printf ala C\n\t\a di bash\n";
printf "My url %s\n %d decimal = %o octal\n" $url $angka $angka;
printf "%d decimal dalam float = %.2f\n" $angka $angka
```

Hasilnya: 

```bash
[aikom@linux$]./aikom
Hi, Pake printf ala C
    di bash
My url  aikomternate.ac.id
32 decimal = 40 octal
32 decimal dalam float = 32.00
```

untuk menggunakan format kontrol sertakan simbol %, bash akan mensubtitusikan format tsb dengan isi variabel yang berada di posisi kanan sesuai dengan urutannya jika lebih dari satu variabel, \n \t \a adalah karakter sekuen lepas newline,tab, dan bell, 

**Format control keterangan**

```bash
%d 	untuk format data integer
%o 	octal
%f 	float atau decimal
%x 	Hexadecimal
```

pada script diatas %.2f akan mencetak 2 angka dibelakang koma, defaultnya 6 angka, informasi lebih lanjut dapat dilihat via man printf 

### Input dengan read

Setelah echo dan printf untuk proses output telah anda ketahui, sekarang kita menggunakan statement read yang cukup ampuh untuk membaca atau menerima masukan dari input standar 

syntax : 

```bash
ead -opsi [nama_variabel...]
```

berikut contoh scriptnya: 

```bash
#!/bin/bash
#aikom

echo -n "Nama anda :"
read nama;

echo    "Hi $nama,  Selamat Pagi";
echo    "Pesan dan kesan :";
read 
echo    "kata $nama, $REPLY";
```

Hasilnya:

```bash
[aikom@linux$]./aikom
Nama anda : aikom
Hi aikom, Selamat Pagi
Pesan & kesan :
 pake linux pasti asyk - asyk aja
kata aikom, pake linux pasti asyk - asyk aja
```

jika nama_variabel tidak disertakan, maka data yang diinput akan disimpan di variabel REPLY contoh lain read menggunakan opsi 

```bash
-t(TIMEOUT), -p (PROMPT), -s(SILENT), -n (NCHAR) dan -d(DELIM)
```

```bash
#!/bin/bash 

read -p "User Name : " user
echo -e "Password 10 karakter,\njika dalam 6 second tidak dimasukkan pengisian password diakhiri"
read -s -n 10 -t 6 pass
echo    "kesan anda selama pake linux, _underscore=>selesai"
read -d _ kesan

echo    "User = $user"
echo    "Password = $pass"
echo    "Kesan selama pake linux = $kesan"
```

Hasilnya: silahkan dicoba sendiri :D

**Opsi Keterangan**

```bash
-p 	memungkinkan kita membuat prompt sebagai informasi pengisian
-s 	membuat input yang dimasukkan tidak di echo ke layar (seperti layaknya password di linux)
-n 	menentukan banyak karakter yang diinput
-d 	menentukan karakter pembatas masukan 
```

informasi secara lengkap lihat man bash 

### Output dengan konstanta ANSI
**Pengaturan Warna**

Untuk pewarnaan tampilan dilayar anda dapat menggunakan konstanta ANSI (salah satu badan nasional amerika yang mengurus standarisasi). 

syntaxnya: 

```bash
\033[warnam
```

Dimana: 

```bash
m menandakan setting color
```

contohnya: 

```bash
[aikom@linux$]echo -e "\033[31m HELLO\033[0m"
HELLO
```

konstanta 31m adalah warna merah dan 0m untuk mengembalikan ke warna normal (none), tentunya konstanta warna ansi ini dapat dimasukkan ke variabel PS1 untuk mengatur tampilan prompt shell anda, contohnya: 

```bash
[aikom@linux$]PS1="\033[34m"
[aikom@linux$]
```

berikut daftar warna yang dapat anda gunakan: 

foreground

```bash
      None    0m 
      Black       0;30     Dark Gray     1;30
      Red         0;31     Light Red     1;31
      Green       0;32     Light Green   1;32
      Brown       0;33     Yellow        1;33
      Blue        0;34     Light Blue    1;34
      Purple      0;35     Light Purple  1;35
      Cyan        0;36     Light Cyan    1;36
      Light Gray  0;37     White         1;37      
```

background 

```bash
dimulai dengan 40 untuk BLACK,41 RED,dst
```

lain-lain 

```bash
4 underscore,5 blink, 7 inverse
```

tentunya untuk mendapatkan tampilan yang menarik anda dapat menggabungkannya antara foreground dan background 

```bash
[aikom@linux$]echo -e "\033[31;1;33m Bash and aikom color\033[0m"
```
Bash and aikom color 

### Pengaturan posisi kursor

sedangkan untuk penempatan posisi kursor, dapat digunakan salah satu cara dibawah. 

- Menentukan posisi baris dan kolom kursor:

```bash
\033[baris;kolomH
```

- Pindahkan kursor keatas N baris:

```bash
\033[NB
```
- Pindahkan kursor kedepan N kolom:

```bash
\033[NC
```

- Pindahkan kursor kebelakang N kolom:

```bash
\033[ND
```

Contohnya: 

```bash
#!/bin/bash

SETMYCOLOR="\033[42;1;37m"
GOTOYX="\033[6;35H"
clear
echo -e "\033[3;20H INI DIBARIS 3, KOLOM 20"
echo -e "\033[44;1;33;5m\033[5;35H HELLO\033[0m";
echo -e "$SETMYCOLOR$GOTOYX ANDA LIHAT INI\033[0m"
```

Hasilnya: Silahkan dicoba sendiri Menggunakan utulity tput untuk penempatan posisi kursor 

kita dapat pula mengatur penempatan posisi kursor di layar dengan memanfaatkan utility tput, 

syntaxnya: 

```bash
tput cup baris kolom
```

contohnya: 

```bash
#!/bin/bash

clear
tput cup 5 10
echo  "HELLO"
tput cup 6 10
echo  "PAKE TPUT"
```

jika dijalankan anda akan mendapatkan string HELLO di koordinat baris 5 kolom 10, dan string PAKE TPUT dibaris 6 kolom 10. informasi selengkapnya tentang tput gunakan man tput, atau info tput 

## Seleksi dan Perulangan

Bagian ini merupakan ciri yang paling khas dari suatu bahasa pemrograman dimana kita dapat mengeksekusi suatu pernyataan dengan kondisi terntentu dan mengulang beberapa pernyataan dengan kode script yang cukup singkat. 

### test dan operator
















