# DETEKSI GARIS - ICHSAN BUDIMAN PUTRA - 202131153

# TEORI YANG MENDUKUNG
Konsep algoritma deteksi tepi pada dasarnya
memanfaatkan 8-ketetanggaan. Jika sekeliling pixel P bernilai sama (semua=1 atau semua=0), maka diasumsikan bahwa pixel P tidak berada di tepi objek.

Terdapat beberapa teori dan konsep yang mendukung project deteksi tepi menggunakan contour dalam gambar. Berikut adalah beberapa materi dan teori yang relevan:

1. Grayscale: Deteksi tepi sering kali dilakukan pada gambar dalam bentuk grayscale. Grayscale adalah representasi gambar yang hanya memiliki satu saluran warna, yaitu tingkat keabuan. Dalam representasi grayscale, setiap piksel diwakili oleh intensitas keabuan tunggal dalam rentang nilai antara 0 hingga 255. Konversi gambar ke grayscale dilakukan untuk mempermudah analisis tepi, karena hanya perlu fokus pada perbedaan intensitas piksel.

2. Thresholding: Thresholding adalah proses mengubah gambar grayscale menjadi gambar biner, yaitu gambar yang hanya memiliki dua nilai piksel, yaitu hitam dan putih. Pada deteksi tepi, thresholding digunakan untuk memisahkan area yang memiliki intensitas tinggi (representasi tepi) dengan area yang memiliki intensitas rendah. Thresholding membantu memfokuskan perhatian pada tepi yang ingin dideteksi.

3. Deteksi Kontur: Deteksi tepi menggunakan contour (kontur) merupakan salah satu metode yang umum digunakan. Kontur adalah garis berkelanjutan yang mengelilingi atau membentuk batas objek dalam gambar. Pada deteksi tepi, kontur digunakan untuk mengidentifikasi area dengan perubahan intensitas yang signifikan, yang menandakan adanya tepi. Metode `cv2.findContours()` digunakan untuk menemukan kontur dalam gambar setelah dilakukan thresholding.

4. Chain Approximation: Chain approximation (aproksimasi rantai) adalah teknik untuk mengurangi jumlah titik pada kontur. Dalam deteksi tepi, hal ini dilakukan untuk menyederhanakan kontur dan mengurangi jumlah titik yang perlu digambar. Chain approximation digunakan dalam parameter `cv2.CHAIN_APPROX_SIMPLE` pada fungsi `cv2.findContours()`.

5. Menggambar Kontur: Setelah kontur ditemukan, fungsi `cv2.drawContours()` digunakan untuk menggambar kontur pada gambar asli. Fungsi ini membutuhkan gambar asli, kontur yang ditemukan, indeks kontur (-1 untuk menggambar semua kontur), warna garis, dan ketebalan garis sebagai parameter. Dalam project di atas, warna garis yang digunakan adalah merah dengan ketebalan 3.

Dengan memahami konsep-konsep tersebut, Kiat dapat menggunakan metode deteksi tepi menggunakan contour dalam proyek-proyek pengolahan gambar yang lebih kompleks atau untuk memecahkan masalah khusus lainnya yang melibatkan analisis tepi dalam gambar.

Penjelasan lebih dapat dibaca pada journal terkait (dipenjelasan deteksi garis) link disertakan dibagian paling bawah README.

# CODINGAN DAN PENJELASAN CODINGAN

    import cv2
    import numpy as np
    import matplotlib.pyplot as plt

    # Baca gambar
    image = cv2.imread('bahan/ICHSAN.jpg')

    # Konversi gambar ke grayscale
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Thresholding gambar
    ret, thresh = cv2.threshold(gray, 127, 255, 0)

    # Cari kontur pada gambar
    contours, hierarchy = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    # Gambar kontur pada gambar asli
    contour_image = cv2.drawContours(image.copy(), contours, -1, (0, 0, 255), 3)

    # Buat gambar dengan background putih
    white_bg = np.ones_like(image) * 255
    contour_white_bg = cv2.drawContours(white_bg.copy(), contours, -1, (0, 0, 0), 3)

    # Tampilkan gambar asli
    plt.subplot(131)
    plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
    plt.title('Original Image')
    plt.axis('on')

    # Tampilkan gambar dengan contour pada background putih
    plt.subplot(132)
    plt.imshow(cv2.cvtColor(contour_white_bg, cv2.COLOR_BGR2RGB))
    plt.title('Contour Image')
    plt.axis('on')

    # Tampilkan gambar dengan contour pada background seperti aslinya
    plt.subplot(133)
    plt.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
    plt.axis('on')

    plt.tight_layout()
    plt.show()

Pada kode diatas, terdapat implementasi deteksi kontur pada gambar menggunakan library OpenCV. Berikut adalah penjelasan singkat mengenai langkah-langkah yang dilakukan dalam project tersebut:

1. Pertama, gambar yang ingin dideteksi konturnya dibaca menggunakan fungsi `cv2.imread()` dan disimpan dalam variabel `image`.

2. Selanjutnya, gambar diubah menjadi grayscale menggunakan fungsi `cv2.cvtColor()` dengan parameter `cv2.COLOR_BGR2GRAY`. Hal ini diperlukan untuk memproses gambar dalam bentuk grayscale yang lebih sederhana.

3. Setelah itu, dilakukan thresholding pada gambar grayscale menggunakan fungsi `cv2.threshold()`. Pada contoh kode, nilai threshold yang digunakan adalah 127, sehingga semua piksel dengan intensitas di atas 127 akan diubah menjadi putih (255), sedangkan piksel dengan intensitas di bawah 127 akan diubah menjadi hitam (0). Hasil thresholding disimpan dalam variabel `thresh`.

4. Selanjutnya, dilakukan pencarian kontur pada gambar menggunakan fungsi `cv2.findContours()`. Parameter `cv2.RETR_EXTERNAL` digunakan untuk mendapatkan hanya kontur eksternal (kontur yang berada di luar kontur lainnya), sedangkan `cv2.CHAIN_APPROX_SIMPLE` digunakan untuk mengompresi kontur yang ditemukan.

5. Setelah kontur ditemukan, kontur tersebut digambar pada gambar asli menggunakan fungsi `cv2.drawContours()` dengan parameter `(0, 0, 255)` yang mewakili warna garis merah. Hasilnya disimpan dalam variabel `contour_image`.

6. Selanjutnya, dilakukan pembuatan gambar dengan background putih menggunakan array numpy. Gambar tersebut digunakan untuk menampilkan kontur dengan background putih. Kontur juga digambar pada gambar dengan background putih menggunakan fungsi `cv2.drawContours()` dengan parameter `(0, 0, 0)` yang mewakili warna garis hitam. Hasilnya disimpan dalam variabel `contour_white_bg`.

7. Terakhir, menggunakan library matplotlib, ketiga gambar (gambar asli, gambar dengan kontur pada background putih, dan gambar dengan kontur pada background aslinya) ditampilkan secara sejajar menggunakan fungsi `plt.subplot()`. Pada contoh kode, fungsi `plt.tight_layout()` juga digunakan untuk memperbaiki tata letak tampilan gambar.

Dengan demikian, kode tersebut akan menampilkan tiga gambar sejajar: gambar asli, gambar dengan kontur pada background putih, dan gambar dengan kontur pada background aslinya.

# JOURNAL TERKAIT
https://www.researchgate.net/publication/358220979_Pengolahan_Citra_Digital_Menggunakan_Python