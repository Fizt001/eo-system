# Pertanyaan 3 & 4 — Deskripsi Use Case & Analisis Konsistensi
## (Berdasarkan Versi Final Konsisten)

> [!NOTE]
> Dokumen ini menjawab Pertanyaan 3 dan 4 berdasarkan **versi final** Use Case Diagram dan Activity Diagram yang telah diiterasi hingga **0 inkonsistensi**. Total: 5 aktor, 28 use case, 8 relasi include, 9 relasi extend, 3 diagram activity swimlane yang kontinu.

---

## Pertanyaan 3: Deskripsi Lengkap 2 Use Case Utama

Dipilih **2 use case yang paling krusial** terhadap kelangsungan proses bisnis:

1. **UC-C02: Mengajukan Permintaan Acara** — titik awal seluruh proses bisnis EO.
2. **UC-EC02: Menyusun Penawaran** — inti dari value creation bisnis EO, memiliki relasi <<include\>> dan <<extend\>>.

---

### 3.1 Use Case: Mengajukan Permintaan Acara (UC-C02)

| Komponen | Uraian |
|----------|--------|
| **a. Nama Use Case** | UC-C02: Mengajukan Permintaan Acara |
| **b. Aktor** | Customer (Pelanggan) |
| **c. Deskripsi** | Use case ini menggambarkan proses pelanggan mengajukan permintaan penyelenggaraan acara baru melalui portal pelanggan. Pelanggan mengisi formulir yang berisi informasi kebutuhan acara, seperti jenis acara, tanggal pelaksanaan, lokasi, konsep, dan estimasi jumlah peserta. Data permintaan ini kemudian disimpan oleh sistem dan diteruskan ke Event Coordinator untuk ditinjau. |
| **d. Pre-condition** | 1. Customer sudah memiliki akun terdaftar (UC-C01: Mendaftar Akun telah dilakukan). |
| | 2. Customer sudah berhasil login ke portal pelanggan (UC-AUTH: Autentikasi Pengguna telah dilakukan). |
| | 3. Sistem dalam keadaan aktif dan dapat diakses. |
| **e. Post-condition** | 1. Data permintaan acara tersimpan dalam sistem dengan status **"Baru"**. |
| | 2. Event Coordinator menerima notifikasi bahwa ada permintaan acara baru yang perlu ditinjau. |
| | 3. Permintaan muncul di halaman "Riwayat Permintaan" Customer dengan status **"Baru"**. |

#### f. Alur Normal (Main Flow)

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 1 | Customer | Memilih menu **"Ajukan Permintaan Acara"** pada portal pelanggan. |
| 2 | Sistem | Menampilkan formulir permintaan acara yang berisi field: jenis acara (dipilih dari master data kategori), tanggal pelaksanaan, lokasi, konsep acara, estimasi jumlah peserta, dan catatan tambahan. |
| 3 | Customer | Mengisi seluruh field yang tersedia pada formulir. |
| 4 | Customer | Menekan tombol **"Kirim Permintaan"**. |
| 5 | Sistem | Melakukan validasi terhadap data yang diisi (memastikan field wajib terisi dan format data benar). |
| 6 | Sistem | Menyimpan data permintaan acara ke dalam database dengan status **"Baru"** dan mencatat waktu pengajuan. |
| 7 | Sistem | Mengirimkan notifikasi ke seluruh Event Coordinator bahwa terdapat permintaan acara baru. |
| 8 | Sistem | Menampilkan pesan konfirmasi kepada Customer: *"Permintaan acara Anda berhasil dikirim dan sedang ditinjau oleh tim kami."* |
| 9 | Customer | Melihat permintaan yang baru diajukan pada halaman **"Riwayat Permintaan"** dengan status **"Baru"**. |

#### g. Alur Alternatif

**Alternatif 5a — Validasi Gagal (Field Wajib Tidak Terisi)**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 5a.1 | Sistem | Mendeteksi bahwa satu atau lebih field wajib belum terisi atau format data tidak valid (contoh: tanggal lampau, estimasi peserta bukan angka). |
| 5a.2 | Sistem | Menampilkan pesan error pada field yang bermasalah (contoh: *"Tanggal pelaksanaan wajib diisi"*, *"Estimasi peserta harus berupa angka"*). |
| 5a.3 | Customer | Memperbaiki data yang salah atau melengkapi field yang kosong. |
| 5a.4 | | Kembali ke **Langkah 4** (Alur Normal). |

