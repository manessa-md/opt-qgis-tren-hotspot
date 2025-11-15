<style>
  body {
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    background: #f5f7fb;
    margin: 0;
  }

  main {
    max-width: 960px;
    margin: 0 auto;
    padding: 2.5rem 1.2rem 3rem 1.2rem;
    background: #ffffff;
    box-shadow: 0 8px 20px rgba(15, 23, 42, 0.08);
    border-radius: 14px;
    margin-top: 2rem;
    margin-bottom: 2rem;
  }

  h1, h2, h3, h4 {
    font-weight: 650;
    color: #111827;
  }

  p, li {
    color: #374151;
    line-height: 1.6;
  }

  .hero {
    text-align: center;
    margin-bottom: 2rem;
  }

  .hero h1 {
    font-size: 2.1rem;
    margin-bottom: 0.4rem;
  }

  .hero h2 {
    font-size: 1.2rem;
    font-weight: 500;
    color: #4b5563;
    margin-top: 0;
  }

  .hero-sub {
    font-size: 0.95rem;
    color: #4b5563;
    margin-top: 0.3rem;
  }

  .hero-tags {
    margin-top: 0.75rem;
    display: inline-flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    justify-content: center;
  }

  .hero-tag {
    background: #e5f0ff;
    color: #1f2937;
    padding: 0.25rem 0.7rem;
    border-radius: 999px;
    font-size: 0.8rem;
  }

  .callout {
    border-left: 4px solid #2563eb;
    background: #eff5ff;
    padding: 0.85rem 1rem;
    border-radius: 0 10px 10px 0;
    margin: 1.2rem 0;
    font-size: 0.95rem;
  }

  .callout strong {
    color: #1d4ed8;
  }

  .nav-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
    gap: 0.8rem;
    margin: 1rem 0 1.8rem 0;
  }

  .nav-card {
    border-radius: 12px;
    padding: 0.9rem 1rem;
    background: #f9fafb;
    border: 1px solid #e5e7eb;
  }

  .nav-card h3 {
    margin: 0 0 0.25rem 0;
    font-size: 1rem;
  }

  .nav-card p {
    margin: 0 0 0.35rem 0;
    font-size: 0.9rem;
  }

  .nav-card a {
    font-size: 0.9rem;
    font-weight: 600;
    text-decoration: none;
    color: #2563eb;
  }

  .nav-card a:hover {
    text-decoration: underline;
  }

  table {
    border-collapse: collapse;
    width: 100%;
  }

  table th, table td {
    border: 1px solid #e5e7eb;
    padding: 0.55rem 0.6rem;
    text-align: left;
  }

  table th {
    background: #f3f4f6;
  }

  .btn-link {
    display: inline-block;
    padding: 0.45rem 0.85rem;
    border-radius: 999px;
    background: #2563eb;
    color: #ffffff !important;
    font-size: 0.9rem;
    text-decoration: none;
    margin-top: 0.3rem;
  }

  .btn-link:hover {
    background: #1d4ed8;
    text-decoration: none;
  }
</style>

<main>

<div align="center" markdown="1">

# 📚 Modul Pelatihan  
## Pembuatan & Analisis Peta **Tren & Hotspot Serangan OPT** dengan QGIS  
*(Data Triwulanan 2018–2025 per Kab/Kota)*  

**Disusun oleh:**  
👩‍🏫 **Masita Dwi Mandini Manessa**  

**Untuk:**  
🌱 **Direktorat Jenderal Perkebunan**  
**Kementerian Pertanian**

</div>


<div class="hero-tags">
  <span class="hero-tag">QGIS</span>
  <span class="hero-tag">Analisis Spasial</span>
  <span class="hero-tag">Tren Serangan OPT</span>
  <span class="hero-tag">Hotspot Kab/Kota</span>
</div>

</div>

<div class="callout">
  <strong>Singkatnya modul ini apa?</strong><br>
  Kita akan mengubah <em>tabel statistik serangan OPT</em> (2018–2025, per kab/kota, per triwulan)
  menjadi <strong>peta tren</strong> dan <strong>peta hotspot</strong> di QGIS untuk membantu
  penentuan wilayah prioritas pengendalian.
