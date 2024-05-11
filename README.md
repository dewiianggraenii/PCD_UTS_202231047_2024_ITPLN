
# Tahapan Penyelesaian Projek Terkait

## 1. Import Library
- OpenCV (cv2): Library populer untuk pemrosesan citra dan video.

- Matplotlib (plt): Library untuk membuat visualisasi data seperti plot grafik.

- NumPy (np): Library untuk komputasi numerik yang kuat, terutama dalam manipulasi array.

## 2. Membaca Data Gambar
- img = cv2.imread("Dewi.jpg"): Baris ini membaca gambar "Dewi.jpg" menggunakan fungsi imread dari OpenCV. Fungsi ini mengembalikan citra dalam bentuk array NumPy. Citra tersebut disimpan dalam variabel img.

- img.shape: Baris ini menggunakan atribut shape dari array NumPy untuk mendapatkan dimensi dari citra yang telah dibaca sebelumnya. Atribut shape mengembalikan tuple yang berisi (tinggi, lebar, jumlah saluran warna) dari citra. Untuk citra berwarna, jumlah saluran warna adalah 3 (untuk warna merah, hijau, dan biru). Jika citra adalah citra grayscale, maka jumlah salurannya adalah 1.

## 3. Membuat Baris Dan Kolom
- (baris, kolom) = img.shape[:2]: Baris ini mendeklarasikan dua variabel, baris dan kolom, yang akan menampung dimensi citra yang telah dibaca sebelumnya. Penggunaan [:2] pada img.shape berarti kita hanya mengambil dua nilai pertama dari tuple yang dikembalikan oleh img.shape, yaitu tinggi (baris) dan lebar (kolom) citra. Variabel baris akan menyimpan tinggi citra, sedangkan variabel kolom akan menyimpan lebarnya.

- img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB): Baris ini mengonversi citra dari ruang warna BGR (Blue, Green, Red) ke ruang warna RGB (Red, Green, Blue). OpenCV secara default membaca citra dalam ruang warna BGR, sedangkan Matplotlib, yang akan kita gunakan untuk menampilkan citra, membutuhkan citra dalam format RGB. Oleh karena itu, kita perlu melakukan konversi ruang warna menggunakan fungsi cv2.cvtColor.

## 4. membuat Citra Kontras
- alpa = 1.15: Inisialisasi variabel alpa dengan nilai 1.15. Ini adalah nilai yang akan digunakan untuk mengatur kontras gambar.

- citra_kontras = np.zeros((baris, kolom, 3)): Membuat matriks tiga dimensi yang berukuran (baris, kolom, 3) yang diinisialisasi dengan nol. Matriks ini akan menyimpan citra kontras.

- for x in range(baris): dan for y in range(kolom):: Ini adalah loop bersarang untuk mengiterasi setiap piksel dalam gambar. Variabel x dan y merepresentasikan koordinat piksel.

- gmx = img[x,y] * alpa: Mengalikan nilai piksel asli pada posisi (x, y) dengan faktor kontras (alpa) dan menyimpan hasilnya dalam variabel gmx.

- citra_kontras[x,y] = gmx: Menyimpan nilai kontras yang dihitung sebelumnya (gmx) ke dalam matriks citra kontras pada posisi (x, y).

- citra_kontras = citra_kontras.astype(np.uint8): Mengonversi matriks citra kontras ke tipe data uint8 yang sesuai untuk representasi gambar.

- fig, axs = plt.subplots(2,2, figsize=(15,10)): Membuat sebuah figure dan array dari subplot dengan ukuran 2x2 (total 4 subplot) dengan ukuran gambar (figsize) 15x10.

- axs[0,0].imshow(img): Menampilkan citra asli di subplot pertama (baris pertama, kolom pertama).

- axs[0,1].hist(img.ravel(),256,[0,256]): Membuat histogram dari citra asli dan menampilkannya di subplot pertama pada kolom kedua.

- axs[1,0].imshow(citra_kontras): Menampilkan citra hasil kontras di subplot kedua (baris kedua, kolom pertama).

