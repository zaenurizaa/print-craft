# PENJELASAN LENGKAP CLASS DIAGRAM DAN SEQUENCE DIAGRAM
**Aplikasi:** PrintCraft - Sistem Manajemen Workshop Sablon Kaos Terpadu  
**Framework:** Laravel (PHP MVC)  
**Basis Data:** MySQL (printcraft_db)  
**Format Dokumen:** Langsung Nama Gambar tanpa nomor, diikuti penjelasan mendalam sesuai ketentuan SRS & Dosen.

---

## DAFTAR SIMBOL DAN ARTI SIMBOL

| Simbol UML | Nama Simbol | Arti & Fungsi dalam Laravel MVC |
| :--- | :--- | :--- |
| **Class Model (Shape UML 2.5)** | Entity Class | Entitas Eloquent Model pengelola logika data bisnis dan atribut tabel database. |
| **Class Controller (<<Controller>>)** | Control Class | Pengendali alur sistem penghubung antara View dan Model/Database. |
| **Class View** | Boundary Class | File antarmuka pengguna berbasis template Blade (.blade.php). |
| **Class Database** | Database Connection | Komponen konfigurasi koneksi database MySQL (config/database.php). |
| **Panah Putus-putus (-->)** | Dependency | Ketergantungan pemanggilan (View ke Controller via Route, Controller ke Model, Model ke Database). |
| **Garis Lurus Solid (---)** | Association | Hubungan struktural relasi data bisnis antar-tabel/model dengan angka multiplicity (1, *, 0..*). |
| **Lifeline Boundary** | Boundary Lifeline | Layar antarmuka input/output tempat pengguna berinteraksi langsung. |
| **Lifeline Control** | Control Lifeline | Controller logika pengendali alur eksekusi aplikasi. |
| **Lifeline Entity** | Entity Lifeline | Model bisnis pengelola data tabel. |
| **Panah Solid Berisi (->)** | Synchronous Call | Pemanggilan method fungsi secara berurutan. |
| **Panah Melingkar** | Self-Call | Eksekusi internal method di dalam kelas yang sama. |
| **Panah Putus-putus Terbuka** | Return Message | Nilai balikan atau hasil respon data/tampilan yang dikirim kembali ke pemanggil. |

---

# BAGIAN 1: PENJELASAN CLASS DIAGRAM

---

### Gambar Class Diagram Fitur Login, Akun, dan Cabang

Gambar Class Diagram Fitur Login, Akun, dan Cabang memodelkan arsitektur kelas pada modul autentikasi dan manajemen hierarki organisasi workshop PrintCraft:
1. **Lapisan View (Boundary):**
   - view_login: Antarmuka formulir login (resources/views/auth/login.blade.php) dengan fungsi event submitLogin().
   - view_cabang: Antarmuka pengelolaan data cabang workshop (resources/views/cabang/index.blade.php) dengan fungsi event tambahCabang() dan ubahCabang().
   - view_akun: Antarmuka manajemen hak akses pengguna (resources/views/akun/index.blade.php) dengan fungsi event tambahAkun() dan ubahStatusAkun().
2. **Lapisan Controller (Control):**
   - AuthController: Mengendalikan rute otentikasi melalui method showLoginForm(), login(request), dan logout(request).
   - CabangController: Mengendalikan operasi cabang workshop via index(), store(request), dan update(request, id).
   - AkunController: Mengendalikan operasi staf workshop via index(), store(request), update(request, id), dan destroy(id).
3. **Lapisan Model (Entity):**
   - Cabang: Mewakili tabel cabang yang menyimpan data identitas workshop dengan method tambahCabang(data), ubahCabang(id, data), dan getCabangAktif().
   - Akun: Mewakili tabel akun dengan atribut kredensial pengguna (id_akun, username, password_hash, role, status_aktif) serta method autentikasi(username, password), buatAkun(data), dan ubahStatus(id, status).
