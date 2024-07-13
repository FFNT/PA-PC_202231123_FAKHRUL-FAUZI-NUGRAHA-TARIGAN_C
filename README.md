# Proyek Ujian Akhir Semester Praktikum Pengolahan Citra Digital - Fakhrul Fauzi Nugraha Tarigan [202231123] - Geomatrix Citra

## Latar Belakang Teoritis

### Pemrosesan Citra
Pemrosesan citra adalah teknik yang digunakan untuk melakukan operasi pada citra guna meningkatkan kualitas atau mengekstrak informasi yang relevan. Ini adalah bagian dari pemrosesan sinyal di mana inputnya adalah citra dan outputnya bisa berupa citra yang ditingkatkan atau fitur-fitur yang diekstraksi dari citra tersebut.

### OpenCV
OpenCV adalah perpustakaan sumber terbuka untuk visi komputer dan pembelajaran mesin yang menyediakan berbagai algoritma untuk pemrosesan citra dan video.

### Matplotlib
Matplotlib adalah perpustakaan plotting untuk Python yang memungkinkan kita untuk membuat visualisasi data, termasuk menampilkan citra hasil pemrosesan.

## Langkah-Langkah Proyek

### 1. Membaca dan Menampilkan Citra
Langkah pertama adalah membaca citra dan menampilkannya menggunakan Matplotlib. Saya menggunakan fungsi `cv2.imread()` untuk membaca citra dan `cv2.cvtColor()` untuk mengkonversi format warna dari BGR (default OpenCV) ke RGB (default Matplotlib).

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt

# Membaca citra dari file
img = cv2.imread("gambar_fauzi.jpeg")

# Mengkonversi format warna dari BGR ke RGB
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Menampilkan citra
plt.imshow(img)
plt.title("Gambar Asli")
plt.show()
```

### 2. Rotasi Citra
Selanjutnya, saya akan memutar citra sebesar 45 derajat. Untuk ini, saya menggunakan fungsi `cv2.getRotationMatrix2D()` untuk membuat matriks rotasi dan `cv2.warpAffine()` untuk menerapkan matriks tersebut pada citra.

```python
# Mendapatkan ukuran citra
rows, cols = img.shape[:2]

# Membuat matriks rotasi
M = cv2.getRotationMatrix2D(((cols-1)/2.0, (rows-1)/2.0), 45, 1)

# Menerapkan rotasi pada citra
img_rotated = cv2.warpAffine(img, M, (cols, rows))

# Menampilkan citra asli dan citra yang dirotasi
fig, axs = plt.subplots(1, 2, figsize=(15, 5))
axs[0].imshow(img)
axs[0].set_title("Gambar Asli")
axs[1].imshow(img_rotated)
axs[1].set_title("Gambar Dirotasi")
plt.show()
```

### 3. Pengubahan Ukuran Citra
Saya akan mengubah ukuran citra menjadi 20% dari ukuran aslinya menggunakan fungsi `cv2.resize()`.

```python
# Mengubah ukuran citra menjadi 20% dari ukuran asli
resized = cv2.resize(img, None, fx=0.2, fy=0.2, interpolation=cv2.INTER_CUBIC)

# Menampilkan citra yang telah diubah ukurannya
plt.imshow(resized)
plt.title("Gambar Diresize")
plt.show()
```

### 4. Pemotongan Citra
Langkah berikutnya adalah memotong bagian tertentu dari citra. Saya menentukan koordinat awal (x, y) dan ukuran (lebar dan tinggi) dari bagian yang akan dipotong.

```python
# Koordinat dan ukuran bagian yang akan dipotong
x = 750  # Koordinat x awal
y = 1250  # Koordinat y awal
w = 1500  # Lebar crop
h = 2250  # Tinggi crop

# Memotong bagian yang ditentukan dari citra
cropped = img[y:y+h, x:x+w]

# Menampilkan citra yang telah dipotong
plt.imshow(cropped)
plt.title("Gambar Dicrop")
plt.show()
```

### 5. Flipping Citra
Membalik citra secara horizontal dengan mengganti setiap kolom dengan kolom dari ujung yang berlawanan.

```python
# Membuat salinan citra untuk di-flip
flipped = img.copy()

# Membalik citra secara horizontal
for x in range(cols):
    flipped[:, x-1] = img[:, cols-x-1]

# Menampilkan citra yang telah di-flip
plt.imshow(flipped)
plt.title("Gambar Diflip")
plt.show()
```

### 6. Translasi Citra
Mentranslasi citra sejauh 1000 piksel ke kanan dan 100 piksel ke bawah menggunakan matriks translasi dan fungsi `cv2.warpAffine()`.

```python
# Membuat matriks translasi
M = np.float32([[1, 0, 1000], [0, 1, 100]])

# Menerapkan translasi pada citra
img_translasi = cv2.warpAffine(img, M, (cols, rows))

# Menampilkan citra yang telah ditranslasi
plt.imshow(img_translasi)
plt.title("Gambar Ditranslasi")
plt.show()
```

### 7. Menampilkan Semua Gambar
Menampilkan semua citra yang telah diproses dalam sebuah grid untuk memudahkan perbandingan.

```python
# Menampilkan semua citra yang telah diproses dalam sebuah grid
fig, axs = plt.subplots(2, 3, figsize=(15, 15))

axs[0][0].imshow(img)
axs[0][0].set_title("Gambar Asli")

axs[0][1].imshow(img_rotated)
axs[0][1].set_title("Gambar Dirotasi")

axs[0][2].imshow(resized)
axs[0][2].set_title("Gambar Diresize")

axs[1][0].imshow(cropped)
axs[1][0].set_title("Gambar Dicrop")

axs[1][1].imshow(flipped)
axs[1][1].set_title("Gambar Diflip")

axs[1][2].imshow(img_translasi)
axs[1][2].set_title("Gambar Ditranslasi")

plt.show()
```