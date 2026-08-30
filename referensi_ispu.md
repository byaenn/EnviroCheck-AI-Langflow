# Dokumen Referensi Perhitungan dan Klasifikasi ISPU
(Indeks Standar Pencemar Udara)

## 1. Kategori dan Rentang ISPU

| Kategori | Rentang | Penjelasan |
|---|---|---|
| Baik | 0 - 50 | Tidak memberikan efek bagi kesehatan manusia/hewan, tidak berpengaruh pada tumbuhan, bangunan, maupun nilai estetika |
| Sedang | 51 - 100 | Tidak berpengaruh pada kesehatan manusia/hewan, tetapi berpengaruh pada tumbuhan sensitif dan nilai estetika |
| Tidak Sehat | 101 - 199 | Merugikan manusia maupun kelompok hewan sensitif, atau menimbulkan kerusakan pada tumbuhan dan nilai estetika |
| Sangat Tidak Sehat | 200 - 299 | Dapat merugikan kesehatan pada sejumlah segmen populasi yang terpapar |
| Berbahaya | ≥ 300 | Berbahaya secara umum bagi kesehatan populasi |

## 2. Pengaruh ISPU per Parameter Pencemar

| Kategori | Rentang | CO | NO2 | O3 | SO2 | Partikulat |
|---|---|---|---|---|---|---|
| Baik | 0-50 | Tidak ada efek | Sedikit berbau | Luka pada beberapa spesies tumbuhan (kombinasi dengan SO2, 4 jam) | Luka pada beberapa spesies tumbuhan (kombinasi O3, 4 jam) | Tidak ada efek |
| Sedang | 51-100 | Perubahan kimia darah tapi tidak terdeteksi | Berbau | Luka pada beberapa spesies tumbuhan | Luka pada beberapa spesies tumbuhan | Penurunan jarak pandang |
| Tidak Sehat | 101-199 | Peningkatan gejala kardiovaskular pada perokok yang sakit jantung | Bau dan kehilangan warna, peningkatan reaktivitas pembuluh tenggorokan pada penderita asma | Penurunan kemampuan atlit berlatih keras | Bau, meningkatnya kerusakan tanaman | Jarak pandang turun, pengotoran debu dimana-mana |
| Sangat Tidak Sehat | 200-299 | Meningkatnya gejala kardiovaskular pada orang bukan perokok yang sakit jantung | Meningkatnya sensitivitas berpenyakit asma dan bronchitis | Olahraga ringan berdampak pada pasien berpenyakit paru-paru kronis | Meningkatnya sensitivitas berpenyakit asma dan bronchitis | Meningkatnya sensitivitas berpenyakit asma dan bronchitis |
| Berbahaya | ≥300 | Berbahaya bagi semua populasi yang terpapar (berlaku untuk semua parameter) |

## 3. Batas ISPU dalam Satuan SI (µg/m³)

| ISPU | PM10 (24 jam) | SO2 (24 jam) | CO (8 jam) | O3 (1 jam) | NO2 (1 jam) |
|---|---|---|---|---|---|
| 50 | 50 | 80 | 5 | 120 | (2) |
| 100 | 150 | 365 | 10 | 235 | (2) |
| 200 | 350 | 800 | 17 | 400 | 1130 |
| 300 | 420 | 1600 | 34 | 800 | 2260 |
| 400 | 500 | 2100 | 46 | 1000 | 3000 |
| 500 | 600 | 2620 | 57,5 | 1200 | 3750 |

> Catatan: tanda (2) pada NO2 di ISPU 50 dan 100 menunjukkan tidak ada data/nilai baku pada rentang tersebut sesuai sumber asli.

## 4. Rumus Interpolasi ISPU

```
I = ((IA - IB) / (XA - XB)) x (Xx - XB) + IB
```

Keterangan:
- I  = ISPU terhitung
- IA = ISPU batas atas
- IB = ISPU batas bawah
- XA = Ambien batas atas
- XB = Ambien batas bawah
- Xx = Kadar ambien nyata hasil pengukuran

**Langkah perhitungan:**
1. Tentukan parameter dan satuan konsentrasi ambien (Xx).
2. Cari baris pada Tabel Batas ISPU (bagian 3) tempat Xx berada di antara dua nilai batas (XB di bawah, XA di atas).
3. Ambil IB dan IA yang berpasangan dengan XB dan XA tersebut.
4. Masukkan ke rumus interpolasi untuk mendapatkan nilai I.
5. Ulangi untuk setiap parameter yang tersedia (PM10, SO2, CO, O3, NO2).
6. Parameter dominan = parameter dengan nilai I tertinggi di antara seluruh parameter.
7. Klasifikasikan nilai I tertinggi tersebut ke dalam kategori pada Tabel 1.

## 5. Contoh Perhitungan (Terverifikasi)

### Contoh 1: SO2 = 322 µg/m³
- Xx = 322, XB = 80, XA = 365, IB = 50, IA = 100
- I = ((100-50)/(365-80)) x (322-80) + 50
- I = (50/285) x 242 + 50
- I = 92,45 → **Kategori Sedang**

### Contoh 2: CO = 7 µg/m³
- Xx = 7, XB = 5, XA = 10, IB = 50, IA = 100
- I = ((100-50)/(10-5)) x (7-5) + 50
- I = (50/5) x 2 + 50
- I = 70 → **Kategori Sedang**

## 6. Soal Latihan (untuk pengujian sistem)

Diketahui: PM10 = 100 µg/m³, SO2 = 82 µg/m³, CO = 7 µg/m³, O3 = 150 µg/m³

Expected hasil perhitungan tiap parameter (untuk validasi output AI):
- CO = 70 (Sedang) — lihat Contoh 2 di atas
- SO2, PM10, O3 dihitung dengan metode yang sama menggunakan Tabel 3
- Parameter dominan = parameter dengan nilai ISPU tertinggi
- Kategori akhir mengikuti nilai ISPU dominan tersebut
