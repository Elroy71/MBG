# Perencanaan Implementasi Teknis & Integrasi API Marketplace MBG (PRD & bukaOlshop Engine)

Dokumen ini merupakan **rencana arsitektur teknis menyeluruh (Implementation Plan)** untuk mentransformasi dan memantapkan ekosistem **Marketplace Makan Bergizi Gratis (MBG)** agar 100% selaras dengan spesifikasi bisnis pada *Product Requirement Document* (**PRD_Marketplace_MBG.docx**) dan kapabilitas mesin **bukaOlshop Open & Closed API** (**scratchpad_936oaaef.md**).

---

## 🎯 Tujuan Utama (Goal Description)

1. **Selaras 100% dengan Alur Bisnis PRD**:
   Menerapkan siklus bisnis dari *Onboarding → Wallet (Top Up Closed-loop) → Marketplace → Checkout → Payment → Split Engine (80/5/5/5/5) → Settlement (H+1)* di dalam 6 modul HTML antarmuka pengguna ramah lansia berikon vektor (*Phosphor Icons*).
2. **Integrasi Open & Closed API bukaOlshop**:
   Memetakan dengan presisi penggunaan *endpoint* Open API untuk *read-only data* dari sisi frontend (*client-side*) dan *endpoint* Closed API untuk operasi tulis/mutasi saldo dari sisi *backend/webhook* agar keamanan token tetap terjaga.
3. **Penggunaan Shortcode & Variabel Platform**:
   Memanfaatkan *shortcode* bawaan (`{{token_user}}`, `{{id_user}}`, `{{saldo_user}}`, `{{json_checkout}}`, `{{json_detail_transaksi}}`) sebagai *data bridging* real-time tanpa latensi tambahan.
4. **Keamanan & Kepatuhan Regulasi (Closed-Loop Wallet MVP)**:
   Memastikan dompet elektronik bersifat *closed-loop* (hanya untuk transaksi internal dapur MBG, tidak dapat ditarik tunai oleh Principal di fase MVP) serta dilindungi validasi *idempotency* dan limitasi akses berbasis peran (*RBAC*).

---

## 🚨 User Review Required (Perhatian Khusus & Review Anda)

> [!IMPORTANT]
> **Pemisahan Peran Open API vs Closed API (Keamanan Token)**
> Sesuai dokumentasi bukaOlshop dan best-practices keamanan, **Open API** (`https://openapi.bukaolshop.net/v1/...`) aman dipanggil langsung di dalam kode HTML/JS *client-side* karena hanya membaca data publik atau data akun yang terautentikasi oleh *shortcode* `{{token_user}}` & `{{id_user}}`.
> Sebaliknya, **Closed API** (`https://bukaolshop.net/api/v1/...` dengan `Authorization: Bearer API_KEY`) **TIDAK BOLEH** diletakkan di dalam JavaScript HTML di sisi ponsel member, karena berisiko dicuri untuk memanipulasi saldo. Closed API wajib dijalankan di server perantara (*webhook/callback processor*) atau dipanggil secara aman melalui mekanisme *override* resmi bukaOlshop.

> [!WARNING]
> **Kebijakan Split Engine & Versioning Persentase**
> Sesuai Bab 6 PRD, pembagian dana (*Revenue Sharing*) ditetapkan sebesar **80% Supplier, 5% PE1 (Pendamping), 5% PE2 (Pengawas), 5% Platform MBG, 5% Cashback Dompet**. Engine kalkulasi split di frontend (`checkout.html` dan `riwayat_transaksi.html`) bertindak sebagai **visualisasi transparan** bagi Principal dan Supplier. Eksekusi perpindahan saldo nyata (*disbursement / settlement*) wajib dilakukan melalui *cron job* / *webhook callback server* (H+1 pukul 01:00 WIB) menggunakan **Closed API (`POST /member/saldo`)**.

> [!TIP]
> **Dompet Closed-Loop (Fase MVP)**
> Untuk menghindari persyaratan izin *e-money* Bank Indonesia pada fase MVP, sistem dompet (`wallet_topup.html` & `wallet_mutasi.html`) dikunci secara sistemik: member hanya dapat menambah saldo (Top Up minimum Rp 50.000, maksimum Rp 50.000.000) dan menggunakannya untuk *Checkout* bahan pangan. Fitur *transfer antar-akun* dan *penarikan tunai (withdraw)* dinonaktifkan di antarmuka Principal.

---

