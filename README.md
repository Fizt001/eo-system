# Blueprint Sistem Manajemen Event Organizer (EO)
*(Versi Update — Tersinkronisasi dengan Use Case & Activity Diagram Final)*

Berdasarkan narasi studi kasus dan penyempurnaan rancangan model sistem (Use Case & Activity Diagram), berikut adalah rumusan konsep *blueprint* sistem yang solid, konsisten, dan dapat diskalakan (*scalable*).

---

## 1. Analisis "Jebakan" & Benang Merah

Berikut adalah beberapa narasi yang berpotensi menjadi "jebakan" jika diimplementasikan secara mentah, beserta solusi sistemiknya:

- **Jebakan 1:** Menganggap sistem harus dirancang spesifik/berbeda untuk "seminar, konser musik, hingga pernikahan".
  - **Benang Merah:** Sistem tidak boleh di-*hardcode* untuk jenis acara tertentu. Harus ada modul **Master Data Kategori Event** yang dinamis, sehingga EO bisa menambah jenis acara baru kapan saja tanpa mengubah kode.
- **Jebakan 2:** "Komunikasi telepon dan pesan instan" yang dilakukan secara manual.
  - **Benang Merah:** Kita tidak perlu membangun aplikasi *chatting* sendiri di dalam sistem. Solusinya adalah menyediakan fitur **Inquiry System** di portal pelanggan dan fitur **Log Aktivitas** (*Activity Log*) bagi Event Coordinator untuk mencatat semua rekam jejak komunikasi dan keputusan penting.
- **Jebakan 3:** "Kerja sama dengan pihak ketiga / vendor".
  - **Benang Merah:** Membangun portal khusus bagi vendor (agar bisa login) mungkin terlalu kompleks untuk fase awal. Solusi fase 1 adalah membuat **Modul Manajemen Vendor Internal** yang dikelola sepihak oleh tim EO untuk mendata, mengalokasikan, dan mencatat biaya vendor.
- **Jebakan 4:** "Perubahan permintaan dari pelanggan".
  - **Benang Merah:** Dokumen Penawaran (RAB) tidak boleh statis. Harus ada mekanisme **Revisi Penawaran (Versioning)** sehingga riwayat perubahan harga dan konsep (dari versi 1.0 ke versi revisi) dapat dilacak secara akurat.

---

## 2. Aktor / Pengguna Sistem (Role-Based Access Control)

Terdapat **5 peran (Role)** spesifik untuk menjaga prinsip pemisahan wewenang (*segregation of duties*) dan mencegah *bug* logika bisnis:

1. **Manager (Internal):** Pemilik/Pimpinan EO. Memiliki otoritas tertinggi untuk menyetujui Penawaran/RAB sebelum dikirim ke pelanggan, mengelola data pengguna internal, master data, serta memantau dashboard laporan (Laba/Rugi).
2. **Event Coordinator (Internal):** Pengelola *project event* (Project Manager). Bertugas merespons permintaan masuk, menyusun Penawaran (RAB), merencanakan tugas, mengalokasikan vendor, memverifikasi hasil kerja Staff, dan mengubah status utama event.
3. **Staff Operasional (Internal):** Eksekutor lapangan. Bertugas melihat daftar tugas dari Event Coordinator, mengerjakan tugas tersebut, serta mengunggah bukti pengerjaan/catatan.
4. **Finance (Internal):** Pengelola keuangan. Fokus pada pembuatan tagihan (Invoice), validasi pembayaran dari pelanggan, dan pencatatan biaya yang dibayarkan ke Vendor (HPP).
5. **Customer / Pelanggan (Eksternal):** Klien EO. Menggunakan portal pelanggan (*Customer Portal*) untuk mengajukan permintaan acara, meninjau/menyetujui Penawaran, mengonfirmasi tagihan, dan melihat progres event secara pasif.

---

## 3. Modul Utama Sistem

Rancangan modul untuk pengembangan aplikasi (Laravel):

### A. Modul Autentikasi & Pengaturan (Universal)
- **Otentikasi Universal:** Login terpusat untuk semua aktor.
- **Registrasi Pelanggan:** Formulir pendaftaran mandiri khusus Customer.
- **Manajemen Pengguna:** Penambahan staf internal oleh Manager.
- **Master Data:** Kelola kategori event, kategori vendor, dan standar item biaya.

