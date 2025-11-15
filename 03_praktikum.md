# 6. Praktikum Langkah demi Langkah

File ini berisi rangkaian praktikum utama dalam pelatihan:

1. Menyiapkan proyek QGIS & peta kab/kota
2. Memuat & menyiapkan data serangan OPT
3. Join data OPT ke peta kab/kota & membuat tabel ringkasan tren
4. Menghitung indikator turunan utama (Field Calculator)
5. Membuat peta tren serangan OPT (triwulanan, tahunan, multi-tahun)
6. Analisis hotspot sederhana serangan OPT antar kab/kota
7. Menyusun layout peta tren & hotspot

---

## Praktikum 1 – Menyiapkan Proyek QGIS & Memuat Peta Administrasi Kab/Kota

**Tujuan:**
Peserta mampu membuka QGIS, membuat proyek baru, dan memuat peta kabupaten/kota.

### Langkah:

1. **Buka aplikasi QGIS 3.x.**

2. **Buat proyek baru**

   * Menu **Project → New**.

3. **Atur CRS proyek (bila diperlukan)**

   * Klik ikon **CRS** di kanan bawah jendela QGIS.
   * Pilih `EPSG:4326 – WGS 84` (atau CRS lain yang disepakati).
   * Klik **OK**.

4. **Tambahkan layer kab/kota**

   * Menu **Layer → Add Layer → Add Vector Layer…**
   * Pada **Source**, pilih file:
     `kabkota.shp` atau `kabkota.gpkg`
   * Klik **Open → Add**.

5. **Periksa atribut peta kab/kota**

   * Klik kanan layer kab/kota → **Open Attribute Table**.
   * Pastikan atribut kunci tersedia, misalnya:

     * `K_ID` / `KODE_KAB`
     * `NAMA_KAB` atau `KAB_KOTA`

6. **Latihan singkat (opsional)**

   * Klik dua kali layer kab/kota → tab **Symbology**:

     * Pilih **Single symbol**.
     * Ganti warna fill agar peta lebih jelas.
   * Aktifkan label:

     * Klik kanan layer → **Properties → Labels**.
     * Pilih **Single labels**.
     * Value: `NAMA_KAB` (atau kolom nama kab/kota lainnya).
     * Klik **Apply → OK**.

---

## Praktikum 2 – Memuat & Menyiapkan Data Serangan OPT

**Tujuan:**
Peserta dapat memuat data serangan OPT (tabular) dan menyiapkan struktur kolom agar mudah digunakan di QGIS.

### 2.1. Mengimpor Data OPT (.csv) ke QGIS

1. Bila data masih `.xlsx`, buka di Excel/LibreOffice dan **simpan sebagai `.csv`**.
2. Pastikan sheet yang digunakan berisi data utama (dbase) dan header kolom ada di baris pertama.
3. Di QGIS, pilih:

   * **Layer → Add Layer → Add Delimited Text Layer…**
4. Pada dialog:

   * **File name**: pilih `opt_triwulan_2018_2025.csv`
   * **File format**: biarkan default (CSV).
   * **Record options**: pastikan **First record has field names** dicentang.
   * **Geometry definition**:

     * Pilih **No geometry (attribute only table)**.
   * Klik **Add** → **Close**.

### 2.2. Merapikan Nama Kolom

> Basis data spasial sangat sensitif terhadap spasi, karakter khusus (`/`, `-`, dll.), dan panjang nama kolom.

Contoh perubahan nama kolom yang disarankan:

* `K.ID` → `K_ID`
* `Kab / Kota` → `KAB_KOTA`
* `Luas Komoditas (Ha)` → `L_KOMOD`
* `Luas Serangan Ringan (Ha)` → `L_RINGAN`
* `Luas Serangan Berat (Ha)` → `L_BERAT`
* `Total Luas Serangan (Ha)` → `L_SERANG`
* `Luas Pengendalian APBN (Ha)` → `L_APBN`
* `Luas Pengendalian APBD I (Ha)` → `L_APBD1`
* `Luas Pengendalian APBD II (Ha)` → `L_APBD2`
* `Luas Pengendalian Swadaya (Ha)` → `L_SWADAYA`
* `Total Luas Pengendalian (Ha)` → `L_PENGEND`
* `Harga Rata-rata Produk` → `HARGA_RATA`
* `Kehilangan Produksi (Kg)` → `K_HILANG`
* `Kerugian Hasil (Rp.000)` → `RUGI_RP`