- axs[1,1].hist(citra_kontras.ravel(),256,[0,256]): Membuat histogram dari citra kontras dan menampilkannya di subplot kedua pada kolom kedua.

- plt.show(): Menampilkan semua subplot yang telah dibuat.

## 5. Operasi Peningkatan Kecerahan
- beta = 30: Variabel beta diinisialisasi dengan nilai 30. Ini adalah nilai yang akan digunakan untuk mengatur kecerahan gambar.

- citra_cerah = np.zeros((baris, kolom, 3)): Membuat matriks tiga dimensi yang berukuran (baris, kolom, 3) yang diinisialisasi dengan nol. Matriks ini akan menyimpan citra yang diterangi.

- for x in range(baris): dan for y in range(kolom):: Loop bersarang untuk mengiterasi setiap piksel dalam gambar. Variabel x dan y merepresentasikan koordinat piksel.

- gyx = img[x,y] + beta: Menambahkan nilai beta ke nilai piksel asli pada posisi (x, y) dan menyimpan hasilnya dalam variabel gyx.

- citra_cerah[x,y] = gyx: Menyimpan nilai kecerahan yang dihitung sebelumnya (gyx) ke dalam matriks citra yang diterangi pada posisi (x, y).

- citra_cerah = citra_cerah.astype(np.uint8): Mengonversi matriks citra yang diterangi ke tipe data uint8 yang sesuai untuk representasi gambar.

- fig, axs = plt.subplots(2,2, figsize=(15,5)): Membuat sebuah figure dan array dari subplot dengan ukuran 2x2 (total 4 subplot) dengan ukuran gambar (figsize) 15x5.

- axs[0,0].imshow(img): Menampilkan citra asli di subplot pertama (baris pertama, kolom pertama).

- axs[0,1].hist(img.ravel(),256,[0,256]): Membuat histogram dari citra asli dan menampilkannya di subplot pertama pada kolom kedua.

- axs[1,0].imshow(citra_cerah): Menampilkan citra yang diterangi di subplot kedua (baris kedua, kolom pertama).

- axs[1,1].hist(citra_cerah.ravel(),256,[0,256]): Membuat histogram dari citra yang diterangi dan menampilkannya di subplot kedua pada kolom kedua.

- plt.show(): Menampilkan semua subplot yang telah dibuat.

## 6. Deteksi Warna Merah Pada Citra
- red_channel = citra_cerah[:,:,0]: Mengambil saluran merah (red channel) dari citra yang diterangi (citra_cerah). Citra tersebut adalah representasi tiga dimensi dari citra, dimana saluran merah diwakili oleh indeks 0.

- plt.figure(figsize=(15, 5)): Membuat suatu figure (gambar) dengan ukuran 15x5.

- plt.subplot(1, 2, 1): Membuat subplot pertama dalam grid 1x2 (satu baris, dua kolom) dan mengatur fokus pada subplot tersebut.

- plt.imshow(red_channel, cmap='gray'): Menampilkan gambar dari saluran merah (red_channel) dengan colormap 'gray' untuk menunjukkan intensitasnya.

- plt.title('Red'): Memberikan judul "Red" pada subplot pertama.

- plt.subplot(1, 2, 2): Membuat subplot kedua dalam grid 1x2 dan mengatur fokus pada subplot tersebut.

- plt.hist(red_channel.ravel(), bins=256, alpha=0.7): Membuat histogram dari saluran merah (red_channel). ravel() digunakan untuk meratakan matriks menjadi satu dimensi, bins=256 menunjukkan jumlah bin yang digunakan dalam histogram, dan alpha=0.7 menunjukkan tingkat transparansi histogram.

- plt.xlabel('Intensity'): Memberikan label "Intensity" pada sumbu x untuk subplot kedua.

- plt.ylabel('Frequency'): Memberikan label "Frequency" pada sumbu y untuk subplot kedua.

- plt.title('Histogram Red'): Memberikan judul "Histogram Red" pada subplot kedua.

- plt.show(): Menampilkan plot yang telah dibuat.

