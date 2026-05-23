# Use Case & Activity Diagram — Sistem Manajemen Event Organizer
## Versi Final (Konsisten)

> [!IMPORTANT]
> Dokumen ini adalah versi **final** yang telah menerapkan seluruh perbaikan dari hasil analisis konsistensi (Pertanyaan 4). Seluruh aktivitas pada Activity Diagram memiliki representasi di Use Case Diagram, dan sebaliknya. **0 inkonsistensi.**

---

## 1. Identifikasi Aktor

| No | Aktor | Tipe | Deskripsi |
|----|-------|------|-----------|
| 1 | Manager | Internal | Pemilik/pimpinan EO. Bertanggung jawab atas persetujuan penawaran, monitoring bisnis, pengelolaan pengguna internal, dan master data. |
| 2 | Event Coordinator | Internal | Pengelola proyek event. Menangani permintaan acara, penyusunan penawaran, perencanaan event, alokasi vendor, verifikasi tugas, dan koordinasi tim. |
| 3 | Staff Operasional | Internal | Pelaksana tugas lapangan. Mengerjakan tugas yang diberikan dan melaporkan perkembangan. |
| 4 | Finance | Internal | Pengelola keuangan. Menangani tagihan, pencatatan pembayaran, pencatatan biaya vendor, dan laporan keuangan. |
| 5 | Customer | Eksternal | Pelanggan yang mengajukan permintaan acara, menyetujui penawaran, memantau perkembangan, dan mengonfirmasi pembayaran. |

---

## 2. Daftar Use Case per Aktor

### 2.0 Semua Aktor (Universal)

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-AUTH | Autentikasi Pengguna (Login) | Semua aktor melakukan proses login sebelum mengakses fitur sistem sesuai hak aksesnya masing-masing. |

### 2.1 Manager

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-M01 | Mengelola Data Pengguna Internal | Menambah, mengubah, dan menghapus akun pengguna internal (Event Coordinator, Staff, Finance) |
| UC-M02 | Mengelola Master Data | Menambah, mengubah, dan menghapus data referensi (kategori event, kategori vendor, dll.) |
| UC-M03 | Menyetujui Penawaran | Memeriksa dan memberikan persetujuan atau penolakan terhadap penawaran yang disusun Event Coordinator |
| UC-M04 | Melihat Dashboard Bisnis | Melihat ringkasan jumlah event, pendapatan, dan status event yang sedang berjalan |
| UC-M05 | Melihat Laporan | Melihat laporan keuangan, histori event, dan evaluasi performa vendor |

### 2.2 Event Coordinator

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-EC01 | Mengelola Permintaan Acara | Menerima, meninjau, dan merespons permintaan acara yang masuk dari pelanggan |
| UC-EC02 | Menyusun Penawaran | Menyusun Rencana Anggaran Biaya (RAB) berdasarkan permintaan acara pelanggan |
| UC-EC03 | Merevisi Penawaran | Membuat versi revisi penawaran apabila ada perubahan permintaan dari pelanggan atau catatan dari Manager |
| UC-EC04 | Mengelola Event | Membuat data event baru setelah penawaran disetujui, mengatur jadwal dan detail pelaksanaan |
| UC-EC05 | Mengelola Tugas Event | Membuat checklist tugas persiapan dan menugaskan ke Staff Operasional |
| UC-EC06 | Mengalokasikan Vendor | Memilih dan menugaskan vendor ke event beserta pencatatan estimasi biaya vendor |
| UC-EC07 | Memantau Perkembangan Event | Melihat status keseluruhan persiapan event berdasarkan progres tugas dan kesiapan vendor |
| UC-EC08 | Mengelola Data Vendor | Menambah, mengubah, dan menghapus data vendor (nama, kategori layanan, kontak) |
| UC-EC09 | Mencatat Log Aktivitas | Mencatat notulensi rapat, hasil komunikasi, dan catatan penting terkait event pada titik-titik kritis proses |
| UC-EC10 | Memverifikasi Hasil Tugas | Memeriksa dan memvalidasi hasil tugas yang dilaporkan selesai oleh Staff Operasional, kemudian menyetujui atau mengembalikan untuk perbaikan |
| UC-EC11 | Mendeklarasikan Pelaksanaan Event | Menandai bahwa seluruh persiapan telah selesai dan event resmi memasuki tahap pelaksanaan, memicu proses pembayaran dan penutupan |

