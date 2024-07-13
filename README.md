
# Laporan UTS Pengolahan Citra C

## Tahapan Pengerjaan

### 1. Membuat Library
- Dipakai tiga library utama untuk membantu pengerjaan projek
- Yaitu cv2 (computer vision) yang digunakan untuk pengolahan gambar
- pyplot dari matplotlib yang digunakan untuk visualisasi gambar/hasil pengolahan
- numpy yang digunakan untuk membantu dalam pengolahan data matriks/array (data gambar)

### 2. Membaca gambar
- Dengan menggunakan cv2.imread, saya memasukkan/membaca gambar kedalam variabel img, untuk kemudian digunakan dan diolah.
- Setelahnya kemudian dilakukan pengecekan terhadap status quo gambar yang ada di dalam variabel img, dengan menampilkannya melalui plt.imshow()

### 3. Mengubah format gambar
- Gambar yang ditampilkan pada fungsi plt.imshow() terlihat masih aneh/tidak sesuai dengan gambar asli, dan diketahui penyebabnya adalah karena plt.imshow() menampilkan gambar dalam format RGB sedangkan gambar yang diambil dengan fungsi cv2.imread() secara default berformat BGR
- Sehingga dilakukan konversi data gambar dari BGR menjadi RGB

### 4. Pemurnian Warna/PIksel
- Sebelum dilakukan pemurnian warna, diambil besar baris dan kolom dari gambar dengan menggunakan bantuan img.shape[:2], yaitu mengambil nilai dari 2 dimensi pertama gambar [baris, kolom]
- Dibuat barisan kode pemurnian warna dengan konsep sebagai berikut (tertulis juga pada comment program)
- _Pada kode dibawah dilakukan pemurnian warna dengan mencari elemen warna (R/G/B) dengan intensitas tertinggi, dan warna dengan intensitas kedua tertinggi kemudian melakukan pembandingan keduanya dengan mencari selisih antar keduanya dan kemudian menghitung apakah mereka lebih besar dari 10 (kemungkinan bukan putih) atau kurang dari 10 (kemungkinan putih), dan apabila warna piksel kemungkinan bukan putih (>10) maka warna-warna lain (selain warna dengan intensitas maksimum) akan menjadi 0 (sehingga piksel menjadi warna yang murni R/G/B)_

### 5. Deteksi Warna Pada Citra (Soal 1)
- Deteksi warna dilakukan dengan memanggil salah satu elemen warna (R/G/B) untuk setiap piksel dan menyajikannya sebagai sebuah citra abu-abu/1 kedalaman
- Dengan syntax umum sebagai berikut:
img[:,:,0/1/2] --> dengan 0 = merah, 1 = hijau, 2 = biru

- Dalam tahapan ini, diberikan juga visualisasi dari hasil deteksi warna berupa visualisasi gambar dan histogram
- Dari gambar, dapat dilihat bahwa gambar yang warnanya di deteksi, memiliki tulisan/huruf yang warnanya merupakan warna yang sedang dideteksi, berubah menjadi putih/mendekati putih. Hal ini terjadi karena, dalam syntax pendeteksian warna yang dipakai (diatas), gambar diubah menjadi citra abu, yang intensitas warnanya ditentukan oleh intensitas warna yang sedang dideteksi, sehingga, warna yang dideteksi, yang memiliki besaran tinggi pada spektrum/elemen warna tersebut, menjadi terlihat putih, dan warna selainnya menjadi hitam (kecuali untuk putih, karena putih terdiri dari ketiga elemen warna yang nilainya relatif sudah tinggi)
- Histogram dibuat dengan menggunakan fungsi .hist, yang menghitung dan menyajikan histogram berupa data intensitas dari gambar.

### 6. Ambang Batas (Soal 2)
- Sesuai dengan instruksi soal, selanjutnya saya mencari ambang-ambang batas untuk munculnya kategori-kategori warna pada gambar dari filter threshold
- Ambang batas dicari dengan pertama-tama mengkonversi gambar dari RGB ke grayscale dengan bantuan cv2.cvtColor()
- Lalu dengan bantuan fungsi threshold, saya dapat mencoba-coba ambang batas mana yang dapat memunculkan, Blue, Red (dan Blue) serta Green (dan Red-Blue).
- Untuk detail syntax threshold (secara umum)

(thresh, binary) = cv2.threshold(gray, x, 255, cv2.THRESH_BINARY)

Dengan x sebagai threshold yang dipakai, dan dengan acuan threshold untuk kasus biner (THRESH_BINARY)

- Setelah dilakukan percobaan ambang batas, didapat ambang batas untuk kategori BLUE = 30, RED-BLUE = 60 dan RED-GREEN-BLUE = 90
- Ambang batas dikatakan ditemukan disaat huruf2 yang memiliki warna yang ingin di kategorikan 