## 7. Deteksi Warna Hijau Pada Citra

- green_channel = citra_cerah[:,:,1]: Mengambil saluran hijau (green channel) dari citra yang diterangi (citra_cerah). Citra ini merupakan representasi tiga dimensi dari citra, di mana saluran hijau direpresentasikan oleh indeks 1.

- plt.figure(figsize=(15, 5)): Membuat suatu figure (gambar) dengan ukuran 15x5.

- plt.subplot(1, 2, 1): Membuat subplot pertama dalam grid 1x2 (satu baris, dua kolom) dan mengatur fokus pada subplot tersebut.

- plt.imshow(green_channel, cmap='gray'): Menampilkan gambar dari saluran hijau (green_channel) dengan colormap 'gray' untuk menunjukkan intensitasnya.

- plt.title('Green'): Memberikan judul "Green" pada subplot pertama.

- plt.subplot(1, 2, 2): Membuat subplot kedua dalam grid 1x2 dan mengatur fokus pada subplot tersebut.

- plt.hist(green_channel.ravel(), bins=256, alpha=0.7): Membuat histogram dari saluran hijau (green_channel). ravel() digunakan untuk meratakan matriks menjadi satu dimensi, bins=256 menunjukkan jumlah bin yang digunakan dalam histogram, dan alpha=0.7 menunjukkan tingkat transparansi histogram.

- plt.xlabel('Intensity'): Memberikan label "Intensity" pada sumbu x untuk subplot kedua.

- plt.ylabel('Frequency'): Memberikan label "Frequency" pada sumbu y untuk subplot kedua.

- plt.title('Histogram Green'): Memberikan judul "Histogram Green" pada subplot kedua.

- plt.show(): Menampilkan plot yang telah dibuat.

## 8. Deteksi Warna Biru Pada Citra

- blue_channel = citra_cerah[:,:,2]: Mengambil saluran biru (blue channel) dari citra yang diterangi (citra_cerah). Citra ini merupakan representasi tiga dimensi dari citra, di mana saluran biru direpresentasikan oleh indeks 2.

- plt.figure(figsize=(15, 5)): Membuat suatu figure (gambar) dengan ukuran 15x5.

- plt.subplot(1, 2, 1): Membuat subplot pertama dalam grid 1x2 (satu baris, dua kolom) dan mengatur fokus pada subplot tersebut.

- plt.imshow(blue_channel, cmap='gray'): Menampilkan gambar dari saluran biru (blue_channel) dengan colormap 'gray' untuk menunjukkan intensitasnya.

- plt.title('Blue'): Memberikan judul "Blue" pada subplot pertama.

- plt.subplot(1, 2, 2): Membuat subplot kedua dalam grid 1x2 dan mengatur fokus pada subplot tersebut.

- plt.hist(blue_channel.ravel(), bins=256, alpha=0.7): Membuat histogram dari saluran biru (blue_channel). ravel() digunakan untuk meratakan matriks menjadi satu dimensi, bins=256 menunjukkan jumlah bin yang digunakan dalam histogram, dan alpha=0.7 menunjukkan tingkat transparansi histogram.

- plt.xlabel('Intensity'): Memberikan label "Intensity" pada sumbu x untuk subplot kedua.

- plt.ylabel('Frequency'): Memberikan label "Frequency" pada sumbu y untuk subplot kedua.

- plt.title('Histogram Blue'): Memberikan judul "Histogram Blue" pada subplot kedua.

- plt.show(): Menampilkan plot yang telah dibuat.

## 9.  Nilai Ambang batas Citra Untuk Dapat Menampilan Kategori Warna Pada Citra

- lower_blue, upper_blue, lower_green, upper_green, lower_red1, upper_red1, lower_red2, dan upper_red2: Menentukan rentang warna untuk setiap warna yang ingin dideteksi dalam ruang warna HSV.

- mask_blue, mask_green, mask_red1, dan mask_red2: Melakukan segmentasi warna biru, hijau, dan merah pada citra HSV menggunakan rentang warna yang telah ditentukan sebelumnya.