### 2.3 Staff Operasional

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-S01 | Melihat Daftar Tugas | Melihat seluruh tugas yang ditugaskan kepadanya beserta tenggat waktu |
| UC-S02 | Memperbarui Progres Tugas | Mengubah status tugas (Belum Dikerjakan → Sedang Dikerjakan → Selesai) |
| UC-S03 | Menambahkan Catatan Tugas | Memberikan catatan atau lampiran pada tugas sebagai bukti pengerjaan |

### 2.4 Finance

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-F01 | Membuat Tagihan | Membuat tagihan pembayaran untuk pelanggan berdasarkan penawaran yang telah disetujui |
| UC-F02 | Mencatat Pembayaran Masuk | Mencatat dan memvalidasi pembayaran yang diterima dari pelanggan (DP, termin, pelunasan) |
| UC-F03 | Mencatat Biaya Vendor | Mencatat pengeluaran ke vendor (Harga Pokok Penjualan) per event |
| UC-F04 | Melihat Laporan Keuangan | Melihat rekap pemasukan, pengeluaran, dan laba/rugi per event maupun keseluruhan |

### 2.5 Customer (Pelanggan)

| Kode | Use Case | Deskripsi |
|------|----------|-----------|
| UC-C01 | Mendaftar Akun | Mendaftar akun baru pada portal pelanggan (registrasi) |
| UC-C02 | Mengajukan Permintaan Acara | Mengisi formulir permintaan acara baru (jenis acara, tanggal, lokasi, konsep, estimasi peserta) |
| UC-C03 | Melihat Penawaran | Melihat detail estimasi biaya yang dikirimkan oleh pihak EO |
| UC-C04 | Menyetujui / Menolak Penawaran | Memberikan persetujuan atau penolakan terhadap penawaran (disertai catatan jika ada) |
| UC-C05 | Memantau Perkembangan Event | Melihat status dan progres persiapan acara secara langsung |
| UC-C06 | Melihat Tagihan & Mengonfirmasi Pembayaran | Melihat daftar tagihan, mengunggah bukti pembayaran, dan mengonfirmasi bahwa pembayaran telah dilakukan |

---

## 3. Relasi Include dan Extend

### 3.1 Penjelasan Singkat

- **<<include\>>**: Relasi **wajib**. Use case induk **selalu** memanggil use case yang di-include.
- **<<extend\>>**: Relasi **opsional/kondisional**. Hanya terjadi pada kondisi tertentu.

### 3.2 Tabel Relasi Include

| Use Case Induk | Relasi | Use Case yang Dipanggil | Penjelasan |
|----------------|--------|-------------------------|------------|
| UC-EC02: Menyusun Penawaran | <<include\>> | Menghitung Estimasi Biaya | Setiap penyusunan penawaran **wajib** menyertakan perhitungan rincian biaya (RAB) |
| UC-M03: Menyetujui Penawaran | <<include\>> | Memeriksa Detail Penawaran | Manager **wajib** memeriksa rincian biaya dan konsep sebelum memberikan keputusan |
| UC-F01: Membuat Tagihan | <<include\>> | Mengacu Penawaran yang Disetujui | Pembuatan tagihan **wajib** berdasarkan penawaran yang sudah berstatus disetujui |
| UC-F02: Mencatat Pembayaran Masuk | <<include\>> | Memvalidasi Data Pembayaran | Setiap pencatatan pembayaran **wajib** melalui proses validasi (nominal, bukti transfer, dll.) |
| UC-EC04: Mengelola Event | <<include\>> | Membuat Jadwal Event | Pembuatan event **wajib** disertai penentuan tanggal pelaksanaan dan timeline persiapan |
| UC-S02: Memperbarui Progres Tugas | <<include\>> | Memverifikasi Status Tugas | Sistem **wajib** memverifikasi transisi status tugas yang valid |
| UC-EC10: Memverifikasi Hasil Tugas | <<include\>> | Memeriksa Catatan & Lampiran Staff | EC **wajib** memeriksa bukti pengerjaan sebelum menandai tugas terverifikasi |
| UC-EC11: Mendeklarasikan Pelaksanaan Event | <<include\>> | Memverifikasi Seluruh Kesiapan | EC **wajib** memastikan semua tugas terverifikasi dan vendor siap sebelum deklarasi |

### 3.3 Tabel Relasi Extend

