# Visualisasi Persentase Jenis Kelamin di Bandar Lampung

![Visualisasi Persentase Jenis Kelamin di Bandar Lampung](https://femboy.beauty/2_ySD.png)

Proyek ini bertujuan untuk memvisualisasikan distribusi jenis kelamin (laki-laki dan perempuan) di setiap kecamatan di Kota Bandar Lampung menggunakan data sensus terbaru dan peta geospasial. Visualisasi ini dapat membantu dalam analisis sosial, ekonomi, serta perencanaan kebijakan publik yang lebih akurat.

## Daftar Isi

1. [Latar Belakang](#latar-belakang)
2. [Data yang Digunakan](#data-yang-digunakan)
3. [Metodologi](#metodologi)
4. [Hasil Visualisasi](#hasil-visualisasi)
5. [Cara Menjalankan](#cara-menjalankan)
6. [Dependensi](#dependensi)
7. [Lisensi](#lisensi)

## Latar Belakang

Distribusi jenis kelamin merupakan salah satu indikator penting dalam analisis demografi dan kebijakan sosial. Dengan mengetahui persentase penduduk laki-laki dan perempuan di setiap kecamatan, para pengambil kebijakan dapat memahami kondisi masyarakat lebih baik dan mengambil keputusan yang tepat.

Proyek ini memanfaatkan **data sensus** dari Kota Bandar Lampung dan divisualisasikan dalam bentuk peta koroplet menggunakan **Python** dan **Geopandas**. Peta ini memberikan gambaran distribusi jenis kelamin di seluruh kecamatan, yang divisualisasikan berdasarkan persentase penduduk laki-laki.

## Data yang Digunakan

- **Data Sensus**: Jumlah penduduk laki-laki dan perempuan di setiap kecamatan di Kota Bandar Lampung.
  - Sumber: [sensus jenis kelamin_bandar lampung.csv](path-to-csv)
  - Kolom: 
    - `KECAMATAN`: Nama kecamatan.
    - `LAKI-LAKI`: Jumlah penduduk laki-laki.
    - `PEREMPUAN`: Jumlah penduduk perempuan.

- **Shapefile Kecamatan**: Batas wilayah kecamatan di Kota Bandar Lampung.
  - Sumber: [ADMINISTRASIKECAMATAN_AR_50K.shp](path-to-shapefile)

## Metodologi

1. **Menghitung Persentase**:
   Persentase penduduk laki-laki dan perempuan dihitung berdasarkan total populasi di setiap kecamatan:
   ```python
   data_jk['Persentase Laki-Laki'] = data_jk['LAKI-LAKI'] / (data_jk['LAKI-LAKI'] + data_jk['PEREMPUAN']) * 100
   data_jk['Persentase Perempuan'] = data_jk['PEREMPUAN'] / (data_jk['LAKI-LAKI'] + data_jk['PEREMPUAN']) * 100
   ```

2. **Pembersihan Data**:
   Nama kecamatan dari data sensus dan shapefile distandarisasi untuk menghindari inkonsistensi:
   ```python
   data_jk['KECAMATAN'] = data_jk['KECAMATAN'].str.strip().str.upper()
   shape['NAMOBJ'] = shape['NAMOBJ'].str.strip().str.upper()
   ```

3. **Menggabungkan Data**:
   Data sensus di-merge dengan shapefile berdasarkan nama kecamatan, memastikan semua kecamatan terwakili:
   ```python
   shape_merged = pd.merge(left=shape, right=data_jk, left_on='NAMOBJ', right_on='KECAMATAN', how='outer')
   ```

4. **Visualisasi Peta Koroplet**:
   Visualisasi ini menggunakan warna hijau dengan palet warna `summer_r`. Semakin gelap warna hijau, semakin tinggi persentase penduduk laki-laki di kecamatan tersebut:
   ```python
   shape_merged.plot(ax=ax, column='Persentase Laki-Laki', legend=True, cmap='summer_r', 
                     legend_kwds={'shrink': 0.3, 'orientation': 'horizontal', 'format': '%.1f%%'})
   ```

## Hasil Visualisasi

Visualisasi ini menggambarkan distribusi jenis kelamin di Kota Bandar Lampung dengan warna gradasi. Semakin gelap warna hijau pada peta, semakin tinggi persentase laki-laki di kecamatan tersebut. Visualisasi ini dapat digunakan untuk memahami distribusi gender di tingkat kecamatan.

## Cara Menjalankan

1. **Clone repositori**:
   ```bash
   git clone https://github.com/username/repo-name.git
   ```
   
2. **Pindah ke direktori proyek**:
   ```bash
   cd repo-name
   ```

3. **Install dependensi yang dibutuhkan**:
   ```bash
   pip install numpy pandas matplotlib geopandas
   ```

4. **Jalankan skrip visualisasi**:
   Jalankan skrip Python berikut untuk menghasilkan visualisasi:
   ```bash
   python visualisasi.py
   ```

## Dependensi

- [NumPy](https://numpy.org/)
- [Pandas](https://pandas.pydata.org/)
- [Matplotlib](https://matplotlib.org/)
- [GeoPandas](https://geopandas.org/)
- [Seaborn](https://seaborn.pydata.org)

Pastikan untuk menginstal semua dependensi sebelum menjalankan skrip.

## Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).