## ❓ Open Questions (Pertanyaan Terbuka untuk Anda)

> [!NOTE]
> 1. **Server Webhook / Callback Processor**: Apakah Anda saat ini sudah memiliki server hosting / domain PHP/Node.js sendiri untuk menerima **Callback Transaksi Baru** dari bukaOlshop (yang nantinya bertugas mengeksekusi Closed API `POST /member/saldo` untuk pembagian split payment & cashback)? Jika belum, untuk tahap MVP kita dapat memanfaatkan skrip otomatisasi di server Anda atau menggunakan engine transaksi langsung bukaOlshop dengan visualisasi kalkulasi di frontend.
> 2. **Persetujuan (Approval) Top Up Saldo**: Apakah saat member melakukan Top Up melalui `wallet_topup.html`, konfirmasi penambahan saldo dilakukan otomatis oleh sistem bukaOlshop (melalui *payment gateway* bawaan/override) atau dikonfirmasi manual oleh Super Admin melalui dasbor?

---

## 🏗️ Pemetaan Arsitektur & Perubahan Modul (Proposed Changes)

Berikut adalah pemetaan spesifikasi teknis dan pembaruan yang akan kita pastikan tertanam sempurna pada 6 modul HTML utama kita di `d:\MBG_project\`, beserta variabel API yang disematkan:

### 1. Modul Checkout & Order Engine (`checkout.html`)
* **Fungsi PRD**: Pemesanan bahan mentah oleh Principal (Dapur MBG) dengan batas waktu bayar 30 menit, visualisasi *split payment*, dan penguncian order setelah dibayar (*Paid*).
* **Shortcode & Data Binding**:
  - `{{json_checkout}}` : Untuk membaca objek keranjang belanja live saat member berada di halaman *override transaksi*.
  - `{{token_user}}` & `{{id_user}}` : Untuk autentikasi pengguna saat memproses pesanan.
* **Integrasi API**:
  - **Open API (`GET /user/info`)**: Membaca saldo live (`jumlah_saldo`) untuk memvalidasi apakah saldo dompet cukup untuk membayar (*Real-time Stock & Balance Validation*).
  - **Visualisasi Split Engine**: Menghitung secara dinamis dari `subtotal`:
    - `Supplier (80%)` : `subtotal * 0.80`
    - `PE1 Pendamping (5%)` : `subtotal * 0.05`
    - `PE2 Pengawas (5%)` : `subtotal * 0.05`
    - `Platform MBG (5%)` : `subtotal * 0.05`
    - `Cashback Principal (5%)` : `subtotal * 0.05`
* **Penempatan di Admin**: **TOKO → API & Callback → CALLBACK → Aktifkan Override Transaksi** *(Arahkan ke halaman ini)*.

---

### 2. Modul Dompet Top-Up Closed-Loop (`wallet_topup.html`)
* **Fungsi PRD**: Layanan pengisian saldo dompet MBG oleh Principal dengan aturan minimum Rp 50.000 dan maksimum Rp 50.000.000 per transaksi.
* **Shortcode & Data Binding**:
  - `{{saldo_user}}` : Menampilkan saldo aktif saat ini secara langsung.
  - `{{token_user}}` & `{{id_user}}` : Identitas akun untuk pencatatan riwayat.
* **Integrasi API**:
  - **Open API (`GET /user/catatan?tipe=saldo`)**: Mengambil 5 riwayat pengisian saldo terakhir untuk ditampilkan di kartu riwayat ringkas bawah form top-up.
  - **Closed API Reference (`POST /member/topup`)**: Saat member memilih nominal dan menekan tombol Top Up, sistem mengalihkan/melakukan *override process* dengan parameter `token_topup` dan `validasi_jumlah_topup` (guna mencegah ketidakcocokan jumlah dana sesuai aturan baru bukaOlshop).
* **Penempatan di Admin**: **TOKO → API & Callback → CALLBACK → Aktifkan Override Saldo** *(Arahkan ke halaman ini)*.

---

### 3. Modul Beranda Etalase & Filter Bahan (`marketplace_home.html`)
* **Fungsi PRD**: Menampilkan daftar produk bahan mentah (Beras, Sayur, Daging, Minyak) dari Supplier dengan indikator stok real-time (*Ready Stock / Menipis / Habis*) dan navigasi ramah lansia.
* **Shortcode & Data Binding**:
  - `{{token_user}}` & `{{id_user}}` : Parameter wajib di setiap panggilan Open API.
* **Integrasi API**:
  - **Open API (`GET /app/kategori`)**: Mengambil daftar kategori produk (Utama dan Sub-kategori) untuk ditampilkan pada baris filter *pill* berikon vektor (*Phosphor*).
  - **Open API (`GET /app/produk?page=1&total_data=20`)**: Mengambil daftar produk aktif (`status_produk = live`), menampilkan `nama_produk`, `harga_produk`, `stok`, dan `url_produk`.
  - **Validasi Stok Real-Time**: Jika `stok <= 0`, kartu otomatis diberi label badge **"Habis"** dan tombol beli dinonaktifkan (*disabled*) untuk mencegah *checkout* barang kosong sesuai Bab 6 PRD.
* **Penempatan di Admin**: **TOKO → Tampilan Aplikasi → Tampilan Olshop → HOME / JELAJAH → Tambah Widget → `HTML/CSS/JavaScript`**.

---

### 4. Modul Pelacakan & Lacak Pesanan (`riwayat_transaksi.html`)
* **Fungsi PRD**: Melacak perjalanan pesanan dari *Draft → Waiting Payment → Paid → Processing → Shipping → Completed*, konfirmasi penerimaan barang, dan pengajuan komplain/retur.
* **Shortcode & Data Binding**:
  - `{{json_detail_transaksi}}` : Membaca seluruh data pesanan, nomor resi kurir, alamat tujuan, dan daftar barang yang dipesan.
* **Integrasi API**:
  - **Open API (`GET /user/transaksi`)**: Sinkronisasi riwayat transaksi member.
  - **Status Mapping**:
    - `pending` / `menunggu` $\rightarrow$ Step 2 (Tunggu Bayar)
    - `lunas` $\rightarrow$ Step 3 (Pembayaran Lunas / *Paid*)
    - `diproses` $\rightarrow$ Step 4 (Disiapkan Supplier / *Processing*)
    - `dikirim` $\rightarrow$ Step 5 (Sedang Dikirim / *Shipping*)
    - `selesai` $\rightarrow$ Step 6 (Pesanan Selesai / *Completed*)
  - **Konfirmasi Terima & Aksi Komplain**: Menyediakan tombol konfirmasi penerimaan yang akan mengubah status menjadi *Completed* dan memicu pencatatan audit log untuk persiapan *settlement* H+1.
* **Penempatan di Admin**: **TOKO → Tampilan Aplikasi → Menu & Kostum Halaman → Buat Halaman (Tujuan: `HTML dan Teks`)**.

---

### 5. Modul Buku Kas & Riwayat Mutasi (`wallet_mutasi.html`)
* **Fungsi PRD**: Buku mutasi keuangan SPJ (Surat Pertanggungjawaban) dapur MBG yang mencatat setiap penambahan saldo (*Top Up*, *Cashback*) dan pengurangan saldo (*Checkout*) secara transparan.
* **Shortcode & Data Binding**:
  - `{{saldo_user}}` : Menampilkan total kas saat ini.
  - `{{token_user}}` & `{{id_user}}` : Autentikasi panggilan data mutasi.
* **Integrasi API**:
  - **Open API (`GET /user/catatan?tipe=saldo&total_data=30`)**: Mengambil daftar lengkap catatan saldo.
  - **Filter & Grouping Kronologis**: Memisahkan parameter `tipe_jumlah` (`tambah` vs `kurang`) menjadi filter tab, serta mengelompokkan entri berdasarkan tanggal (`tanggal`) agar mudah dibaca oleh bendahara dapur atau lansia.
  - **Bridging Transaksi**: Jika mutasi memiliki `link_transaksi`, disediakan tombol/link tautan untuk langsung membuka detail pesanan terkait.
* **Penempatan di Admin**: **TOKO → Tampilan Aplikasi → Menu & Kostum Halaman → Buat Halaman (Tujuan: `HTML dan Teks`)**.

---

### 6. Modul Portal & Manajemen Supplier (`supplier_produk.html`)
* **Fungsi PRD**: Portal bagi Supplier untuk mengelola stok bahan pangan, melihat statistik produk (*Live, Review, Non-aktif*), dan mengajukan produk baru untuk diverifikasi Super Admin.
* **Shortcode & Data Binding**:
  - `{{token_user}}` & `{{id_user}}` : Mengidentifikasi Supplier yang sedang login.
* **Integrasi API**:
  - **Open API (`GET /app/produk?page=1&total_data=50`)**: Menampilkan seluruh katalog produk milik toko untuk dimonitor stok dan statusnya.
  - **Simulasi Upload & Stok**: Menyediakan antarmuka penambahan produk baru yang selaras dengan spesifikasi **Closed API (`POST /produk/create`)** dengan parameter `nama_barang`, `harga_barang`, `stok_barang`, dan `id_kategori`. Pada UI ini, produk baru otomatis berstatus *Review* sebelum disetujui Super Admin sesuai aturan *RBAC* Bab 4 PRD.
* **Penempatan di Admin**: **TOKO → Tampilan Aplikasi → Menu & Kostum Halaman → Buat Halaman (Tujuan: `HTML dan Teks`)**.

---

## 🔒 Matriks Keamanan & Alur Settlement Webhook (Backend Architecture Reference)

Sesuai spesifikasi PRD Bab 5, 9, dan 10, berikut adalah desain alur integrasi server belakang (*backend webhook*) yang bekerja berdampingan dengan 6 modul HTML kita:

```
[Principal / Supplier (Aplikasi My MBG)]
       |
       | (1. Berinteraksi via 6 Modul HTML / Shortcode {{token_user}})
       v
