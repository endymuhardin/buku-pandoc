# Sintaks Markdown #

Untuk menulis buku, kita menggunakan sintaks markdown. Markdown pertama kali diciptakan oleh John Gruber. Berikut filosofi Markdown menurut John Gruber.

> A Markdown-formatted document should be publishable as-is, as plain
> text, without looking like it's been marked up with tags or formatting
> instructions.
> -- [John Gruber](http://daringfireball.net/projects/markdown/syntax#philosophy)

Diterjemahkan secara bebas sebagai berikut.

> Dokumen berformat Markdown harus bisa diterbitkan apa adanya dalam bentuk _plain text_,
> tanpa terlihat bahwa dokumen tersebut sudah dihiasi perintah formatting tertentu.

Versi Markdown asli dari John Gruber memiliki beberapa kekurangan, 
diantaranya dia tidak menjelaskan 
bagaimana cara membuat tabel. 
Selain versi John Gruber, 
ada juga versi lain seperti MultiMarkdown dan Pandoc. 

Kita akan menggunakan versi Pandoc yang lebih lengkap, karena sudah mendukung:

* tabel
* mewarnai source code
* sampul
* catatan kaki

Selanjutnya, kita akan membahas tentang cara-cara memformat tulisan dengan sintaks markdown aliran Pandoc.

## Paragraf ##

Paragraf adalah satu atau lebih baris tulisan. Paragraf satu dan lainnya dibatasi oleh satu baris kosong. 
Pergantian baris yang kita ketik tidak menentukan pergantian baris di hasil akhir, 
sehingga kita bisa mengganti baris sesuka kita. Kalau kita menginginkan hasil akhirnya juga ganti baris, 
kita dapat menggunakan spasi ganda di akhir baris, atau backslash (\\) diikuti oleh baris baru.

## Headers ##

Ada dua jenis penulisan header, setext dan atx. Kita hanya akan membahas atx saja. 

Atx-header diawali oleh satu sampai enam tanda `#`. Berikut contohnya:

    # Bab 1
    
    ## Sub bab 1.1
    
    ### Subnya sub bab 1.1.1

Kita boleh menambahkan akhiran `#` ataupun menghilangkannya. Contoh berikut:

    # Bab 1
    
sama dengan ini:

    # Bab 1 #
    
Pada waktu dikonversi menjadi HTML, tiap header akan diberikan id supaya bisa dijadikan tautan. 
Berikut aturan pemberian id:

  - Semua formatting, link, dsb, dihilangkan.
  - Semua tanda baca kecuali underscore, hyphen, dan titik.
  - Mengganti spasi dan ganti baris dengan hyphen.
  - Semua huruf dijadikan huruf kecil.
  - Semua karakter aneh dihapus sampai huruf pertama (id tidak boleh diawali angka atau tanda baca).
  - Bila habis semua, gunakan id `section`.

Contohnya:

  Header                            Identifier
  -------------------------------   ----------------------------
  Header identifiers in HTML        `header-identifiers-in-html`
  *Dogs*?--in *my* house?           `dogs--in-my-house`
  [HTML], [S5], or [RTF]?           `html-s5-or-rtf`
  3. Applications                   `applications`
  33                                `section`

Bila dalam prosesnya ditemukan identifier yang sama, maka akan ditambahi angka urutan, 
misalnya `section-1`, `section-2`, dan seterusnya.

Identifier ini bisa digunakan sebagai link di dalam dokumen, 
seperti ini:

    Silahkan lihat di 
    [penjelasan tentang sintaks markdown](#sintaks-markdown).
    
Selain itu, identifier ini juga digunakan dalam pembuatan daftar isi.

## Kutipan ##

Untuk menampilkan kutipan, kita menggunakan sintaks seperti pada waktu membalas email, 
yaitu menggunakan penanda `>`. Penanda ini bisa ditulis hanya di awal kutipan seperti ini:

    > The difference between stupidity and genius 
    is that genius has its limits.

Dan bisa juga di tiap barisnya seperti ini:

    > Have you ever noticed that 
    > anybody driving slower than you is an idiot, 
    > and anyone going faster than you is a maniac?

Kecuali di awal file, kutipan harus didahului satu baris kosong.

## Kode Program ##

Untuk menampilkan kode program, kita menggunakan tiga backtick (`), seperti ini:

    ```
    System.out.println("Halo dunia");
    ```

Ini akan menghasilkan tampilan seperti ini:

```
System.out.println("Halo dunia");
```
    
Kita bisa mengaktifkan _syntax highlighting_ dengan mencantumkan jenis bahasa pemrograman yang digunakan.

    ```java
    System.out.println("Halo dunia");
    ```

Ini akan menghasilkan tampilan seperti ini:

```java
System.out.println("Halo dunia");
```

Kalau kita output menjadi PDF, contoh kedua ini akan 
diwarnai sesuai keyword bahasa pemrograman yang dipilih.

## List dan Nomor ##

### List ###

List diawali oleh tanda *, +, atau -. Berikut contohnya:

    * apel
    * mangga
    * durian
    
Bila terlalu panjang, kita bebas untuk ganti baris, seperti ini:

    * markdown. Ini adalah 
      format yang ditemukan oleh John Gruber
    * docbook
    * latex

Kita juga bisa membuat list di dalam list, seperti ini:

    * buah
        + apel
        + mangga
            - indramayu
            - harum manis
        + durian
      
    * sayur
        + kangkung
        + bayam

Syaratnya, list level kedua harus diindentasi 4 spasi. Contoh di atas akan menghasilkan tampilan seperti ini:

* buah
    + apel
    + mangga
        - indramayu
        - harum manis
    + durian
  
* sayur
    + kangkung
    + bayam

### Nomor ###

Secara garis besar, nomor sama dengan list. Bedanya cuma di karakter penandanya. 
Nomor ditandai dengan angka seperti ini:

    1. Adi
    2. Awan
    3. Ifnu
    
Nomornya tidak harus urut, begini juga boleh: 

    1. Adi
    3. Awan
    1. Ifnu

Nomor awal akan mengikuti nomor pertama yang kita gunakan. Bila kita tulis seperti ini:

    4. Adi
    2. Awan
    3. Ifnu
    
maka hasilnya adalah 

    4. Adi
    5. Awan
    6. Ifnu

Selain menggunakan angka arab, kita juga bisa menggunakan huruf dan angka romawi. Selain itu, masih ada fitur lain seperti penomoran contoh, cara memutus list, dan sebagainya. Detailnya bisa dilihat di [dokumentasi Pandoc](http://johnmacfarlane.net/pandoc/README.html).

## Garis Mendatar ##

Baris yang memuat tiga atau lebih karakter `*`, `-`, atau `_` 
secara berturut-turut (boleh diselingi spasi) 
akan dikonversi menjadi garis mendatar.

Contohnya sebagai berikut:

    ***
    halo
    - - -

akan menghasilkan output seperti ini:

***

## Tabel ##

Berikut contoh cara penulisan tabel:

      Kanan     Kiri     Tengah     Default
    -------     ------ ----------   -------
         12     12        12            12
        123     123       123          123
          1     1          1             1

    Table:  Contoh tabel sederhana.

Yang akan menghasilkan tabel seperti ini:

  Kanan     Kiri     Tengah     Default
-------     ------ ----------   -------
     12     12        12            12
    123     123       123          123
      1     1          1             1

Table:  Contoh tabel sederhana.

Dari contoh di atas, kita juga dapat memahami cara membuat rata kiri, rata kanan, dan tengah. 
Selain itu, kita juga bisa memberikan judul tabel.

Bila satu row terdiri dari banyak baris, contohnya seperti ini:

    -------------------------------------------------------------
       Rata     Default            Rata Rata
      Tengah    Aligned           Kanan Kiri
    ----------- ------- --------------- -------------------------
     Pertama    halo               12.0 Contoh row yang lebih
                                        dari satu baris

       Kedua    coba                5.0 Ini row kedua. Antar row
                                        dipisahkan oleh baris
                                        kosong.
    -------------------------------------------------------------

    Table: Ini labelnya.
    Label juga boleh multi baris

Hasilnya seperti ini:

-------------------------------------------------------------
   Rata     Default            Rata Rata
  Tengah    Aligned           Kanan Kiri
----------- ------- --------------- -------------------------
 Pertama    halo               12.0 Contoh row yang lebih
                                    dari satu baris

   Kedua    coba                5.0 Ini row kedua. Antar row
                                    dipisahkan oleh baris
                                    kosong.
-------------------------------------------------------------

Table: Ini labelnya.
Label juga boleh multi baris

## Cover ##

Untuk membuat cover buku, kita harus membuat satu file berisi title block seperti ini:

    % Menggunakan Pandoc dan Markdown
    % Endy Muhardin
    % 5 September 2012

Baris pertama adalah judul, baris kedua adalah pengarang, dan baris ketiga adalah tanggal penulisan. 
Bila pengarang lebih dari satu, ditulis seperti ini:

    % Menggunakan Pandoc dan Markdown
    % Endy Muhardin
      Ifnu Bima
    % 5 September 2012

## Backslash ##
Kecuali dalam code block atau inline code, semua tanda baca dan spasi yang didahului backspace
akan ditulis apa adanya, termasuk karakter formatting. Contoh:

    *\*halo\**

akan menghasilkan

    <em>*halo*</em>

bukannya

    <strong>halo</strong>

## Inline Formatting ##

### Huruf Miring ###

Untuk membuat *huruf miring*, gunakan karakter `*` atau `_`. Contohnya:

    Penulisan kode program di Java adalah _case sensitive_.
    Berbeda dengan SQL yang *case insensitive*.

Contoh di atas akan menghasilkan tampilan seperti ini:

> Penulisan kode program di Java adalah _case sensitive_.
Berbeda dengan SQL yang *case insensitive*.

### Huruf Tebal ###

Huruf **tebal** sama dengan huruf miring, tapi menggunakan dua karakter.
Contohnya:

    Penulisan kode program di Java adalah __case sensitive__.
    Berbeda dengan SQL yang **case insensitive**.

Contoh di atas akan menghasilkan tampilan seperti ini:

> Penulisan kode program di Java adalah __case sensitive__.
Berbeda dengan SQL yang **case insensitive**.

### Strikeout ###
Untuk menulis ~~correction~~ koreksi, gunakan \~\~ seperti ini: 

    Kelemahan Spring Framework adalah 
    ~~keharusan untuk menulis file xml yang banyak~~.

### Verbatim ###

Verbatim artinya apa adanya, tidak dikonversi menjadi apapun. Untuk membuat verbatim, kita gunakan backtick seperti ini:

    Untuk membandingkan angka, gunakan tanda lebih besar `>`

## Link ##

Untuk menampilkan link ke website tertentu, formatnya seperti ini:

    Silahkan lihat ke 
    [website saya](http://software.endy.muhardin.com/about "Websitenya Endy") 
    untuk informasi lebih lengkap.

Ada tiga bagian untuk membuat link, yaitu:

1. Tulisan yang akan diberi link. Ditulis di dalam kurung kotak `[]`
2. URL untuk link tersebut, ditulis dalam tanda kurung biasa `()`
3. Judul link, ditulis dalam tanda kurung, setelah URL, dilengkapi dengan tanda kutip ganda. Judul link ini optional, boleh ada ataupun tidak.

Contoh di atas akan menghasilkan output seperti ini:

> Silahkan lihat ke 
> [website saya](http://software.endy.muhardin.com/about "Websitenya Endy") 
> untuk informasi lebih lengkap.

## Image ##

Menampilkan image mirip dengan link. Bedanya, di depan kurung kotak kita berikan tanda seru. Contohnya menggunakan relative path seperti ini:

    ![logo artivisi](resources/logo-artivisi.png)

Contoh di atas akan menghasilkan tampilan seperti ini: 

![logo artivisi](./resources/logo-artivisi.png)


## Catatan kaki ##

Catatan kaki ditulis seperti ini:

    Tulisan ini ada catatan kakinya,[^1] dan ini juga.[^longnote]

    [^1]: Catatan kaki nomer satu.

    [^longnote]: Catatan kaki panjang multi baris.

        Paragraf berikutnya diindentasi untuk menunjukkan
        bahwa dia bagian dari catatan kaki di atasnya.

            { contoh kode program }

        Indentasi boleh di baris pertama saja atau 
        di seluruh paragraf

    Paragraf ini tidak termasuk catatan kaki, karena tidak diindentasi.

Contoh di atas akan menghasilkan tampilan sebagai berikut:

***

Tulisan ini ada catatan kakinya,[^1] dan ini juga.[^longnote]

[^1]: Catatan kaki nomer satu.

[^longnote]: Catatan kaki panjang multi baris.

    Paragraf berikutnya diindentasi untuk menunjukkan
    bahwa dia bagian dari catatan kaki di atasnya.

        { contoh kode program }

    Indentasi boleh di baris pertama saja atau 
    di seluruh paragraf

Paragraf ini tidak termasuk catatan kaki, karena tidak diindentasi.

***

Catatan kaki perlu diberikan identifier, yaitu label berawalan `^` di dalam kurung kotak. Identifier ini tidak boleh mengandung spasi, tab, atau ganti baris. Identifier hanya digunakan untuk menghubungkan titik referensi dengan catatan kakinya. Sedangkan penomoran di outputnya akan dihitung otomatis.

## Referensi dan Bibliografi ##

Pandoc juga mendukung referensi (citation) ke tulisan orang lain, seperti yang biasa dicantumkan sebagai daftar pustaka. Ini biasanya digunakan kalau kita membuat tulisan ilmiah seperti jurnal, skripsi, atau thesis. 

Untuk lebih jelasnya, bisa dilihat di dokumentasi pandoc.