</div>

## 🎯 1. Latar Belakang

Serangan Organisme Pengganggu Tanaman (OPT) berkontribusi langsung terhadap:

- Penurunan produksi dan produktivitas.
- Peningkatan biaya pengendalian.
- Kerugian ekonomi petani dan pelaku usaha.

Data statistik serangan OPT sudah dikumpulkan rutin per kabupaten/kota, tahun, dan periode tanam (misalnya per triwulan). Namun ketika hanya disajikan dalam bentuk tabel, seringkali:

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

### 3.1. Sasaran Peserta

Modul ini ditujukan terutama untuk:

- Penyuluh pertanian dan staf dinas pertanian/perkebunan.
- Analis data/statistik serangan OPT.
- Peneliti/mahasiswa di bidang perlindungan tanaman, agronomi, atau geografi.
- Operator GIS di instansi pusat/daerah.

### 3.2. Prasyarat Minimal

Tidak perlu mahir GIS, cukup:

- Mampu mengoperasikan komputer (folder, file, copy–paste).
- Memahami konsep dasar wilayah administrasi kabupaten/kota.
- Pernah melihat atau membuka QGIS akan membantu, tetapi **tidak wajib**.

---

## 🧩 4. Struktur Modul

Modul dibagi menjadi beberapa bagian utama:

<div class="nav-grid">

  <div class="nav-card">
    <h3>📘 Pendahuluan & Konsep Dasar</h3>
    <p>Latar belakang, alur pikir, dan peran peta tren & hotspot dalam analisis serangan OPT.</p>
    <a href="./01_pendahuluan.html">Buka Pendahuluan →</a>
  </div>

  <div class="nav-card">
    <h3>🖥️ Perangkat & Data</h3>
    <p>Instalasi QGIS, struktur data spasial kab/kota, dan data statistik serangan OPT 2018–2025.</p>
    <a href="./02_data.html">Buka Perangkat & Data →</a>
  </div>

  <div class="nav-card">
    <h3>🧪 Praktikum QGIS</h3>
    <p>Langkah demi langkah: join data, indikator turunan, peta tren, hotspot, dan layout peta.</p>
    <a href="./03_praktikum.html">Buka Praktikum →</a>
  </div>

</div>

---

## 🧭 5. Rekomendasi Alur Belajar

Agar pelatihan dan belajar mandiri lebih efektif, urutan berikut disarankan:

1. **Mulai dari halaman ini (Beranda Modul)**  
   Pahami gambaran besar modul dan alur analisis yang akan dilakukan.

2. **Baca Pendahuluan**  
   ➜ [Pendahuluan](./01_pendahuluan.html)  
   Untuk memahami *mengapa* peta tren & hotspot penting dalam konteks serangan OPT.

3. **Siapkan Perangkat & Data**  
   ➜ [Perangkat & Data](./02_data.html)  
   - Instal QGIS (jika belum terpasang).  
   - Siapkan folder kerja, peta kab/kota, dan tabel OPT.

4. **Ikuti Praktikum secara berurutan**  
   ➜ [Praktikum QGIS](./03_praktikum.html)  
   Ikuti dari Praktikum 1 sampai 7: setup proyek → join data → indikator → tren → hotspot → layout.

5. **Lanjutkan dengan Tugas Mandiri**  
   Di akhir praktikum tersedia saran tugas asinkron, misalnya:
   - Mengganti indikator hotspot dari luas serangan ke kerugian per hektar.
   - Membuat peta perbandingan dan ringkasan interpretasi.

---

## 🔗 6. Navigasi Cepat

| Halaman | Link |
|--------|------|
| 📘 Pendahuluan | [Buka Pendahuluan](./01_pendahuluan.html) |
| 🖥️ Perangkat & Data | [Buka Perangkat dan Data](./02_data.html) |
| 🧪 Praktikum QGIS | [Buka Praktikum Langkah demi Langkah](./03_praktikum.html) |

</main>
