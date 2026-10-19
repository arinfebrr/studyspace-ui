# StudySpace UI — WebGIS tempat belajar

StudySpace UI adalah antarmuka direktori dan peta interaktif untuk dataset tempat belajar di dalam dan sekitar Universitas Indonesia, Depok. Proyek ini mempertahankan data GeoJSON dan aset Leaflet/QGIS2Web dari arsip sumber.

## Menjalankan secara lokal

Disarankan menggunakan server lokal agar pemuatan data dan tile peta konsisten di berbagai browser:

1. Ekstrak folder proyek.
2. Buka terminal di folder `qgis2web_2026_10_19-00_52_16_829317`.
3. Jalankan `python -m http.server 8000` (atau `py -m http.server 8000` pada beberapa instalasi Windows).
4. Buka `http://localhost:8000/` untuk landing page atau `http://localhost:8000/map.html` untuk WebGIS.

Peta membutuhkan koneksi internet untuk tile OpenStreetMap. Basemap satelit memakai tile URL yang sudah ada di implementasi; ketersediaan/ketentuan layanan penyedianya dapat berubah. Tidak ada API key baru yang ditambahkan. Sebagian browser mungkin dapat membuka halaman langsung lewat `file://`, tetapi server lokal lebih dapat diandalkan.

## Struktur penting

- `index.html` — landing page.
- `map.html` — halaman direktori dan peta.
- `css/studyspace.css` — sistem visual dan responsive layout.
- `js/studyspace-home.js` — kategori dan kartu lokasi dari dataset.
- `js/studyspace-map.js` — marker, popup, pencarian, filter, daftar, dan sinkronisasi.
- `js/studyspace-photo.js` — fallback foto lokal.
- `data/amenity_university_2.js`, `data/highway_3.js`, `data/study_place_updated_4.js` — data asli; tidak diganti dengan data contoh.
- `qgis2web_original.html` — ekspor HTML QGIS2Web asli yang dipertahankan sebagai referensi.
- `photos/` — tempat opsional untuk foto lokal bernama `<id_spot>.jpg` (misalnya `UI-001.jpg`) atau `.webp`, `.png`, `.jpeg`.

## Catatan data

Dataset tempat belajar berisi 50 fitur dengan kategori yang tercatat: `Cafe Study-Friendly`, `Coworking & Creative Space`, dan `Perpustakaan & Ruang Baca`. Kategori `Ruang Belajar Kampus` belum memiliki fitur dengan label tersebut di dataset saat ini, sehingga tidak ditampilkan sebagai kategori berisi lokasi. Tambahkan data terverifikasi melalui alur data sumber/QGIS jika kategori itu perlu ditampilkan.

Kolom `foto_url` yang saat ini berisi tautan halaman pencarian (misalnya Google Images) tidak dianggap sebagai URL gambar langsung. Tautannya tersedia sebagai sumber foto, sementara UI menampilkan fallback visual hingga foto lokal atau URL gambar langsung yang valid tersedia. Foto lokal tidak disediakan dalam arsip saat ini.

Beberapa atribut seperti `wifi`, `stop_kontak`, dan `indoor` digunakan untuk filter fasilitas hanya jika nilainya mengindikasikan ketersediaan (mis. `Ya`). Data kosong atau `Belum diketahui` tidak dianggap sebagai konfirmasi.

## Yang diubah

- Landing page editorial dengan palet cream, olive, sage, tipografi serif/sans, section kategori, lokasi awal dari dataset, dan CTA.
- Halaman peta dengan panel daftar, pencarian nama/alamat/deskripsi, filter kategori/fasilitas/rentang harga, jumlah hasil, reset, dan empty state.
- Marker kategori konsisten; pemilihan kartu dan marker disinkronkan.
- Popup menghindari nilai kosong, menampilkan fasilitas yang diketahui, mengamankan teks atribut, menautkan Google Maps/Instagram/website jika URL valid, serta membedakan URL gambar langsung dari halaman sumber foto.
- Layout adaptif desktop dan mobile.


## Pembaruan editorial
- Landing page editorial menggunakan aset `assets/studyspace-ui-hero.png` dan logo SVG.
- Kartu enam lokasi unggulan dibentuk dari fitur yang cocok di dataset. Foto khusus tiap lokasi dapat ditambahkan ke `photos/` sesuai `photos/DAFTAR_NAMA_FILE.csv`; foto tidak dikarang.
- Peta menyediakan cluster marker, tiga basemap (OSM, satelit, peta terang CARTO), geolokasi + radius, ekspor GeoJSON, dan alat gambar geometri sederhana.