4. **Relasi dan Multiplicity:**
   - Model Cabang berelasi asosiasi struktural dengan Model Akun dengan kardinalitas 1 ke * (satu cabang dapat memiliki banyak staf akun pengguna, namun setiap akun terdaftar secara unik pada satu cabang tertentu).
   - Setiap Class View terhubung ke Controller yang bersangkutan menggunakan relasi *Dependency* (pemanggilan route HTTP).
   - Setiap Class Controller terhubung ke Model yang bersangkutan melalui relasi *Dependency*.
   - Model Cabang dan Akun terhubung ke class Database via relasi *Dependency*.

---

### Gambar Class Diagram Fitur Master Data dan Kalkulator Harga

Gambar Class Diagram Fitur Master Data dan Kalkulator Harga memodelkan konfigurasi dasar produksi sablon dan logika simulasi perhitungan harga:
1. **Lapisan View (Boundary):**
   - view_master_produk: Antarmuka manajemen katalog bahan kaos (tambahProduk(), editProduk()).
   - view_tarif_sablon: Antarmuka konfigurasi tarif teknik sablon (updateTarif()).
   - view_kalkulator: Antarmuka formulir simulasi estimasi harga sablon secara otomatis (hitungEstimasi(), resetForm()).
2. **Lapisan Controller (Control):**
   - MasterDataController: Mengelola rute katalog barang dan tarif via index(), storeProduk(request), dan updateTarif(request).
   - KalkulatorController: Menghitung formula estimasi biaya secara otomatis melalui method hitung(request) dan getHargaDasar(id_produk).
3. **Lapisan Model (Entity):**
   - ProdukKaos: Entitas data katalog kain kaos polos (tipe bahan kain, ukuran, warna, harga pokok per pcs).
   - TarifSablon: Entitas tarif jenis sablon berdasarkan teknik (DTF, Rubber, Plastisol) dan ukuran area cetak (A4, A3, Logo).
   - KalkulatorHarga: Service model pengolah formula biaya dengan method kalkulasi: total = (harga_kaos + tarif_sablon + biaya_desain) * jumlah_pcs - diskon_member.
4. **Relasi dan Multiplicity:**
   - ProdukKaos berelasi asosiasi 1 ke * terhadap TarifSablon saat dikombinasikan dalam paket sablon.
   - KalkulatorHarga memiliki relasi ketergantungan (*Dependency*) terhadap ProdukKaos dan TarifSablon untuk membaca data harga dasar.
   - Model berelasi *Dependency* ke class koneksi Database.

---

### Gambar Class Diagram Fitur Landing Page dan Daftar Member

Gambar Class Diagram Fitur Landing Page dan Daftar Member memodelkan interaksi publik calon pelanggan pada portal website PrintCraft (sesuai Gambar 53 SRS):
1. **Lapisan View (Boundary):**
   - view_landing_page: Halaman utama profil workshop PrintCraft dengan tombol aksi daftarMember().
   - form_member: Formulir pendaftaran member baru dengan event prosesDaftar().
   - view_konfirmasi_member: Halaman ucapan selamat dan informasi nomor WhatsApp terdaftar dengan event tampilKonfirmasi().
2. **Lapisan Controller (Control):**
   - LandingPageController: Menangani rute beranda publik melalui method index().
   - DaftarMemberController: Menangani proses registrasi member via method create(), store(request), dan berhasil(id_customer).
3. **Lapisan Model (Entity):**
   - DaftarMember: Mengelola data dan validasi pelanggan dengan atribut identitas (id_customer, nama, nomor_whatsapp, email, alamat, id_kategori_customer) serta method validasiData(data), nomorWhatsappTerdaftar(nomor_whatsapp), ambilKategoriMember(), buatDataMember(data, id_kategori_customer), simpanMember(data_member), dan ambilInfoPotonganMember(id_kategori_customer).
   - KategoriCustomer (PC-002): Entitas acuan tingkatan keanggotaan pelanggan.
   - Pesanan (PC-003): Entitas pesanan yang terhubung ke data member.
