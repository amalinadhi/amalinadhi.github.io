# Product Research with Conjoint Analysis


## Sulitnya melakukan riset
---
Riset fitur dalam pengembangan produk sangat krusial. Ketika Anda mengetahui fitur yang pas untuk customer, maka customer akan senang dan membeli produk Anda. 
Namun melakukan riset tersebut tidaklah mudah. 

Mari kita simulasikan riset sederhana dengan mengajukan pertanyaan tentang sentimen customer terhadap pilihan feature dalam kasus pengembangan bootcamp.

<br>
**Customer tidak selalu paham kebutuhannya**

> Berapa lama waktu belajar ideal yang Anda butuhkan untuk persiapan kerja? <br>
> a) 2 Bulan <br>b) 8 Bulan <br>c) 12 Bulan

Pertanyaan ini diajukan untuk menentukan fitur durasi belajar bootcamp.
Customer sangat mungkin memilih opsi `(A)` karena itu durasi waktu tersingkat yang ada dalam pilihan.
Jawaban pertanyaan tersebut bisa bias.

<br>
**Jawaban customer bisa tidak konsisten**

> Berapa lama waktu yang Anda habiskan untuk persiapan kerja tiap minggu-nya?<br>
> a) 2 jam/minggu <br>b) 8 jam/minggu <br>c) 12 jam/minggu
>
> Apa harapan Anda setelah mengikuti bootcamp?<br>
> a) Tambah skill <br>b) Ganti karir
>
> Berapa gaji yang Anda harapkan di karir Anda setelah mengikuti bootcamp?<br>
> a) 5-10 juta <br> b) 10-15 juta <br> c) di atas 15 juta

Apabila pertanyaan sebelumnya dilanjutkan dengan 3 pertanyaan di atas, Anda bisa mendapatkan jawaban `(A) 2 jam/minggu`, `(B) Ganti karir`, dan `(C) di atas 15 juta` dari customer karena 3 jawaban tersebut yang 
sangat menguntungkan bagi customer.

Apabila Anda rangkum hipotesa pilihan jawaban customer tadi, Anda dapatkan customer ingin

* Ganti karir
* Yang gajinya di atas 15 juta
* Dengan persiapan belajar 2 bulan saja
* Dengan komitmen belajar 2 jam/minggu

Suatu hal yang sulit diimplementasikan ke dalam product karena keinginan customer tinggi namun usaha customer tidak sebanding. 
Apabila simpulan riset seperti itu, tentu tidak bisa dijadikan acuan sebagai fitur produk karena tidak masuk akal. 

Sederhananya, ada 2 hal yang bisa dilakukan
 
* Perbaiki pertanyaan dalam riset produk, cari pertanyaan yang jawabannya tidak *obvious*
* Gunakan metode riset lain


## Tanyakan pilihan sulit: Conjoint Analysis
---
Bertanya 1 fitur dalam 1 pertanyaan akan sangat mudah membuat customer menjawab hal yang *obvious*, bagaimana kalau Anda bertanya kombinasi beberapa fitur dalam 1 pertanyaan?

<center>

||Opsi A|Opsi B|
|:-|:-:|:-:|
|Durasi belajar|8 bulan|12 bulan|
|Target karir|Tambah skill|Ganti karir|
|Target gaji|5-10 juta|di atas 15 juta|

</center>

Pertanyaan di atas akan meminta customer untuk menimbang-nimbang keuntungan yang didapat dari kombinasi beberapa fitur sehingga

* mengurangi potensi customer menjawab hal *obvious*
* dapat membantu analis mencari fitur mana yang penting dari user

Ini adalah contoh sederhana melakukan **conjoint analysis**. Lecture berikut dapat menjabarkan dengan baik conjoint analysis.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Wum3_Y0AO4A?si=IJuz9nxzyztDs6A5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>


## Melakukan Conjoint Analysis
---

Berikut tahapan melakukan analisa

* Membuat survey conjoint
* Menentukan responden
* Menganalisa hasil survey menggunakan logistic regression


### Membuat Survey Conjoint
---