Cara paling mudah: ubah di Excel sebelum ekspor ke `.csv`.
Alternatif (di QGIS): gunakan **Processing → Refactor Fields** untuk mengganti nama field.

### 2.3. Memeriksa Tabel OPT di QGIS

* Klik kanan layer tabel `opt_triwulan_2018_2025` → **Open Attribute Table**.
* Pastikan kolom-kolom kunci tersedia:

  * `K_ID` / `KAB_KOTA`
  * `Tahun`
  * `Periode_Triwulan`
  * Kolom luas serangan (`L_RINGAN`, `L_BERAT`, `L_SERANG`).
  * Kolom pengendalian (`L_APBN`, `L_APBD1`, `L_APBD2`, `L_SWADAYA`, `L_PENGEND`).
  * Kolom kerugian (`K_HILANG`, `RUGI_RP`).

---

## Praktikum 3 – Join Data OPT ke Peta Kab/Kota & Ringkasan Tren

**Tujuan:**
Peserta mampu:

* Menggabungkan tabel serangan OPT ke layer kab/kota (berdasarkan kolom kunci).
* Membuat tabel ringkasan multi-tahun dan menghitung tren serangan (slope regresi).

---

### 3.1. Join untuk Satu Tahun & Satu Triwulan (Subset)

**Langkah:**

1. **Filter tabel OPT untuk subset tertentu**
   Contoh: Tahun 2022 Triwulan I

   * Klik kanan tabel `opt_triwulan_2018_2025` → **Filter…**

   * Ekspresi:

     ```sql
     "Tahun" = 2022 AND "Periode_Tri" = 'I'
     ```

   * Klik **OK** → hanya baris tahun 2022 Triwulan I yang tampil.

2. **Simpan subset sebagai tabel baru** (opsional tetapi membuat project lebih rapi)

   * Klik kanan tabel → **Export → Save Features As…**
   * Format: `GeoPackage` atau `CSV`
   * Nama file: `opt_2022_Q1`
   * Klik **OK**.

3. **Lakukan join ke layer kab/kota**

   * Klik kanan layer `kabkota` → **Properties… → Joins**.
   * Klik tombol **+ (Add new join)**.
   * Isi:

     * **Join layer**: `opt_2022_Q1`
     * **Join field**: `KAB_KOTA` (di tabel OPT)
     * **Target field**: `KAB_KOTA` atau field nama kab/kota di layer kab/kota
   * Klik **OK → OK**.

4. **Periksa hasil join**

   * Buka **Attribute Table** layer `kabkota`.
   * Kolom-kolom dari `opt_2022_Q1` sekarang menempel di tabel kab/kota.

**Latihan:**
Ulangi untuk subset lain (misalnya 2020 Triwulan III), lalu bandingkan peta `L_SERANG` kedua periode ini.

---

### 3.2. Membuat Tabel Ringkasan Multi-Tahun (2018–2025)

Untuk analisis tren dan hotspot, lebih efisien menggunakan **tabel ringkasan per kab/kota**:

* `mean_L_SERANG` = rata-rata total luas serangan per tahun.
* `mean_RUGI_RP` = rata-rata kerugian (Rp.000) per tahun.
* `trend_serangan` = slope tren serangan per tahun.

#### 3.2.1. Membuat Virtual Layer Ringkasan Tren

1. Menu **Layer → Add Layer → Add/Edit Virtual Layer…**
2. Name: `ringkasan_tren_OPT`
3. **Geometry type**: pilih **No geometry**
4. Pada kotak SQL, paste query berikut (sesuaikan nama tabel sumber, misalnya `dataOPT`):

