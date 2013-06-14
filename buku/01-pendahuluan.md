# Pendahuluan #

## Tentang Markdown ##

### Apa itu Markdown ###

[Markdown](http://daringfireball.net/projects/markdown/) adalah format penulisan dokumen yang ditemukan oleh [John Gruber](http://daringfireball.net/). Markdown dibuat dengan filosofi sebagai berikut:

> The idea is that a Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions. - [John Gruber](http://daringfireball.net/projects/markdown/)

Markdown memiliki beberapa karakteristik, diantaranya:

* berbasis teks biasa (plain text)
* mudah dibaca apa adanya (tanpa aplikasi khusus)
* bisa dikonversi menjadi format lain (misalnya PDF, HTML, dsb)

### Mengapa memilih Markdown ###

Di ArtiVisi, kita ingin melakukan standarisasi dalam penulisan dokumen. Kriteria utama dari format dokumentasi yang kita inginkan adalah **berbasis text**. Format berbasis text memiliki beberapa keunggulan, diantaranya:

* bisa memanfaatkan fitur version control secara maksimal seperti diff, blame, branch, merge, dan sebagainya.
* mudah diedit, pakai notepad pun jadi
* bisa diedit dimana saja, misalnya di tablet atau handphone (contohnya bab ini saya ketik di angkutan umum menggunakan aplikasi DroidEdit di handphone)
* ukurannya kecil
* mudah disimpan di layanan berbasis cloud seperti Dropbox

Ada beberapa format yang memenuhi kriteria tersebut, diantaranya:

* html
* markdown
* docbook
* \LaTeX

Aplikasi Office baik Microsoft maupun Open langsung gugur pada babak pertama ini karena formatnya bukan text.

Selanjutnya, kriteria kedua adalah mudah dipahami. Pekerjaan membuat dokumentasi di ArtiVisi biasanya diserahkan ke anak magang. Untuk itu, kita harus bisa mengajarkan sistem dokumentasi ini dengan cepat, karena tingkat turnover anak magang relatif singkat. Jangan sampai terjadi, masa magangnya cuma 3 bulan, 2 minggu dihabiskan untuk belajar sistem dokumentasi. 

Dari empat kandidat di atas, \LaTeX gugur karena dia relatif sulit dipelajari. Tinggal tersisa tiga kontestan. Kita lanjutkan ke babak selanjutnya.

Kriteria ketiga adalah kemampuan konversi ke berbagai format lain. Kita ingin konversi ke PDF agar bisa dicetak. Kita juga ingin bisa konversi ke HTML agar bisa dipublish di internet. Di jaman modern ini, perlu juga kemampuan konversi menjadi format buku digital (epub). Selain itu, kadangkala perlu juga konversi ke format OpenOffice atau MS Office. 

Di babak ketiga ini, format HTML gugur. Untuk mengkonversi format HTML ke format lain, dibutuhkan prosedur yang rumit dan panjang. Dengan demikian, kita sudah mencapai babak final, mempertandingkan Markdown vs Docbook.

Dari sini, sebetulnya kedua format sudah layak untuk digunakan. Walaupun demikian, kita akan melihat beberapa kriteria lain yang bersifat _nice to have_, ada bagus, tidak ada juga tidak apa-apa. 

Kriteria tambahan pertama adalah ketersediaan tools. Docbook dapat dikonversi menjadi beberapa format dengan banyak tools, diantaranya:

* Maven (Java)
* Bookshop (Ruby)
* Pandoc (Haskell)
* Tools lain (misalnya xsltproc, makefile, dsb)

Sedangkan untuk Markdown, sebagian besar toolsnya adalah untuk konversi menjadi HTML, seperti misalnya:

* Markdown.pl
* Pandoc
* Jekyll

Untuk urusan tools juga nilainya seri. Kedua format dapat dikonversi dengan mudah ke format lainnya. Mari kita tinjau dari sisi user.

Nantinya, urusan dokumentasi akan diserahkan ke kasta terbawah dari rantai makanan programmer, yaitu para magang dan karyawan baru. Karakteristik dari user ini adalah tingkat ketelitiannya yang minim, tidak seperti para senior programmer yang dapat menemukan kelebihan satu spasi (_ingat, spasi tidak terlihat oleh mata telanjang_) di dalam ribuan baris kode program. 

Oleh karena itu, format dokumentasi harus _foolproof_. Dia harus bisa ditulis dengan tingkat ketelitian yang rendah. Nah, di sini kita menemukan pemenangnya. Docbook berbasis XML yang terkenal ketat (strict). Kurang satu tanda kutip saja, dokumen tidak dapat diproses. Ini menyebabkan format ini rentan error. Jangan sampai nanti para senior programmer harus direpotkan karena dokumennya tidak dapat dikonversi dengan baik.

Berbeda halnya dengan Markdown. Dia sangat permisif. Kalaupun ada kesalahan, paling hanya berdampak merusak format tampilan, tidak sampai error pemrosesan.

Dengan demikian, format yang akan kita gunakan adalah Markdown.

## Tentang Pandoc ##

Dokumen dalam format text saja tidak cukup. Seringkali kita ingin mengirimkan dokumen tersebut ke orang lain, yang kemudian akan dicetak, ataupun ditampilkan di website. Untuk itu, kita butuh format lain seperti misalnya PDF dan HTML. 

Kita bisa mengkonversi Markdown menjadi PDF dan HTML menggunakan aplikasi yang bernama [Pandoc](http://johnmacfarlane.net/pandoc/). 
Pandoc ini adalah aplikasi yang dibuat oleh [John MacFarlane](http://johnmacfarlane.net), seorang profesor filosofi di University of California, Berkeley. Pandoc dibuat dengan bahasa pemrograman [Haskell](http://en.wikipedia.org/wiki/Haskell_(programming_language)).

## Tentang Buku Ini ##

### Mengapa buku ini ditulis ###

Di ArtiVisi, kami banyak menulis buku, modul pelatihan, slide presentasi, user manual aplikasi, dan berbagai dokumen lainnya. Daripada menjelaskan berkali-kali setiap ada karyawan atau magang yang baru bergabung, lebih baik saya investasikan waktu dan tenaga satu kali saja untuk menulis panduan ini.

### Siapa yang sebaiknya membaca ###

Buku ini bisa bermanfaat buat: 

* Karyawan / magang di ArtiVisi yang ditugaskan membuat buku, modul pelatihan, slide presentasi, user manual, dan sebagainya.
* Guru, dosen, atau mahasiswa yang ingin membuat skripsi, thesis, atau tulisan ilmiah lainnya. Dengan Pandoc, dokumen Markdown bisa dikonversi menjadi \LaTeX, yaitu format dokumen yang lazim digunakan untuk membuat tulisan ilmiah. Format \LaTeX ini [jauh lebih superior daripada word processor seperti MS Word atau OpenOffice Writer](http://ricardo.ecn.wfu.edu/~cottrell/wp.html).


### Lisensi ###

Buku ini memiliki lisensi Creative Commons Attribution Share Alike
(CC-BY-SA). Artinya, semua orang:

-   bebas menggunakan buku ini tanpa harus membayar, baik untuk
    keperluan non-profit maupun komersil. Anda boleh membuka pelatihan
    berbayar menggunakan buku ini.
-   bebas membagikan buku ini kepada siapa saja.
-   bebas membuat perubahan terhadap isi buku ini.

Semua kebebasan di atas hanya memiliki syarat yaitu tetap harus
menyebutkan nama pengarang yang aslinya. Ini disebut dengan istilah
attribution. Singkatnya, boleh dipakai dan dibagikan asal jangan diakui
sebagai karya sendiri. Selain itu, segala perubahan yang dibuat juga
harus dilisensikan sama dengan buku ini. Ini disebut dengan istilah
Share-Alike. Lebih lanjut tentang lisensi ini bisa dilihat di
[website Creative Commons](http://creativecommons.org/licenses/)

### Tools 

Buku ini dibuat menggunakan perangkat pembantu :

- Markdown : format text untuk menulis buku
- Pandoc : aplikasi untuk mengkonversi markdown menjadi PDF atau HTML
- \LaTeX : format perantara dari Markdown menjadi PDF

### Kontribusi ###

Semua orang boleh dan dianjurkan untuk ikut membantu penulisan buku ini. Bagaimana caranya? Gampang. Ada beberapa pekerjaan yang dapat dilakukan.

### Reviewer ###

Tugasnya adalah memeriksa isi buku dan memberikan koreksi. Apa saja
boleh dikoreksi, mulai dari tanda baca, salah ketik, contoh latihan
tidak bisa dijalankan, apa saja. Kalau ada penjelasan yang kurang jelas
juga boleh dikomentari. Apapun yang bisa membuat buku ini lebih baik.
Hasil review dapat dientri di [halaman Issue di
Github](https://github.com/endymuhardin/buku-pandoc/issues).

### Penulis ###

Bagus sekali kalau Anda ingin menyumbangkan tulisan. Lebih banyak yang
mencerdaskan bangsa lebih baik. Begini caranya. Sebagai penulis buku
Git, tentu Anda sudah paham cara menggunakan Git, dan juga kemungkinan
besar sudah punya account di Github. Langsung saja fork repository
buku-git ini dan segeralah berkarya. Begitu dirasa sudah memadai,
kirimkan pull request ke saya. Nanti akan saya merge ke repository saya.
