---

# Modul Pelatihan

## Pembuatan dan Analisis Peta Tren & Hotspot Serangan OPT dengan QGIS

*(Data Triwulanan 2018–2025 per Kab/Kota)*

Disusun oleh: **Masita Dwi Mandini Manessa**
Untuk: **Direktorat Jenderal Perkebunan, Kementerian Pertanian**

---

## 1. Deskripsi Singkat

Serangan Organisme Pengganggu Tanaman (OPT) berkontribusi langsung terhadap penurunan produksi dan kerugian ekonomi petani. Data statistik serangan OPT sebenarnya sudah rutin dikumpulkan per kabupaten/kota, per tahun, dan per periode tanam (misalnya triwulan), tetapi seringkali masih disajikan dalam bentuk tabel sehingga sulit untuk:

* Melihat pola spasial (kabupaten/kota mana yang paling terdampak).
* Melacak tren temporal (apakah serangan cenderung naik, turun, atau stabil).
* Mengaitkan serangan dengan upaya pengendalian dan kerugian produksi.

Modul ini memperkenalkan pemanfaatan **QGIS** untuk mengubah data statistik serangan OPT triwulanan **2018–2025** menjadi:

* **Peta tren serangan** (multi-tahun per kab/kota).
* **Peta hotspot sederhana** untuk mengidentifikasi wilayah prioritas pengendalian.

Modul dirancang untuk pelatihan 1 hari dengan pendekatan **praktikum langkah demi langkah**, sehingga peserta dengan kemampuan QGIS dasar sekalipun tetap dapat mengikuti.

---

## 2. Tujuan Pembelajaran

Setelah mengikuti pelatihan dan mempelajari modul ini, peserta diharapkan mampu:

* Menjelaskan alur kerja pembuatan peta tren & hotspot serangan OPT menggunakan QGIS.
* Memuat peta administrasi kab/kota dan menggabungkannya dengan data statistik serangan OPT triwulan 2018–2025.
* Menghitung indikator utama, seperti:

  * Intensitas serangan relatif terhadap luas komoditas.
  * Proporsi serangan ringan vs berat.
  * Cakupan pengendalian terhadap luas serangan.
  * Kerugian ekonomi per hektar.
* Membuat peta tren serangan OPT (triwulanan, tahunan, dan ringkasan multi-tahun).
* Melakukan analisis hotspot sederhana antar kabupaten/kota.
* Menyusun layout peta tren & hotspot yang siap digunakan dalam laporan.

---

## 3. Sasaran Peserta

Modul ini ditujukan terutama untuk:

* Penyuluh pertanian dan staf dinas pertanian/perkebunan.
* Analis data/statistik serangan OPT.
* Peneliti/mahasiswa di bidang perlindungan tanaman, agronomi, atau geografi.
* Operator GIS di instansi pusat/daerah yang mengelola data statistik serangan OPT.

**Prasyarat minimal:**

* Mampu mengoperasikan komputer dasar (pengelolaan folder dan file).
* Memahami konsep wilayah administrasi kabupaten/kota.
* Tidak diwajibkan mahir QGIS, tetapi idealnya sudah pernah melihat/membuka QGIS.

---

## 4. Struktur Modul

Modul ini dibagi ke dalam beberapa halaman utama:

1. **Pendahuluan & Konsep Dasar**
   Penjelasan latar belakang, alur pikir, dan gambaran umum analisis tren & hotspot serangan OPT.
   → [Baca: Pendahuluan](./01_pendahuluan.html)

2. **Perangkat & Data yang Dibutuhkan**
   Berisi petunjuk instalasi QGIS, struktur data spasial (peta kab/kota), dan data statistik serangan OPT triwulanan 2018–2025, termasuk rekomendasi penyiapan dataset *long* dan ringkasan.
   → [Baca: Perangkat dan Data](./02_data.html)

3. **Praktikum QGIS Langkah demi Langkah**
   Bagian utama modul yang berisi tutorial praktis:

   * Menyiapkan proyek QGIS dan memuat peta administrasi.
   * Mengimpor dan merapikan data OPT.
   * Join tabel OPT ke kab/kota.
   * Menghitung indikator turunan (Field Calculator).
   * Membuat peta tren (triwulanan, tahunan, multi-tahun).
   * Menyusun analisis hotspot sederhana.
   * Membuat layout peta tren & hotspot untuk laporan.
     → [Baca: Praktikum QGIS](./03_praktikum.html)

---

## 5. Cara Menggunakan Modul Ini

Disarankan alur belajar sebagai berikut:

1. **Mulai dari Pendahuluan**
   Baca bagian [Pendahuluan](./01_pendahuluan.html) untuk memahami konteks dan tujuan analisis.

2. **Siapkan Perangkat & Data**
   Ikuti petunjuk di [Perangkat dan Data](./02_data.html) untuk:

   * Menginstal QGIS (jika belum terpasang).
   * Menyiapkan peta kab/kota dan tabel statistik serangan OPT.

3. **Ikuti Praktikum Secara Berurutan**
   Buka [Praktikum QGIS](./03_praktikum.html) dan ikuti langkah demi langkah:

   * Praktikum 1 → 7, dari setup proyek hingga layout peta.

4. **Lanjutkan dengan Tugas Mandiri**
   Di akhir praktikum terdapat saran tugas asinkron, misalnya:

   * Mengganti indikator hotspot dari luas serangan ke kerugian ekonomi per hektar.
   * Menulis ringkasan interpretasi peta untuk bahan laporan.

---

## 6. Navigasi Cepat

* 👉 [Pendahuluan](./01_pendahuluan.html)
* 👉 [Perangkat dan Data](./02_data.html)
* 👉 [Praktikum QGIS Langkah demi Langkah](./03_praktikum.html)

---
