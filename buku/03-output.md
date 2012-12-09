# Output #

Dokumen markdown yang sudah kita tulis bisa dikonversi menjadi berbagai format sesuai kebutuhan.
Di antara format yang sering digunakan adalah:

* PDF : untuk dicetak atau dikirim melalui email
* HTML : untuk ditampilkan di website
* Slide Presentasi : 
    sebetulnya format slide presentasi yang dihasilkan adalah HTML. 
    Tapi karena formatnya spesifik dan berbeda, maka baiklah kita pisahkan.

## Beberapa kesepakatan ##


### Lokasi eksekusi perintah ###
Proses konversi dilakukan dengan cara mengetik perintah `pandoc` di command prompt. 
Perintah ini dilakukan di lokasi folder tempat file yang akan diproses berada. 
Jika file yang akan diproses berada di folder lain, 
saya asumsikan pembaca sudah mengetahui [cara penulisan path baik absolute ataupun relative](http://en.wikipedia.org/wiki/Path_(computing)).

### Ekstensi File ###
Walaupun file markdown bisa diberikan ekstensi `.txt`, tapi kita akan menggunakan ekstensi `.md`
supaya bisa ditampilkan dengan baik di text editor seperti Gedit atau Notepad++.


## PDF ##

Untuk menghasilkan file PDF, perintahnya adalah sebagai berikut:

```
pandoc -o hasil.pdf *.md
```

Kita bisa menambahkan daftar isi (Table of Contents) dengan opsi `--toc`. 
Supaya bab dan sub-bab diberi nomer, sertakan opsi `-N`.

```
pandoc --toc -N -o hasil.pdf *.md
```

Khusus untuk dokumen ArtiVisi, biasanya saya sudah menyertakan template LaTeX tersendiri. 
Template ini memiliki opsi untuk mengganti font dan menaruh nomer versi. 
Kita membutuhkan engine Xetex agar template ini bisa digunakan. 
Berikut perintahnya (jalankan dalam satu baris):

```
pandoc \
--template artivisi-template.tex \
--variable mainfont="Droid Serif" \
--variable sansfont="Droid Sans" \
--variable fontsize=12pt \
--variable version=1.0 \
--latex-engine=xelatex --toc -N -o hasil.pdf *md
```

Khusus PDF, biasanya kita menginginkan tampilan cetak yang rapi dan bagus. 
Layout otomatis yang disediakan LaTeX kadangkala kurang baik dalam mengatur penempatan gambar, 
sehingga seringkali gambar tampil meleset tidak sesuai dengan urutan tulisan yang disebabkan karena pengaturan _page break_. 
Untuk itu, kita membutuhkan pengaturan manual. Caranya adalah dengan menambahkan perintah LaTeX seperti ini:

```
Paragraf pertama
\newpage
Paragraf ini akan ditulis di halaman baru
```

Ini dijelaskan oleh John MacFarlane melalui email

> There’s no general way to force page breaks, by the way. 
> If you just want page breaks in PDF (via latex), you can insert a raw latex command,

```
\newpage
```

> This should be ignored in HTML and ODT output, so it will only affect latex and PDF via latex.

Perintah `\newpage` ini akan diabaikan bila kita menghasilkan output HTML dan ODT.

## Slide Presentasi ##

Untuk menghasilkan slide presentasi, perintahnya adalah sebagai berikut:

```
pandoc -s --self-contained -t s5 -o slide.html menggunakan-pandoc.md
```

Perintah di atas akan menghasilkan slide presentasi yang sudah siap pakai, lengkap dengan warna dan setting font standar dari [S5](http://en.wikipedia.org/wiki/S5_(file_format)). 

Kadangkala kita ingin menggunakan theme lain seperti yang bisa didapatkan di [S5 Reloaded](http://www.netzgesta.de/S5/). 
Untuk itu, kita tidak memproduksi slide presentasi yang lengkap, tapi cukup HTMLnya saja supaya nanti bisa diganti theme nya sesuai keinginan. 

Gunakan perintah berikut:

```
pandoc -s -t s5 -o slide.html menggunakan-pandoc.md
```

Setelah itu, file `slide.html` yang dihasilkan bisa diedit, isi tag `<head></head>` diganti dengan yang ada di dalam custom theme dari S5 Reloaded.


Supaya _bullet point_ tampil satu persatu, kita perlu memberikan opsi `-i` yaitu incremental.

```
pandoc -s --self-contained -i -t s5 -o slide.html menggunakan-pandoc.md
```


## Open Office ##

Untuk menghasilkan file OpenOffice Writer, perintahnya adalah sebagai berikut:

```
pandoc -o hasil.odt *md
```

Bila kita ingin menyesuaikan style, yaitu setting jenis huruf, ukuran huruf, jarak antar paragraf, dsb, 
kita bisa mengedit file `hasil.odt` tersebut dan menjadikannya template. 

Setelah kita memiliki template, kita berikan kepada pandoc dengan opsi `--reference-odt` sebagai berikut:

```
pandoc --reference-odt=template.odt -o hasil.odt *md
```

## HTML ##

Untuk menghasilkan output HTML, perintahnya sebagai berikut:

```
pandoc -o hasil.html *md
```

Seperti halnya PDF, kita juga bisa membuatkan daftar isi:

```
pandoc --toc -N -o hasil.html *md
```

Agar daftar isinya tampil, kita perlu memberikan opsi `-s` yaitu standalone. Artinya menghasilkan output yang komplit dengan halaman cover.

```
pandoc -s --toc -N -o hasil.html *md
```