4. **Relasi dan Multiplicity:**
   - Model DaftarMember berelasi asosiasi * ke 1 dengan KategoriCustomer (banyak member berada dalam 1 kategori).
   - Model DaftarMember berelasi asosiasi 1 ke 0..* dengan Pesanan (satu member dapat memiliki nol atau banyak pesanan).
   - Controller dan Model terhubung ke class Database via relasi *Dependency*.

---

### Gambar Class Diagram Fitur Pesanan dan Data Customer

Gambar Class Diagram Fitur Pesanan dan Data Customer memodelkan proses inti operasional transaksi workshop sablon:
1. **Lapisan View (Boundary):**
   - view_pesanan: Tampilan daftar pesanan dengan filter status produksi dan status pembayaran (tambahPesanan(), filterStatus()).
   - form_pesanan: Formulir pembuatan pesanan baru (pemilihan bahan, ukuran, jumlah pcs, file desain sablon, dan pencatatan DP minimal 50%).
   - view_detail_pesanan: Halaman rincian pengerjaan, linimasa status sablon, dan pelunasan pembayaran.
2. **Lapisan Controller (Control):**
   - PesananController: Mengendalikan aliran transaksi via index(), create(), store(request), show(id), dan updateStatusProduksi(id, status).
   - PembayaranController: Mengelola pencatatan transaksi uang muka dan pelunasan via storePembayaran(request).
3. **Lapisan Model (Entity):**
   - Customer: Entitas penyimpan data profil pembeli (id_customer, nama, nomor_whatsapp, email).
   - Pesanan: Entitas master pesanan (id_pesanan, kode_pesanan, total_harga, sisa_pembayaran, status_produksi, status_pembayaran).
   - DetailPesanan: Entitas rincian item pesanan (tipe sablon, ukuran, jumlah pcs, subtotal).
   - Pembayaran: Entitas pencatatan pembayaran DP dan pelunasan (id_pembayaran, jumlah_bayar, metode_transfer, bukti_transfer).
4. **Relasi dan Multiplicity:**
   - Customer berelasi asosiasi 1 ke 0..* dengan Pesanan (satu pelanggan dapat memiliki banyak transaksi).
   - Pesanan berelasi asosiasi 1 ke 1..* dengan DetailPesanan (satu pesanan memiliki satu atau lebih rincian item sablon).
   - Pesanan berelasi asosiasi 1 ke 1..* dengan Pembayaran (satu pesanan memiliki riwayat pembayaran DP hingga pelunasan).
   - Seluruh model berelasi *Dependency* ke class Database.

---

### Gambar Class Diagram Fitur Pengadaan Kaos

Gambar Class Diagram Fitur Pengadaan Kaos memodelkan pengelolaan rantai pasok bahan baku kaos polos ke vendor rekanan:
1. **Lapisan View (Boundary):**
   - view_pengadaan: Antarmuka monitoring status pengadaan bahan antar-cabang (buatPengadaan(), filterVendor()).
   - form_pengadaan: Formulir pemesanan stok kaos polos ke vendor (submitPengadaan()).
2. **Lapisan Controller (Control):**
   - PengadaanController: Mengendalikan siklus pengadaan melalui method index(), store(request), dan updateStatusTiba(id).
3. **Lapisan Model (Entity):**
   - Vendor: Entitas rekanan penyedia kaos (id_vendor, nama_vendor, kontak, alamat).
   - PengadaanKaos: Entitas transaksi pengadaan (id_pengadaan, nomor_po, total_pcs, biaya_pengadaan, status_pengiriman).
   - ItemPengadaan: Rincian spesifikasi kaos yang dipesan (ukuran, gramasi kain 30s/24s, warna).
4. **Relasi dan Multiplicity:**
   - Vendor berelasi asosiasi 1 ke * terhadap PengadaanKaos (satu vendor dapat menerima banyak pesanan pengadaan).
   - PengadaanKaos berelasi asosiasi 1 ke 1..* terhadap ItemPengadaan.
   - Model berelasi *Dependency* ke class Database.

