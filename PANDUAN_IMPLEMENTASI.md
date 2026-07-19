# 📱 Panduan Implementasi My MBG — bukaOlshop Admin
### Cara Pasang 6 Modul HTML ke Aplikasi, Step-by-Step (Akurat berdasarkan Screenshot)

> **Prasyarat**: Login ke aplikasi bukaOlshop sebagai Admin/Pemilik Toko.

---

## 🗺️ Peta Jalur Lengkap (Revisi Final)

```
bukaOlshop Admin App → Tab TOKO
│
├── Tampilan Aplikasi
│   ├── Tampilan Olshop → HOME       → marketplace_home.html
│   └── Menu & Kostum Halaman        → wallet_mutasi.html
│                                    → riwayat_transaksi.html
│                                    → supplier_produk.html
│
└── Personal Branding → KOSTUM HTML
    ├── Kostum Halaman Checkout      → checkout.html
    ├── Kostum Halaman TopUp Saldo   → wallet_topup.html
    └── Kostum Halaman Detail Transaksi → riwayat_transaksi.html (alternatif)
```

> [!NOTE]
> **Keranjang & Akun (Fitur Native):**
> Halaman **Keranjang Belanja (`/cart/`)** dan **Akun (`/akun/`)** menggunakan antarmuka asli (*default*) BukaOlshop yang sudah sangat lengkap, stabil, dan terintegrasi otomatis. Tidak diperlukan file HTML kustom untuk kedua menu tersebut.

---

## 💡 Panduan Pengaturan Tinggi Layout (Webview)

Saat memasukkan kode HTML ke editor **HTML/CSS/JavaScript**, Anda akan menemukan 3 opsi pengaturan tinggi. Berikut panduan memilihnya untuk file MBG:

| Opsi | Cocok Untuk | Gunakan Untuk File MBG |
|------|-------------|------------------------|
| **WRAP_CONTENT** | HTML sederhana, bisa dipakai bareng widget lain. Perubahan via JS kadang tidak muncul. | ❌ Tidak disarankan (file kita kompleks) |
| **MATCH_PARENT** | HTML kompleks, floating elements, elemen tersembunyi. Memenuhi satu layar penuh. | ✅ **Gunakan ini untuk semua file MBG** |
| **Fixed Height** | HTML kompleks tapi ingin widget lain tetap tampil. Mulai dari 1500px, coba-coba. | ⚠️ Gunakan jika MATCH_PARENT bermasalah |

> [!IMPORTANT]
> Karena semua file MBG memiliki struktur kompleks (bottom bar fixed, modal, animasi), pilih **MATCH_PARENT** saat memasukkan kode. Hapus widget HOME lainnya agar loading lebih cepat.

---

## 📦 MODUL 1 — `marketplace_home.html`
**Nama Menu di Aplikasi:** `Beranda MBG` / `Marketplace MBG`

**Fungsi:** Halaman utama etalase produk bahan mentah, filter kategori, dan info saldo Principal.

### 📍 Jalur
```
TOKO → Tampilan Aplikasi → Tampilan Olshop → Tab HOME → (+) → HTML/CSS/JavaScript
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Tampilan Olshop** (bagian Tampilan Aplikasi)
3. Pastikan tab **HOME** aktif → ketuk tombol **`+`** (ungu, pojok kanan bawah)
4. Pilih **`HTML/CSS/JavaScript`**
5. Di halaman editor **HTML**:
   - **Nama Widget:** isi `Marketplace MBG`
   - **Pengaturan Tinggi Layout:** pilih **`MATCH_PARENT`** ✅
   - **Area kode:** ketuk kolom teks → **paste seluruh isi `marketplace_home.html`**
6. Ketuk **✓** (pojok kanan atas) untuk menyimpan

### ✅ Verifikasi
Buka aplikasi → Tab **Home** → Muncul daftar produk bahan mentah dengan filter kategori dan header saldo.

> **Tips:** Jika HOME sudah ada widget lain (List Kategori, Produk Unggulan, dll.), **hapus dulu** agar tidak bentrok dengan `marketplace_home.html`.

---

## 📦 MODUL 2 — `checkout.html`
**Nama Menu di Aplikasi:** (Otomatis — muncul saat member Checkout)

**Fungsi:** Override halaman checkout — tampil otomatis saat member tekan bayar. Menampilkan countdown 30 menit, ringkasan pesanan, dan distribusi dana 80/5/5/5/5%.

### 📍 Jalur
```
TOKO → Personal Branding → Tab KOSTUM HTML → Kostum Halaman Checkout
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Personal Branding** (bagian Tampilan Aplikasi)
3. Ketuk tab **KOSTUM HTML** (tab kanan)
4. Ketuk **`Kostum Halaman Checkout`**
   > *"Gunakan HTML sebagai halaman ketika membuat sebuah transaksi baru"*