**Alternatif 4a — Customer Melampirkan Dokumen Pendukung (<<extend\>>)**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 4a.1 | Customer | Sebelum menekan "Kirim", memilih opsi **"Lampirkan Dokumen"**. |
| 4a.2 | Sistem | Menampilkan area upload dokumen (format: JPG, PNG, PDF, maks 5MB per file). |
| 4a.3 | Customer | Mengunggah dokumen pendukung (contoh: referensi gambar, denah lokasi, rundown acara). |
| 4a.4 | Sistem | Memvalidasi format dan ukuran file. Jika tidak valid, tampilkan pesan error. |
| 4a.5 | | Kembali ke **Langkah 4** (Alur Normal). |

**Alternatif 4b — Customer Membatalkan Pengajuan**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 4b.1 | Customer | Menekan tombol **"Batal"** sebelum mengirim formulir. |
| 4b.2 | Sistem | Menampilkan dialog konfirmasi: *"Apakah Anda yakin ingin membatalkan? Data yang sudah diisi tidak akan disimpan."* |
| 4b.3 | Customer | Memilih **"Ya, Batalkan"**. |
| 4b.4 | Sistem | Menghapus data formulir dan mengarahkan Customer kembali ke halaman utama portal. |
| 4b.5 | | **Use case berakhir.** |

---

### 3.2 Use Case: Menyusun Penawaran (UC-EC02)

| Komponen | Uraian |
|----------|--------|
| **a. Nama Use Case** | UC-EC02: Menyusun Penawaran |
| **b. Aktor** | Event Coordinator |
| **c. Deskripsi** | Use case ini menggambarkan proses Event Coordinator menyusun dokumen penawaran berupa Rencana Anggaran Biaya (RAB) berdasarkan permintaan acara yang diajukan oleh pelanggan. Proses ini **wajib mencakup** perhitungan estimasi biaya (<<include\>>: Menghitung Estimasi Biaya) dan **dapat memicu** revisi penawaran jika ada perubahan dari pelanggan atau Manager (<<extend\>>: UC-EC03 Merevisi Penawaran). Setelah penawaran selesai disusun, Event Coordinator mencatat log aktivitas (UC-EC09), lalu dokumen dikirim ke Manager untuk mendapatkan persetujuan. |
| **d. Pre-condition** | 1. Event Coordinator sudah berhasil login ke sistem (UC-AUTH telah dilakukan). |
| | 2. Terdapat permintaan acara dengan status **"Baru"** yang sudah ditinjau dan dinyatakan layak diproses (UC-EC01 telah dilakukan). |
| | 3. Data master kategori biaya dan data vendor tersedia dalam sistem (UC-M02 dan UC-EC08 telah dilakukan sebagai setup awal). |
| **e. Post-condition** | 1. Dokumen penawaran / RAB tersimpan dalam sistem dengan status **"Menunggu Persetujuan Manager"**, versi 1.0. |
| | 2. Penawaran terhubung (linked) ke data permintaan acara yang bersangkutan. |
| | 3. Log aktivitas tercatat (UC-EC09). |
| | 4. Manager menerima notifikasi bahwa ada penawaran baru yang perlu disetujui (UC-M03). |