- mask_red: Menggabungkan dua mask merah menggunakan operasi bitwise OR, karena warna merah memiliki dua rentang pada ruang warna HSV.

- gray = cv2.cvtColor(citra_cerah, cv2.COLOR_RGB2GRAY): Mengubah citra asli menjadi citra dalam skala abu-abu (grayscale) untuk digunakan dalam plot pertama.

- fig, axs = plt.subplots(2, 2, figsize=(10,10)): Membuat sebuah figure dan array dari subplot dengan ukuran 2x2 (total 4 subplot) dengan ukuran gambar (figsize) 10x10.

- (thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY): Menerapkan thresholding pada citra grayscale untuk mendapatkan citra biner.

- axs[0,0].imshow(binary1, cmap = 'gray'): Menampilkan citra biner hasil thresholding pada subplot pertama.

- plt.subplot(2, 2, 2), plt.subplot(2, 2, 3), plt.subplot(2, 2, 4): Mengatur fokus pada subplot kedua, ketiga, dan keempat.

- plt.imshow(mask_blue, cmap='gray'), plt.imshow(np.maximum(mask_red, mask_blue), cmap='gray'), plt.imshow(mask_green, cmap='gray'): Menampilkan hasil segmentasi warna biru, merah-biru, dan hijau pada masing-masing subplot.

- plt.xticks(np.arange(0, mask_blue.shape[1]+1, 800)), plt.yticks(np.arange(0, mask_blue.shape[0]+1, 500)): Mengatur penanda sumbu x dan y pada plot untuk menunjukkan nilai piksel.

- plt.axis('on'): Menampilkan sumbu pada plot.

-  plt.tight_layout(): Mengatur layout plot agar rapih.

- plt.show(): Menampilkan plot yang telah dibuat.

## 10. Analisis  Hasil Yang Terjadi Pada Citra kontras

Analisis Citra:

Citra tersebut tampaknya berupa grafik yang menunjukkan hubungan antara dua variabel. Sumbu x diberi label "Jumlah Kata", dan sumbu y diberi label "Frekuensi". Grafik menunjukkan tren naik secara umum, yang menunjukkan bahwa ada lebih banyak gambar dengan jumlah kata yang lebih tinggi. Namun, ada juga beberapa variasi dalam frekuensi, menunjukkan bahwa ada keragaman gambar dalam hal jumlah kata mereka.

Analisis Histogram:

Histogram menunjukkan distribusi nilai piksel dalam citra. Sumbu x mewakili nilai piksel (berkisar dari 0 hingga 255), dan sumbu y mewakili jumlah piksel dengan setiap nilai piksel. Histogram menunjukkan bahwa sebagian besar piksel dalam citra memiliki nilai piksel antara 150 dan 255, menunjukkan bahwa citra tersebut sebagian besar berwarna terang.

Pengamatan Keseluruhan:

Berdasarkan analisis citra dan histogram, tampak bahwa citra tersebut merupakan representasi dari kumpulan data gambar dengan jumlah kata yang bervariasi. Tren naik pada grafik menunjukkan bahwa ada lebih banyak gambar dengan jumlah kata yang lebih tinggi, sementara variasi dalam frekuensi menunjukkan bahwa ada keragaman gambar dalam hal jumlah kata mereka. Histogram menunjukkan bahwa citra tersebut sebagian besar berwarna terang.

## 11. Analisis  Hasil Yang Terjadi Pada Citra Merah

Citra:

Citra menunjukkan pesan tulisan tangan yang bertuliskan "DEWLANGGRAENI". Pesan tersebut ditulis dengan tinta merah dan memiliki latar belakang putih.

Histogram:

Histogram menunjukkan distribusi nilai intensitas merah dalam gambar. Sumbu x mewakili nilai intensitas, berkisar dari 0 (hitam) hingga 255 (merah cerah). Sumbu y mewakili jumlah piksel yang memiliki nilai intensitas tersebut.

## 12. Analisis  Hasil Yang Terjadi Pada Citra Hijau
Citra:

Citra menunjukkan pesan tulisan tangan yang bertuliskan "DEWLANGGRAENI". Pesan tersebut ditulis dengan tinta biru dan memiliki latar belakang putih.

Histogram:

Histogram menunjukkan distribusi nilai intensitas biru dalam gambar. Sumbu x mewakili nilai intensitas, berkisar dari 0 (hitam) hingga 255 (biru cerah). Sumbu y mewakili jumlah piksel yang memiliki nilai intensitas tersebut.

## Nilai Ambang batas Citra Untuk Dapat Menampilan Kategori None dan Blue

#### Citra:

Citra yang Anda berikan menunjukkan histogram yang menampilkan distribusi nilai intensitas warna pada sebuah citra. Histogram tersebut menunjukkan bahwa terdapat beberapa kategori warna yang dominan dalam citra, yaitu:

- Hitam: Terdapat nilai intensitas 0 yang menunjukkan adanya piksel berwarna hitam pada citra.
- Putih: Terdapat nilai intensitas 255 yang menunjukkan adanya piksel berwarna putih pada citra.

#### Nilai Ambang Batas:

Nilai ambang batas dalam citra adalah nilai intensitas yang digunakan untuk membedakan antara kategori warna yang berbeda. Dalam histogram yang Anda berikan, terdapat satu nilai ambang batas yang terlihat:

- Nilai ambang batas 128: Nilai ini digunakan untuk membedakan antara piksel berwarna hitam dan putih. Piksel dengan nilai intensitas di bawah 128 dikategorikan sebagai hitam, sedangkan piksel dengan nilai intensitas 128 atau lebih dikategorikan sebagai putih.

#### Kategori Warna:

Berdasarkan nilai ambang batas yang telah disebutkan, terdapat dua kategori warna yang dapat diidentifikasi pada citra, yaitu:

- Hitam: Piksel dengan nilai intensitas di bawah 128.

- Putih: Piksel dengan nilai intensitas 128 atau lebih.

#### Alasan Pemilihan Nilai Ambang Batas:
Nilai ambang batas 128 dipilih dalam analisis ini didasarkan pada beberapa pertimbangan, yaitu:

- Distribusi Nilai Intensitas: Nilai ambang batas 128 berada di tengah rentang nilai intensitas untuk piksel berwarna hitam dan putih. Hal ini membantu memisahkan piksel berwarna hitam dan putih dengan lebih baik.
- Kualitas Hasil Segmentasi: Nilai ambang batas 128 menghasilkan segmentasi yang baik untuk piksel berwarna hitam dan putih. Hal ini membantu memisahkan piksel berwarna hitam dari piksel berwarna putih dengan lebih baik.
- Penyesuaian Visual: Nilai ambang batas juga disesuaikan dengan observasi visual terhadap citra. Hal ini dilakukan untuk memastikan bahwa hasil segmentasi sesuai dengan apa yang terlihat pada citra.

##### Kesimpulan:
Nilai ambang batas 128 yang dipilih dalam analisis ini menghasilkan segmentasi yang baik untuk citra yang diberikan. Nilai ambang batas tersebut didasarkan pada distribusi nilai intensitas, kualitas hasil segmentasi, dan penyesuaian visual terhadap citra.

## Nilai Ambang batas Citra Untuk Dapat Menampilan Kategori Red-Blue dan Red-Green-Blue

#### Citra:
Citra yang Anda berikan menunjukkan histogram yang menampilkan distribusi nilai intensitas warna pada sebuah citra. Histogram tersebut menunjukkan bahwa terdapat beberapa kategori warna yang dominan dalam citra, yaitu:

- Hitam: Terdapat nilai intensitas 0 yang menunjukkan adanya piksel berwarna hitam pada citra.
Biru: Terdapat nilai intensitas yang berkisar antara 500 hingga 1000 yang menunjukkan adanya piksel berwarna biru pada citra.
- Putih: Terdapat nilai intensitas 255 yang menunjukkan adanya piksel berwarna putih pada citra.

#### Nilai Ambang Batas:

Nilai ambang batas dalam citra adalah nilai intensitas yang digunakan untuk membedakan antara kategori warna yang berbeda. Dalam histogram yang Anda berikan, terdapat dua nilai ambang batas yang terlihat:

- Nilai ambang batas 500: Nilai ini digunakan untuk membedakan antara piksel berwarna hitam dan biru. Piksel dengan nilai intensitas di bawah 500 dikategorikan sebagai hitam, sedangkan piksel dengan nilai intensitas 500 atau lebih dikategorikan sebagai biru.
- Nilai ambang batas 2500: Nilai ini digunakan untuk membedakan antara piksel berwarna biru dan putih. Piksel dengan nilai intensitas di bawah 2500 dikategorikan sebagai biru, sedangkan piksel dengan nilai intensitas 2500 atau lebih dikategorikan sebagai putih.

#### Kategori Warna:
Berdasarkan nilai ambang batas yang telah disebutkan, terdapat tiga kategori warna yang dapat diidentifikasi pada citra, yaitu:

- Hitam: Piksel dengan nilai intensitas di bawah 500.
Biru: Piksel dengan nilai intensitas antara 500 dan 2500.
- Putih: Piksel dengan nilai intensitas 2500 atau lebih.

#### Alasan Pemilihan Nilai Ambang Batas:

Nilai ambang batas yang dipilih dalam analisis ini didasarkan pada beberapa pertimbangan, yaitu:

- Distribusi Nilai Intensitas: Nilai ambang batas 500 dipilih karena nilai tersebut berada di tengah rentang nilai intensitas untuk piksel berwarna biru. Hal ini membantu memisahkan piksel berwarna biru dari piksel berwarna hitam dengan lebih baik.
- Kualitas Hasil Segmentasi: Nilai ambang batas 2500 dipilih karena nilai tersebut menghasilkan segmentasi yang lebih baik untuk piksel berwarna putih. Hal ini membantu memisahkan piksel berwarna putih dari piksel berwarna biru dengan lebih baik.
- Penyesuaian Visual: Nilai ambang batas juga disesuaikan dengan observasi visual terhadap citra. Hal ini dilakukan untuk memastikan bahwa hasil segmentasi sesuai dengan apa yang terlihat pada citra.

#### Kesimpulan:

Nilai ambang batas 500 dan 2500 yang dipilih dalam analisis ini menghasilkan segmentasi yang baik untuk citra yang diberikan. Nilai ambang batas tersebut didasarkan pada distribusi nilai intensitas, kualitas hasil segmentasi, dan penyesuaian visual terhadap citra.

## Teori Yang Mendukung Projek Terkait
### Peregangan Kontras
Kontras menyatakan sebaran terang (lightness) dan gelap (darkness) di dalam
sebuah gambar. Citra dapat dikelompokkan ke dalam tiga kategori kontras: citra
kontras-rendah (low contrast), citra kontras-bagus (good contrast atau normal
contrast), dan citra kontras-tinggi (high contrast). Ketiga kategori ini umumnya
dibedakan secara intuitif.
Citra kontras-rendah dicirikan dengan sebagian besar komposisi citranya adalah
terang atau sebagian besar gelap. Dari histogramnya terlihat sebagian besar
derajat keabuannya terkelompok (clustered) bersama atau hanya menempati
sebagian kecil dari rentang nilai-nilai keabuan yang mungkin. Jika pengelompokan
nilai-nilai pixel berada di bagian kiri (yang berisi nilai keabuan yang rendah),
citranya cenderung gelap. Jika pengelompokan nilai-nilai pixel berada di bagian
kanan (yang berisi nilai keabuan yang tinggi), citranya cenderung terang. Tetapi,
mungkin saja suatu citra tergolong kontras-rendah meskipun tidak terlalu terang
atau tidak terlalu gelap bila semua pengelompokan nilai keabuan berada di tengah
histogram.
Citra kontras-bagus memperlihatkan jangkauan nilai keabuan yang lebar tanpa
ada suatu nilai keabuan yang mendominasi. Histogram citranya memperlihatkan
sebaran nilai keabuan yang relatif seragam.
Citra kontras-tinggi, seperti halnya citra kontras bagus, memiliki jangkauan nilai
keabuan yang lebar, tetapi terdapat area yang lebar yang didominasi oleh warna
gelap dan area yang lebar yang didominasi oleh warna terang. Gambar dengan
langit terang denganlatar depan yang gelap adalah contoh citra kontras-tinggi.
Pada histogramnya terlihat dua puncak, satu pada area nilai keabuan yang rendah
dan satu lagi pada area nilai keabuan yang tinggi.
Citra dengan kontras-rendah dapat diperbaiki kualitasnya dengan operasi
peregangan kontras. Melalui operasi ini, nilai-nilai keabuan pixel akan merentang
dari 0 sampai 255 (pada citra 8-bit), dengan kata lain seluruh nilai keabuan pixel
terpakai secara merata.