### B. Modul Customer Relationship Management (CRM)
- **Inquiry Management:** Formulir pengajuan acara dari portal pelanggan (mencakup tanggal, konsep, lokasi, lampiran file).
- **Riwayat Pelanggan:** Pencatatan *history* event yang pernah diselenggarakan oleh pelanggan bersangkutan.

### C. Modul Penawaran (Quotation)
- **Penyusunan RAB:** Kalkulator otomatis subtotal dan grand total untuk estimasi biaya oleh Event Coordinator. Termasuk fitur *template* dari event lama.
- **Approval Berjenjang:** Penawaran wajib disetujui Manager di internal, baru kemudian disetujui oleh Customer di eksternal.
- **Quotation Versioning:** Fitur salinan revisi penawaran jika terjadi penolakan atau *change request*.

### D. Modul Project & Task Management (Inti Operasional)
- **Event Workspace:** Ruang kerja digital untuk mengelola satu acara tertentu (mencakup timeline, status event).
- **Task Delegation & Verification:** Event Coordinator membuat *checklist* tugas $\rightarrow$ dikerjakan Staff $\rightarrow$ dikembalikan ke EC untuk diverifikasi (*Approval Tasks*).
- **Activity Logging:** Catatan manual (*log*) pada titik-titik kritis (setelah menyusun RAB, penutupan event, dll).

### E. Modul Manajemen Vendor
- **Direktori Vendor:** Database kontak dan spesialisasi layanan vendor.
- **Alokasi Vendor:** Penunjukan vendor untuk event tertentu yang berjalan paralel dengan eksekusi tugas tim internal.

### F. Modul Keuangan (Finance & Billing)
- **Invoicing:** Pembuatan tagihan secara parsial (DP / Termin) atau lunas penuh.
- **Konfirmasi Pembayaran:** Pelanggan unggah bukti transfer $\rightarrow$ divalidasi oleh Finance.
- **Pencatatan HPP (Harga Pokok Penjualan):** Pencatatan *cost* modal yang dibayarkan EO kepada vendor.
- **Laporan Laba/Rugi:** Perhitungan otomatis selisih Pendapatan (Tagihan Pelanggan) dikurangi Pengeluaran (Biaya Vendor) per event.

---

## 4. Alur Kerja (Workflow) Sistem Terintegrasi

Alur ini dirancang tanpa titik buntu (*dead-end*) dan sejalan dengan Activity Diagram final:

1. **Fase Permintaan (Inquiry):**
   - Customer *login* ke portal dan mengajukan Permintaan Acara.
   - Event Coordinator (EC) meninjau kelayakan permintaan tersebut.
2. **Fase Penawaran (Quotation):**
   - EC menganalisis permintaan dan menyusun draf Penawaran (RAB).
   - Penawaran diverifikasi dan **disetujui oleh Manager**.
   - Sistem meneruskan Penawaran ke Customer.
   - Customer me-*review* dan menekan **Setuju** (atau meminta Revisi). Sistem otomatis membuatkan Ruang Kerja (*Event Workspace*).
3. **Fase Persiapan (Paralel):**
   - EC menyusun timeline dan *checklist* tugas.
   - **Fork A (Tugas):** EC menugaskan pekerjaan $\rightarrow$ Staff Operasional mengerjakan $\rightarrow$ EC memverifikasi hasil.
   - **Fork B (Vendor):** Secara bersamaan, EC mengalokasikan dan *booking* vendor yang dibutuhkan.
4. **Fase Pelaksanaan:**
   - Setelah semua tugas diverifikasi dan vendor siap, EC mendeklarasikan bahwa **Event Dilaksanakan**.
5. **Fase Penagihan & Penutupan (Paralel):**
   - **Fork A (Status):** EC mengubah status event menjadi **"Selesai"** dan mencatat *log* akhir.
   - **Fork B (Keuangan):** Finance merilis *Invoice*, Customer melunasi pembayaran, Finance mencatat biaya Vendor (HPP).
   - Sistem secara otomatis mengalkulasi Laba/Rugi. Setelah jalur A dan B terpenuhi, sistem mengunci status event menjadi **"Closed"**.