#### f. Alur Normal (Main Flow)

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 1 | Event Coordinator | Membuka data permintaan acara yang berstatus **"Layak Diproses"**. |
| 2 | Sistem | Menampilkan detail permintaan acara dari pelanggan (jenis acara, tanggal, lokasi, konsep, estimasi peserta, dokumen lampiran jika ada). |
| 3 | Event Coordinator | Memilih menu **"Buat Penawaran"** pada halaman detail permintaan. |
| 4 | Sistem | Menampilkan formulir penyusunan penawaran yang berisi: judul penawaran, deskripsi layanan, tabel rincian biaya (item, kategori, satuan, harga, jumlah, subtotal), catatan/syarat & ketentuan, dan masa berlaku penawaran. |
| 5 | Event Coordinator | Mengisi deskripsi layanan dan konsep acara yang akan ditawarkan. |
| 6 | Event Coordinator | **[<<include\>>: Menghitung Estimasi Biaya]** — Menambahkan item-item biaya ke dalam tabel RAB. Untuk setiap item, EC mengisi: nama item, kategori biaya, satuan, harga per satuan, dan jumlah. |
| 7 | Sistem | Menghitung dan menampilkan **subtotal per item** dan **total estimasi biaya** keseluruhan secara real-time setiap kali item ditambahkan atau diubah. |
| 8 | Event Coordinator | Mengisi catatan, syarat & ketentuan, serta masa berlaku penawaran. |
| 9 | Event Coordinator | Menekan tombol **"Kirim ke Manager untuk Persetujuan"**. |
| 10 | Sistem | Memvalidasi kelengkapan data penawaran (minimal 1 item biaya, deskripsi layanan terisi, masa berlaku terisi). |
| 11 | Sistem | Menyimpan dokumen penawaran dengan status **"Menunggu Persetujuan Manager"**, versi **1.0**, dan mencatat waktu pembuatan. |
| 12 | Event Coordinator | **[UC-EC09: Mencatat Log Aktivitas]** — Sistem otomatis mencatat log bahwa penawaran telah disusun dan dikirim ke Manager. |
| 13 | Sistem | Mengirimkan notifikasi ke Manager bahwa terdapat penawaran baru yang memerlukan persetujuan. |
| 14 | Sistem | Mengubah status permintaan acara terkait menjadi **"Sedang Diproses"**. |

#### g. Alur Alternatif

**Alternatif 10a — Validasi Gagal (Data Tidak Lengkap)**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 10a.1 | Sistem | Mendeteksi data penawaran tidak lengkap (contoh: tabel biaya kosong, deskripsi layanan kosong, masa berlaku belum diisi). |
| 10a.2 | Sistem | Menampilkan pesan error pada bagian yang belum lengkap. |
| 10a.3 | Event Coordinator | Melengkapi data yang kurang. |
| 10a.4 | | Kembali ke **Langkah 9** (Alur Normal). |

**Alternatif 9a — Menyimpan sebagai Draft**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 9a.1 | Event Coordinator | Menekan tombol **"Simpan Draft"** alih-alih mengirim ke Manager. |
| 9a.2 | Sistem | Menyimpan penawaran dengan status **"Draft"**. Penawaran belum dikirim ke Manager dan belum ada notifikasi. |
| 9a.3 | Sistem | Menampilkan pesan: *"Penawaran berhasil disimpan sebagai draft. Anda dapat melanjutkan penyusunan kapan saja."* |
| 9a.4 | | **Use case berakhir.** EC dapat kembali mengedit draft di lain waktu dan melanjutkan dari **Langkah 5**. |

**Alternatif 6a — Menggunakan Template Biaya dari Event Sebelumnya**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| 6a.1 | Event Coordinator | Memilih opsi **"Gunakan Template dari Event Sebelumnya"**. |
| 6a.2 | Sistem | Menampilkan daftar penawaran/event sebelumnya yang sejenis (berdasarkan kategori acara dari master data). |
| 6a.3 | Event Coordinator | Memilih salah satu template. |
| 6a.4 | Sistem | Menyalin seluruh item biaya dari template ke formulir penawaran saat ini. |
| 6a.5 | Event Coordinator | Menyesuaikan harga, item, dan jumlah sesuai kebutuhan event yang baru. |
| 6a.6 | | Kembali ke **Langkah 7** (Alur Normal). |

**Alternatif Post — Revisi Penawaran (<<extend\>>: UC-EC03)**