```sql
WITH per_tahun AS (
    SELECT
        Kab_Kota,
        Tahun,
        SUM(L_SERANG) AS L_SERANG_tahun,
        SUM(RUGI_RP)  AS RUGI_RP_tahun
    FROM dataOPT
    WHERE Tahun BETWEEN 2018 AND 2025
    GROUP BY Kab_Kota, Tahun
),
stat AS (
    SELECT
        Kab_Kota,
        COUNT(*)                    AS n,
        SUM(Tahun)                  AS sumX,
        SUM(L_SERANG_tahun)         AS sumY,
        SUM(Tahun * Tahun)          AS sumX2,
        SUM(Tahun * L_SERANG_tahun) AS sumXY,
        AVG(L_SERANG_tahun)         AS mean_L_SERANG,
        AVG(RUGI_RP_tahun)          AS mean_RUGI_RP
    FROM per_tahun
    GROUP BY Kab_Kota
)
SELECT
    Kab_Kota,
    mean_L_SERANG,
    mean_RUGI_RP,
    CASE
        WHEN (n * sumX2 - sumX * sumX) = 0 THEN NULL
        ELSE
            (1.0 * n * sumXY - sumX * sumY)
            / (1.0 * n * sumX2 - sumX * sumX)
    END AS trend_serangan
FROM stat;
```

5. Klik **Add → Close**.
   Virtual Layer `ringkasan_tren_OPT` sekarang muncul sebagai tabel baru.

#### 3.2.2. Penjelasan Singkat Query

* `per_tahun`
  Mengubah data triwulanan menjadi **total per tahun per kab/kota**:

  * `L_SERANG_tahun`
  * `RUGI_RP_tahun`

* `mean_L_SERANG`
  Rata-rata total luas serangan tahunan (2018–2025).

* `mean_RUGI_RP`
  Rata-rata kerugian (Rp.000) per tahun.

* `trend_serangan`
  Slope regresi linear luas serangan tahunan (`y`) terhadap tahun (`x`) dengan rumus:

  [
  b = \frac{n\sum xy - (\sum x)(\sum y)}{n\sum x^2 - (\sum x)^2}
  ]

  Di mana:

  * ( x ) = tahun (2018, 2019, …, 2025)
  * ( y ) = total luas serangan per tahun

  Satuan **b** = hektar per tahun (**Ha/tahun**):

  * b > 0 → tren serangan **naik**.
  * b < 0 → tren serangan **turun**.

#### 3.2.3. Interpretasi Nilai Tren

1. **Apa yang dihitung?**
   Slope **b** menyatakan berapa besar perubahan luas serangan setiap 1 tahun.

   Contoh: `trend_serangan = -773`
   → Rata-rata luas serangan **berkurang ~773 Ha per tahun**.

2. **Mengapa nilainya tidak antara -1 dan 1?**

   * Range -1 sampai +1 itu untuk **koefisien korelasi (r)**, bukan slope.
   * Slope bebas tergantung skala y (cek satuan hektar, ribuan hektar, dsb.).

3. **Bagaimana menguji “masuk akal”?**

   * Plot grafik sederhana (tahun vs L_SERANG_tahun).
   * Jika grafik menurun → b harus negatif.
   * Jika menanjak → b positif.
   * Besarnya b sebanding dengan selisih total serangan antar tahun.

4. **Opsi nilai “standar” -1 sampai 1 (opsional)**

   * Hitung **koefisien korelasi r** saja, bukan slope.
   * Atau lakukan **rescaling**:

     * `Tahun_rel = Tahun - 2018`
     * `L_SERANG_scaled = L_SERANG / 100` atau transformasi lain.

#### 3.2.4. Join Ringkasan Tren ke Peta Kab/Kota

1. Klik kanan layer `kabkota` → **Properties → Joins**.
2. Tambahkan join baru:

   * **Join layer**: `ringkasan_tren_OPT`
   * **Join field**: `Kab_Kota`
   * **Target field**: `KAB_KOTA` di kabkota