5. Di halaman editor:
   - **Pilih Sumber Script:** pilih **`Input HTML/CSS/JS`** (radio button pertama)
   - **Area kode:** paste seluruh isi **`checkout.html`**
6. Ketuk **✓** untuk menyimpan

### ✅ Verifikasi
Masukkan produk ke keranjang → Ketuk **Checkout/Bayar** → Halaman `checkout.html` muncul dengan countdown timer dan tabel split payment.

---

## 📦 MODUL 3 — `wallet_topup.html`
**Nama Menu di Aplikasi:** (Otomatis — muncul saat member Top Up)

**Fungsi:** Override halaman top-up — tampil saat member tekan tombol **Top Up**. Menampilkan saldo aktif, pilihan nominal, dan riwayat mutasi.

### 📍 Jalur
```
TOKO → Personal Branding → Tab KOSTUM HTML → Kostum Halaman TopUp Saldo
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Personal Branding**
3. Ketuk tab **KOSTUM HTML**
4. Ketuk **`Kostum Halaman TopUp Saldo`**
   > *"Gunakan HTML sebagai halaman ketika member ingin membuat topup baru"*
5. Di halaman editor:
   - **Pilih Sumber Script:** pilih **`Input HTML/CSS/JS`**
   - **Area kode:** paste seluruh isi **`wallet_topup.html`**
6. Ketuk **✓** untuk menyimpan

### ✅ Verifikasi
Buka aplikasi → Ketuk **Top Up** di header → Halaman `wallet_topup.html` muncul dengan hero saldo navy, pilihan nominal, dan riwayat mutasi di bawah.

---

## 📦 MODUL 4 — `riwayat_transaksi.html`
**Nama Menu di Aplikasi:** (Otomatis — muncul saat member buka detail transaksi)

**Fungsi:** Override halaman detail transaksi — tampil saat member buka detail pesanan. Menampilkan tracker 6 langkah, nomor resi, distribusi dana, tombol Konfirmasi/Komplain.

### 📍 Jalur (Opsi Terbaik)
```
TOKO → Personal Branding → Tab KOSTUM HTML → Kostum Halaman Detail Transaksi
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Personal Branding**
3. Ketuk tab **KOSTUM HTML**
4. Ketuk **`Kostum Halaman Detail Transaksi`**
   > *"Gunakan HTML sebagai halaman ketika melihat detail transaksi"*
5. Di halaman editor:
   - **Pilih Sumber Script:** pilih **`Input HTML/CSS/JS`**
   - **Area kode:** paste seluruh isi **`riwayat_transaksi.html`**
6. Ketuk **✓** untuk menyimpan

### ✅ Verifikasi
Buka aplikasi → Tab **Transaksi** → Ketuk salah satu pesanan → Halaman `riwayat_transaksi.html` muncul dengan tracker status dan tombol aksi di bawah.

> **Info Shortcode:** `{{json_detail_transaksi}}` otomatis diisi engine bukaOlshop saat dibuka dari dalam detail transaksi member.

---

## 📦 MODUL 5 — `wallet_mutasi.html`
**Nama Menu di Aplikasi:** `Riwayat Saldo`

**Fungsi:** Buku kas digital — menampilkan mutasi saldo uang masuk (+) dan keluar (-) berkelompok per tanggal.

