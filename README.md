# PA-PC_202231050_Andika-Surya-Saputra_A
``` python
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
 OpenCV untuk pemrosesan citra (cv2), NumPy untuk manipulasi array (np), dan Matplotlib untuk plotting (plt).
 
``` python
# Membaca gambar asli
image_path = '/mnt/data/image.png'
image = cv2.imread(image_path)
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
Membaca gambar dari path yang diberikan (image_path).
Mengonversi gambar dari format BGR (standar OpenCV) ke RGB untuk penampilan yang benar di Matplotlib.

``` python
# Membuat mask untuk anggur menggunakan segmentasi warna sederhana
# Ubah gambar ke dalam ruang warna HSV
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
```
Mengonversi gambar dari ruang warna BGR ke HSV (Hue, Saturation, Value) untuk mempermudah segmentasi berdasarkan warna.

``` python
# Definisikan rentang warna untuk anggur (dalam hal ini merah)
lower_red = np.array([0, 70, 50])
upper_red = np.array([10, 255, 255])
mask1 = cv2.inRange(hsv, lower_red, upper_red)

lower_red = np.array([170, 70, 50])
upper_red = np.array([180, 255, 255])
mask2 = cv2.inRange(hsv, lower_red, upper_red)
```
Mendefinisikan dua rentang warna merah dalam ruang warna HSV. Anggur biasanya merah, jadi kita memilih warna merah.
cv2.inRange membuat mask biner untuk warna dalam rentang yang ditentukan.

``` python
# Gabungkan kedua mask
mask_anggur = mask1 | mask2
```
Menggabungkan dua mask merah untuk mendapatkan mask lengkap dari anggur.

``` python
# Terapkan mask ke gambar asli
segmented_anggur = cv2.bitwise_and(image_rgb, image_rgb, mask=mask_anggur)
```
Menerapkan mask ke gambar asli untuk mendapatkan segmentasi anggur.

```python
# Membuat mask untuk daun (menggunakan warna hijau sebagai asumsi)
lower_green = np.array([35, 100, 100])
upper_green = np.array([85, 255, 255])
mask_daun = cv2.inRange(hsv, lower_green, upper_green)
```
Mendefinisikan rentang warna hijau dalam ruang warna HSV, diasumsikan sebagai warna daun.
Membuat mask biner untuk warna hijau.

``` python
# Terapkan mask ke gambar asli
segmented_daun = cv2.bitwise_and(image_rgb, image_rgb, mask=mask_daun)
```
Menerapkan mask ke gambar asli untuk mendapatkan segmentasi daun.

``` python
# Menampilkan hasil
plt.figure(figsize=(12, 8))

plt.subplot(2, 2, 1)
plt.imshow(image_rgb)
plt.title('Gambar Asli')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(mask_anggur, cmap='gray')
plt.title('Mask Anggur')
plt.axis('off')

plt.subplot(2, 2, 3)
plt.imshow(segmented_anggur)
plt.title('Segmentasi Anggur')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.imshow(segmented_daun)
plt.title('Segmentasi Daun')
plt.axis('off')

plt.tight_layout()
plt.show()
```
Menampilkan gambar asli, mask anggur, segmentasi anggur, dan segmentasi daun menggunakan Matplotlib.
plt.figure(figsize=(12, 8)) membuat kanvas figure dengan ukuran yang ditentukan.
plt.subplot membagi kanvas menjadi grid 2x2 untuk menampilkan gambar secara terpisah.
plt.imshow menampilkan gambar.
plt.title memberikan judul pada setiap subplot.
plt.axis('off') menyembunyikan sumbu.
plt.tight_layout() mengatur tata letak agar tidak ada overlap.
plt.show() menampilkan semua plot.