3. Klik **OK → OK**.

Sekarang layer kabkota memiliki field:

* `mean_L_SERANG`
* `mean_RUGI_RP`
* `trend_serangan`

---

### 3.3. Analisis Tren Spesifik Komoditas (Contoh: Vanili)

Untuk menganalisis tren per komoditas tertentu, misalnya **Vanili**:

1. Menu **Layer → Add Layer → Add/Edit Virtual Layer…**
2. Name: `ringkasan_tren_OPT_Vanili`
3. Geometry type: **No geometry**
4. Paste SQL berikut:

```sql
WITH per_tahun AS (
    SELECT
        Kab_Kota,
        Tahun,
        upper(trim("Jenis_Komoditas")) AS Komoditas,
        SUM(L_SERANG) AS L_SERANG_tahun,
        SUM(RUGI_RP)  AS RUGI_RP_tahun
    FROM dataOPT
    WHERE
        Tahun BETWEEN 2018 AND 2025
        AND upper(trim("Jenis_Komoditas")) = 'VANILI'
    GROUP BY
        Kab_Kota,
        Tahun,
        upper(trim("Jenis_Komoditas"))
),
stat AS (
    SELECT
        Kab_Kota,
        Komoditas,
        COUNT(*)                    AS n,
        SUM(Tahun)                  AS sumX,
        SUM(L_SERANG_tahun)         AS sumY,
        SUM(Tahun * Tahun)          AS sumX2,
        SUM(Tahun * L_SERANG_tahun) AS sumXY,
        AVG(L_SERANG_tahun)         AS mean_L_SERANG,
        AVG(RUGI_RP_tahun)          AS mean_RUGI_RP
    FROM per_tahun
    GROUP BY
        Kab_Kota,
        Komoditas
)
SELECT
    Kab_Kota,
    Komoditas,
    mean_L_SERANG,
    mean_RUGI_RP,
    CASE
        WHEN (n * sumX2 - sumX * sumX) = 0 THEN NULL
        ELSE
            (1.0 * n * sumXY - sumX * sumY)
            / (1.0 * n * sumX2 - sumX * sumX)
    END AS trend_serangan
FROM stat;
```

**Penjelasan:**

* `AND upper(trim("Jenis_Komoditas")) = 'VANILI'`
  → hanya mengambil baris komoditas Vanili (tahan terhadap spasi & huruf besar-kecil).

* Output:

  * `Kab_Kota`
  * `Komoditas` (VANILI)
  * `mean_L_SERANG`
  * `mean_RUGI_RP`
  * `trend_serangan` (Ha/tahun)

Layer ini bisa di-join ke kabkota dan dipetakan sebagai peta tren khusus Vanili.

---

## Praktikum 4 – Menghitung Indikator Turunan Utama (Field Calculator)

**Tujuan:**
Peserta mampu membuat beberapa indikator turunan penting untuk analisis tren & hotspot.

> Pastikan layer `kabkota` sudah memiliki kolom-kolom OPT hasil join (L_SERANG, L_RINGAN, L_BERAT, L_PENGEND, RUGI_RP, L_KOMOD, dsb.).

### 4.1. Intensitas Serangan Relatif terhadap Luas Komoditas

Field baru: `SERANG_REL`
Tipe: **Decimal (real)**

Expression:

```sql
CASE
WHEN "L_KOMOD" IS NULL OR "L_KOMOD" = 0 THEN NULL
ELSE "L_SERANG" / "L_KOMOD"
END
```

Makna:
Proporsi luas serangan terhadap luas komoditas (0–1).
Bisa dikalikan 100 untuk persen (`SERANG_REL * 100`).

---

### 4.2. Proporsi Serangan Ringan & Berat

Field baru: `PROP_RINGAN` (Decimal):

```sql
CASE
WHEN "L_SERANG" IS NULL OR "L_SERANG" = 0 THEN NULL
ELSE "L_RINGAN" / "L_SERANG"
END
```