| Langkah | Aktor | Aksi |
|---------|-------|------|
| Ext.1 | | **Kondisi pemicu:** Manager mengembalikan penawaran dengan catatan revisi (dari UC-M03) **ATAU** Customer meminta perubahan setelah menerima penawaran (dari UC-C04 extend: Mengajukan Catatan Revisi). |
| Ext.2 | Event Coordinator | Membuka penawaran yang dikembalikan dan membaca catatan revisi. |
| Ext.3 | Event Coordinator | Memilih menu **"Buat Revisi Penawaran"**. |
| Ext.4 | Sistem | Membuat salinan penawaran sebelumnya sebagai versi baru (versi 1.0 → 2.0, dst.) dengan riwayat perubahan tercatat. Versi lama tetap tersimpan sebagai arsip. |
| Ext.5 | Event Coordinator | Mengubah item biaya, deskripsi, atau ketentuan sesuai catatan revisi. |
| Ext.6 | Event Coordinator | **[UC-EC09: Mencatat Log Aktivitas]** — Mencatat alasan revisi dan perubahan yang dilakukan. |
| Ext.7 | | Kembali ke **Langkah 9** (Alur Normal) — mengirim ulang ke Manager untuk persetujuan. |

---
---

## Pertanyaan 4: Analisis Keterkaitan Use Case Diagram dan Activity Diagram

### 4a. Apakah seluruh aktivitas memiliki representasi dalam Use Case?

**Ya, seluruh aktivitas pada Activity Diagram memiliki representasi dalam Use Case Diagram.** Berikut bukti pemetaan lengkap:

#### Pemetaan Diagram 5.1 (Fase 1: Permintaan → Konfirmasi Event)

| Aktivitas pada Activity Diagram | Use Case | Status |
|--------------------------------|----------|--------|
| Customer login ke portal | UC-AUTH: Autentikasi Pengguna | ✅ |
| Customer mengisi formulir Permintaan Acara | UC-C02: Mengajukan Permintaan Acara | ✅ |
| Sistem menyimpan permintaan status "Baru" | *(Aksi sistem otomatis — post-condition UC-C02)* | ✅ |
| Sistem mengirim notifikasi ke EC | *(Aksi sistem otomatis — post-condition UC-C02)* | ✅ |
| EC login ke sistem | UC-AUTH: Autentikasi Pengguna | ✅ |
| EC menerima & meninjau permintaan | UC-EC01: Mengelola Permintaan Acara | ✅ |
| EC menolak permintaan dengan alasan | UC-EC01: Mengelola Permintaan Acara | ✅ |
| EC menganalisis kebutuhan & menyusun RAB | UC-EC02: Menyusun Penawaran | ✅ |
| EC mencatat Log Aktivitas | UC-EC09: Mencatat Log Aktivitas | ✅ |
| Manager login ke sistem | UC-AUTH: Autentikasi Pengguna | ✅ |
| Manager memeriksa detail penawaran | UC-M03 <<include\>>: Memeriksa Detail Penawaran | ✅ |
| Manager menyetujui / menolak penawaran | UC-M03: Menyetujui Penawaran | ✅ |
| Manager mengembalikan dengan catatan revisi | UC-M03: Menyetujui Penawaran (jalur alternatif) | ✅ |
| Sistem mengirim penawaran ke Customer | *(Aksi sistem — post-condition UC-M03)* | ✅ |
| Customer meninjau penawaran | UC-C03: Melihat Penawaran | ✅ |
| Customer menyetujui / menolak penawaran | UC-C04: Menyetujui / Menolak Penawaran | ✅ |
| Customer mengirim catatan revisi | UC-C04 <<extend\>>: Mengajukan Catatan Revisi | ✅ |
| EC merevisi penawaran (loop) | UC-EC03: Merevisi Penawaran | ✅ |
| Sistem mengubah status → "Terkonfirmasi" | *(Aksi sistem — post-condition UC-C04)* | ✅ |
| Sistem membuat Ruang Kerja Event | *(Aksi sistem otomatis — trigger untuk UC-EC04)* | ✅ |

#### Pemetaan Diagram 5.2 (Fase 2: Persiapan → Penutupan)