| Use Case Induk | Relasi | Use Case Tambahan | Kondisi Pemicu |
|----------------|--------|-------------------|----------------|
| UC-EC02: Menyusun Penawaran | <<extend\>> | UC-EC03: Merevisi Penawaran | Terjadi **jika** pelanggan meminta perubahan atau Manager meminta revisi |
| UC-C04: Menyetujui / Menolak Penawaran | <<extend\>> | Mengajukan Catatan Revisi | Terjadi **jika** pelanggan tidak langsung menyetujui dan memberikan catatan perubahan |
| UC-S02: Memperbarui Progres Tugas | <<extend\>> | UC-S03: Menambahkan Catatan Tugas | Terjadi **jika** Staff perlu menyertakan bukti foto, catatan kendala, atau lampiran |
| UC-F01: Membuat Tagihan | <<extend\>> | Membuat Tagihan Bertahap (Termin) | Terjadi **jika** skema pembayaran menggunakan sistem termin/bertahap |
| UC-EC04: Mengelola Event | <<extend\>> | Membatalkan Event | Terjadi **jika** pelanggan membatalkan acara setelah event sudah dibuat |
| UC-EC07: Memantau Perkembangan Event | <<extend\>> | Mengirim Notifikasi Keterlambatan | Terjadi **jika** ada tugas yang melewati tenggat waktu |
| UC-C02: Mengajukan Permintaan Acara | <<extend\>> | Melampirkan Dokumen Pendukung | Terjadi **jika** pelanggan ingin menyertakan referensi gambar, denah, atau dokumen |
| UC-C06: Melihat Tagihan & Mengonfirmasi Pembayaran | <<extend\>> | Mengunggah Bukti Pembayaran | Terjadi **jika** pelanggan melakukan pembayaran dan perlu mengunggah bukti transfer |
| UC-EC10: Memverifikasi Hasil Tugas | <<extend\>> | Mengembalikan Tugas untuk Perbaikan | Terjadi **jika** hasil tugas tidak memenuhi standar dan perlu dikerjakan ulang |

---

## 4. Use Case Diagram

### 4.0 Diagram Use Case — Autentikasi (Semua Aktor)

```mermaid
flowchart LR
    subgraph Sistem["Sistem Manajemen EO"]
        UC_AUTH["UC-AUTH: Autentikasi\nPengguna / Login"]
        UC_C01["UC-C01: Mendaftar\nAkun"]
    end

    M["🧑‍💼 Manager"]
    EC["🧑‍💻 Event Coordinator"]
    S["👷 Staff Operasional"]
    F["💰 Finance"]
    C["👤 Customer"]

    M --- UC_AUTH
    EC --- UC_AUTH
    S --- UC_AUTH
    F --- UC_AUTH
    C --- UC_AUTH
    C --- UC_C01
```

### 4.1 Diagram Use Case — Manager

```mermaid
flowchart LR
    M["🧑‍💼 Manager"]

    subgraph Sistem["Sistem Manajemen EO"]
        UC_M01["UC-M01: Mengelola Data\nPengguna Internal"]
        UC_M02["UC-M02: Mengelola\nMaster Data"]
        UC_M03["UC-M03: Menyetujui\nPenawaran"]
        UC_M04["UC-M04: Melihat\nDashboard Bisnis"]
        UC_M05["UC-M05: Melihat\nLaporan"]
        INC_M03["Memeriksa Detail\nPenawaran"]
    end

    M --- UC_M01
    M --- UC_M02
    M --- UC_M03
    M --- UC_M04
    M --- UC_M05

    UC_M03 -.->|"≪include≫"| INC_M03
```

### 4.2 Diagram Use Case — Event Coordinator

