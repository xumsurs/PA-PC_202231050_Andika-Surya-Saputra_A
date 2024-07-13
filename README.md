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