| Aktivitas pada Activity Diagram | Use Case | Status |
|--------------------------------|----------|--------|
| EC membuat perencanaan Event & timeline | UC-EC04: Mengelola Event | ✅ |
| EC membuat daftar tugas persiapan | UC-EC05: Mengelola Tugas Event | ✅ |
| EC menugaskan tugas ke Staff (Fork 1 Jalur A) | UC-EC05: Mengelola Tugas Event | ✅ |
| EC mengalokasikan Vendor (Fork 1 Jalur B) | UC-EC06: Mengalokasikan Vendor | ✅ |
| Staff menerima & melihat tugas | UC-S01: Melihat Daftar Tugas | ✅ |
| Staff mengerjakan tugas → update progres | UC-S02: Memperbarui Progres Tugas (detail di Sub-proses 5.3) | ✅ |
| EC memantau & memverifikasi kesiapan | UC-EC07: Memantau Perkembangan Event | ✅ |
| EC mendeklarasikan pelaksanaan event | UC-EC11: Mendeklarasikan Pelaksanaan Event | ✅ |
| EC mengubah status Event → "Selesai" (Fork 2 Jalur A) | UC-EC04: Mengelola Event | ✅ |
| EC mencatat Log Aktivitas | UC-EC09: Mencatat Log Aktivitas | ✅ |
| Finance login ke sistem | UC-AUTH: Autentikasi Pengguna | ✅ |
| Finance membuat tagihan (Fork 2 Jalur B) | UC-F01: Membuat Tagihan | ✅ |
| Customer melihat tagihan di Portal | UC-C06: Melihat Tagihan & Mengonfirmasi Pembayaran | ✅ |
| Customer mengonfirmasi & mengunggah bukti bayar | UC-C06 <<extend\>>: Mengunggah Bukti Pembayaran | ✅ |
| Finance mencatat & memvalidasi pembayaran | UC-F02: Mencatat Pembayaran Masuk | ✅ |
| Finance membuat tagihan berikutnya (loop) | UC-F01 <<extend\>>: Membuat Tagihan Bertahap | ✅ |
| Finance mencatat biaya vendor sebagai HPP | UC-F03: Mencatat Biaya Vendor | ✅ |
| Sistem menghitung Laba/Rugi | *(Aksi sistem — terkait UC-F04)* | ✅ |

#### Pemetaan Diagram 5.3 (Sub-proses: Staff Mengerjakan Tugas)

| Aktivitas pada Activity Diagram | Use Case | Status |
|--------------------------------|----------|--------|
| Staff login ke sistem | UC-AUTH: Autentikasi Pengguna | ✅ |
| Staff melihat daftar tugas | UC-S01: Melihat Daftar Tugas | ✅ |
| Staff memilih tugas | UC-S01: Melihat Daftar Tugas | ✅ |
| Staff mengubah status → "Sedang Dikerjakan" | UC-S02: Memperbarui Progres Tugas | ✅ |
| Staff mengerjakan tugas di lapangan | *(Aktivitas fisik di luar sistem)* | ✅ |
| Staff menambahkan catatan & lampiran | UC-S03: Menambahkan Catatan Tugas | ✅ |
| Staff mengubah status → "Selesai" | UC-S02: Memperbarui Progres Tugas | ✅ |
| EC menerima notifikasi & memeriksa hasil tugas | UC-EC10: Memverifikasi Hasil Tugas | ✅ |
| EC mengembalikan tugas untuk perbaikan | UC-EC10 <<extend\>>: Mengembalikan Tugas untuk Perbaikan | ✅ |
| EC menandai tugas → "Terverifikasi" | UC-EC10: Memverifikasi Hasil Tugas | ✅ |
| EC mencatat Log Aktivitas | UC-EC09: Mencatat Log Aktivitas | ✅ |
| Sistem memperbarui progres keseluruhan Event | *(Aksi sistem — terkait UC-EC07)* | ✅ |

#### Verifikasi Arah Sebaliknya (Use Case → Activity Diagram)

Use Case yang **tidak muncul langsung** dalam Activity Diagram beserta justifikasinya:

