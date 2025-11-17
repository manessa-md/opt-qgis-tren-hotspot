# 4. Perangkat dan Data

## 4.1. Instalasi QGIS

Subbab ini menjelaskan langkah-langkah singkat untuk menginstal QGIS. Peserta disarankan sudah menginstal QGIS sebelum hari pelatihan, namun instruktur dapat tetap memandu instalasi di awal sesi jika diperlukan.

### 4.1.1. Persyaratan Sistem

QGIS dapat dijalankan di:

- Windows 10 atau lebih baru (64-bit)
- macOS (Intel atau Apple Silicon)
- Linux (Ubuntu, Debian, dsb.)

Spesifikasi minimal:

- RAM ≥ 4 GB (disarankan 8 GB)
- Ruang kosong disk ≥ 2–3 GB
- Resolusi layar minimal 1366×768

### 4.1.2. Mengunduh QGIS

1. Buka browser.
2. Kunjungi situs resmi QGIS.
3. Pilih installer sesuai sistem operasi (Windows/macOS/Linux).

### 4.1.3. Instalasi QGIS di Windows

Ringkas:

1. Jalankan file installer (`QGIS-OSGeo4W-3.x.x-setup-x86_64.exe`).
2. Ikuti wizard: Next → I Agree → Typical → Install → Finish.
3. Buka QGIS dari **Start Menu → QGIS 3.x Desktop**.

### 4.1.4. Instalasi di macOS & Linux (Ringkas)

- **macOS**: buka file `.dmg`, seret ikon QGIS ke **Applications**, jalankan dari Launchpad.
- **Linux**: tambah repository QGIS (sesuai distro), lalu instal via `sudo apt install qgis` (contoh Ubuntu).

### 4.1.5. Mengecek QGIS Setelah Instalasi

- Buka QGIS 3.x.
- Pastikan panel **Layers**, **Browser**, dan menu utama tampil normal.
- Coba **Project → New** dan **Project → Save** untuk uji hak akses folder.

### 4.1.6. Pengaturan Awal yang Disarankan

- Aktifkan panel **Layers**, **Browser**, **Processing Toolbox**.
- Atur CRS ke `EPSG:4326 – WGS 84` bila diperlukan.
- Buat struktur folder latihan, misalnya:

  ```text
  D:\Pelatihan_QGIS_OPT\
      data_spasial\
      data_tabel\
      project\
  ```

  
## 4.2. Data Spasial

### 4.2.1. Peta Administrasi Kab/Kota

- **Format**: Shapefile (`.shp`) atau GeoPackage (`.gpkg`).
- **Atribut minimal**:
  - `K_ID` / `KODE_KAB`
  - `NAMA_KAB`
- **CRS**: `WGS 84 (EPSG:4326)` atau sistem lain yang konsisten.

---

## 4.3. Data Statistik Serangan OPT

**Struktur kolom contoh:**

- `K_ID`
- `KAB_KOTA`
- `Tahun`
- `Periode_Triwulan`
- Kolom-kolom luas serangan, pengendalian, kehilangan produksi, kerugian, dan variabel terkait lainnya.

**Format file**: `.csv` atau `.xlsx`  
**Periode**: 2018–2025, per triwulan (1–4).

**Disarankan menyiapkan:**

- **Dataset long**:  
  1 baris = 1 kombinasi *kab/kota – tahun – triwulan*.
- **Dataset ringkasan per kab/kota** berisi, misalnya:
  - rata-rata serangan per tahun,
  - rata-rata kerugian per tahun,
  - indikator tren (`trend_serangan`).

---

## 5. Alur Kegiatan Pelatihan (1 Hari)

Secara garis besar, alur pelatihan:

1. Menyiapkan proyek QGIS dan memuat data kab/kota.
2. Memuat dan memeriksa data serangan OPT.
3. Melakukan join data kab/kota dengan data OPT.
4. Membuat peta tren (triwulanan, tahunan, dan multi-tahun).
5. Melakukan analisis hotspot antar kab/kota.
6. Menyusun layout peta tren & hotspot.

   ---



## 🔗 Navigasi Cepat

| Halaman             | Link                                                      |
|---------------------|-----------------------------------------------------------|
| 🏠 Beranda Modul      | [Beranda Modul](./index.html)             |
| 📘 Pendahuluan | [Pendahuluan](./01_pendahuluan.html)                |
| 🧪 Praktikum QGIS   | [Buka Praktikum Langkah demi Langkah](./03_praktikum.html) |

---