[Open API bukaOlshop (openapi.bukaolshop.net/v1)]
       |
       | (2. Webhook Callback dikirim saat order/topup terjadi)
       v
[Server Webhook / Callback Processor Kita (PHP/Node.js)]
       |
       +---> (Validasi Secret Key & Idempotency Key)
       |
       +---> [Closed API bukaOlshop (bukaolshop.net/api/v1)]
       |          |-- PATCH /transaksi/id (Update Resi/Status)
       |          |-- POST /member/saldo (Settlement H+1 pukul 01:00 WIB)
       |          |    |-- Supplier : +80% Saldo
       |          |    |-- PE1      : +5% Saldo
       |          |    |-- PE2      : +5% Saldo
       |          |    |-- Platform : +5% Saldo
       |          |    +-- Cashback : +5% Saldo ke Principal
       |          +-- POST /member/notifikasi (Kirim Push Notif Android)
```

---

## 🧪 Verification Plan (Rencana Verifikasi & Pengujian)

Untuk memastikan seluruh modul bekerja sempurna di lingkungan bukaOlshop, kita akan menjalankan pengujian dua lapis:

### 1. Verifikasi Otomatis & Inspeksi Kode (Automated / Code Check)
* **Validasi Sintaks & Shortcode**: Memeriksa bahwa setiap file HTML kita memiliki penanganan *Fallback / Mock Data* ketika `{{json_checkout}}` atau token API belum dieksekusi oleh engine (sehingga layar tidak pernah *blank white*).
* **Validasi Ikon & Kontras**: Memeriksa bahwa 100% ikon menggunakan `ph-bold` / `ph-duotone` dari `@phosphor-icons/web@2.1.1` tanpa ada sisa karakter emoji, serta ukuran font sesuai standar aksesibilitas lansia (`Plus Jakarta Sans`).

### 2. Verifikasi Manual di Admin & Ponsel Anda (Manual Verification)
* **Pengujian Top Up Override**:
  1. Pasang `wallet_topup.html` di menu **CALLBACK $\rightarrow$ Override Saldo**.
  2. Buka aplikasi `My MBG` di ponsel, klik tombol **Top Up**.
  3. Pastikan layar beralih ke UI baru kita, klik tombol nominal cepat **Rp 100.000**, dan verify kalkulasi minimum/maksimum berjalan baik.
* **Pengujian Checkout & Split Calculation**:
  1. Pasang `checkout.html` di menu **CALLBACK $\rightarrow$ Override Transaksi**.
  2. Masukkan 2 produk ke keranjang di aplikasi, lalu klik **Checkout**.
  3. Pastikan hitung mundur 30 menit berjalan aktif, alamat otomatis terisi dari akun, dan rincian pembagian dana (*Split Payment*) 80/5/5/5/5% terhitung akurat sesuai subtotal belanja.
* **Pengujian Mutasi & Pelacakan Pesanan**:
  1. Buka menu **Riwayat Saldo** (`wallet_mutasi.html`) dan **Lacak Pesanan** (`riwayat_transaksi.html`).
  2. Verifikasi bahwa pengelompokan tanggal kronologis dan status 6 langkah (*tracker*) rendered dengan kontras tajam serta tombol aksi merespon dengan cepat saat disentuh.