Dokumen [Sawtooth - CBC technical paper](https://sawtoothsoftware.com/resources/technical-papers/cbc-technical-paper) dapat Anda jadikan sebagai referensi dalam pengembangan survey.
Anda bisa siapkan beberapa atribut & karakter fitur yang ingin diuji sentimennya. Contoh

<center>

|Atribut|Karakter|
|:-|:-|
|Durasi belajar|- 2 bulan <br>- 8 bulan <br>- 12 bulan|
|Target karir|- Tambah skill <br>- Ganti skill|
|Target gaji|- 5-10 Juta <br>- 10-15 juta <br>- > 15 juta|

</center>

Dalam CBC, Anda akan menyiapkan pertanyaan berupa kombinasi seluruh atribut dan karakter tersebut

<center>

|No.|Durasi Belajar|Target Karir|Target Gaji|
|:-:|:-|:-|:-|
|1|2 bulan|Tambah skill|5-10 juta|
|2|2 bulan|Tambah skill|10-15 juta|
|3|2 bulan|Tambah skill|>15 juta|
|4|2 bulan|Ganti skill|5-10 juta|
|5|2 bulan|Ganti skill|10-15 juta|
|...|...|...|
|18|12 bulan|Ganti skill|>15 juta|

</center>

Berarti dalam survey, Anda akan memiliki 18 pertanyaan yang dilempar ke customer. Anda bisa rangkum ke dalam 6 pertanyaan apabila Anda memiliki 3 opsi di dalam 1 pertanyaan.

<center>

||Opsi A|Opsi B|Opsi C|
|:-|:-:|:-:|:-:|
|Durasi belajar|8 bulan|12 bulan|2 bulan|
|Target karir|Tambah skill|Ganti karir|Tambah skill
|Target gaji|5-10 juta|di atas 15 juta|>15 juta|

</center>


### Menentukan Responden & Menjalankan Survey
---

Sesuaikan dengan karakter target market. Agar hasil analisa cukup general, Anda bisa menyeimbangkan proporsi responden berdasarkan

* Status pekerjaan
* Background pekerjaan
* Background pendidikan
* Usia

Jalankan survey sesuai dengan kebutuhan. 

* Apabila Anda ingin melakukan riset ini dengan rinci, Anda dapat mengestimasi jumlah responden berdasarkan target confidence level.
* Pastikan Anda mendapatkan karakter responden yang proporsional agar hasilnya berimbang untuk masing-masing karakter responden


### Analisa Conjoint
---

Ringkasnya, 

* Anda akan membuat model untuk memprediksi apakah customer akan membeli produk dengan kombinasi fitur yang anda tawarkan atau tidak. Model yang digunakan adalah model klasifikasi.
* Tapi Anda ingin agar model klasifikasnya dapat diinterpretasikan, sehingga Anda dapat memahami fitur mana yang punya korelasi terhadap potensi customer melakukan pembelian. 

Berarti model yang Anda gunakan adalah **Logistic Regression**

<center>
\(
\begin{align*}
P(\text{buy}) = \sigma(&w_{0} + w_{1}\cdot\text{belajar 2 bulan} + w_{2}\cdot\text{belajar 8 bulan} + w_{3}\cdot\text{belajar 12 bulan} \\
    & + w_{4}\cdot\text{tambah skill} + w_{5}\cdot\text{ganti karir} \\
    & + w_{6}\cdot\text{gaji 5-10 juta} + w_{7}\cdot\text{gaji 10-15 juta} + w_{8}\cdot\text{gaji >15 juta})
\end{align*}
\)
</center>

Saat nilai di dalam fungsi sigmoid, $\sigma(\cdot)$, makin tinggi, maka nilai probability customer melakukan pembelian, $P(\text{buy})$ makin tinggi. Artinya fitur dengan nilai $w$ positif berarti fitur yang lebih dipilih karena meningkatkan $P(\text{buy})$.

Data survey yang Anda dapatkan kira-kira seperti ini (contoh survey yang dilakukan via google form)

<center>

|Timestamp|email|pertanyaan-1|pertanyaan-2|...|pertanyaan-6|
|:-|:-|:-|:-|:-:|:-|
|xxx|ppp|A|A|...|C|
|xxx|qqq|B|A|...|C|
|xxx|rrr|A|C|...|A|
|...|...|...|...|...|...|

</center>

Dari hasil tersebut, konversi menjadi

<center>

|Email|Choice|Durasi Belajar|Target Karir|Target Gaji|
|:-|:-|:-|:-|:-|
|xxx|1|2 bulan|Tambah skill|5-10 juta|
|xxx|0|2 bulan|Tambah skill|10-15 juta|
|xxx|0|2 bulan|Tambah skill|>15 juta|
|xxx|1|2 bulan|Ganti skill|5-10 juta|
|xxx|1|2 bulan|Ganti skill|10-15 juta|
|...|...|...|...|
|xxx|0|12 bulan|Ganti skill|>15 juta|

</center>

`choice` pada tabel di atas menunjukkan apakah user dengan email `xxx` melakukan pilihan pada kombinasi fitur tersebut, `1` untuk memilih dan `0` untuk sebaliknya. Maka Anda dapat membuat model logistic regression dengan `choice` sebagai target yang akan diprediksi.