```mermaid
flowchart LR
    EC["🧑‍💻 Event\nCoordinator"]

    subgraph Sistem["Sistem Manajemen EO"]
        UC_EC01["UC-EC01: Mengelola\nPermintaan Acara"]
        UC_EC02["UC-EC02: Menyusun\nPenawaran"]
        UC_EC03["UC-EC03: Merevisi\nPenawaran"]
        UC_EC04["UC-EC04: Mengelola\nEvent"]
        UC_EC05["UC-EC05: Mengelola\nTugas Event"]
        UC_EC06["UC-EC06: Mengalokasikan\nVendor"]
        UC_EC07["UC-EC07: Memantau\nPerkembangan Event"]
        UC_EC08["UC-EC08: Mengelola\nData Vendor"]
        UC_EC09["UC-EC09: Mencatat\nLog Aktivitas"]
        UC_EC10["UC-EC10: Memverifikasi\nHasil Tugas"]
        UC_EC11["UC-EC11: Mendeklarasikan\nPelaksanaan Event"]
        INC_EC02["Menghitung\nEstimasi Biaya"]
        INC_EC04["Membuat\nJadwal Event"]
        INC_EC10["Memeriksa Catatan\n& Lampiran Staff"]
        INC_EC11["Memverifikasi Seluruh\nKesiapan Event"]
        EXT_BATAL["Membatalkan\nEvent"]
        EXT_NOTIF["Mengirim Notifikasi\nKeterlambatan"]
        EXT_KEMBALI["Mengembalikan Tugas\nuntuk Perbaikan"]
    end

    EC --- UC_EC01
    EC --- UC_EC02
    EC --- UC_EC03
    EC --- UC_EC04
    EC --- UC_EC05
    EC --- UC_EC06
    EC --- UC_EC07
    EC --- UC_EC08
    EC --- UC_EC09
    EC --- UC_EC10
    EC --- UC_EC11

    UC_EC02 -.->|"≪include≫"| INC_EC02
    UC_EC02 -.->|"≪extend≫"| UC_EC03
    UC_EC04 -.->|"≪include≫"| INC_EC04
    UC_EC04 -.->|"≪extend≫"| EXT_BATAL
    UC_EC07 -.->|"≪extend≫"| EXT_NOTIF
    UC_EC10 -.->|"≪include≫"| INC_EC10
    UC_EC10 -.->|"≪extend≫"| EXT_KEMBALI
    UC_EC11 -.->|"≪include≫"| INC_EC11
```

### 4.3 Diagram Use Case — Staff Operasional

```mermaid
flowchart LR
    S["👷 Staff\nOperasional"]

    subgraph Sistem["Sistem Manajemen EO"]
        UC_S01["UC-S01: Melihat\nDaftar Tugas"]
        UC_S02["UC-S02: Memperbarui\nProgres Tugas"]
        UC_S03["UC-S03: Menambahkan\nCatatan Tugas"]
        INC_S02["Memverifikasi\nStatus Tugas"]
    end

    S --- UC_S01
    S --- UC_S02
    S --- UC_S03

    UC_S02 -.->|"≪include≫"| INC_S02
    UC_S02 -.->|"≪extend≫"| UC_S03
```

### 4.4 Diagram Use Case — Finance

```mermaid
flowchart LR
    F["💰 Finance"]

    subgraph Sistem["Sistem Manajemen EO"]
        UC_F01["UC-F01: Membuat\nTagihan"]
        UC_F02["UC-F02: Mencatat\nPembayaran Masuk"]
        UC_F03["UC-F03: Mencatat\nBiaya Vendor"]
        UC_F04["UC-F04: Melihat\nLaporan Keuangan"]
        INC_F01["Mengacu Penawaran\nyang Disetujui"]
        INC_F02["Memvalidasi Data\nPembayaran"]
        EXT_TERMIN["Membuat Tagihan\nBertahap / Termin"]
    end

    F --- UC_F01
    F --- UC_F02
    F --- UC_F03
    F --- UC_F04

    UC_F01 -.->|"≪include≫"| INC_F01
    UC_F01 -.->|"≪extend≫"| EXT_TERMIN
    UC_F02 -.->|"≪include≫"| INC_F02
```

### 4.5 Diagram Use Case — Customer (Pelanggan)

```mermaid
flowchart LR
    subgraph Sistem["Sistem Manajemen EO"]
        UC_C01["UC-C01: Mendaftar\nAkun"]
        UC_C02["UC-C02: Mengajukan\nPermintaan Acara"]
        UC_C03["UC-C03: Melihat\nPenawaran"]
        UC_C04["UC-C04: Menyetujui /\nMenolak Penawaran"]
        UC_C05["UC-C05: Memantau\nPerkembangan Event"]
        UC_C06["UC-C06: Melihat Tagihan &\nMengonfirmasi Pembayaran"]
        EXT_REVISI["Mengajukan Catatan\nRevisi Penawaran"]
        EXT_LAMPIRAN["Melampirkan Dokumen\nPendukung"]
        EXT_BUKTI["Mengunggah Bukti\nPembayaran"]
    end

    C["👤 Customer\n/ Pelanggan"]

    C --- UC_C01
    C --- UC_C02
    C --- UC_C03
    C --- UC_C04
    C --- UC_C05
    C --- UC_C06

    UC_C04 -.->|"≪extend≫"| EXT_REVISI
    UC_C02 -.->|"≪extend≫"| EXT_LAMPIRAN
    UC_C06 -.->|"≪extend≫"| EXT_BUKTI
```