| Use Case | Justifikasi | Status |
|----------|-------------|--------|
| UC-C01: Mendaftar Akun | Merupakan **pra-kondisi satu kali** sebelum seluruh alur dimulai. Tidak masuk alur operasional berulang. | ✅ Wajar |
| UC-M01: Mengelola Data Pengguna Internal | Merupakan aktivitas **setup/administratif** yang dilakukan sebelum operasional berjalan. | ✅ Wajar |
| UC-M02: Mengelola Master Data | Merupakan aktivitas **setup/administratif** (kategori event, kategori vendor). | ✅ Wajar |
| UC-M04: Melihat Dashboard Bisnis | Merupakan fitur **monitoring pasif** yang dapat diakses kapan saja tanpa mengubah alur proses. | ✅ Wajar |
| UC-M05: Melihat Laporan | Merupakan fitur **monitoring/reporting pasif**. | ✅ Wajar |
| UC-C05: Memantau Perkembangan Event | Merupakan fitur **monitoring pasif** di portal pelanggan. | ✅ Wajar |
| UC-EC08: Mengelola Data Vendor | Merupakan aktivitas **master data/setup** sebelum vendor dialokasikan ke event. | ✅ Wajar |
| UC-F04: Melihat Laporan Keuangan | Merupakan fitur **reporting pasif** untuk Finance. | ✅ Wajar |

> **Catatan:** Seluruh use case di atas bersifat **administratif**, **setup**, atau **monitoring pasif** — artinya tidak mengubah alur proses bisnis utama dan dapat diakses kapan saja secara independen. Maka tidak dimasukkan dalam Activity Diagram yang menggambarkan **alur proses bisnis operasional** agar diagram tetap fokus dan tidak terlalu kompleks.

---

### 4b. Apakah terdapat inkonsistensi model?

**Tidak, tidak terdapat inkonsistensi model** antara Use Case Diagram dan Activity Diagram yang telah dirancang. 

Seluruh alur operasional di Activity Diagram (Fase 1, Fase 2, maupun Sub-proses) telah dipetakan secara presisi 1-ke-1 dengan Use Case yang bersangkutan. Tidak ada aktivitas "liar" yang dilakukan oleh aktor di Activity Diagram tanpa didasari oleh Use Case, dan tidak ada Use Case operasional yang menggantung tanpa representasi di Activity Diagram.

---

### 4c. Jelaskan perbaikan yang seharusnya dilakukan

Karena desain yang dibuat telah memiliki tingkat konsistensi 100%, **tidak ada perbaikan lebih lanjut yang perlu dilakukan pada saat ini.** 

Konsistensi ini dapat tercapai berkat penerapan prinsip-prinsip desain berikut sejak awal perancangan:

1. **Aksi Aktif Selalu Menjadi Use Case**
   Setiap tindakan yang mensyaratkan aktor memberikan input, mengubah status, atau memicu proses baru (seperti "Mengonfirmasi Pembayaran" oleh Customer atau "Mendeklarasikan Pelaksanaan Event" oleh Event Coordinator) dibuatkan Use Case eksplisit (UC-C06 dan UC-EC11), sehingga Activity Diagram berjalan mulus.
2. **Sentralisasi Autentikasi**
   Langkah "Login" yang diulang-ulang oleh berbagai aktor di Activity Diagram diikat pada satu Use Case universal (**UC-AUTH**), menghindari redundansi pendaftaran fungsi login untuk tiap aktor.
3. **Representasi Fungsi Cross-Cutting**
   Fungsi pencatatan (seperti log aktivitas pada UC-EC09) secara sadar didistribusikan ke titik-titik transisi kritis pada Activity Diagram (seperti setelah menyusun RAB, memverifikasi tugas, dan menutup event) agar keberadaan Use Case-nya berdasar.
4. **Pengecualian yang Terdokumentasi**
   Use Case yang murni bersifat "Setup Data" (mengelola pengguna/master data) dan "Monitoring Pasif" (melihat dashboard/laporan) secara sengaja dihindarkan dari Activity Diagram operasional. Hal ini dilakukan bukan sebagai inkonsistensi, melainkan pemisahan *concern* agar diagram alur proses bisnis inti tidak menjadi *cluttered* (rumit) oleh langkah-langkah administratif yang berjalan asinkron.

Dengan demikian, arsitektur *blueprint* ini telah solid dan siap untuk dijadikan dasar perancangan database maupun pengembangan *codebase* aplikasi.