---

### Gambar Class Diagram Fitur Invoice dan WOP

Gambar Class Diagram Fitur Invoice dan WOP memodelkan pencetakan berkas resmi penagihan dan surat perintah kerja produksi sablon:
1. **Lapisan View (Boundary):**
   - view_detail_pesanan: Halaman rincian pesanan yang menyediakan tombol aksi cetak (cetakInvoice(), cetakWOP()).
   - view_pdf_preview: Antarmuka penampil pratinjau berkas PDF di tab browser sebelum dicetak fisik.
2. **Lapisan Controller (Control):**
   - DokumenController: Mengatur ekstraksi data dan pemanggilan generator PDF via cetakInvoice(id_pesanan) dan cetakWOP(id_pesanan).
3. **Lapisan Library & Model:**
   - Dompdf / PDFRenderer: Service library (*barryvdh/laravel-dompdf*) pengonversi view Blade menjadi file PDF ukuran A4.
   - Pesanan & Pembayaran: Model entity penyedia data transaksi.
4. **Relasi dan Batasan Keamanan:**
   - Method cetakWOP() secara sistematis memfilter dan menyembunyikan kolom harga serta informasi nominal uang agar informasi rahasia biaya tidak beredar di area produksi bengkel sablon.

---

### Gambar Class Diagram Fitur Dashboard dan Rekap Laporan

Gambar Class Diagram Fitur Dashboard dan Rekap Laporan memodelkan visualisasi statistik transaksi dan laporan manajerial:
1. **Lapisan View (Boundary):**
   - view_dashboard: Panel utama penyaji ringkasan statistik harian (*revenue*, antrean sablon, pesanan selesai).
   - view_laporan: Antarmuka penyaring laporan keuangan berkala (filterLaporan(), eksporExcel(), eksporPDF()).
2. **Lapisan Controller (Control):**
   - DashboardController: Memproses widget data statistik harian via method index().
   - LaporanController: Menghitung kueri agregasi keuangan via method filterLaporan(cabang_id, periode).
3. **Lapisan Model (Entity):**
   - Mengakses Model Pesanan, Pembayaran, dan Cabang untuk mengeksekusi kalkulasi agregat (SUM(total_harga), SUM(jumlah_bayar), COUNT(id_pesanan)).
4. **Relasi dan Hak Akses:**
   - Owner memiliki otorisasi multi-cabang (dapat memilih seluruh cabang workshop).
   - Admin workshop dibatasi secara otomatis oleh sistem (*session branching*) hanya dapat mengakses data cabang tempat ia bertugas.

---

# BAGIAN 2: PENJELASAN SEQUENCE DIAGRAM

---

### Gambar Sequence Diagram Fitur Landing Page

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Aktor (Customer) membuka alamat website PrintCraft pada peramban web (*browser*).
2. Form view_landing_page mengeksekusi request route GET / yang memanggil fungsi daftarMember() pada antarmuka.
3. Fungsi tersebut memanggil method index() yang terdapat pada LandingPageController.
4. LandingPageController mengeksekusi operasi internal dan mengembalikan visualisasi halaman beranda landing page ke layar view_landing_page Customer. Karena halaman bersifat statis, Controller tidak memanggil Model maupun Database.

#### Komponen yang Terlibat:
1. Aktor (Customer)
2. Class View / Boundary (view_landing_page)
3. Class Controller / Control (LandingPageController)

#### Penjelasan Gambar Sequence Diagram Fitur Landing Page:
Gambar Sequence Diagram Fitur Landing Page memodelkan alur saat Customer mengakses website publik PrintCraft (sesuai Gambar 54 SRS). Customer berinteraksi langsung dengan form view_landing_page untuk membuka website. Form mengeksekusi rute fungsi daftarMember() via route GET / ke controller LandingPageController, sehingga controller mengeksekusi method internal index() dan mengembalikan tampilan visual beranda ke pengguna. Respon pesan balikan (*return message*) berhenti pada layar view_landing_page.