---

## 5. Activity Diagram (Format Swimlane)

> [!NOTE]
> Seluruh aktivitas pada diagram di bawah telah dipetakan ke Use Case yang bersangkutan (ditandai dengan kode UC pada label node). Diagram dipecah menjadi 2 fase besar yang dihubungkan melalui **Titik Sambung ●A**, plus 1 sub-proses detail. **UC-AUTH** (Login) merupakan prasyarat untuk semua diagram dan ditampilkan secara eksplisit pada langkah awal.

### Peta Koneksi Antar Diagram

```mermaid
flowchart LR
    D1["📋 Diagram 5.1\nFase 1: Permintaan →\nKonfirmasi Event"]
    PA(("●A"))
    D2["📋 Diagram 5.2\nFase 2: Persiapan →\nPelaksanaan → Penutupan"]
    D3["📋 Diagram 5.3\nSub-proses: Detail\nStaff Mengerjakan Tugas"]

    D1 -->|"Event Terkonfirmasi"| PA --> D2
    D2 -.->|"Dipanggil saat\nlangkah Persiapan"| D3
```

---

### 5.1 Fase 1: Permintaan Acara → Konfirmasi Event

Swimlane: **Customer** · **Event Coordinator** · **Manager** · **Sistem**
Berlanjut ke → **Diagram 5.2** melalui titik sambung **●A**

```mermaid
flowchart LR

    subgraph CUS["👤 CUSTOMER"]
        direction LR
        START(["▶ Mulai"]) --> C0["UC-AUTH:\nLogin ke Portal"]
        C0 --> C1["UC-C02:\nMengisi formulir\nPermintaan Acara"]
        C2["UC-C03:\nMeninjau\nPenawaran"]
        C3{"UC-C04:\nKeputusan\nPenawaran?"}
        C4["UC-C04 extend:\nMengirim catatan\nrevisi ke EO"]
        C5["UC-C04:\nMenyetujui\nPenawaran"]
        C6["UC-C04:\nMenolak\nPenawaran"]
    end

    subgraph SIS1["⚙️ SISTEM"]
        direction LR
        S1["Menyimpan permintaan\nstatus → 'Baru'"]
        S2["Mengirim notifikasi\npermintaan baru ke EC"]
        S3["Mengubah status\n→ 'Ditolak EO'"]
        S4["Mengirim Penawaran\nke Portal Customer"]
        S5["Mengubah status\n→ 'Terkonfirmasi'"]
        S6["Membuat Ruang Kerja\nEvent / Workspace"]
        S7["Mengubah status\n→ 'Ditolak Customer'"]
    end

    subgraph EC1["🧑‍💻 EVENT COORDINATOR"]
        direction LR
        E0["UC-AUTH:\nLogin ke Sistem"]
        E1["UC-EC01:\nMenerima &\nmeninjau permintaan"]
        E2{"UC-EC01:\nLayak\ndiproses?"}
        E3["UC-EC01:\nMenolak permintaan\ndengan alasan"]
        E4["UC-EC02:\nMenganalisis kebutuhan\n& menyusun RAB"]
        E4L["UC-EC09:\nMencatat Log\nAktivitas"]
    end

    subgraph MGR["🧑‍💼 MANAGER"]
        direction LR
        M0["UC-AUTH:\nLogin ke Sistem"]
        M1["UC-M03 include:\nMemeriksa detail\nPenawaran / RAB"]
        M2{"UC-M03:\nPenawaran\ndisetujui?"}
        M3["UC-M03:\nMengembalikan dengan\ncatatan revisi"]
    end

    C1 --> S1 --> S2 --> E0 --> E1 --> E2
    E2 -->|"Tidak Layak"| E3 --> S3
    E2 -->|"Layak"| E4 --> E4L --> M0 --> M1 --> M2
    M2 -->|"Perlu Revisi"| M3 --> E4
    M2 -->|"Disetujui"| S4 --> C2 --> C3
    C3 -->|"Minta Revisi"| C4 --> E4
    C3 -->|"Ditolak"| C6 --> S7
    C3 -->|"Disetujui"| C5 --> S5 --> S6

    S6 --> PA(("●A\nLanjut ke\nDiagram 5.2"))

    style PA fill:#ff6b35,stroke:#fff,color:#fff
```

---

