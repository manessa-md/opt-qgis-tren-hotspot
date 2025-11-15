<div align="center">

# 📊🗺️ Modul Pelatihan  
## Pembuatan & Analisis Peta **Tren & Hotspot Serangan OPT** dengan QGIS  
*(Data Triwulanan 2018–2025 per Kab/Kota)*

---

**Disusun oleh:**  
🧑‍🏫 **Masita Dwi Mandini Manessa**

**Untuk:**  
🌱 **Direktorat Jenderal Perkebunan**  
**Kementerian Pertanian**

</div>

---

> 💡 **Singkatnya modul ini apa?**  
> Kita akan mengubah **tabel statistik serangan OPT** (2018–2025, per kab/kota, per triwulan) menjadi  
> **peta tren** dan **peta hotspot** di QGIS untuk membantu penentuan wilayah prioritas pengendalian.

---

## 🎯 1. Latar Belakang

Serangan Organisme Pengganggu Tanaman (OPT) berkontribusi langsung terhadap:

- Penurunan produksi dan produktivitas.
- Peningkatan biaya pengendalian.
- Kerugian ekonomi petani dan pelaku usaha.

Data statistik serangan OPT sebenarnya sudah rutin dikumpulkan per kabupaten/kota, tahun, dan periode tanam (misalnya per triwulan). Namun, ketika hanya disajikan dalam bentuk tabel, seringkali:

- Sulit terlihat **pola spasial** → kabupaten/kota mana yang paling terdampak?
- Sulit terbaca **pola temporal** → tren serangan naik, turun, atau stabil?
- Sulit dikaitkan dengan **pengendalian** dan **kerugian ekonomi**.

Melalui modul ini, data tabel tersebut diolah menjadi:

- **Peta tren serangan OPT** (multi-tahun per kab/kota).  
- **Peta hotspot sederhana** untuk mengidentifikasi wilayah prioritas.  

Pendekatan yang digunakan sepenuhnya berbasis **QGIS** dan dirancang agar dapat diikuti dalam **pelatihan 1 hari**.

---

## 🎓 2. Tujuan Pembelajaran

Setelah mengikuti pelatihan dan mempelajari modul ini, peserta diharapkan mampu:

- Menjelaskan **alur kerja** pembuatan peta tren & hotspot serangan OPT di QGIS.
- Memuat peta administrasi kab/kota dan melakukan **join** dengan tabel statistik serangan OPT triwulan 2018–2025.
- Menghitung indikator utama, antara lain:
  - Intensitas serangan relatif terhadap luas komoditas.
  - Proporsi serangan ringan vs berat.
  - Cakupan pengendalian terhadap luas serangan.
  - Kerugian ekonomi per hektar.
- Membuat peta tren serangan OPT:
  - per triwulan,
  - per tahun,
  - dan ringkasan multi-tahun.
- Menyusun **peta hotspot sederhana** antar kab/kota.
- Menyusun layout peta tren & hotspot yang siap digunakan dalam **laporan** atau **bahan presentasi**.

---

## 👥 3. Sasaran Peserta & Prasyarat

### 3.1. Siapa yang cocok ikut?

Modul ini ditujukan terutama untuk:

- Penyuluh pertanian dan staf dinas pertanian/perkebunan.
- Analis data/statistik serangan OPT.
- Peneliti/mahasiswa di bidang perlindungan tanaman, agronomi, atau geografi.
- Operator GIS di instansi pusat/daerah.

### 3.2. Prasyarat minimal

Tidak perlu mahir GIS, cukup:

- Mampu mengoperasikan komputer (folder, file, copy–paste).
- Memahami konsep dasar wilayah administrasi kabupaten/kota.
- Pernah melihat atau membuka QGIS akan membantu, tapi **tidak wajib**.

---

## 🧩 4. Struktur Modul

Modul dibagi menjadi beberapa bagian utama:

---

### 📘 4.1. Pendahuluan & Konsep Dasar

- Latar belakang pemanfaatan SIG untuk analisis serangan OPT.
- Gambaran umum konsep **tren** dan **hotspot** dalam konteks kabupaten/kota.
- Alur kerja dari **data tabel → peta → informasi kebijakan**.

➡️ **Baca:** [Pendahuluan](./01_pendahuluan.html)

---

### 🖥️ 4.2. Perangkat & Data yang Dibutuhkan

- Petunjuk singkat instalasi QGIS.
- Spesifikasi data spasial:
  - Peta administrasi kab/kota (Shapefile/GeoPackage).
- Spesifikasi data statistik serangan OPT:
  - Per kab/kota, per tahun, per triwulan (2018–2025).
- Rekomendasi penyiapan:
  - Dataset *long* (1 baris = kab/kota–tahun–triwulan).
  - Dataset ringkasan untuk analisis tren & hotspot.

➡️ **Baca:** [Perangkat dan Data](./02_data.html)

---

### 🧪 4.3. Praktikum QGIS Langkah demi Langkah

Ini adalah bagian inti modul (hands-on):

- Menyiapkan proyek QGIS & memuat peta kab/kota.
- Mengimpor & merapikan tabel serangan OPT.
- Join tabel OPT ke poligon kab/kota.
- Menghitung indikator turunan (Field Calculator).
- Membuat peta tren:
  - Triwulanan
  - Tahunan
  - Multi-tahun (rata-rata dan tren)
- Menyusun analisis hotspot sederhana antar kab/kota.
- Membuat layout peta tren & hotspot yang siap diekspor (PDF/PNG).

➡️ **Baca:** [Praktikum QGIS](./03_praktikum.html)

---

## 🧭 5. Rekomendasi Alur Belajar

Agar pelatihan dan belajar mandiri lebih efektif, urutan berikut disarankan:

1. **Mulai di halaman ini (Beranda Modul)**  
   Pahami dulu gambaran besar modul dan alur analisis.

2. **Baca Pendahuluan**  
   ➜ [Pendahuluan](./01_pendahuluan.html)  
   Untuk mengerti *mengapa* peta tren & hotspot ini penting.

3. **Siapkan Perangkat & Data**  
   ➜ [Perangkat dan Data](./02_data.html)  
   - Instal QGIS (jika belum).
   - Siapkan folder kerja, peta kab/kota, dan tabel OPT.

4. **Ikuti Praktikum secara berurutan**  
   ➜ [Praktikum QGIS](./03_praktikum.html)  
   Dari Praktikum 1 sampai 7 (setup → join → indikator → tren → hotspot → layout).

5. **Lanjutkan dengan Tugas Mandiri**  
   Di akhir praktikum terdapat tugas asinkron, misalnya:
   - Mengganti indikator hotspot dari luas serangan ke kerugian per hektar.
   - Membuat peta perbandingan dan ringkasan interpretasi.

---

## 🔗 6. Navigasi Cepat

<div align="center">

| Halaman | Link |
|--------|------|
| 📘 Pendahuluan | [Buka Pendahuluan](./01_pendahuluan.html) |
| 🖥️ Perangkat & Data | [Buka Perangkat dan Data](./02_data.html) |
| 🧪 Praktikum QGIS | [Buka Praktikum Langkah demi Langkah](./03_praktikum.html) |

</div>

---

Selamat belajar dan bereksperimen dengan data serangan OPT di QGIS.  
Semoga modul ini membantu memperkuat analisis dan pengambilan keputusan di lapangan. 🌱🗺️📊