---

### Gambar Sequence Diagram Fitur Daftar Member

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Aktor (Customer) membuka landing page, lalu mengklik tombol "Daftar Member" pada view_landing_page.
2. Antarmuka mengeksekusi rute GET /daftar-member ke method create() pada DaftarMemberController, lalu menampilkan form pendaftaran form_member di layar Customer.
3. Customer mengisikan data diri (nama, nomor WhatsApp, email, dan alamat), kemudian menekan tombol "Daftar".
4. Antarmuka form_member mengeksekusi function prosesDaftar() via POST /daftar-member yang memanggil method store(request) pada DaftarMemberController.
5. DaftarMemberController memanggil Model DaftarMember untuk:
   - Menjalankan validasiData(data) guna memeriksa kelengkapan isian formulir.
   - Menjalankan nomorWhatsappTerdaftar(nomor_whatsapp) guna memeriksa keunikan nomor ponsel ke tabel Database.
6. Evaluasi kondisi percabangan (*Alt Fragment*):
   - **Kondisi Valid dan Nomor Belum Terdaftar [True]:**
     a. Controller memanggil ambilKategoriMember() pada Model.  
     b. Controller memanggil buatDataMember(data, id_kategori_customer) pada Model.  
     c. Controller memanggil simpanMember(data_member) untuk menyimpan data ke Database (return id_customer).  
     d. Controller memanggil ambilInfoPotonganMember(id_kategori_customer) untuk membaca diskon.  
     e. Controller menjalankan *self-call* berhasil(id_customer) dan mengarahkan navigasi ke view_konfirmasi_member.  
     f. Pada view_konfirmasi_member dijalankan *self-call* tampilKonfirmasi() untuk merender konfirmasi pendaftaran berhasil.  
   - **Kondisi Data Tidak Valid atau Nomor WhatsApp Sudah Terdaftar [False]:**
     Controller membatalkan proses simpan dan mengembalikan pesan kesalahan (return pesan error) ke tampilan form_member untuk diperbaiki pengguna.

#### Komponen yang Terlibat:
1. Aktor (Customer)
2. Class View / Boundary (view_landing_page, form_member, view_konfirmasi_member)
3. Class Controller / Control (DaftarMemberController)
4. Class Model / Entity (DaftarMember)
5. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Daftar Member:
Gambar Sequence Diagram Fitur Daftar Member memodelkan alur pendaftaran member pelanggan baru website PrintCraft (sesuai Gambar 55 SRS). Customer berinteraksi dengan antarmuka view_landing_page dan form_member. Controller menerima data pendaftaran dan memanggil model DaftarMember untuk validasi isian serta pemeriksaan nomor WhatsApp ke basis data. Jika data valid dan nomor belum pernah terdaftar, sistem menyimpan identitas member baru, menentukan kategori diskon, dan menampilkan kartu konfirmasi pada view_konfirmasi_member. Jika terjadi kesalahan atau nomor telah terdaftar, sistem menampilkan pesan error pada form pendaftaran.

---

### Gambar Sequence Diagram Fitur Login Pengguna

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Aktor (Owner, Admin) membuka peramban web dan mengakses URL login PrintCraft.
2. Form view_login memanggil request GET /login ke AuthController yang mengeksekusi method showLoginForm(), menampilkan form login.
3. Aktor mengisikan username dan password, kemudian mengklik tombol "Login".
4. Form view_login mengeksekusi request POST /login ke method login(request) pada AuthController.
5. AuthController memanggil Model Akun dengan function cekKredensial(username, password) yang memeriksa kesesuaian data ke tabel akun di Database.
6. Evaluasi kredensial:
   - Jika kredensial valid, AuthController membuat sesi login (session(role, id_cabang)) dan mengarahkan pengguna ke halaman view_dashboard sesuai hak akses cabangnya.
   - Jika username atau password salah, AuthController mengembalikan respon galat (return error) ke form view_login.