### 5.2 Fase 2: Persiapan → Pelaksanaan → Pembayaran → Penutupan

Swimlane: **Event Coordinator** · **Staff Operasional** · **Finance** · **Customer** · **Sistem**
Dimulai dari titik sambung **●A** (lanjutan Diagram 5.1)

#### Proses Paralel (Fork/Join) pada Fase 2

| | Fork (Percabangan Paralel) | Jalur A | Jalur B | Join (Penggabungan) |
|---|---|---|---|---|
| **Fork 1** | Setelah EC membuat daftar tugas persiapan | Menugaskan & eksekusi Tugas oleh Staff | Mengalokasikan Vendor & pencatatan biaya | Kedua jalur selesai → **"Memverifikasi kesiapan"** |
| **Fork 2** | Setelah EC mendeklarasikan pelaksanaan event | EC mengubah status Event → 'Selesai' + mencatat Log Aktivitas | Finance memulai siklus Tagihan → Pembayaran → HPP → Laba/Rugi | Kedua jalur selesai → **"Status Event → Closed"** |

```mermaid
flowchart LR

    PA(("●A\nDari\nDiagram 5.1")) --> EC_1

    subgraph EC2["🧑‍💻 EVENT COORDINATOR"]
        direction LR
        EC_1["UC-EC04:\nMembuat perencanaan\nEvent & timeline"]
        EC_2["UC-EC05:\nMembuat daftar\nTugas persiapan"]
        EC_3["UC-EC05:\nMenugaskan Tugas\nke Staff"]
        EC_4["UC-EC06:\nMengalokasikan\nVendor"]
        EC_5["UC-EC07:\nMemantau &\nmemverifikasi kesiapan"]
        EC_6{"UC-EC11:\nEvent siap\ndilaksanakan?"}
        EC_7["UC-EC07:\nMeninjau ulang\ntugas tertunda"]
        EC_8["UC-EC11:\nMendeklarasikan\nPelaksanaan Event"]
        EC_9["UC-EC04:\nMengubah status\nEvent → 'Selesai'"]
        EC_LOG["UC-EC09:\nMencatat Log\nAktivitas"]
    end

    subgraph FORKJOIN["⚡ FORK / JOIN"]
        direction LR
        FORK1["══ FORK 1 ══"]
        JOIN1["══ JOIN 1 ══"]
        FORK2["══ FORK 2 ══"]
        JOIN2["══ JOIN 2 ══"]
    end

    subgraph STF["👷 STAFF OPERASIONAL"]
        direction LR
        ST_1["UC-S01:\nMenerima &\nmelihat Tugas"]
        ST_2["Sub-proses 5.3:\nMengerjakan Tugas\n→ update progres"]
        ST_3{"Semua tugas\nterverifikasi?"}
    end

    subgraph SIS2["⚙️ SISTEM"]
        direction LR
        SY_1["Notifikasi Tugas\nbaru ke Staff"]
        SY_2["Mencatat alokasi\n& biaya vendor"]
        SY_3["Notifikasi tugas\nterverifikasi ke EC"]
        SY_4["Mengirim Tagihan\nke Portal Customer"]
        SY_5["Memperbarui status\npembayaran"]
        SY_6{"Sudah\nlunas?"}
        SY_7["Status pembayaran\n→ 'Lunas'"]
        SY_8["Menghitung Laba/Rugi\nper Event"]
        SY_9["Status Event\n→ 'Closed'"]
        FINISH(["⏹ Selesai"])
    end

    subgraph FIN["💰 FINANCE"]
        direction LR
        F_0["UC-AUTH:\nLogin ke Sistem"]
        F_1["UC-F01:\nMembuat Tagihan\n(DP / Termin / Penuh)"]
        F_2["UC-F02:\nMencatat &\nmemvalidasi pembayaran"]
        F_3["UC-F01 extend:\nMembuat Tagihan\nberikutnya"]
        F_4["UC-F03:\nMencatat biaya\nVendor sebagai HPP"]
    end

    subgraph CUS2["👤 CUSTOMER"]
        direction LR
        CU_1["UC-C06:\nMelihat Tagihan\ndi Portal"]
        CU_2["UC-C06:\nMengonfirmasi &\nmengunggah bukti bayar"]
    end

    %% Alur awal
    EC_1 --> EC_2

    %% ══ FORK 1: Tugas & Vendor paralel ══
    EC_2 --> FORK1
    FORK1 -->|"Jalur A"| EC_3 --> SY_1 --> ST_1 --> ST_2
    FORK1 -->|"Jalur B"| EC_4 --> SY_2
    ST_2 --> ST_3
    ST_3 -->|"Belum"| ST_2
    ST_3 -->|"Sudah"| SY_3

    %% ══ JOIN 1 ══
    SY_3 --> JOIN1
    SY_2 --> JOIN1
    JOIN1 --> EC_5

    EC_5 --> EC_6
    EC_6 -->|"Belum Siap"| EC_7 --> ST_2
    EC_6 -->|"Siap"| EC_8

    %% ══ FORK 2: Status & Pembayaran paralel ══
    EC_8 --> FORK2
    FORK2 -->|"Jalur A"| EC_9 --> EC_LOG
    FORK2 -->|"Jalur B"| F_0 --> F_1 --> SY_4 --> CU_1 --> CU_2 --> F_2 --> SY_5 --> SY_6
    SY_6 -->|"Belum"| F_3 --> SY_4
    SY_6 -->|"Lunas"| SY_7 --> F_4 --> SY_8

    %% ══ JOIN 2 ══
    EC_LOG --> JOIN2
    SY_8 --> JOIN2
    JOIN2 --> SY_9 --> FINISH

    style PA fill:#ff6b35,stroke:#fff,color:#fff
    style FINISH fill:#2ecc71,stroke:#fff,color:#fff
    style FORK1 fill:#333,stroke:#333,color:#fff
    style JOIN1 fill:#333,stroke:#333,color:#fff
    style FORK2 fill:#333,stroke:#333,color:#fff
    style JOIN2 fill:#333,stroke:#333,color:#fff
```

