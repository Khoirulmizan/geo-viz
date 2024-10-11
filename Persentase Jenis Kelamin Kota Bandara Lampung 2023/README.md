# Visualisasi Persentase Jenis Kelamin di Bandar Lampung

![Visualisasi Persentase Jenis Kelamin di Bandar Lampung](https://femboy.beauty/2_ySD.png)

Proyek ini memvisualisasikan distribusi jenis kelamin (laki-laki dan perempuan) di setiap kecamatan di Kota Bandar Lampung menggunakan data sensus terbaru dan peta geospasial. Visualisasi ini mendukung analisis sosial, ekonomi, serta perencanaan kebijakan publik yang lebih akurat.

## Daftar Isi

1. [Latar Belakang](#latar-belakang)
2. [Data yang Digunakan](#data-yang-digunakan)
3. [Metodologi](#metodologi)
4. [Hasil Visualisasi](#hasil-visualisasi)
5. [Cara Menjalankan](#cara-menjalankan)
6. [Dependensi](#dependensi)
7. [Lisensi](#lisensi)

## Latar Belakang

Distribusi jenis kelamin adalah indikator penting dalam analisis demografi dan kebijakan sosial. Dengan mengetahui persentase penduduk laki-laki dan perempuan di setiap kecamatan, pengambil kebijakan dapat memahami kondisi masyarakat dengan lebih baik dan merencanakan kebijakan yang sesuai.

Proyek ini memanfaatkan data sensus dari Kota Bandar Lampung dan divisualisasikan dalam bentuk **peta koroplet ganda** menggunakan **Python** dan **Geopandas**. Peta ini menampilkan persentase penduduk laki-laki dan perempuan di setiap kecamatan.

## Data yang Digunakan

- **Data Sensus**: Jumlah penduduk laki-laki dan perempuan di setiap kecamatan di Kota Bandar Lampung.
  - Sumber: [sensus jenis kelamin_bandar lampung.csv]()
  - Kolom: 
    - `KECAMATAN`: Nama kecamatan.
    - `LAKI-LAKI`: Jumlah penduduk laki-laki.
    - `PEREMPUAN`: Jumlah penduduk perempuan.

- **Shapefile Kecamatan**: Batas wilayah kecamatan di Kota Bandar Lampung.
  - Sumber: [ADMINISTRASIKECAMATAN_AR_50K.shp]()

## Metodologi

1. **Menghitung Persentase**:
   Persentase penduduk laki-laki dan perempuan dihitung dari total populasi:
   ```python
   data_jk['Persentase Laki-Laki'] = data_jk['LAKI-LAKI'] / (data_jk['LAKI-LAKI'] + data_jk['PEREMPUAN']) * 100
   data_jk['Persentase Perempuan'] = data_jk['PEREMPUAN'] / (data_jk['LAKI-LAKI'] + data_jk['PEREMPUAN']) * 100
   ```

2. **Pembersihan Data**:
   Nama kecamatan di data sensus dan shapefile distandarisasi:
   ```python
   data_jk['KECAMATAN'] = data_jk['KECAMATAN'].str.strip().str.upper()
   shape['NAMOBJ'] = shape['NAMOBJ'].str.strip().str.upper()
   ```

3. **Menggabungkan Data**:
   Data sensus digabung dengan shapefile untuk visualisasi peta:
   ```python
   shape_merged = pd.merge(left=shape, right=data_jk, left_on='NAMOBJ', right_on='KECAMATAN', how='outer')
   ```

4. **Visualisasi Peta Koroplet Ganda**:
   Peta koroplet ganda dibuat untuk menampilkan persentase laki-laki dan perempuan dengan dua palet warna (`Blues` dan `Reds`):
   ```python
   aes_choropleth(ax1, shape_merged, 'Persentase Laki-Laki', 'Persentase Laki-Laki', plt.cm.Blues, vmin, vmax)
   aes_choropleth(ax2, shape_merged, 'Persentase Perempuan', 'Persentase Perempuan', plt.cm.Reds, vmin, vmax)
   ```

## Hasil Visualisasi

Visualisasi ini menunjukkan distribusi persentase laki-laki dan perempuan di Bandar Lampung dalam dua peta dengan gradasi warna. Peta pertama menunjukkan persentase laki-laki (warna biru), dan peta kedua menunjukkan persentase perempuan (warna merah). Label kecamatan juga ditambahkan sesuai dengan ukuran wilayah kecamatan tersebut.

## Cara Menjalankan

1. **Clone repositori**:
   ```bash
   git clone https://github.com/username/geo-viz.git
   ```

2. **Pindah ke direktori proyek**:
   ```bash
   cd geo-viz
   ```

3. **Install dependensi yang dibutuhkan**:
   ```bash
   pip install numpy pandas matplotlib geopandas seaborn
   ```

4. **Jalankan skrip visualisasi**:
   ```bash
   python visualisasi.py
   ```

## Dependensi

- [NumPy](https://numpy.org/)
- [Pandas](https://pandas.pydata.org/)
- [Matplotlib](https://matplotlib.org/)
- [GeoPandas](https://geopandas.org/)
- [Seaborn](https://seaborn.pydata.org/)

## Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).