Field baru: `PROP_BERAT` (Decimal):

```sql
CASE
WHEN "L_SERANG" IS NULL OR "L_SERANG" = 0 THEN NULL
ELSE "L_BERAT" / "L_SERANG"
END
```

Interpretasi:

* `PROP_RINGAN` tinggi → mayoritas serangan kategori ringan.
* `PROP_BERAT` tinggi → dominasi serangan berat.

---

### 4.3. Cakupan Pengendalian terhadap Serangan

Field baru: `PENGEND_REL` (Decimal):

```sql
CASE
WHEN "L_SERANG" IS NULL OR "L_SERANG" = 0 THEN NULL
ELSE "L_PENGEND" / "L_SERANG"
END
```

Makna:
Seberapa besar area serangan yang tercakup pengendalian (0–1).

---

### 4.4. Kerugian Ekonomi per Ha Komoditas

Field baru: `RUGI_PERHA` (Decimal):

```sql
CASE
WHEN "L_KOMOD" IS NULL OR "L_KOMOD" = 0 THEN NULL
ELSE "RUGI_RP" / "L_KOMOD"
END
```

**Latihan tambahan:**
Buat indikator:

* `RUGI_PERHA_SERANG` = `RUGI_RP / L_SERANG`

untuk mengukur kerugian per hektar wilayah yang diserang.

---

## Praktikum 5 – Pemetaan Tren Serangan OPT (Triwulanan, Tahunan, Multi-Tahun)

**Tujuan:**
Peserta mampu membuat peta tematik (choropleth) untuk melihat pola spasio-temporal serangan OPT.

---

### 5.1. Peta Triwulanan

1. Pastikan join subset waktu (misalnya `opt_2022_Q1`) sudah dilakukan ke layer kabkota.
2. Klik dua kali layer `kabkota` → tab **Symbology**.
3. Pilih:

   * **Graduated**
   * Column: `L_SERANG` (atau `SERANG_REL`)
   * Mode: **Natural Breaks (Jenks)** atau **Quantile**
   * Classes: **5**
   * Color ramp: gradasi hijau muda → merah tua (rendah → tinggi)
4. Klik **Classify** → **Apply**.

**Latihan:**

* Buat dua peta:

  * Peta `L_SERANG` untuk 2018 Q1
  * Peta `L_SERANG` untuk 2024 Q1
* Bandingkan kab/kota mana yang menunjukkan kenaikan/penurunan serangan.

---

### 5.2. Peta Tahunan

Jika tersedia kolom agregat tahunan, misalnya:

* `L_SERANG_2018`
* `L_SERANG_2020`
* `L_SERANG_2025`

Gunakan simbolisasi **Graduated** yang sama:

* Column: `L_SERANG_2018` → buat peta pertama
* Column: `L_SERANG_2025` → buat peta kedua

Diskusikan perubahan pola spasial antar tahun.

---

### 5.3. Peta Multi-Tahun (Rata-rata & Tren)

Gunakan field dari `ringkasan_tren_OPT`:

* `mean_L_SERANG` → peta tingkat serangan rata-rata.
* `trend_serangan` → peta arah tren.

**Contoh simbolisasi `mean_L_SERANG`:**

* **Graduated**, 5 kelas, warna hijau → merah.

**Contoh simbolisasi `trend_serangan`:**

* **Graduated** dengan **color ramp divergen**:

  * Biru → tren menurun (nilai negatif)
  * Putih → relatif stabil (dekat nol)
  * Merah → tren meningkat (nilai positif)

---

## Praktikum 6 – Hotspot Sederhana Serangan OPT antar Kab/Kota

**Tujuan:**
Peserta mampu:

* Mengidentifikasi kab/kota dengan nilai tertinggi `mean_L_SERANG`.
* Mengelompokkan kab/kota menjadi **hotspot**, **sedang**, dan **coldspot**.
* Membuat peta hotspot sederhana.