---

### 5.3 Sub-proses: Detail Staff Operasional Mengerjakan Tugas

Swimlane: **Staff Operasional** · **Event Coordinator** · **Sistem**
Sub-proses ini dipanggil pada **Diagram 5.2** setiap kali Staff mengerjakan tugas.

```mermaid
flowchart LR

    subgraph STF2["👷 STAFF OPERASIONAL"]
        direction LR
        START2(["▶ Mulai"]) --> S2_0["UC-AUTH:\nLogin ke Sistem"]
        S2_0 --> S2_2["UC-S01:\nMelihat daftar\nTugas yang ditugaskan"]
        S2_3{"Ada tugas\nyang perlu\ndikerjakan?"}
        S2_4["UC-S01:\nMemilih Tugas"]
        S2_5["UC-S02:\nMengubah status\n→ 'Sedang Dikerjakan'"]
        S2_6["Mengerjakan tugas\ndi lapangan"]
        S2_7{"UC-S03:\nPerlu catatan\n/ lampiran?"}
        S2_8["UC-S03:\nMenambahkan catatan\n& lampiran bukti"]
        S2_9["UC-S02:\nMengubah status\n→ 'Selesai'"]
        S2_10["UC-S02:\nMengerjakan ulang\nsesuai catatan"]
        DONE1(["⏹ Selesai\n(tidak ada tugas)"])
    end

    subgraph SIS3["⚙️ SISTEM"]
        direction LR
        SY3_1["Mencatat waktu\nmulai pengerjaan"]
        SY3_2["Mencatat waktu\npenyelesaian"]
        SY3_3["Notifikasi tugas selesai\nke Event Coordinator"]
        SY3_4["Memperbarui progres\nkeseluruhan Event"]
        DONE2(["⏹ Selesai"])
    end

    subgraph EC3["🧑‍💻 EVENT COORDINATOR"]
        direction LR
        EC3_1["UC-EC10:\nMenerima notifikasi &\nmemeriksa hasil tugas"]
        EC3_2{"UC-EC10:\nHasil tugas\nditerima?"}
        EC3_3["UC-EC10 extend:\nMengembalikan tugas\ndengan catatan perbaikan"]
        EC3_4["UC-EC10:\nMenandai tugas\n→ 'Terverifikasi'"]
        EC3_LOG["UC-EC09:\nMencatat Log\nAktivitas"]
    end

    S2_2 --> S2_3
    S2_3 -->|"Tidak Ada"| DONE1
    S2_3 -->|"Ada"| S2_4 --> S2_5 --> SY3_1
    SY3_1 --> S2_6 --> S2_7
    S2_7 -->|"Ya"| S2_8 --> S2_9
    S2_7 -->|"Tidak"| S2_9
    S2_9 --> SY3_2 --> SY3_3 --> EC3_1 --> EC3_2
    EC3_2 -->|"Perlu Perbaikan"| EC3_3 --> S2_10 --> S2_5
    EC3_2 -->|"Diterima"| EC3_4 --> EC3_LOG --> SY3_4 --> DONE2

    style DONE1 fill:#95a5a6,stroke:#fff,color:#fff
    style DONE2 fill:#2ecc71,stroke:#fff,color:#fff
```

