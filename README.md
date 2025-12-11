# Aplikasi Peta Rawan Longsor Sederhana
#Deskripsi
Aplikasi ini dirancang untuk menganalisis peta kawasan rawan longsor berdasarkan data Elevasi Digital Model (DEM) dan curah hujan. Aplikasi ini menghitung risiko longsor dengan memadukan dua faktor penting: kemiringan (slope) dan curah hujan. Hasilnya berupa peta risiko yang ditampilkan dalam bentuk heatmap.
# Fitur Utama

1. Upload File DEM (TIFF): Model Elevasi Digital untuk memetakan kondisi topografi area.

2. Upload Data Curah Hujan (CSV atau TIFF): Data curah hujan untuk menggambarkan intensitas curah hujan yang mempengaruhi risiko longsor.

3. Hitung Risiko Longsor: Menghitung risiko longsor berdasarkan kemiringan dan curah hujan, dan menghasilkan peta heatmap.

4. Visualisasi Heatmap: Peta risiko longsor yang dapat dilihat dalam bentuk heatmap.

# Cara Penggunaan

1. Upload File DEM:

Format yang didukung: .tif atau .tiff.

File DEM digunakan untuk menghitung kemiringan atau slope dari wilayah yang dianalisis.

2 Upload Data Curah Hujan:

Format yang didukung: .csv, .tif, atau .tiff.

Jika menggunakan file .csv, aplikasi akan menghitung nilai rata-rata curah hujan dan menggunakannya sebagai data curah hujan untuk seluruh area.

Jika menggunakan file .tif untuk curah hujan, maka data tersebut akan dibaca langsung sebagai data curah hujan spasial.

# Hasil Analisis:

Setelah kedua file diupload, aplikasi akan menghitung risiko longsor berdasarkan kemiringan dan curah hujan yang ada.

Hasilnya akan ditampilkan dalam bentuk heatmap dengan rentang warna yang menggambarkan tingkat risiko.

# Instalasi

Untuk menjalankan aplikasi ini, Anda memerlukan Python 3.10.10 dan beberapa library yang diperlukan. Berikut adalah langkah-langkah instalasinya:

Instalasi dependensi : menggunakan terminal di visual code

pip install streamlit rasterio numpy pandas matplotlib


# Menjalankan aplikasi:
1. Simpan file Python yang berisi kode ini dalam file landslide_risk_app.py dan jalankan aplikasi dengan perintah:

streamlit run landslide_risk_app.py


2. Aplikasi akan terbuka di browser, dan Anda bisa meng-upload file DEM dan Curah Hujan untuk mendapatkan peta risiko longsor.

# Penjelasan Kode

1. Bagian Pembacaan File DEM: Menggunakan rasterio untuk membaca file DEM dalam format .tif. Kemudian, slope dihitung dengan menggunakan perbedaan elevasi antar piksel.

2. Bagian Pembacaan Data Curah Hujan: File CSV atau TIFF dibaca menggunakan pandas untuk CSV dan rasterio untuk file TIFF. Nilai curah hujan dihitung dan normalisasi dilakukan untuk perbandingan.

3. Perhitungan Risiko Longsor: Risiko dihitung dengan menjumlahkan nilai normalisasi slope dan curah hujan, kemudian menghasilkan peta risiko yang dinormalisasi.

4. Visualisasi Heatmap: Menggunakan matplotlib untuk membuat visualisasi heatmap dari peta risiko longsor.

# Struktur Proyek     
## File utama aplikasi
landslide_risk_app.py           
## Dokumentasi
README.md  
## Daftar dependensi
requirements.txt 
# Pengembangan Lanjutan
1. Integrasi lebih banyak data: Menggabungkan lebih banyak faktor risiko seperti penggunaan lahan atau vegetasi.

2. Peningkatan visualisasi: Menambahkan lebih banyak opsi visualisasi seperti peta interaktif.