> Catatan:
> Di praktikum ini, istilah **hotspot** digunakan secara operasional (berdasarkan nilai tertinggi `mean_L_SERANG`), bukan berdasarkan uji statistik spasial (misalnya Local Moran’s I).

---

### 6.1. Data yang Digunakan

* Layer poligon `kabkota` yang sudah di-join dengan tabel `ringkasan_tren_OPT`.
* Field kunci:

  * `mean_L_SERANG` = rata-rata total luas serangan OPT per tahun (2018–2025).

---

### 6.2. Menentukan Batas Kelas Hotspot (Metode Kuantil)

1. Klik dua kali layer `kabkota` → **Properties → Symbology**.
2. Pilih:

   * **Graduated**
   * Column: `mean_L_SERANG`
   * Mode: **Quantile**
   * Classes: **5**
3. Klik **Classify**.

QGIS akan membagi data menjadi 5 kelas dengan jumlah kab/kota relatif seimbang (±20% per kelas).

* Kelas 1 → nilai terendah
* Kelas 5 → nilai tertinggi

Catat batas kelas, terutama:

* Batas antara kelas 3–4
* Batas antara kelas 4–5

Contoh (sesuaikan dengan hasil nyata):

| Kelas | From – To (mean_L_SERANG) |
| ----- | ------------------------- |
| 1     | 0 – 120                   |
| 2     | 120 – 350                 |
| 3     | 350 – 700                 |
| 4     | 700 – 1500                |
| 5     | 1500 – 4500               |

Dari contoh di atas dapat didefinisikan:

* **Hotspot**  = kelas 4 dan 5 (≥ 700 Ha/tahun)
* **Coldspot** = kelas 1 (≤ 120 Ha/tahun)
* **Sedang**   = kelas 2 dan 3

---

### 6.3. Membuat Field Kategori Hotspot

1. Buka **Attribute Table** layer `kabkota`.
2. Klik ikon **Field Calculator**.
3. Centang **Create a new field**.
4. Nama field: `KAT_HOTSPOT`
5. Output type: **Text (string)**
6. Expression (sesuaikan nilai ambang dengan hasil kuantil Ibu):

```sql
CASE
  WHEN "mean_L_SERANG" >= 700 THEN 'Hotspot'
  WHEN "mean_L_SERANG" <= 120 THEN 'Coldspot'
  ELSE 'Sedang'
END
```

7. Klik **OK**.

Sekarang tiap kab/kota punya kategori:

* `Hotspot`
* `Sedang`
* `Coldspot`

---

### 6.4. Simbolisasi Peta Hotspot Sederhana

1. Buka **Properties → Symbology**.
2. Pilih **Categorized**.
3. Column: `KAT_HOTSPOT`.
4. Klik **Classify**.
5. Atur warna:

   * `Hotspot` → merah tua.
   * `Sedang` → kuning / oranye.
   * `Coldspot` → biru.
6. Klik **Apply → OK**.

Peta sekarang menonjolkan:

* Kab/kota dengan rata-rata serangan tinggi (hotspot).
* Kab/kota dengan rata-rata serangan rendah (coldspot).
* Daerah lainnya (kategori sedang).

---

### 6.5. Interpretasi dan Diskusi

Pertanyaan yang dapat digunakan untuk diskusi kelas:

* Di mana konsentrasi hotspot? Apakah mengelompok pada satu provinsi atau wilayah tertentu?
* Apakah hotspot cenderung memiliki nilai `trend_serangan` **positif** (masih naik) atau **negatif** (mulai turun)?
* Bagaimana jika definisi hotspot diubah (misalnya hanya 10% tertinggi)?

  * Ulangi klasifikasi dengan 10 kelas, lalu pilih kelas 9–10 sebagai hotspot.
* Bagaimana implikasi kebijakan bila hotspot didefinisikan berdasarkan **luas serangan** saja vs **kerugian ekonomi**?

---

## Praktikum 7 – Pembuatan Layout Peta Tren & Hotspot