---

## 6. Checklist Konsistensi

Berikut verifikasi bahwa **seluruh Use Case memiliki representasi di Activity Diagram** dan sebaliknya:

| Use Case | Muncul di Activity Diagram | Status |
|----------|---------------------------|--------|
| UC-AUTH: Autentikasi Pengguna | Diagram 5.1 (Customer, EC, Manager), 5.2 (Finance), 5.3 (Staff) | ✅ |
| UC-C01: Mendaftar Akun | Pra-kondisi untuk UC-AUTH (di luar alur operasional) | ✅ |
| UC-C02: Mengajukan Permintaan Acara | Diagram 5.1 — Customer | ✅ |
| UC-C03: Melihat Penawaran | Diagram 5.1 — Customer | ✅ |
| UC-C04: Menyetujui / Menolak Penawaran | Diagram 5.1 — Customer | ✅ |
| UC-C05: Memantau Perkembangan Event | Tersedia di Portal (fitur pasif, tidak mengubah alur) | ✅ |
| UC-C06: Melihat Tagihan & Mengonfirmasi Pembayaran | Diagram 5.2 — Customer | ✅ |
| UC-M01: Mengelola Data Pengguna Internal | Pra-kondisi (setup awal, tidak masuk alur operasional) | ✅ |
| UC-M02: Mengelola Master Data | Pra-kondisi (setup awal, tidak masuk alur operasional) | ✅ |
| UC-M03: Menyetujui Penawaran | Diagram 5.1 — Manager | ✅ |
| UC-M04: Melihat Dashboard Bisnis | Fitur monitoring pasif (tidak mengubah alur) | ✅ |
| UC-M05: Melihat Laporan | Fitur monitoring pasif (tidak mengubah alur) | ✅ |
| UC-EC01: Mengelola Permintaan Acara | Diagram 5.1 — Event Coordinator | ✅ |
| UC-EC02: Menyusun Penawaran | Diagram 5.1 — Event Coordinator | ✅ |
| UC-EC03: Merevisi Penawaran | Diagram 5.1 — loop revisi (<<extend\>>) | ✅ |
| UC-EC04: Mengelola Event | Diagram 5.2 — Event Coordinator (perencanaan & penutupan) | ✅ |
| UC-EC05: Mengelola Tugas Event | Diagram 5.2 — Event Coordinator (buat & assign tugas) | ✅ |
| UC-EC06: Mengalokasikan Vendor | Diagram 5.2 — Event Coordinator (Fork 1 Jalur B) | ✅ |
| UC-EC07: Memantau Perkembangan Event | Diagram 5.2 — Event Coordinator (verifikasi kesiapan) | ✅ |
| UC-EC08: Mengelola Data Vendor | Pra-kondisi (master data, setup sebelum alur operasional) | ✅ |
| UC-EC09: Mencatat Log Aktivitas | Diagram 5.1 (setelah menyusun RAB), 5.2 (setelah event selesai), 5.3 (setelah verifikasi tugas) | ✅ |
| UC-EC10: Memverifikasi Hasil Tugas | Diagram 5.3 — Event Coordinator | ✅ |
| UC-EC11: Mendeklarasikan Pelaksanaan Event | Diagram 5.2 — Event Coordinator (decision + deklarasi) | ✅ |
| UC-S01: Melihat Daftar Tugas | Diagram 5.2 & 5.3 — Staff Operasional | ✅ |
| UC-S02: Memperbarui Progres Tugas | Diagram 5.3 — Staff Operasional | ✅ |
| UC-S03: Menambahkan Catatan Tugas | Diagram 5.3 — Staff Operasional (<<extend\>>) | ✅ |
| UC-F01: Membuat Tagihan | Diagram 5.2 — Finance | ✅ |
| UC-F02: Mencatat Pembayaran Masuk | Diagram 5.2 — Finance | ✅ |
| UC-F03: Mencatat Biaya Vendor | Diagram 5.2 — Finance (setelah lunas) | ✅ |
| UC-F04: Melihat Laporan Keuangan | Fitur monitoring pasif (tidak mengubah alur) | ✅ |