#### Komponen yang Terlibat:
1. Aktor (Owner, Admin)
2. Class View / Boundary (view_login, view_dashboard)
3. Class Controller / Control (AuthController)
4. Class Model / Entity (Akun)
5. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Login Pengguna:
Gambar Sequence Diagram Fitur Login Pengguna memodelkan alur autentikasi hak akses petugas workshop. Pengguna berinteraksi dengan formulir login untuk mengirimkan username dan password. Controller AuthController memverifikasi kredensial melalui model Akun ke basis data MySQL. Jika verifikasi cocok, sistem membentuk session dan mengalihkan halaman ke dashboard workshop. Jika gagal, pesan kesalahan ditampilkan kembali pada formulir login.

---

### Gambar Sequence Diagram Fitur Pesanan dan Validasi DP 50%

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas (Owner, Admin) membuka antarmuka formulir pesanan baru pada form_pesanan.
2. Petugas menginput identitas customer, spesifikasi kaos sablon, jumlah pcs, serta mencatat setoran uang muka (DP).
3. Form form_pesanan mengirimkan request POST /pesanan ke method store(request) pada PesananController.
4. PesananController memverifikasi nilai uang muka:
   - Apabila uang muka minimal 50% dari total tagihan (uang_muka >= total_harga * 0.50), controller memanggil Model Pesanan dan Pembayaran untuk menyimpan data ke Database, lalu menetapkan status pesanan menjadi Menunggu Antrean Produksi.
   - Apabila uang muka kurang dari 50%, sistem menolak penyimpanan dan mengembalikan respon validasi uang muka.
5. Sistem mengarahkan navigasi ke layar view_detail_pesanan yang menampilkan kode pesanan resmi.

#### Komponen yang Terlibat:
1. Aktor (Owner, Admin)
2. Class View / Boundary (form_pesanan, view_detail_pesanan)
3. Class Controller / Control (PesananController)
4. Class Model / Entity (Pesanan, Pembayaran)
5. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Pesanan dan Validasi DP 50%:
Gambar Sequence Diagram Fitur Pesanan memodelkan kepatuhan klausul bisnis utama PrintCraft di mana antrean sablon kaos hanya dapat diproses apabila pelanggan telah menyetorkan uang muka sekurang-kurangnya 50% dari total nilai transaksi. Controller memvalidasi nominal uang muka sebelum mencatat mutasi pesanan dan pembayaran ke dalam basis data.

---

### Gambar Sequence Diagram Fitur Pengadaan Stok Kaos

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas workshop membuka antarmuka pengadaan pada form form_pengadaan.
2. Petugas memilih vendor rekanan dan menginput rincian kebutuhan kaos polos (tipe bahan kain, warna, dan ukuran).
3. Form form_pengadaan mengirimkan request POST /pengadaan ke method store(request) pada PengadaanController.
4. PengadaanController memvalidasi data dan menyimpan penerbitan Purchase Order (PO) baru melalui model PengadaanKaos ke tabel Database.
5. Saat paket kaos tiba di workshop cabang, petugas mengklik tombol "Konfirmasi Tiba" pada antarmuka view_pengadaan.
6. Controller menjalankan method updateStatusTiba(id) yang memperbarui ketersediaan bahan baku di basis data, sehingga antrean sablon dapat segera dieksekusi operator.

#### Komponen yang Terlibat:
1. Aktor (Owner, Admin)
2. Class View / Boundary (form_pengadaan, view_pengadaan)
3. Class Controller / Control (PengadaanController)
4. Class Model / Entity (PengadaanKaos)
5. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Pengadaan Stok Kaos:
Gambar Sequence Diagram Fitur Pengadaan Stok Kaos memodelkan alur pemesanan bahan baku kaos polos ke vendor pihak ketiga. Sistem mencatat penerbitan PO pengadaan dan menghubungkannya dengan alokasi pesanan sablon. Ketika stok kaos tiba dan dikonfirmasi di workshop cabang, sistem memperbarui status bahan menjadi siap produksi.