### Deteksi Warna
Deteksi warna adalah salah satu teknik penting dalam pengolahan citra digital yang dapat digunakan dalam berbagai aplikasi seperti pengenalan objek, pemrosesan medis, visi komputer, dan lainnya. Berikut adalah beberapa materi dasar tentang deteksi warna dalam citra digital:

##### Model Warna:

Memahami model warna seperti RGB (Red, Green, Blue), HSV (Hue, Saturation, Value), dan lainnya penting untuk memahami cara citra digital merepresentasikan warna.

##### Segmentasi Warna:
Segmentasi warna adalah proses membagi citra menjadi beberapa bagian berdasarkan warna. Ini sering digunakan dalam deteksi objek berwarna dalam citra.
Deteksi 

##### Tepi Berwarna:
Deteksi tepi berwarna melibatkan menemukan perbatasan antara dua wilayah warna yang berbeda dalam citra.
Ekstraksi 

##### Fitur Berwarna:
Ekstraksi fitur berwarna melibatkan pemilihan fitur-fitur khusus dari citra berdasarkan informasi warna, seperti histogram warna, distribusi warna, dll.
Klasifikasi 

##### Berbasis Warna:
Menggunakan informasi warna untuk mengklasifikasikan objek dalam citra. Ini dapat dilakukan dengan menggunakan metode klasifikasi seperti k-nearest neighbors (k-NN), Support Vector Machines (SVM), dll.
Teknik 

###### Pra-Pemrosesan:
Pra-pemrosesan sering kali diperlukan sebelum deteksi warna, termasuk operasi seperti segmentasi, pengurangan noise, dan peningkatan kontras.

### Nilai Ambang Batas Citra
Nilai ambang batas citra (thresholding) adalah salah satu teknik dasar dalam pengolahan citra digital yang digunakan untuk mengonversi citra ke dalam citra biner. Materi mengenai nilai ambang batas citra mencakup konsep dasar tentang bagaimana teknik ini bekerja, metode pemilihan nilai ambang yang tepat, dan aplikasi praktisnya.

##### Konsep Dasar Thresholding
Thresholding adalah teknik dalam pengolahan citra digital yang digunakan untuk mengonversi citra menjadi citra biner dengan membagi piksel-piksel menjadi dua kelas berdasarkan nilai ambang yang ditentukan. Piksel dengan intensitas di atas nilai ambang akan diberi label satu kelas, sementara yang di bawahnya diberi label kelas lainnya.

##### Metode Pemilihan Nilai Ambang
Nilai ambang dapat dipilih secara manual oleh pengguna, berdasarkan analisis histogram citra, atau menggunakan pendekatan iteratif. Metode Otsu's merupakan salah satu metode populer yang otomatis menentukan nilai ambang berdasarkan kriteria varian dalam dan antara kelas.

##### Algoritma Thresholding
Ada beberapa algoritma thresholding yang umum digunakan, seperti global thresholding, di mana nilai ambang tunggal diterapkan pada seluruh citra, serta adaptive thresholding, di mana nilai ambang disesuaikan berdasarkan cakupan lokal dalam citra.