**Tujuan:**
Peserta dapat menyusun layout peta yang rapi dan siap dimasukkan ke laporan atau presentasi.

---

### 7.1. Layout Peta Tren

1. Menu **Project → New Print Layout…**
2. Beri nama layout: `Peta_Tren_OPT`.
3. Di jendela layout:

   * Klik ikon **Add Map**, tarik kotak di kanvas.
   * Pastikan layer yang akan ditampilkan (misal peta `mean_L_SERANG`) sudah aktif di jendela utama QGIS.
4. Tambahkan elemen:

   * **Add Label** (judul peta):

     * Contoh:
       *“Peta Rata-rata Total Luas Serangan OPT per Kab/Kota, 2018–2025”*
   * **Add Legend**:

     * Sesuaikan judul legenda, hapus field yang tidak perlu.
   * **Add Scale Bar**:

     * Pilih satuan (kilometer).
   * **Add North Arrow**:

     * Pilih style yang sederhana.
   * Tambahkan teks sumber data:

     * Contoh:
       *“Sumber data: Statistik Serangan OPT 2018–2025, diolah.”*

---

### 7.2. Layout Peta Hotspot

1. Buat layout baru atau duplikasi layout sebelumnya.

2. Judul contoh:

   *“Peta Hotspot Serangan OPT berdasarkan Rata-rata Luas Serangan (2018–2025)”*

3. Tampilkan peta dengan simbolisasi `KAT_HOTSPOT`.

Pastikan legenda menjelaskan dengan jelas:

* Merah tua = kab/kota **Hotspot**.
* Kuning/Oranye = kab/kota **Sedang**.
* Biru = kab/kota **Coldspot**.

---

### 7.3. Ekspor Layout

1. Di jendela layout:

   * Menu **Layout → Export as PDF** atau **Export as Image**.
2. Beri nama file yang jelas, misalnya:

   * `Peta_Tren_OPT_2018_2025.pdf`
   * `Peta_Hotspot_OPT_2018_2025.pdf`
3. Simpan di folder:

   * `project\output_peta\` atau struktur lain yang disepakati.

---

# 7. Penutup dan Tugas Lanjutan

## 7.1. Ringkasan Praktikum

Melalui rangkaian praktikum ini, peserta telah:

* Menggabungkan data statistik serangan OPT triwulanan (2018–2025) dengan peta kabupaten/kota di QGIS.
* Menghitung indikator turunan utama: intensitas serangan, proporsi ringan/berat, cakupan pengendalian, dan kerugian per hektar.
* Membuat peta tren serangan OPT pada berbagai skala waktu (triwulanan, tahunan, multi-tahun).
* Melakukan analisis hotspot sederhana untuk mengidentifikasi kab/kota prioritas pengendalian.
* Menyusun layout peta tren & hotspot yang siap digunakan dalam laporan.

---

## 7.2. Tugas Mandiri (Asinkron)

Sebagai latihan mandiri, peserta dapat mencoba:

1. **Mengganti variabel hotspot**

   * Ulangi analisis hotspot dengan mengganti variabel utama dari `mean_L_SERANG` menjadi `RUGI_PERHA`.

2. **Membuat peta perbandingan**

   * Peta hotspot berdasarkan **luas serangan** (`mean_L_SERANG`).
   * Peta hotspot berdasarkan **kerugian ekonomi** (`RUGI_PERHA`).

3. **Menulis ringkasan singkat (1–2 halaman)**

   * Wilayah mana yang menjadi prioritas jika fokus utamanya **luas serangan**?
   * Apakah daftar prioritas tersebut sama ketika fokusnya adalah **kerugian ekonomi**?
   * Apa implikasi praktisnya bagi perencanaan pengendalian OPT di lapangan?

Dengan tugas ini, peserta diharapkan dapat menghubungkan analisis spasial dengan prioritas kebijakan dan pengambilan keputusan di sektor perkebunan.


---

**Navigasi**

- ⬅️ [Perangkat dan Data](./02_data.html)
- ⬅️ [Beranda Modul](./index.html)