---

### Gambar Sequence Diagram Fitur Cetak Invoice dan WOP

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas membuka layar detail pesanan (view_detail_pesanan) dan menekan tombol "Cetak Invoice" atau "Cetak WOP".
2. Antarmuka mengirimkan request GET /pesanan/{id}/invoice atau GET /pesanan/{id}/wop ke DokumenController.
3. DokumenController mengeksekusi cetakInvoice(id) atau cetakWOP(id) dengan memanggil data transaksi dari model Pesanan dan Pembayaran.
4. Untuk dokumen WOP, Controller secara ketat memfilter data agar kolom harga, tarif, dan informasi pembayaran dihilangkan.
5. Controller memanggil library Dompdf via generatePDF(view, data) untuk merender template Blade ukuran A4 menjadi dokumen PDF.
6. Berkas stream PDF dikembalikan ke jendela view_pdf_preview pada browser pengguna untuk dicetak langsung ke mesin printer atau diunduh.

#### Komponen yang Terlibat:
1. Aktor (Owner, Admin)
2. Class View / Boundary (view_detail_pesanan, view_pdf_preview)
3. Class Controller / Control (DokumenController)
4. Class Model / Entity (Pesanan, Pembayaran)
5. Library Cetak (Dompdf)
6. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Cetak Invoice dan WOP:
Gambar Sequence Diagram Fitur Cetak Invoice dan WOP memodelkan alur penerbitan dokumen resmi transaksi dan surat perintah kerja produksi. Controller mengekstraksi data transaksi, memformat dokumen sesuai template, dan mengonversinya menjadi berkas PDF siap cetak. Dokumen invoice memuat rincian nominal penagihan untuk customer, sedangkan lembar kerja WOP menyembunyikan kolom harga demi keamanan data bengkel sablon.

---

### Gambar Sequence Diagram Fitur Dashboard dan Rekap Laporan

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas (Owner, Admin) mengakses menu laporan pada antarmuka view_laporan dan memilih rentang tanggal serta filter cabang.
2. Form view_laporan mengirimkan request GET /laporan ke LaporanController.
3. LaporanController mengeksekusi filterLaporan(cabang_id, periode). Sistem memverifikasi hak akses: Owner dapat melihat seluruh cabang, sedangkan Admin terkunci hanya pada cabangnya sendiri.
4. Controller mengeksekusi kueri kalkulasi agregasi pendapatan, piutang, dan volume sablon melalui model Pesanan dan Pembayaran ke basis data.
5. Kumpulan data rekapitulasi dikembalikan oleh Database ke Controller.
6. Controller mengembalikan data terstruktur ke antarmuka view_laporan untuk disajikan dalam bentuk diagram grafik visual dan tabel ringkasan keuangan.

#### Komponen yang Terlibat:
1. Aktor (Owner, Admin)
2. Class View / Boundary (view_dashboard, view_laporan)
3. Class Controller / Control (LaporanController)
4. Class Model / Entity (Pesanan, Pembayaran, Cabang)
5. Class Database (Database)

#### Penjelasan Gambar Sequence Diagram Fitur Dashboard dan Rekap Laporan:
Gambar Sequence Diagram Fitur Dashboard dan Rekap Laporan memodelkan pengolahan data intelijen bisnis workshop PrintCraft. Pengguna memilih parameter periode dan cabang di antarmuka laporan. Controller menjalankan kalkulasi matematis terhadap transaksi yang tersimpan di basis data, lalu memvisualisasikan hasilnya dalam bentuk diagram tren penjualan dan tabel rekapitulasi laba rugi.

---
*Dokumen ini disusun untuk melengkapi Tugas 5 TPDB Workshop Sablon PrintCraft sesuai format penamaan tanpa nomor gambar.*