### 📍 Jalur
```
TOKO → Tampilan Aplikasi → Menu & Kostum Halaman → (+) → Buat Halaman
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Menu & Kostum Halaman** (bagian Tampilan Aplikasi)
3. Ketuk tombol **`+`** (pojok kanan bawah)
4. Isi form **"Buat Halaman"**:

   | Field | Nilai |
   |-------|-------|
   | **Judul** | `Riwayat Saldo` |
   | **Tujuan** | Pilih **`HTML dan Teks`** dari dropdown |
   | **Icon Halaman** | Ketuk gambar → upload icon dompet |
   | **Aktif** | Toggle **ON** ✅ |
   | **Sembunyikan dari 'Halaman Kami'** | Kosongkan (tidak perlu disembunyikan) |

5. Setelah pilih "HTML dan Teks" → muncul area editor → paste seluruh isi **`wallet_mutasi.html`**
6. Ketuk **✓** (pojok kanan atas) untuk menyimpan

### ✅ Verifikasi
Menu **Riwayat Saldo** muncul di daftar Menu & Kostum Halaman → Buka dari aplikasi → Muncul daftar mutasi dengan warna hijau (+) dan merah (-) per tanggal.

---

## 📦 MODUL 6 — `supplier_produk.html`
**Nama Menu di Aplikasi:** `Portal Supplier`

**Fungsi:** Dashboard khusus Supplier untuk pantau stok, status produk (Live/Review/Non-aktif), dan ajukan produk baru ke admin.

### 📍 Jalur
```
TOKO → Tampilan Aplikasi → Menu & Kostum Halaman → (+) → Buat Halaman
```

### Langkah-Langkah

1. Buka aplikasi bukaOlshop → Tab **TOKO**
2. Ketuk **Menu & Kostum Halaman**
3. Ketuk tombol **`+`**
4. Isi form **"Buat Halaman"**:

   | Field | Nilai |
   |-------|-------|
   | **Judul** | `Portal Supplier` |
   | **Tujuan** | Pilih **`HTML dan Teks`** dari dropdown |
   | **Icon Halaman** | Upload icon toko/gudang |
   | **Aktif** | Toggle **ON** ✅ |
   | **Sembunyikan dari 'Halaman Kami'** | ✅ **Centang** — agar tidak terlihat member biasa |

5. Paste seluruh isi **`supplier_produk.html`** di area editor
6. Ketuk **✓** untuk menyimpan

### ✅ Verifikasi
Bagikan link halaman langsung ke akun Supplier → Muncul statistik produk, daftar dengan badge Live/Review, dan tombol Tambah Produk.

---

## 🗂️ Ringkasan Lengkap Semua Modul

| File | Nama Menu | Jalur Admin | Tipe |
|------|-----------|-------------|------|
| `marketplace_home.html` | `Marketplace MBG` | TOKO → Tampilan Olshop → HOME → + → **HTML/CSS/JS** | Widget |
| `checkout.html` | *(Otomatis saat Checkout)* | TOKO → Personal Branding → **KOSTUM HTML** → Kostum Halaman Checkout | Kostum HTML |
| `wallet_topup.html` | *(Otomatis saat Top Up)* | TOKO → Personal Branding → **KOSTUM HTML** → Kostum Halaman TopUp Saldo | Kostum HTML |
| `riwayat_transaksi.html` | *(Otomatis saat buka Transaksi)* | TOKO → Personal Branding → **KOSTUM HTML** → Kostum Halaman Detail Transaksi | Kostum HTML |
| `wallet_mutasi.html` | `Riwayat Saldo` | TOKO → Menu & Kostum Halaman → + → **HTML dan Teks** | Kostum Halaman |
| `supplier_produk.html` | `Portal Supplier` | TOKO → Menu & Kostum Halaman → + → **HTML dan Teks** *(tersembunyi)* | Kostum Halaman |

---

## 📋 Fitur Kostum HTML Lain yang Tersedia (Referensi)

Dari halaman **Personal Branding → KOSTUM HTML**, tersedia juga slot kosong untuk kebutuhan lanjutan:

| Slot Kostum | Kegunaan |
|-------------|----------|
| Kostum Halaman Login | Kustomisasi halaman login & pendaftaran |
| Kostum Detail Produk | Kustomisasi halaman detail produk |
| Kostum Halaman Transaksi Baru | Notifikasi saat transaksi member berhasil |
| Kostum Halaman Cetak Struk | Struk resi/print thermal bluetooth |
| Kostum Input PIN | Halaman input PIN saldo |
| Kostum Email Pendaftaran Member | Template email konfirmasi member |

> [!NOTE]
> **Kostum Halaman Login** memerlukan paket **BISNIS** di bukaOlshop. Fitur lainnya tersedia di paket standar.

---

## ⚠️ Catatan Penting Sebelum Deploy

> [!IMPORTANT]
> **Pilih MATCH_PARENT** untuk semua file MBG agar tampilan fullscreen dan bottom bar fixed bekerja dengan benar.

> [!WARNING]
> **Shortcode hanya aktif di dalam App** — `{{saldo_user}}`, `{{token_user}}`, `{{id_user}}`, `{{json_checkout}}`, `{{json_detail_transaksi}}` hanya diganti engine bukaOlshop jika dibuka dari dalam aplikasi. Jika dibuka di browser biasa = teks literal. Ini normal.

> [!NOTE]
> **Urutan Deploy yang Disarankan:**
> 1. `marketplace_home.html` — Beranda langsung aktif
> 2. `wallet_topup.html` — Top Up bisa diuji
> 3. `checkout.html` — Alur beli bisa diuji
> 4. `riwayat_transaksi.html` — Detail pesanan aktif
> 5. `wallet_mutasi.html` dan `supplier_produk.html` — Menu tambahan
