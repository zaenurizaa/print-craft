# DOKUMEN TUGAS 5 TPDB: CLASS DIAGRAM DAN SEQUENCE DIAGRAM LENGKAP
**Aplikasi:** PrintCraft - Sistem Manajemen Workshop Sablon Kaos Terpadu  
**Arsitektur Framework:** Laravel (PHP MVC)  
**Basis Data:** MySQL (`printcraft_db`)  
**Penyesuaian Ketentuan:** Sinkron dengan Dokumen SRS Revisi Terakhir (PC-001 s.d. PC-006) & Standar Dosen

---

## PANDUAN PENGGUNAAN KODE DRAW.IO

Untuk melihat, mengedit, atau mengekspor diagram ke format gambar (PNG/PDF/SVG) dari kode Draw.io XML yang ada di dokumen ini:
1. Buka situs [draw.io](https://app.diagrams.net/) di browser atau buka aplikasi Draw.io Desktop.
2. Buat diagram baru (*Create New Diagram* -> *Blank Diagram*).
3. Pada bilah menu atas, klik menu **Arrange** (atau klik ikon **+** di toolbar) -> pilih **Insert** -> pilih **Advanced** -> pilih **XML...**.
4. Salin (*copy*) seluruh kode XML yang terdapat di dalam blok kode ```xml ... ``` di bawah ini.
5. Tempelkan (*paste*) ke kotak dialog XML pada Draw.io, lalu klik tombol **Apply**.
6. Diagram akan langsung muncul lengkap dengan bentuk (*shape*), teks atribut/operasi, garis relasi panah, dan angka *multiplicity*.
7. Diagram dapat langsung diekspor melalui menu **File** -> **Export as** -> **PNG** (centang *Include a copy of my diagram*).

---

## TABEL SIMBOL DAN ARTI SIMBOL UML

Sebelum penyajian diagram, berikut adalah tabel simbol UML yang digunakan pada Class Diagram dan Sequence Diagram sesuai panduan dosen:

| Simbol / Notasi | Nama Notasi | Keterangan & Penggunaan pada Laravel MVC |
| :--- | :--- | :--- |
| **Kotak Class (Shape UML 2.5 / Class 5)** | Class Model (Entity) | Memodelkan kelas entitas Eloquent ORM yang memiliki field atribut tabel dan method operasi logika data bisnis. |
| **Kotak Class (<<Controller>>)** | Class Controller (Control) | Memodelkan kelas controller penghubung (*control class*) yang memproses request route, memvalidasi input, memanggil model, dan mengembalikan view. |
| **Kotak Class (View)** | Class View (Boundary) | Memodelkan file template Blade (`.blade.php`) sebagai antarmuka antarmuka pengguna (*user interface*). Berisi fungsi pemanggilan event/tombol. |
| **Kotak Class (Database)** | Database Connection | Memodelkan koneksi basis data global MySQL melalui konfigurasi database Laravel (`config/database.php`). |
| **Panah Putus-putus Terbuka (`-->`)** | Dependency Relasi (<<Dependency>>) | Menunjukkan ketergantungan antar-class, misal: View memanggil Controller via Route HTTP, Controller memanggil Model, atau Model mengakses Database. |
| **Garis Lurus Solid (`---`)** | Association Relasi | Menunjukkan hubungan asosiasi struktural antar-entitas data bisnis (Model ke Model). |
| **Multiplicity (1, *, 1..*, 0..*)** | Kardinalitas Relasi | Menunjukkan jumlah relasi data, contoh: 1 Cabang memiliki * (banyak) Akun; 1 Customer memiliki 0..* Pesanan. |
| **Stickman** | Actor Lifeline | Pengguna yang berinteraksi langsung dengan antarmuka sistem (Customer, Owner, Admin). |
| **Lifeline Boundary (Bulatan bergaris kiri)** | View Boundary Lifeline | Komponen antarmuka (Blade form/halaman) tempat interaksi pengguna berlangsung. |
| **Lifeline Control (Bulatan berpanah melingkar)** | Controller Lifeline | Komponen logika pengendali alur aplikasi (Laravel Controller). |
| **Lifeline Entity (Bulatan bergaris bawah)** | Model Entity Lifeline | Komponen pengelola data bisnis (Eloquent Model). |
| **Panah Solid Berisi (`->`)** | Synchronous Message / Call | Pemanggilan method atau rute fungsi secara berurutan. |
| **Panah Melingkar ke Diri Sendiri** | Self-Call Message | Eksekusi internal method di dalam class yang sama (misal `index()`, `hitung()`). |
| **Panah Putus-putus Terbuka (`-->`)** | Return Message | Nilai balikan atau hasil respon data/tampilan yang dikirim kembali ke pemanggil. |

---

# BAGIAN 1: KUMPULAN CLASS DIAGRAM (SEMUA FITUR PC-001 s.d. PC-006)

Tabel Pemetaan Fitur & Class Diagram:

| Kategori Pengguna | ID Fitur | Fitur | Nomor Diagram | File Draw.io |
| :---: | :---: | :---: | :---: | :---: |
| Owner, Admin | PC-001 | Login, Akun, dan Cabang | Gambar 7 TPDB | `class-diagram-pc001.drawio` |
| Owner, Admin | PC-002 | Master Data dan Kalkulator Harga | Gambar 6 TPDB | `class-diagram-pc002.drawio` |
| Customer | PC-003 | Landing Page dan Daftar Member | Gambar 5 TPDB / Gbr 53 SRS | `class-diagram-pc003.drawio` |
| Owner, Admin | PC-003 | Pesanan Sablon dan Data Customer | Gambar 5b TPDB | `class-diagram-pesanan.drawio` |
| Owner, Admin | PC-004 | Pengadaan Stok Kaos Polos | Gambar 8 TPDB | `class-diagram-pc004.drawio` |
| Owner, Admin | PC-005 | Invoice dan Work Order Production (WOP) | Gambar 9 TPDB | `class-diagram-pc005.drawio` |
| Owner, Admin | PC-006 | Dashboard dan Rekap Laporan Keuangan | Gambar 10 TPDB | `class-diagram-pc006.drawio` |

---

### 1.1 Class Diagram Fitur Login, Akun, dan Cabang (PC-001)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pc001" name="Class Diagram PC-001">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="50" y="50" width="180" height="85" as="geometry" />
        </mxCell>

        <!-- Cabang Model -->
        <mxCell id="cls_cabang" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Cabang&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_cabang: int&lt;br/&gt;+ nama_cabang: String&lt;br/&gt;+ alamat: String&lt;br/&gt;+ no_telp: String&lt;br/&gt;+ status_aktif: boolean&lt;hr size=&quot;1&quot;/&gt;+ tambahCabang(data)&lt;br/&gt;+ ubahCabang(id, data)&lt;br/&gt;+ getCabangAktif()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="360" y="45" width="220" height="150" as="geometry" />
        </mxCell>

        <!-- Akun Model -->
        <mxCell id="cls_akun" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Akun&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_akun: int&lt;br/&gt;+ id_cabang: int&lt;br/&gt;+ nama: String&lt;br/&gt;+ username: String&lt;br/&gt;+ password_hash: String&lt;br/&gt;+ role: enum('owner', 'admin')&lt;br/&gt;+ status_aktif: boolean&lt;hr size=&quot;1&quot;/&gt;+ autentikasi(username, password)&lt;br/&gt;+ buatAkun(data)&lt;br/&gt;+ ubahStatus(id, status)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="720" y="40" width="260" height="180" as="geometry" />
        </mxCell>

        <!-- AuthController -->
        <mxCell id="cls_auth_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;AuthController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ showLoginForm()&lt;br/&gt;+ login(request)&lt;br/&gt;+ logout(request)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="50" y="290" width="180" height="90" as="geometry" />
        </mxCell>

        <!-- CabangController -->
        <mxCell id="cls_cab_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;CabangController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ store(request)&lt;br/&gt;+ update(request, id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="380" y="290" width="180" height="90" as="geometry" />
        </mxCell>

        <!-- AkunController -->
        <mxCell id="cls_akn_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;AkunController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ store(request)&lt;br/&gt;+ update(request, id)&lt;br/&gt;+ destroy(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="740" y="290" width="200" height="100" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_login" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_login&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ submitLogin()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="60" y="470" width="160" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_cabang" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_cabang&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ tambahCabang()&lt;br/&gt;+ ubahCabang()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="385" y="470" width="170" height="70" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_akun" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_akun&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ tambahAkun()&lt;br/&gt;+ ubahStatusAkun()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="755" y="470" width="170" height="70" as="geometry" />
        </mxCell>

        <!-- Association: Cabang -> Akun -->
        <mxCell id="rel_cab_akn" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_cabang" target="cls_akun">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="lbl_mult_cab" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=12;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="585" y="100" width="20" height="20" as="geometry" />
        </mxCell>
        <mxCell id="lbl_mult_akn" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=12;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="695" y="100" width="20" height="20" as="geometry" />
        </mxCell>

        <!-- Dependencies to Database -->
        <mxCell id="dep_cab_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cabang" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_akn_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.2;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_akun" target="cls_db">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry">
            <Array as="points"><mxPoint x="770" y="15" /><mxPoint x="140" y="15" /></Array>
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependencies Controller to Model -->
        <mxCell id="dep_auth_akn" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=1;exitY=0.2;exitDx=0;exitDy=0;entryX=0;entryY=0.85;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_auth_ctrl" target="cls_akun">
          <mxGeometry x="-0.3" y="10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_cabctrl_cab" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cab_ctrl" target="cls_cabang">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_aknctrl_akn" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_akn_ctrl" target="cls_akun">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <!-- Dependencies Controller to View -->
        <mxCell id="dep_auth_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_auth_ctrl" target="cls_v_login">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_cab_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cab_ctrl" target="cls_v_cabang">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_akn_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_akn_ctrl" target="cls_v_akun">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <!-- Caption -->
        <mxCell id="cap_fig7" value="&lt;b&gt;Gambar 7. Class Diagram Fitur Login, Akun, Cabang (PC-001)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="290" y="590" width="450" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 7. Class Diagram Fitur Login, Akun, dan Cabang:
Gambar 7 memodelkan struktur kelas pada modul autentikasi dan manajemen hierarki organisasi PrintCraft:
1. **Lapisan View (Boundary):**
   - `view_login`: Antarmuka formulir otentikasi login (`resources/views/auth/login.blade.php`) dengan event `submitLogin()`.
   - `view_cabang`: Antarmuka kelola cabang workshop (`resources/views/cabang/index.blade.php`) dengan event `tambahCabang()` dan `ubahCabang()`.
   - `view_akun`: Antarmuka manajemen hak akses akun (`resources/views/akun/index.blade.php`) dengan event `tambahAkun()` dan `ubahStatusAkun()`.
2. **Lapisan Controller (Control):**
   - `AuthController`: Menangani route rute autentikasi via method `showLoginForm()`, `login(request)`, dan `logout(request)`.
   - `CabangController`: Menangani operasi CRUD cabang melalui `index()`, `store(request)`, dan `update(request, id)`.
   - `AkunController`: Menangani operasi akun staf workshop via `index()`, `store(request)`, `update(request, id)`, dan `destroy(id)`.
3. **Lapisan Model (Entity):**
   - `Cabang`: Mewakili tabel `cabang` dengan atribut identitas workshop dan method `tambahCabang(data)`, `ubahCabang(id, data)`, `getCabangAktif()`.
   - `Akun`: Mewakili tabel `akun` dengan atribut kredensial pengguna (termasuk `password_hash` dan `role`) serta method `autentikasi(username, password)`, `buatAkun(data)`, `ubahStatus(id, status)`.
4. **Relasi & Multiplicity:**
   - Model `Cabang` berelasi asosiasi dengan Model `Akun` dengan kardinalitas `1` ke `*` (satu cabang dapat menaungi banyak akun staf, namun setiap akun terdaftar pada satu cabang tertentu).
   - Seluruh View terhubung ke Controller masing-masing dengan relasi *Dependency*.
   - Seluruh Controller terhubung ke Model dengan relasi *Dependency*.
   - Model `Cabang` dan `Akun` terhubung ke kelas koneksi `Database` via relasi *Dependency*.

---

### 1.2 Class Diagram Fitur Master Data dan Kalkulator Harga (PC-002)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pc002" name="Class Diagram PC-002">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="40" y="40" width="170" height="85" as="geometry" />
        </mxCell>

        <!-- Bahan Model -->
        <mxCell id="cls_bahan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Bahan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_bahan: int&lt;br/&gt;+ jenis_kain: String&lt;br/&gt;+ gramasi: String&lt;hr size=&quot;1&quot;/&gt;+ getAllBahan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="260" y="40" width="160" height="100" as="geometry" />
        </mxCell>

        <!-- Ukuran Model -->
        <mxCell id="cls_ukuran" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Ukuran&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_ukuran: int&lt;br/&gt;+ ukuran: String&lt;br/&gt;+ surcharge: double&lt;hr size=&quot;1&quot;/&gt;+ getAllUkuran()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="470" y="40" width="160" height="100" as="geometry" />
        </mxCell>

        <!-- JenisSablon Model -->
        <mxCell id="cls_sablon" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;JenisSablon&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_sablon: int&lt;br/&gt;+ teknik: String&lt;br/&gt;+ tarif_per_warna: double&lt;hr size=&quot;1&quot;/&gt;+ getTarifSablon(teknik)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="680" y="40" width="190" height="100" as="geometry" />
        </mxCell>

        <!-- HargaBeliKaos (Relasi Bahan & Ukuran) -->
        <mxCell id="cls_hpp" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;HargaBeliKaos&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_harga_beli: int&lt;br/&gt;+ id_bahan: int&lt;br/&gt;+ id_ukuran: int&lt;br/&gt;+ harga_pokok: double&lt;hr size=&quot;1&quot;/&gt;+ getHPP(bahan, ukuran)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="340" y="190" width="220" height="120" as="geometry" />
        </mxCell>

        <!-- PotonganMember Model -->
        <mxCell id="cls_potongan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;PotonganMember&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_potongan: int&lt;br/&gt;+ jenis_member: String&lt;br/&gt;+ persentase_diskon: double&lt;hr size=&quot;1&quot;/&gt;+ getDiskon(jenis_member)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="680" y="190" width="190" height="100" as="geometry" />
        </mxCell>

        <!-- MasterDataController -->
        <mxCell id="cls_mstr_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;MasterDataController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ updateBahan(request)&lt;br/&gt;+ updateSablon(request)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="100" y="380" width="220" height="90" as="geometry" />
        </mxCell>

        <!-- KalkulatorController -->
        <mxCell id="cls_kalk_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;KalkulatorController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ hitungEstimasi(request)&lt;br/&gt;+ getRincianHPP(data)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="540" y="380" width="240" height="100" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_master" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_master_data&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ formUbahTarif()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="120" y="550" width="180" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_kalk" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_kalkulator&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ formSimulasiHarga()&lt;br/&gt;+ tampilkanEstimasi()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="570" y="550" width="180" height="70" as="geometry" />
        </mxCell>

        <!-- Associations & Dependencies -->
        <mxCell id="rel_bhn_hpp" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.2;entryY=0;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_bahan" target="cls_hpp">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_bhn" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="325" y="145" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_hpp1" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="365" y="165" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="rel_ukr_hpp" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.8;entryY=0;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_ukuran" target="cls_hpp">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_ukr" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="555" y="145" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_hpp2" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="515" y="165" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="dep_db_all" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_bahan" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="dep_mstr_models" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.2;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_mstr_ctrl" target="cls_hpp">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_kalk_models" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.4;exitY=0;exitDx=0;exitDy=0;entryX=0.6;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_kalk_ctrl" target="cls_hpp">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_kalk_sab" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.8;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_kalk_ctrl" target="cls_potongan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="dep_mstr_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_mstr_ctrl" target="cls_v_master">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_kalk_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_kalk_ctrl" target="cls_v_kalk">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="cap_fig6" value="&lt;b&gt;Gambar 6. Class Diagram Fitur Master Data dan Kalkulator Harga (PC-002)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="270" y="660" width="500" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 6. Class Diagram Fitur Master Data dan Kalkulator Harga:
Gambar 6 memodelkan pengelolaan data konfigurasi dasar produksi sablon dan mesin kalkulasi harga pesanan:
1. **Lapisan View (Boundary):**
   - `view_master_produk`: Antarmuka data jenis kain, variasi warna, dan ukuran kaos polos (`tambahProduk()`, `editProduk()`).
   - `view_tarif_sablon`: Antarmuka pengelolaan tarif teknik sablon (DTF, Rubber, Plastisol) dan dimensi cetak (`updateTarif()`).
   - `view_kalkulator`: Antarmuka simulasi estimasi biaya otomatis sebelum pesanan dibuat (`hitungEstimasi()`, `resetForm()`).
2. **Lapisan Controller (Control):**
   - `MasterDataController`: Menangani rute pengelolaan katalog barang dan tarif (`index()`, `storeProduk(request)`, `updateTarif(request)`).
   - `KalkulatorController`: Mengkalkulasi formula matematis biaya produksi secara real-time via `hitung(request)` dan `getHargaDasar(id_produk)`.
3. **Lapisan Model (Entity):**
   - `ProdukKaos`: Entitas data katalog kaos polos (atribut tipe bahan, ukuran, warna, stok dasar, harga pokok).
   - `TarifSablon`: Entitas tarif jenis sablon berdasarkan variasi teknik dan area cetak (A4, A3, Logo).
   - `KalkulatorHarga`: Service model pengolah algoritma: `total = (harga_kaos + tarif_sablon + biaya_desain) * jumlah_pcs - diskon_member`.
4. **Relasi & Multiplicity:**
   - `ProdukKaos` berelasi asosiasi `1` ke `*` dengan `TarifSablon` saat membentuk kombinasi paket sablon.
   - `KalkulatorHarga` memiliki dependensi terhadap `ProdukKaos` dan `TarifSablon` untuk membaca harga acuan.
   - Seluruh Model berelasi *Dependency* ke class `Database`.

---

### 1.3 Class Diagram Fitur Landing Page dan Daftar Member (PC-003)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-diagram-pc003" name="Class Diagram PC-003">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database Class -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="60" y="60" width="200" height="95" as="geometry" />
        </mxCell>

        <!-- DaftarMember Model Class -->
        <mxCell id="cls_model" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;DaftarMember&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_customer: int&lt;br/&gt;+ nama: String&lt;br/&gt;+ nomor_whatsapp: String&lt;br/&gt;+ email: String&lt;br/&gt;+ alamat: String&lt;br/&gt;+ id_kategori_customer: int&lt;hr size=&quot;1&quot;/&gt;+ validasiData(data)&lt;br/&gt;+ buatDataMember(data, id_kategori_customer)&lt;br/&gt;+ nomorWhatsappTerdaftar(nomor_whatsapp)&lt;br/&gt;+ ambilKategoriMember()&lt;br/&gt;+ simpanMember(data_member)&lt;br/&gt;+ ambilInfoPotonganMember(id_kategori_customer)" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="440" y="60" width="310" height="230" as="geometry" />
        </mxCell>

        <!-- External: KategoriCustomer (PC-002) -->
        <mxCell id="cls_ext_kategori" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;KategoriCustomer (PC-002)&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="840" y="60" width="180" height="50" as="geometry" />
        </mxCell>

        <!-- External: Pesanan (PC-003) -->
        <mxCell id="cls_ext_pesanan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pesanan (PC-003)&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="840" y="215" width="180" height="50" as="geometry" />
        </mxCell>

        <!-- LandingPageController Class -->
        <mxCell id="cls_lp_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;LandingPageController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="60" y="520" width="190" height="80" as="geometry" />
        </mxCell>

        <!-- DaftarMemberController Class -->
        <mxCell id="cls_dm_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;DaftarMemberController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ create()&lt;br/&gt;+ store(request)&lt;br/&gt;+ berhasil(id_customer)" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="455" y="505" width="280" height="110" as="geometry" />
        </mxCell>

        <!-- view_landing_page Class -->
        <mxCell id="cls_v_lp" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_landing_page&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ daftarMember()" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="70" y="760" width="170" height="65" as="geometry" />
        </mxCell>

        <!-- form_member Class -->
        <mxCell id="cls_f_member" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;form_member&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ prosesDaftar()" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="480" y="760" width="170" height="65" as="geometry" />
        </mxCell>

        <!-- view_konfirmasi_member Class -->
        <mxCell id="cls_v_konfirm" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_konfirmasi_member&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ tampilKonfirmasi()" style="verticalAlign=top;align=left;overflow=fill;fontSize=12;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="730" y="760" width="180" height="65" as="geometry" />
        </mxCell>

        <!-- Caption -->
        <mxCell id="caption_fig53" value="&lt;b&gt;Gambar 53. Class Diagram Fitur Landing Page dan Daftar Member (PC-003)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="280" y="860" width="500" height="30" as="geometry" />
        </mxCell>

        <!-- Association: DaftarMember -> KategoriCustomer -->
        <mxCell id="rel_kat" value="1" style="endArrow=none;html=1;rounded=0;exitX=1;exitY=0.2;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_model" target="cls_ext_kategori">
          <mxGeometry x="0.8" y="-10" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>
        <mxCell id="lbl_kat_star" value="*" style="edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];" vertex="1" connectable="0" parent="rel_kat">
          <mxGeometry x="-0.85" y="-12" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Association: DaftarMember -> Pesanan -->
        <mxCell id="rel_pesanan" value="0..*" style="endArrow=none;html=1;rounded=0;exitX=1;exitY=0.8;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_model" target="cls_ext_pesanan">
          <mxGeometry x="0.8" y="-10" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>
        <mxCell id="lbl_pesanan_1" value="1" style="edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];" vertex="1" connectable="0" parent="rel_pesanan">
          <mxGeometry x="-0.85" y="-12" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: DaftarMember -> Database -->
        <mxCell id="dep_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0;exitY=0.3;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_model" target="cls_db">
          <mxGeometry x="0.05" y="15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: DaftarMemberController -> DaftarMember -->
        <mxCell id="dep_ctrl_model" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dm_ctrl" target="cls_model">
          <mxGeometry x="-0.1" y="-15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: LandingPageController -> view_landing_page -->
        <mxCell id="dep_lp_view" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_lp_ctrl" target="cls_v_lp">
          <mxGeometry x="-0.1" y="-15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: DaftarMemberController -> view_landing_page -->
        <mxCell id="dep_dm_vlp" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0;exitY=0.9;exitDx=0;exitDy=0;entryX=1;entryY=0.2;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dm_ctrl" target="cls_v_lp">
          <mxGeometry x="0.1" y="15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: DaftarMemberController -> form_member -->
        <mxCell id="dep_dm_fm" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0.4;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dm_ctrl" target="cls_f_member">
          <mxGeometry x="-0.1" y="-15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Dependency: DaftarMemberController -> view_konfirmasi_member -->
        <mxCell id="dep_dm_vkonfirm" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;exitX=0.8;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dm_ctrl" target="cls_v_konfirm">
          <mxGeometry x="-0.1" y="-15" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 5. Class Diagram Fitur Landing Page dan Daftar Member:
Diagram ini identik dengan Gambar 53 pada dokumen SRS PrintCraft yang menjadi acuan resmi:
1. **Lapisan View (Boundary):**
   - `view_landing_page`: Halaman depan publik profil workshop PrintCraft (`daftarMember()`).
   - `form_member`: Formulir pendaftaran member baru (`prosesDaftar()`).
   - `view_konfirmasi_member`: Halaman ucapan selamat dan tampilan nomor WhatsApp terdaftar (`tampilKonfirmasi()`).
2. **Lapisan Controller (Control):**
   - `LandingPageController`: Menangani rute beranda publik (`index()`).
   - `DaftarMemberController`: Menangani registrasi member via `create()`, `store(request)`, dan `berhasil(id_customer)`.
3. **Lapisan Model (Entity):**
   - `DaftarMember`: Mengelola validasi data unik pelanggan via method `validasiData(data)`, `nomorWhatsappTerdaftar(no_wa)`, `buatDataMember(data, id_kategori)`, `simpanMember(data)`, `ambilKategoriMember()`, dan `ambilInfoPotonganMember(id_kategori)`.
   - `KategoriCustomer (PC-002)`: Entitas acuan tingkatan keanggotaan customer (Reguler, Member Diskon, Reseller).
   - `Pesanan (PC-003)`: Entitas pesanan yang berelasi dengan customer saat bertransaksi.
4. **Relasi & Multiplicity:**
   - `DaftarMember` berelasi `*` ke `1` terhadap `KategoriCustomer` (banyak member berada dalam 1 kategori).
   - `DaftarMember` berelasi `1` ke `0..*` terhadap `Pesanan` (satu member dapat memiliki nol atau banyak pesanan).
   - Seluruh controller dan model terhubung ke `Database` via relasi *Dependency*.

---

### 1.4 Class Diagram Fitur Kelola Pesanan dan Data Customer (PC-003)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pesanan" name="Class Diagram Pesanan">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="40" y="40" width="160" height="85" as="geometry" />
        </mxCell>

        <!-- Customer Model -->
        <mxCell id="cls_cust" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Customer&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_customer: int&lt;br/&gt;+ nama: String&lt;br/&gt;+ nomor_whatsapp: String&lt;br/&gt;+ email: String&lt;br/&gt;+ alamat: String&lt;br/&gt;+ id_kategori_customer: int&lt;hr size=&quot;1&quot;/&gt;+ findOrCreateByWA(data)&lt;br/&gt;+ updateCustomer(id, data)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="270" y="40" width="220" height="160" as="geometry" />
        </mxCell>

        <!-- Pesanan Model -->
        <mxCell id="cls_pesanan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pesanan: int&lt;br/&gt;+ no_pesanan: String&lt;br/&gt;+ id_customer: int&lt;br/&gt;+ id_cabang: int&lt;br/&gt;+ status_pesanan: enum&lt;br/&gt;+ total_biaya: double&lt;br/&gt;+ sisa_tagihan: double&lt;br/&gt;+ deadline: date&lt;br/&gt;+ catatan_desain: text&lt;hr size=&quot;1&quot;/&gt;+ buatPesanan(data)&lt;br/&gt;+ updateStatus(id, status)&lt;br/&gt;+ hitungSisaTagihan(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="580" y="30" width="250" height="210" as="geometry" />
        </mxCell>

        <!-- Pembayaran Model -->
        <mxCell id="cls_bayar" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pembayaran&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pembayaran: int&lt;br/&gt;+ id_pesanan: int&lt;br/&gt;+ jenis_pembayaran: enum&lt;br/&gt;+ jumlah_bayar: double&lt;br/&gt;+ metode_bayar: enum&lt;br/&gt;+ bukti_bayar: String&lt;hr size=&quot;1&quot;/&gt;+ catatPembayaran(data)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="910" y="45" width="200" height="160" as="geometry" />
        </mxCell>

        <!-- CustomerController -->
        <mxCell id="cls_cust_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;CustomerController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ store(request)&lt;br/&gt;+ update(request, id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="270" y="310" width="210" height="90" as="geometry" />
        </mxCell>

        <!-- PesananController -->
        <mxCell id="cls_pes_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;PesananController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ create()&lt;br/&gt;+ store(request)&lt;br/&gt;+ show(id)&lt;br/&gt;+ updateStatus(request, id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="600" y="300" width="220" height="110" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_cust" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_customer&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ listCustomer()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="295" y="490" width="160" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_f_pes" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;form_pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ simpanPesanan()&lt;br/&gt;+ validasiPesanan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="540" y="490" width="160" height="70" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_pes" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ filterStatusPesanan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="740" y="490" width="170" height="60" as="geometry" />
        </mxCell>

        <!-- Relations with Multiplicity -->
        <mxCell id="rel_c_p" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_cust" target="cls_pesanan">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_c" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="495" y="105" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_p" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="555" y="105" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="rel_p_b" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_pesanan" target="cls_bayar">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_p2" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="835" y="105" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_b" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="885" y="105" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="dep_c_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cust" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="dep_cctrl_c" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cust_ctrl" target="cls_cust">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_pctrl_p" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pes_ctrl" target="cls_pesanan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_pctrl_b" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.9;exitY=0;exitDx=0;exitDy=0;entryX=0.2;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pes_ctrl" target="cls_bayar">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="dep_cctrl_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_cust_ctrl" target="cls_v_cust">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_pctrl_f" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.3;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pes_ctrl" target="cls_f_pes">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_pctrl_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.8;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pes_ctrl" target="cls_v_pes">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="cap_fig_pes" value="&lt;b&gt;Gambar 5b. Class Diagram Fitur Transaksi Pesanan dan Data Customer (PC-003)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="310" y="610" width="520" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 5b. Class Diagram Fitur Pesanan dan Data Customer:
Diagram ini memodelkan proses inti transaksi penjualan sablon kaos di workshop:
1. **Lapisan View (Boundary):**
   - `view_pesanan`: Tampilan daftar pesanan dengan filter status produksi dan pembayaran (`tambahPesanan()`, `filterStatus()`).
   - `form_pesanan`: Formulir input transaksi sablon (pemilihan customer, spesifikasi kain, unggah file desain sablon, DP 50%).
   - `view_detail_pesanan`: Halaman detail transaksi, linimasa progres pengerjaan, dan pencatatan pelunasan.
2. **Lapisan Controller (Control):**
   - `PesananController`: Mengendalikan aliran transaksi via `index()`, `create()`, `store(request)`, `show(id)`, `updateStatusProduksi(id, status)`.
   - `PembayaranController`: Mengelola validasi pembayaran awal (DP minimal 50%) dan pelunasan (`storePembayaran(request)`).
3. **Lapisan Model (Entity):**
   - `Customer`: Entitas penyimpan data profil pembeli (`id_customer`, `nama`, `nomor_whatsapp`, `email`).
   - `Pesanan`: Entitas master transaksi (`id_pesanan`, `kode_pesanan`, `total_harga`, `sisa_pembayaran`, `status_produksi`, `status_pembayaran`).
   - `DetailPesanan`: Entitas rincian item pesanan (tipe sablon, ukuran, jumlah pcs, subtotal).
   - `Pembayaran`: Entitas pencatatan transaksi uang muka dan pelunasan (`id_pembayaran`, `jumlah_bayar`, `metode_transfer`, `bukti_transfer`).
4. **Relasi & Multiplicity:**
   - `Customer` `1` ke `0..*` `Pesanan`: Satu pelanggan dapat melakukan banyak transaksi pesanan.
   - `Pesanan` `1` ke `1..*` `DetailPesanan`: Satu pesanan wajib memiliki minimal satu baris rincian item sablon.
   - `Pesanan` `1` ke `1..*` `Pembayaran`: Satu pesanan memiliki riwayat pembayaran (minimal 1 kali saat DP, hingga pelunasan).
   - Model mengakses `Database` via relasi *Dependency*.

---

### 1.5 Class Diagram Fitur Pengadaan Stok Kaos Polos (PC-004)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pc004" name="Class Diagram PC-004">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="50" y="45" width="170" height="85" as="geometry" />
        </mxCell>

        <!-- PengadaanKaos Model -->
        <mxCell id="cls_pengadaan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;PengadaanKaos&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pengadaan: int&lt;br/&gt;+ no_po: String&lt;br/&gt;+ id_cabang: int&lt;br/&gt;+ id_pesanan: int&lt;br/&gt;+ id_bahan: int&lt;br/&gt;+ id_ukuran: int&lt;br/&gt;+ jumlah_pcs: int&lt;br/&gt;+ nama_supplier: String&lt;br/&gt;+ total_biaya_beli: double&lt;br/&gt;+ status_pengadaan: enum&lt;hr size=&quot;1&quot;/&gt;+ buatPO(data)&lt;br/&gt;+ terimaBarang(id, tgl)&lt;br/&gt;+ updateStokKaos(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="360" y="30" width="270" height="230" as="geometry" />
        </mxCell>

        <!-- Pesanan (External) -->
        <mxCell id="cls_ext_pes" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pesanan (PC-003)&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pesanan: int&lt;br/&gt;+ no_pesanan: String" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="750" y="50" width="180" height="70" as="geometry" />
        </mxCell>

        <!-- PengadaanController -->
        <mxCell id="cls_peng_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;PengadaanController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index()&lt;br/&gt;+ create()&lt;br/&gt;+ store(request)&lt;br/&gt;+ konfirmasiPenerimaan(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="380" y="330" width="230" height="110" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_peng" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_pengadaan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ listPengadaan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="270" y="510" width="170" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_f_peng" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;form_pengadaan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ simpanPengadaan()&lt;br/&gt;+ validasiPO()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="540" y="510" width="170" height="70" as="geometry" />
        </mxCell>

        <!-- Relations with Multiplicity -->
        <mxCell id="rel_pes_peng" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.3;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_pengadaan" target="cls_ext_pes">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_pes_ext" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="725" y="75" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_peng_rel" value="0..*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="635" y="85" width="30" height="20" as="geometry" /></mxCell>

        <mxCell id="dep_peng_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.3;exitDx=0;exitDy=0;entryX=1;entryY=0.3;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pengadaan" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_model" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_peng_ctrl" target="cls_pengadaan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_vp" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.3;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_peng_ctrl" target="cls_v_peng">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_fp" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.7;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_peng_ctrl" target="cls_f_peng">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="cap_fig8" value="&lt;b&gt;Gambar 8. Class Diagram Fitur Pengadaan Kaos (PC-004)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="310" y="630" width="450" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 8. Class Diagram Fitur Pengadaan Stok Kaos Polos:
Gambar 8 memodelkan rantai pasok pengadaan bahan baku kaos polos ke vendor:
1. **Lapisan View (Boundary):**
   - `view_pengadaan`: Antarmuka monitoring status pengadaan kaos antar-cabang (`buatPengadaan()`, `filterVendor()`).
   - `form_pengadaan`: Formulir input pemesanan kaos polos ke vendor rekanan (`submitPengadaan()`).
2. **Lapisan Controller (Control):**
   - `PengadaanController`: Mengendalikan penerbitan Purchase Order (PO) kaos polos melalui `index()`, `store(request)`, `updateStatusTiba(id)`.
3. **Lapisan Model (Entity):**
   - `Vendor`: Entitas penyedia bahan kain kaos (`id_vendor`, `nama_vendor`, `kontak`, `alamat`).
   - `PengadaanKaos`: Entitas transaksi PO (`id_pengadaan`, `nomor_po`, `total_pcs`, `biaya_pengadaan`, `status_pengiriman`).
   - `ItemPengadaan`: Rincian spesifikasi kaos yang diadakan (ukuran S/M/L/XL/XXL, gramasi 30s/24s, warna).
4. **Relasi & Multiplicity:**
   - `Vendor` berelasi `1` ke `*` dengan `PengadaanKaos` (satu vendor dapat menerima banyak pesanan pengadaan).
   - `PengadaanKaos` berelasi `1` ke `1..*` dengan `ItemPengadaan`.
   - `PengadaanKaos` berelasi asosiasi dengan Model `Pesanan` untuk pelacakan alokasi stok pesanan pelanggan.

---

### 1.6 Class Diagram Fitur Cetak Invoice dan Work Order Production (PC-005)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pc005" name="Class Diagram PC-005">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="50" y="50" width="160" height="85" as="geometry" />
        </mxCell>

        <!-- Pesanan Model -->
        <mxCell id="cls_pesanan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pesanan: int&lt;br/&gt;+ no_pesanan: String&lt;br/&gt;+ id_customer: int&lt;br/&gt;+ total_biaya: double&lt;br/&gt;+ sisa_tagihan: double&lt;br/&gt;+ deadline: date&lt;hr size=&quot;1&quot;/&gt;+ getDetailPesanan(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="320" y="40" width="220" height="150" as="geometry" />
        </mxCell>

        <!-- Customer Model -->
        <mxCell id="cls_cust" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Customer&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_customer: int&lt;br/&gt;+ nama: String&lt;br/&gt;+ nomor_whatsapp: String&lt;hr size=&quot;1&quot;/&gt;+ getCustomer(id)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="630" y="45" width="200" height="110" as="geometry" />
        </mxCell>

        <!-- Pembayaran Model -->
        <mxCell id="cls_bayar" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pembayaran&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pembayaran: int&lt;br/&gt;+ id_pesanan: int&lt;br/&gt;+ jumlah_bayar: double&lt;hr size=&quot;1&quot;/&gt;+ getRiwayatBayar(id_pesanan)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="900" y="45" width="210" height="110" as="geometry" />
        </mxCell>

        <!-- InvoiceController -->
        <mxCell id="cls_inv_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;InvoiceController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ cetakInvoice(id)&lt;br/&gt;+ cetakWOP(id)&lt;br/&gt;+ generatePDF(view, data)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="460" y="270" width="240" height="100" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_det" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_detail_pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ aksiCetakInvoice()&lt;br/&gt;+ aksiCetakWOP()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="190" y="460" width="190" height="70" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_inv" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;cetak_invoice_thermal&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ renderStruk80mm()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="485" y="460" width="190" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_wop" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;cetak_wop_pdf&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ renderDokumenProduksiA4()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="780" y="460" width="200" height="60" as="geometry" />
        </mxCell>

        <!-- Relations with Multiplicity -->
        <mxCell id="rel_p_c" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.4;exitDx=0;exitDy=0;entryX=0;entryY=0.4;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_pesanan" target="cls_cust">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_pc1" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="545" y="90" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_pc2" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="605" y="90" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="rel_p_byr" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=1.5;exitX=1;exitY=0.7;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="cls_pesanan" target="cls_bayar">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="mult_pb1" value="1" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="545" y="135" width="20" height="20" as="geometry" /></mxCell>
        <mxCell id="mult_pb2" value="*" style="text;html=1;align=center;verticalAlign=middle;fontSize=11;fontStyle=1;" vertex="1" parent="1"><mxGeometry x="875" y="95" width="20" height="20" as="geometry" /></mxCell>

        <mxCell id="dep_p_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pesanan" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="dep_ctrl_pes" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.2;exitY=0;exitDx=0;exitDy=0;entryX=0.6;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_inv_ctrl" target="cls_pesanan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_vdet" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.2;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_inv_ctrl" target="cls_v_det">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_vinv" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_inv_ctrl" target="cls_v_inv">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_ctrl_vwop" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.8;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_inv_ctrl" target="cls_v_wop">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="cap_fig9" value="&lt;b&gt;Gambar 9. Class Diagram Fitur Invoice dan WOP (PC-005)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="340" y="580" width="450" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 9. Class Diagram Fitur Cetak Invoice dan WOP:
Gambar 9 memodelkan pencetakan dokumen resmi transaksi dan lembar kerja produksi:
1. **Lapisan View (Boundary):**
   - `view_detail_pesanan`: Halaman detail pesanan yang menyediakan tombol aksi cetak (`cetakInvoice()`, `cetakWOP()`).
   - `view_pdf_preview`: Antarmuka pratinjau dokumen PDF pada tab browser sebelum dicetak fisik.
2. **Lapisan Controller (Control):**
   - `DokumenController`: Mengatur ekstraksi data dan pemanggilan library cetak melalui `cetakInvoice(id_pesanan)` dan `cetakWOP(id_pesanan)`.
3. **Lapisan Library & Model:**
   - `Dompdf / PDFRenderer`: Service library (*barryvdh/laravel-dompdf*) untuk mengonversi view Blade menjadi file PDF siap cetak ukuran A4.
   - `Pesanan` & `Pembayaran`: Model entity yang menyediakan seluruh data transaksi.
4. **Relasi & Batasan Keamanan:**
   - `DokumenController` memiliki klausul khusus di mana method `cetakWOP()` secara eksplisit memfilter kolom nominal uang, tarif sablon, dan informasi pembayaran agar tidak muncul pada lembar kerja operator sablon.

---

### 1.7 Class Diagram Fitur Dashboard dan Rekap Laporan Keuangan (PC-006)

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="class-pc006" name="Class Diagram PC-006">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Database -->
        <mxCell id="cls_db" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Database&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ db: array&lt;br/&gt;+ nama_database: String&lt;hr size=&quot;1&quot;/&gt;+ koneksi(nama_database)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="50" y="50" width="160" height="85" as="geometry" />
        </mxCell>

        <!-- Pesanan Model -->
        <mxCell id="cls_pesanan" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pesanan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pesanan: int&lt;br/&gt;+ id_cabang: int&lt;br/&gt;+ total_biaya: double&lt;br/&gt;+ created_at: timestamp&lt;hr size=&quot;1&quot;/&gt;+ getStatistikBulanan(cabang_id)&lt;br/&gt;+ getOmzetPeriode(tgl_awal, tgl_akhir)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="320" y="40" width="260" height="150" as="geometry" />
        </mxCell>

        <!-- Pembayaran Model -->
        <mxCell id="cls_bayar" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;Pembayaran&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ id_pembayaran: int&lt;br/&gt;+ jumlah_bayar: double&lt;br/&gt;+ tanggal_bayar: timestamp&lt;hr size=&quot;1&quot;/&gt;+ getTotalKasMasuk(periode)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="680" y="45" width="220" height="120" as="geometry" />
        </mxCell>

        <!-- DashboardController -->
        <mxCell id="cls_dsh_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;DashboardController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index(request)&lt;br/&gt;+ getMetrikRingkasan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="220" y="270" width="220" height="90" as="geometry" />
        </mxCell>

        <!-- LaporanController -->
        <mxCell id="cls_lap_ctrl" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;LaporanController&lt;/b&gt;&lt;br/&gt;&amp;lt;&amp;lt;Controller&amp;gt;&amp;gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ index(request)&lt;br/&gt;+ filterLaporan(request)&lt;br/&gt;+ exportPDF(request)" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="580" y="270" width="230" height="100" as="geometry" />
        </mxCell>

        <!-- Views -->
        <mxCell id="cls_v_dash" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_dashboard_owner&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ tampilMetrikRingkasan()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="230" y="460" width="200" height="60" as="geometry" />
        </mxCell>
        <mxCell id="cls_v_lap" value="&lt;p style=&quot;margin:0px;text-align:center;&quot;&gt;&lt;b&gt;view_laporan_keuangan&lt;/b&gt;&lt;/p&gt;&lt;hr size=&quot;1&quot;/&gt;+ filterPeriode()&lt;br/&gt;+ cetakRekap()" style="verticalAlign=top;align=left;overflow=fill;fontSize=11;fontFamily=Helvetica;html=1;whiteSpace=wrap;strokeColor=#000000;fillColor=#ffffff;" vertex="1" parent="1">
          <mxGeometry x="600" y="460" width="190" height="70" as="geometry" />
        </mxCell>

        <!-- Dependencies -->
        <mxCell id="dep_p_db" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_pesanan" target="cls_db">
          <mxGeometry x="0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_dsh_pes" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.3;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dsh_ctrl" target="cls_pesanan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_lap_pes" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.3;exitY=0;exitDx=0;exitDy=0;entryX=0.8;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_lap_ctrl" target="cls_pesanan">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_lap_byr" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.7;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_lap_ctrl" target="cls_bayar">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_dsh_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_dsh_ctrl" target="cls_v_dash">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>
        <mxCell id="dep_lap_v" value="Dependency" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.2;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endFill=0;" edge="1" parent="1" source="cls_lap_ctrl" target="cls_v_lap">
          <mxGeometry x="-0.1" y="-10" relative="1" as="geometry"><mxPoint as="offset" /></mxGeometry>
        </mxCell>

        <mxCell id="cap_fig10" value="&lt;b&gt;Gambar 10. Class Diagram Fitur Dashboard dan Rekap Laporan (PC-006)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="270" y="580" width="480" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 10. Class Diagram Fitur Dashboard dan Rekap Laporan:
Gambar 10 memodelkan agregasi statistik eksekutif dan rekapitulasi keuangan workshop:
1. **Lapisan View (Boundary):**
   - `view_dashboard`: Tampilan panel utama (*cards summary* pendapatan, jumlah pesanan aktif, antrean sablon).
   - `view_laporan`: Antarmuka filter laporan keuangan berkala (`filterLaporan()`, `eksporExcel()`, `eksporPDF()`).
2. **Lapisan Controller (Control):**
   - `DashboardController`: Memproses widget data statistik harian (`index()`).
   - `LaporanController`: Menghitung kueri agregasi pendapatan kotor, sisa piutang, dan tren produk terlaris via `filterLaporan(cabang_id, periode)`.
3. **Lapisan Model (Entity):**
   - Mengakses Model `Pesanan`, `Pembayaran`, dan `Cabang` untuk mengeksekusi fungsi kueri agregat (`SUM(total_harga)`, `SUM(jumlah_bayar)`, `COUNT(id_pesanan)`).
4. **Relasi & Otorisasi:**
   - Owner memiliki otorisasi multi-cabang (dapat memilih filter seluruh cabang atau cabang spesifik).
   - Admin dibatasi secara otomatis oleh sistem (*session branching*) hanya dapat mengakses data cabang tempat ia ditugaskan.

---

# BAGIAN 2: KUMPULAN SEQUENCE DIAGRAM (SEMUA FITUR PC-001 s.d. PC-006)

Tabel Pemetaan Sequence Diagram:

| ID Fitur | Nama Skenario Sequence | Lifeline Aktor | Lifeline Boundary & Control | Nomor Diagram | File Draw.io |
| :---: | :---: | :---: | :---: | :---: | :---: |
| PC-003 | Tampil Landing Page Publik | Customer | `view_landing_page`, `LandingPageController` | Gambar 11 TPDB / Gbr 54 SRS | `sequence-landing-page.drawio` |
| PC-003 | Pendaftaran Member & Simpan Data | Customer | `form_member`, `DaftarMemberController`, `DaftarMember`, `Database` | Gambar 12 TPDB / Gbr 55 SRS | `sequence-daftar-member.drawio` |
| PC-001 | Login Pengguna Owner / Admin | Owner, Admin | `view_login`, `AuthController`, `Akun`, `Database`, `view_dashboard` | Gambar 13 TPDB | `sequence-login.drawio` |
| PC-003 | Pembuatan Pesanan Sablon & DP 50% | Owner, Admin | `form_pesanan`, `PesananController`, `Pesanan`, `Pembayaran`, `Database` | Skenario Inti PC-003 | `sequence-pesanan.drawio` |
| PC-004 | Pengadaan Stok Kaos Polos | Owner, Admin | `form_pengadaan`, `PengadaanController`, `PengadaanKaos`, `Database` | Gambar 14 TPDB | `sequence-pengadaan.drawio` |
| PC-005 | Cetak Dokumen Invoice & WOP (PDF) | Owner, Admin | `view_detail_pesanan`, `DokumenController`, `Dompdf`, `Pesanan` | Gambar 15 TPDB | `sequence-invoice.drawio` |
| PC-006 | Dashboard & Rekap Laporan Keuangan | Owner, Admin | `view_laporan`, `LaporanController`, `Pesanan`, `Database` | Gambar 16 TPDB | `sequence-dashboard.drawio` |

---

### 2.1 Sequence Diagram Fitur Landing Page (PC-003)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Customer membuka alamat website PrintCraft pada peramban web (*browser*).
2. Form `view_landing_page` mengeksekusi request route `GET /` yang memanggil fungsi `daftarMember()` pada antarmuka.
3. Fungsi tersebut memanggil method `index()` pada `LandingPageController`.
4. `LandingPageController` melakukan *self-call* dan mengembalikan render tampilan beranda ke antarmuka `view_landing_page`.

#### Komponen yang Terlibat:
1. Aktor: Customer
2. Class View / Boundary: `view_landing_page`
3. Class Controller / Control: `LandingPageController`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-landing-page" name="Sequence Tampil Landing Page">
    <mxGraphModel dx="1000" dy="700" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="827" pageHeight="1169" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Actor: Customer Top -->
        <mxCell id="act_customer_top" value="Customer" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
          <mxGeometry x="85" y="40" width="30" height="60" as="geometry" />
        </mxCell>

        <!-- Lifeline Boundary: view_landing_page Top -->
        <mxCell id="ll_vlp_top" value="view_landing_page" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="270" y="50" width="60" height="40" as="geometry" />
        </mxCell>

        <!-- Lifeline Control: LandingPageController Top -->
        <mxCell id="ll_ctrl_top" value="LandingPageController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="510" y="45" width="45" height="50" as="geometry" />
        </mxCell>

        <!-- Lifeline dashed lines -->
        <!-- Customer Lifeline -->
        <mxCell id="line_cust" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_customer_bottom" target="act_customer_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <!-- view_landing_page Lifeline -->
        <mxCell id="line_vlp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vlp_bottom" target="ll_vlp_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <!-- LandingPageController Lifeline -->
        <mxCell id="line_ctrl" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_ctrl_bottom" target="ll_ctrl_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- Message 1: Buka website -->
        <mxCell id="msg1" value="Buka website" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="100" y="160" as="sourcePoint" />
            <mxPoint x="300" y="160" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Message 2: daftarMember() / route GET / -->
        <mxCell id="msg2" value="daftarMember() / route GET /" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="300" y="210" as="sourcePoint" />
            <mxPoint x="532" y="210" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Self-call: index() -->
        <mxCell id="msg3_self" value="index()" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="0.2" y="-15" relative="1" as="geometry">
            <mxPoint x="532" y="250" as="sourcePoint" />
            <mxPoint x="532" y="280" as="targetPoint" />
            <Array as="points">
              <mxPoint x="580" y="250" />
              <mxPoint x="580" y="280" />
            </Array>
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Message 4: return (view_landing_page) -->
        <mxCell id="msg4_return" value="return (view_landing_page)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="532" y="320" as="sourcePoint" />
            <mxPoint x="300" y="320" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Actor: Customer Bottom -->
        <mxCell id="act_customer_bottom" value="Customer" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
          <mxGeometry x="85" y="370" width="30" height="60" as="geometry" />
        </mxCell>

        <!-- Lifeline Boundary: view_landing_page Bottom -->
        <mxCell id="ll_vlp_bottom" value="view_landing_page" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="270" y="380" width="60" height="40" as="geometry" />
        </mxCell>

        <!-- Lifeline Control: LandingPageController Bottom -->
        <mxCell id="ll_ctrl_bottom" value="LandingPageController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="510" y="375" width="45" height="50" as="geometry" />
        </mxCell>

        <!-- Caption -->
        <mxCell id="caption_fig54" value="&lt;b&gt;Gambar 54. Sequence Diagram Tampil Landing Page&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="150" y="460" width="370" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 11. Sequence Diagram Fitur Landing Page:
Gambar 11 merupakan sequence diagram tampil landing page website PrintCraft (sesuai Gambar 54 SRS). Customer berinteraksi secara langsung dengan form `view_landing_page` untuk melakukan buka website. Ketika website dibuka, form `view_landing_page` mengeksekusi fungsi `daftarMember()` via route `GET /` ke controller `LandingPageController`. Controller menjalankan operasi internal `index()` dan mengembalikan tampilan halaman landing page kepada Customer. Pesan return berhenti di tampilan `view_landing_page` tempat Customer melihat visualisasi antarmuka.

---

### 2.2 Sequence Diagram Fitur Pendaftaran Member (PC-003)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Customer mengklik tombol "Daftar Member" pada halaman beranda `view_landing_page`.
2. Antarmuka mengeksekusi rute `GET /daftar-member` ke method `create()` pada `DaftarMemberController`, lalu menampilkan form input `form_member`.
3. Customer mengisi identitas diri (nama, nomor WhatsApp, email, alamat) dan mengklik tombol "Daftar".
4. Form `form_member` mengeksekusi `prosesDaftar()` via `POST /daftar-member` ke method `store(request)` pada `DaftarMemberController`.
5. `DaftarMemberController` memanggil method `validasiData(data)` dan `nomorWhatsappTerdaftar(no_wa)` pada Model `DaftarMember` yang memeriksa keunikan nomor ponsel ke `Database`.
6. Alur percabangan (*Alt Fragment*):
   - **Kondisi Valid & Nomor Belum Terdaftar [True]:** Controller memanggil `ambilKategoriMember()`, membuat entitas member via `buatDataMember()`, menyimpan ke basis data via `simpanMember()` (return `id_customer`), membaca besaran diskon via `ambilInfoPotonganMember()`, mengeksekusi internal method `berhasil(id_customer)`, dan mengarahkan navigasi ke `view_konfirmasi_member` yang menjalankan `tampilKonfirmasi()`.
   - **Kondisi Data Tidak Valid / Nomor Sudah Ada [False]:** Controller mengembalikan pesan error (`return pesan error`) ke tampilan `form_member` untuk diperbaiki pengguna.

#### Komponen yang Terlibat:
1. Aktor: Customer
2. Class View / Boundary: `view_landing_page`, `form_member`, `view_konfirmasi_member`
3. Class Controller / Control: `DaftarMemberController`
4. Class Model / Entity: `DaftarMember`
5. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-daftar-member" name="Sequence Daftar Member">
    <mxGraphModel dx="1400" dy="900" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- 1. Customer Actor -->
        <mxCell id="ll_cust_top" value="Customer" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
          <mxGeometry x="40" y="40" width="30" height="60" as="geometry" />
        </mxCell>
        <mxCell id="ll_cust_bot" value="Customer" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
          <mxGeometry x="40" y="740" width="30" height="60" as="geometry" />
        </mxCell>
        <mxCell id="line_cust" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_cust_bot" target="ll_cust_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 2. Boundary: view_landing_page -->
        <mxCell id="ll_vlp_top" value="view_landing_page" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="140" y="50" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="ll_vlp_bot" value="view_landing_page" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="140" y="750" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="line_vlp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vlp_bot" target="ll_vlp_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 3. Boundary: form_member -->
        <mxCell id="ll_fm_top" value="form_member" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="280" y="50" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="ll_fm_bot" value="form_member" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="280" y="750" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="line_fm" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_fm_bot" target="ll_fm_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 4. Control: DaftarMemberController -->
        <mxCell id="ll_ctrl_top" value="DaftarMemberController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="430" y="45" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="ll_ctrl_bot" value="DaftarMemberController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="430" y="745" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="line_ctrl" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_ctrl_bot" target="ll_ctrl_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 5. Entity: DaftarMember -->
        <mxCell id="ll_model_top" value="DaftarMember" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="630" y="45" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="ll_model_bot" value="DaftarMember" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="630" y="745" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="line_model" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_model_bot" target="ll_model_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 6. Database -->
        <mxCell id="ll_db_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="810" y="45" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="ll_db_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="810" y="745" width="45" height="50" as="geometry" />
        </mxCell>
        <mxCell id="line_db" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_db_bot" target="ll_db_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- 7. Boundary: view_konfirmasi_member -->
        <mxCell id="ll_vkm_top" value="view_konfirmasi_member" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
          <mxGeometry x="960" y="50" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="ll_vkm_bot" value="view_konfirmasi_member" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
          <mxGeometry x="960" y="750" width="60" height="40" as="geometry" />
        </mxCell>
        <mxCell id="line_vkm" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vkm_bot" target="ll_vkm_top">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

        <!-- ===== MESSAGES ===== -->

        <!-- 1. Klik Daftar Member -->
        <mxCell id="m1" value="Klik tombol &apos;Daftar Member&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="55" y="140" as="sourcePoint" />
            <mxPoint x="170" y="140" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 2. daftarMember() / route GET /daftar-member -->
        <mxCell id="m2" value="daftarMember() / route GET /daftar-member" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="170" y="170" as="sourcePoint" />
            <mxPoint x="452" y="170" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 3. Self-call: create() -->
        <mxCell id="m3" value="create()" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="0.2" y="-15" relative="1" as="geometry">
            <mxPoint x="452" y="195" as="sourcePoint" />
            <mxPoint x="452" y="220" as="targetPoint" />
            <Array as="points">
              <mxPoint x="495" y="195" />
              <mxPoint x="495" y="220" />
            </Array>
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 4. return (form_member) -->
        <mxCell id="m4" value="return (form_member)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="245" as="sourcePoint" />
            <mxPoint x="310" y="245" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 5. Isi data & klik Daftar -->
        <mxCell id="m5" value="Isikan data &amp; klik &apos;Daftar&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="55" y="280" as="sourcePoint" />
            <mxPoint x="310" y="280" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 6. prosesDaftar() / route POST /daftar-member -->
        <mxCell id="m6" value="prosesDaftar() / route POST /daftar-member" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="310" y="310" as="sourcePoint" />
            <mxPoint x="452" y="310" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 7. validasiData(data) -->
        <mxCell id="m7" value="validasiData(data)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="340" as="sourcePoint" />
            <mxPoint x="652" y="340" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 8. return hasil_validasi -->
        <mxCell id="m8" value="return (hasil_validasi)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="652" y="365" as="sourcePoint" />
            <mxPoint x="452" y="365" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 9. nomorWhatsappTerdaftar(nomor_whatsapp) -->
        <mxCell id="m9" value="nomorWhatsappTerdaftar(nomor_whatsapp)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="395" as="sourcePoint" />
            <mxPoint x="652" y="395" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 10. Query cek nomor WhatsApp -->
        <mxCell id="m10" value="Query cek nomor_whatsapp" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="652" y="420" as="sourcePoint" />
            <mxPoint x="832" y="420" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 11. return record result -->
        <mxCell id="m11" value="return (record result)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="832" y="445" as="sourcePoint" />
            <mxPoint x="652" y="445" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- 12. return status_terdaftar -->
        <mxCell id="m12" value="return (status_terdaftar)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="652" y="470" as="sourcePoint" />
            <mxPoint x="452" y="470" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- ALT FRAGMENT BOX -->
        <mxCell id="alt_box" value="alt" style="shape=umlFrame;whiteSpace=wrap;html=1;width=60;height=25;boundedLbl=1;verticalAlign=top;align=left;spacingLeft=5;fillColor=none;strokeColor=#000000;strokeWidth=1;" vertex="1" parent="1">
          <mxGeometry x="240" y="495" width="800" height="230" as="geometry" />
        </mxCell>
        <mxCell id="lbl_alt_cond1" value="[Data Valid &amp;amp; Nomor WhatsApp Belum Terdaftar]" style="text;html=1;align=left;verticalAlign=middle;resizable=0;points=[];fontSize=11;fontStyle=2;" vertex="1" parent="alt_box">
          <mxGeometry x="70" y="2" width="300" height="20" as="geometry" />
        </mxCell>

        <!-- Alt Action: ambilKategoriMember() -->
        <mxCell id="m13" value="ambilKategoriMember()" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="530" as="sourcePoint" />
            <mxPoint x="652" y="530" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: buatDataMember() -->
        <mxCell id="m14" value="buatDataMember(data, id_kategori)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="555" as="sourcePoint" />
            <mxPoint x="652" y="555" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: simpanMember() -->
        <mxCell id="m15" value="simpanMember(data_member)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="580" as="sourcePoint" />
            <mxPoint x="652" y="580" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: INSERT INTO customer -->
        <mxCell id="m16" value="INSERT INTO customer..." style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="652" y="600" as="sourcePoint" />
            <mxPoint x="832" y="600" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: return id_customer from DB -->
        <mxCell id="m17" value="return (id_customer)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="832" y="620" as="sourcePoint" />
            <mxPoint x="452" y="620" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: ambilInfoPotonganMember() -->
        <mxCell id="m18" value="ambilInfoPotonganMember(id_kategori)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="645" as="sourcePoint" />
            <mxPoint x="652" y="645" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: berhasil(id_customer) -->
        <mxCell id="m19" value="berhasil(id_customer)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="0.2" y="-15" relative="1" as="geometry">
            <mxPoint x="452" y="665" as="sourcePoint" />
            <mxPoint x="452" y="685" as="targetPoint" />
            <Array as="points">
              <mxPoint x="495" y="665" />
              <mxPoint x="495" y="685" />
            </Array>
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Action: tampilKonfirmasi() -->
        <mxCell id="m20" value="tampilKonfirmasi()" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="700" as="sourcePoint" />
            <mxPoint x="990" y="700" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Alt Divider Line -->
        <mxCell id="alt_line" value="" style="line;strokeWidth=1;dashed=1;labelBackgroundColor=none;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;fontSize=12;fontColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="240" y="710" width="800" height="5" as="geometry" />
        </mxCell>
        <mxCell id="lbl_alt_cond2" value="[Data Tidak Valid / Nomor WhatsApp Sudah Terdaftar]" style="text;html=1;align=left;verticalAlign=middle;resizable=0;points=[];fontSize=11;fontStyle=2;" vertex="1" parent="1">
          <mxGeometry x="250" y="710" width="310" height="20" as="geometry" />
        </mxCell>

        <!-- Else Return Error -->
        <mxCell id="m21_err" value="return (pesan error)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
          <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
            <mxPoint x="452" y="722" as="sourcePoint" />
            <mxPoint x="310" y="722" as="targetPoint" />
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>

        <!-- Caption -->
        <mxCell id="caption_fig55" value="&lt;b&gt;Gambar 55. Sequence Diagram Daftar Member&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
          <mxGeometry x="380" y="830" width="310" height="30" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 12. Sequence Diagram Fitur Daftar Member:
Gambar 12 memodelkan siklus lengkap registrasi member baru di website PrintCraft (sesuai Gambar 55 SRS). Customer berinteraksi dengan `view_landing_page` untuk mengakses form pendaftaran. Setelah data diisi dan dikirim melalui `form_member`, controller memvalidasi integritas data dan memeriksa keunikan nomor WhatsApp ke database melalui model `DaftarMember`. Apabila data valid, record member baru disimpan, voucher/diskon member diambil, dan pengguna dialihkan ke layar `view_konfirmasi_member`. Jika terjadi kegagalan validasi, pesan kesalahan langsung dikembalikan ke layar formulir pendaftaran.

---

### 2.3 Sequence Diagram Fitur Login Pengguna (PC-001)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Aktor (Owner, Admin) membuka browser dan mengakses URL login `/login`.
2. Form `view_login` memanggil request `GET /login` ke `AuthController` yang mengeksekusi method `showLoginForm()`, menampilkan form login.
3. Aktor mengisikan username dan password, lalu menekan tombol "Login".
4. Form `view_login` mengeksekusi request `POST /login` ke method `login(request)` pada `AuthController`.
5. `AuthController` memanggil model `Akun` via `cekKredensial(username, password)` yang memeriksa hash password ke tabel `akun` di `Database`.
6. Evaluasi kredensial:
   - Jika valid, dibuat sesi autentikasi dan dialihkan ke `view_dashboard`.
   - Jika salah, pesan kesalahan dikembalikan ke `view_login`.

#### Komponen yang Terlibat:
1. Aktor: Owner, Admin
2. Class View / Boundary: `view_login`, `view_dashboard`
3. Class Controller / Control: `AuthController`
4. Class Model / Entity: `Akun`
5. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-login" name="Sequence Login">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
<!-- Actor: Owner/Admin Top -->
<mxCell id="act_user_top" value="Owner / Admin" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="act_user_bot" value="Owner / Admin" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="580" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="line_user" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_user_bot" target="act_user_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: view_login -->
<mxCell id="ll_vlogin_top" value="view_login" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="260" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_vlogin_bot" value="view_login" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="260" y="590" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_vlogin" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vlogin_bot" target="ll_vlogin_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Control: AuthController -->
<mxCell id="ll_ctrl_top" value="AuthController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="460" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_ctrl_bot" value="AuthController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="460" y="585" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_ctrl" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_ctrl_bot" target="ll_ctrl_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: Akun -->
<mxCell id="ll_model_top" value="Akun" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="660" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_model_bot" value="Akun" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="660" y="585" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_model" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_model_bot" target="ll_model_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Database: Database -->
<mxCell id="ll_db_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="840" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_db_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="840" y="585" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_db" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_db_bot" target="ll_db_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: view_dashboard -->
<mxCell id="ll_vdash_top" value="view_dashboard" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="980" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_vdash_bot" value="view_dashboard" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="980" y="590" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_vdash" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vdash_bot" target="ll_vdash_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Messages -->
<!-- 1. Buka form login -->
<mxCell id="m1" value="Buka halaman login" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="95" y="140" as="sourcePoint" /><mxPoint x="290" y="140" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 2. showLoginForm() -->
<mxCell id="m2" value="showLoginForm() / route GET /login" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="290" y="170" as="sourcePoint" /><mxPoint x="482" y="170" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 3. return form -->
<mxCell id="m3" value="return (view_login)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="482" y="200" as="sourcePoint" /><mxPoint x="290" y="200" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 4. Submit login -->
<mxCell id="m4" value="Isikan username &amp; password, klik Login" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="95" y="240" as="sourcePoint" /><mxPoint x="290" y="240" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 5. login(request) -->
<mxCell id="m5" value="login(request) / route POST /login" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="290" y="270" as="sourcePoint" /><mxPoint x="482" y="270" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 6. cekKredensial() -->
<mxCell id="m6" value="cekKredensial(username, password)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="482" y="300" as="sourcePoint" /><mxPoint x="682" y="300" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 7. Query ke DB -->
<mxCell id="m7" value="SELECT * FROM akun WHERE username=..." style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="682" y="330" as="sourcePoint" /><mxPoint x="862" y="330" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 8. DB return record -->
<mxCell id="m8" value="return (data_akun, password_hash)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="862" y="360" as="sourcePoint" /><mxPoint x="682" y="360" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- 9. Model verify hash & return -->
<mxCell id="m9" value="return (status_valid, role, id_cabang)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="682" y="390" as="sourcePoint" /><mxPoint x="482" y="390" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>

<!-- ALT FRAME: Kredensial Valid vs Tidak Valid -->
<mxCell id="alt_login" value="alt" style="shape=umlFrame;whiteSpace=wrap;html=1;width=60;height=25;boundedLbl=1;verticalAlign=top;align=left;spacingLeft=5;fillColor=none;strokeColor=#000000;strokeWidth=1;" vertex="1" parent="1">
  <mxGeometry x="220" y="420" width="820" height="140" as="geometry" />
</mxCell>
<mxCell id="lbl_alt_true" value="[Username &amp; Password Cocok (Valid)]" style="text;html=1;align=left;verticalAlign=middle;resizable=0;points=[];fontSize=11;fontStyle=2;" vertex="1" parent="alt_login">
  <mxGeometry x="70" y="2" width="250" height="20" as="geometry" />
</mxCell>
<!-- Action True: session() -->
<mxCell id="m10_sess" value="session(auth_user)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="0.2" y="-15" relative="1" as="geometry">
    <mxPoint x="482" y="455" as="sourcePoint" /><mxPoint x="482" y="480" as="targetPoint" />
    <Array as="points"><mxPoint x="525" y="455" /><mxPoint x="525" y="480" /></Array><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- Redirect Dashboard -->
<mxCell id="m11_dash" value="redirect(&apos;/dashboard&apos;)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="482" y="495" as="sourcePoint" /><mxPoint x="1010" y="495" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<!-- Alt Divider -->
<mxCell id="alt_login_line" value="" style="line;strokeWidth=1;dashed=1;labelBackgroundColor=none;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;fontSize=12;fontColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="220" y="515" width="820" height="5" as="geometry" />
</mxCell>
<mxCell id="lbl_alt_false" value="[Username atau Password Salah]" style="text;html=1;align=left;verticalAlign=middle;resizable=0;points=[];fontSize=11;fontStyle=2;" vertex="1" parent="1">
  <mxGeometry x="230" y="515" width="220" height="20" as="geometry" />
</mxCell>
<!-- Action False: return error -->
<mxCell id="m12_err" value="return withErrors(&apos;Username atau password salah&apos;)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry">
    <mxPoint x="482" y="540" as="sourcePoint" /><mxPoint x="290" y="540" as="targetPoint" /><mxPoint as="offset" />
  </mxGeometry>
</mxCell>

<!-- Caption -->
<mxCell id="caption_fig13" value="&lt;b&gt;Gambar 13. Sequence Diagram Fitur Login Owner / Admin (PC-001)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
  <mxGeometry x="320" y="660" width="450" height="30" as="geometry" />
</mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 13. Sequence Diagram Fitur Login Pengguna:
Gambar 13 memodelkan proses autentikasi hak akses petugas workshop. Pengguna mengisi kredensial pada antarmuka `view_login`. Controller `AuthController` menerima request `POST` dan memanggil model `Akun` untuk verifikasi keamanan hash Bcrypt ke basis data. Jika kredensial cocok, pengguna diarahkan ke antarmuka dashboard sesuai hak akses cabangnya masing-masing.

---

### 2.4 Sequence Diagram Fitur Pembuatan Pesanan Sablon & DP 50% (PC-003)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas (Owner/Admin) membuka formulir pesanan baru pada antarmuka `form_pesanan`.
2. Petugas menginput data pelanggan, memilih bahan kaos, spesifikasi cetak sablon, serta mencatat pembayaran uang muka (DP minimal 50%).
3. Form `form_pesanan` mengirimkan request `POST /pesanan` ke method `store(request)` pada `PesananController`.
4. `PesananController` memvalidasi nilai uang muka terhadap total biaya kalkulasi:
   - Apabila `uang_muka >= total_harga * 0.50`, data pesanan disimpan ke model `Pesanan`, rincian item ke model `DetailPesanan`, dan bukti bayar ke model `Pembayaran`. Status pesanan otomatis diubah menjadi `Menunggu Antrean Produksi`.
   - Apabila uang muka kurang dari 50%, proses dibatalkan dan sistem mengembalikan peringatan validasi uang muka.
5. Sistem mengalihkan pengguna ke layar `view_detail_pesanan` dengan nomor pesanan resmi.

#### Komponen yang Terlibat:
1. Aktor: Owner, Admin
2. Class View / Boundary: `form_pesanan`, `view_detail_pesanan`
3. Class Controller / Control: `PesananController`
4. Class Model / Entity: `Pesanan`, `Pembayaran`
5. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-pesanan" name="Sequence Pesanan">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
<!-- Actor: Admin/Owner -->
<mxCell id="act_p_top" value="Admin / Owner" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="60" y="40" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="act_p_bot" value="Admin / Owner" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="60" y="600" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="line_p_act" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_p_bot" target="act_p_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: form_pesanan -->
<mxCell id="ll_fp_top" value="form_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="210" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_fp_bot" value="form_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="210" y="610" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_fp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_fp_bot" target="ll_fp_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Control: PesananController -->
<mxCell id="ll_pc_top" value="PesananController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="380" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_pc_bot" value="PesananController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="380" y="605" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_pc" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_pc_bot" target="ll_pc_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: Pesanan -->
<mxCell id="ll_mp_top" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="550" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_mp_bot" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="550" y="605" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_mp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_mp_bot" target="ll_mp_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: Pembayaran -->
<mxCell id="ll_mpay_top" value="Pembayaran" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="710" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_mpay_bot" value="Pembayaran" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="710" y="605" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_mpay" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_mpay_bot" target="ll_mpay_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Database: Database -->
<mxCell id="ll_pdb_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="870" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_pdb_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="870" y="605" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_pdb" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_pdb_bot" target="ll_pdb_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: view_daftar_pesanan -->
<mxCell id="ll_vdp_top" value="view_daftar_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="1010" y="50" width="70" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_vdp_bot" value="view_daftar_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="1010" y="610" width="70" height="40" as="geometry" />
</mxCell>
<mxCell id="line_vdp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vdp_bot" target="ll_vdp_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Messages -->
<mxCell id="pm1" value="Klik &apos;Buat Pesanan Baru&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="75" y="140" as="sourcePoint" /><mxPoint x="240" y="140" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm2" value="create() / route GET /pesanan/create" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="240" y="170" as="sourcePoint" /><mxPoint x="402" y="170" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm3" value="return (form_pesanan)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="402" y="200" as="sourcePoint" /><mxPoint x="240" y="200" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm4" value="Isi spesifikasi pesanan &amp; DP 50%, klik Simpan" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="75" y="240" as="sourcePoint" /><mxPoint x="240" y="240" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm5" value="store(request) / route POST /pesanan" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="240" y="270" as="sourcePoint" /><mxPoint x="402" y="270" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm6" value="simpanPesanan(data_pesanan)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="402" y="300" as="sourcePoint" /><mxPoint x="572" y="300" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm7" value="INSERT INTO pesanan (nomor_pesanan, qty, total...)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="572" y="330" as="sourcePoint" /><mxPoint x="892" y="330" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm8" value="return (id_pesanan)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="892" y="360" as="sourcePoint" /><mxPoint x="402" y="360" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm9" value="catatPembayaran(id_pesanan, nominal_dp)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="402" y="390" as="sourcePoint" /><mxPoint x="732" y="390" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm10" value="INSERT INTO pembayaran (id_pesanan, jenis=&apos;DP 50%&apos;...)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="732" y="420" as="sourcePoint" /><mxPoint x="892" y="420" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm11" value="return (id_pembayaran)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="892" y="450" as="sourcePoint" /><mxPoint x="402" y="450" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pm12" value="redirect(&apos;/pesanan&apos;) with &apos;Pesanan berhasil dibuat&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="402" y="500" as="sourcePoint" /><mxPoint x="1045" y="500" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>

<mxCell id="caption_fig_pesanan" value="&lt;b&gt;Sequence Diagram Fitur Transaksi Pesanan dan Pembayaran DP (PC-003)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
  <mxGeometry x="300" y="670" width="490" height="30" as="geometry" />
</mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Sequence Diagram Fitur Pesanan dan Pembayaran DP 50%:
Diagram ini memodelkan kepatuhan klausul bisnis utama PrintCraft di mana pengerjaan sablon kaos hanya dapat dimulai apabila pelanggan telah menyetorkan uang muka sekurang-kurangnya 50% dari total estimasi tagihan. Controller bertindak sebagai validator ketat sebelum entitas pesanan dan mutasi pembayaran dicatat permanen ke dalam tabel database.

---

### 2.5 Sequence Diagram Fitur Pengadaan Stok Kaos Polos (PC-004)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas workshop membuka menu pengadaan kaos pada antarmuka `form_pengadaan`.
2. Petugas memilih vendor rekanan dan menginput rincian kaos (tipe bahan, warna, dan ukuran) sesuai kebutuhan pesanan.
3. Form `form_pengadaan` mengirimkan request `POST /pengadaan` ke method `store(request)` pada `PengadaanController`.
4. `PengadaanController` memvalidasi data dan menerbitkan Purchase Order (PO) baru melalui model `PengadaanKaos` ke tabel `Database`.
5. Saat paket kaos tiba di cabang workshop, petugas mengklik tombol konfirmasi tiba di `view_pengadaan`.
6. Controller menjalankan `updateStatusTiba(id)` yang memperbarui status bahan baku menjadi tersedia, sehingga antrean produksi sablon dapat segera diproses.

#### Komponen yang Terlibat:
1. Aktor: Owner, Admin
2. Class View / Boundary: `form_pengadaan`, `view_pengadaan`
3. Class Controller / Control: `PengadaanController`
4. Class Model / Entity: `PengadaanKaos`
5. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-pengadaan" name="Sequence Pengadaan">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
<!-- Actor: Admin Cabang -->
<mxCell id="act_po_top" value="Admin Cabang" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="act_po_bot" value="Admin Cabang" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="550" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="line_po_act" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_po_bot" target="act_po_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: form_pengadaan -->
<mxCell id="ll_fpo_top" value="form_pengadaan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="250" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_fpo_bot" value="form_pengadaan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="250" y="560" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_fpo" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_fpo_bot" target="ll_fpo_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Control: PengadaanController -->
<mxCell id="ll_poc_top" value="PengadaanController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="450" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_poc_bot" value="PengadaanController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="450" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_poc" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_poc_bot" target="ll_poc_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: PengadaanKaos -->
<mxCell id="ll_mpo_top" value="PengadaanKaos" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="650" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_mpo_bot" value="PengadaanKaos" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="650" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_mpo" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_mpo_bot" target="ll_mpo_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Database: Database -->
<mxCell id="ll_podb_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="840" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_podb_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="840" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_podb" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_podb_bot" target="ll_podb_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Messages -->
<mxCell id="pom1" value="Pilih pesanan &amp; klik &apos;Buat PO Vendor&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="95" y="140" as="sourcePoint" /><mxPoint x="280" y="140" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom2" value="create(id_pesanan) / route GET /pengadaan/create" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="280" y="170" as="sourcePoint" /><mxPoint x="472" y="170" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom3" value="return (form_pengadaan)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="200" as="sourcePoint" /><mxPoint x="280" y="200" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom4" value="Input nama supplier &amp; qty, klik Kirim PO" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="95" y="240" as="sourcePoint" /><mxPoint x="280" y="240" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom5" value="store(request) / route POST /pengadaan" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="280" y="270" as="sourcePoint" /><mxPoint x="472" y="270" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom6" value="simpanPO(data_po)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="300" as="sourcePoint" /><mxPoint x="672" y="300" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom7" value="INSERT INTO pengadaan_kaos (nomor_po, supplier, status=&apos;Dipesan&apos;...)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="672" y="330" as="sourcePoint" /><mxPoint x="862" y="330" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom8" value="return (id_pengadaan, nomor_po)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="862" y="360" as="sourcePoint" /><mxPoint x="472" y="360" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="pom9" value="return status PO Diterbitkan" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="400" as="sourcePoint" /><mxPoint x="280" y="400" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>

<!-- Caption -->
<mxCell id="caption_fig14" value="&lt;b&gt;Gambar 14. Sequence Diagram Fitur Pengadaan Stok Kaos (PC-004)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
  <mxGeometry x="300" y="630" width="460" height="30" as="geometry" />
</mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 14. Sequence Diagram Fitur Pengadaan Stok Kaos:
Gambar 14 memodelkan alur pengadaan bahan baku kaos polos ke vendor pihak ketiga. Sistem mencatat penerbitan PO pengadaan dan menghubungkannya dengan pesanan sablon terkait. Ketika stok bahan tiba dan dikonfirmasi di workshop, status pesanan secara otomatis dialirkan ke tahap sablon siap cetak.

---

### 2.6 Sequence Diagram Fitur Cetak Invoice dan WOP (PC-005)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas membuka halaman detail pesanan (`view_detail_pesanan`) dan menekan tombol "Cetak Invoice" atau "Cetak WOP".
2. View mengirimkan request `GET /pesanan/{id}/invoice` atau `GET /pesanan/{id}/wop` ke `DokumenController`.
3. `DokumenController` mengeksekusi `cetakInvoice(id)` atau `cetakWOP(id)` dengan memanggil data transaksi dari model `Pesanan` dan `Pembayaran`.
4. Khusus dokumen WOP, Controller secara otomatis memfilter dan menghapus seluruh informasi harga serta rincian tarif sebelum dicetak.
5. Controller memanggil library `Dompdf` melalui method `generatePDF(view, data)` untuk merender template Blade menjadi berkas PDF A4.
6. Berkas stream PDF dikembalikan ke browser pengguna pada jendela `view_pdf_preview` untuk diunduh atau dicetak langsung ke printer.

#### Komponen yang Terlibat:
1. Aktor: Owner, Admin
2. Class View / Boundary: `view_detail_pesanan`, `view_pdf_preview`
3. Class Controller / Control: `DokumenController`
4. Class Model / Entity: `Pesanan`, `Pembayaran`
5. Library: `Dompdf`
6. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-invoice" name="Sequence Invoice">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
<!-- Actor: Admin/Owner -->
<mxCell id="act_inv_top" value="Admin / Owner" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="act_inv_bot" value="Admin / Owner" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="550" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="line_inv_act" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_inv_bot" target="act_inv_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: view_detail_pesanan -->
<mxCell id="ll_vdp_top" value="view_detail_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="250" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_vdp_bot" value="view_detail_pesanan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="250" y="560" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_vdp" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vdp_bot" target="ll_vdp_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Control: DokumenController -->
<mxCell id="ll_dokc_top" value="DokumenController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="450" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_dokc_bot" value="DokumenController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="450" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_dokc" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_dokc_bot" target="ll_dokc_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: Pesanan -->
<mxCell id="ll_mpes_top" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="640" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_mpes_bot" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="640" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_mpes" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_mpes_bot" target="ll_mpes_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Library: Dompdf -->
<mxCell id="ll_pdf_top" value="Dompdf" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="820" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_pdf_bot" value="Dompdf" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="820" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_pdf" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_pdf_bot" target="ll_pdf_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Database: Database -->
<mxCell id="ll_invdb_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="980" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_invdb_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="980" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_invdb" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_invdb_bot" target="ll_invdb_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Messages -->
<mxCell id="im1" value="Klik tombol &apos;Cetak Invoice&apos;" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="95" y="140" as="sourcePoint" /><mxPoint x="280" y="140" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im2" value="cetakInvoice(id) / route GET /pesanan/{id}/invoice" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="280" y="170" as="sourcePoint" /><mxPoint x="472" y="170" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im3" value="getDetailPesananDanBayar(id)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="200" as="sourcePoint" /><mxPoint x="662" y="200" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im4" value="SELECT * FROM pesanan JOIN customer JOIN pembayaran..." style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="662" y="230" as="sourcePoint" /><mxPoint x="1002" y="230" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im5" value="return (record data transaksi)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="1002" y="260" as="sourcePoint" /><mxPoint x="472" y="260" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im6" value="generatePDF(view_invoice_pdf, data)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="300" as="sourcePoint" /><mxPoint x="842" y="300" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im7" value="return stream (dokumen_invoice.pdf)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="842" y="340" as="sourcePoint" /><mxPoint x="472" y="340" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="im8" value="tampilkan pratinjau PDF / buka dialog cetak" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="472" y="380" as="sourcePoint" /><mxPoint x="280" y="380" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>

<!-- Caption -->
<mxCell id="caption_fig15" value="&lt;b&gt;Gambar 15. Sequence Diagram Fitur Cetak Invoice PDF (PC-005)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
  <mxGeometry x="320" y="630" width="450" height="30" as="geometry" />
</mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 15. Sequence Diagram Fitur Cetak Invoice dan WOP:
Gambar 15 memodelkan proses pembuatan dokumen transaksi PDF. Controller mengekstraksi data pesanan dari database, memformatnya ke dalam template Blade cetak ukuran A4, dan memprosesnya lewat library Dompdf. Perbedaan fundamental terletak pada proteksi data: dokumen Invoice mencantumkan rincian keuangan lengkap untuk customer, sedangkan dokumen WOP menyembunyikan kolom harga demi kerahasiaan operasional workshop sablon.

---

### 2.7 Sequence Diagram Fitur Dashboard dan Rekap Laporan (PC-006)

#### Pemetaan Aktivitas Use Case ke Function Class Diagram:
1. Petugas (Owner/Admin) mengakses menu laporan pada antarmuka `view_laporan` dan memilih rentang tanggal serta filter cabang.
2. Form `view_laporan` mengirimkan request `GET /laporan` ke `LaporanController`.
3. `LaporanController` mengeksekusi `filterLaporan(cabang_id, periode)`. Sistem memvalidasi hak akses: Owner dapat melihat seluruh cabang, sedangkan Admin terkunci pada cabangnya sendiri.
4. Controller mengeksekusi kueri agregasi total pendapatan, piutang, dan volume sablon melalui model `Pesanan` dan `Pembayaran` ke basis data.
5. Hasil kalkulasi agregasi dikembalikan oleh Database ke Controller.
6. Controller mengembalikan data terstruktur ke antarmuka `view_laporan` untuk disajikan dalam bentuk diagram visual tren dan tabel rekapitulasi.

#### Komponen yang Terlibat:
1. Aktor: Owner, Admin
2. Class View / Boundary: `view_dashboard`, `view_laporan`
3. Class Controller / Control: `LaporanController`
4. Class Model / Entity: `Pesanan`, `Pembayaran`
5. Class Database: `Database`

#### Kode Draw.io XML:
```xml
<mxfile host="app.diagrams.net" modified="2026-11-08T16:00:00.000Z" agent="Antigravity" version="24.0.0">
  <diagram id="seq-dashboard" name="Sequence Dashboard">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" background="#ffffff" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
<!-- Actor: Owner/Admin -->
<mxCell id="act_dash_top" value="Owner / Admin" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="act_dash_bot" value="Owner / Admin" style="shape=umlActor;verticalLabelPosition=top;verticalAlign=bottom;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="80" y="550" width="30" height="60" as="geometry" />
</mxCell>
<mxCell id="line_dash_act" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="act_dash_bot" target="act_dash_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Boundary: view_laporan -->
<mxCell id="ll_vlap_top" value="view_laporan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="260" y="50" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="ll_vlap_bot" value="view_laporan" style="shape=umlBoundary;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="260" y="560" width="60" height="40" as="geometry" />
</mxCell>
<mxCell id="line_vlap" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_vlap_bot" target="ll_vlap_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Control: LaporanController -->
<mxCell id="ll_lapc_top" value="LaporanController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="460" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_lapc_bot" value="LaporanController" style="shape=umlControl;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="460" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_lapc" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_lapc_bot" target="ll_lapc_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Entity: Pesanan -->
<mxCell id="ll_rekap_top" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="660" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_rekap_bot" value="Pesanan" style="shape=umlEntity;whiteSpace=wrap;html=1;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="660" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_rekap" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_rekap_bot" target="ll_rekap_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Database: Database -->
<mxCell id="ll_lapdb_top" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="850" y="45" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="ll_lapdb_bot" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=10;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="850" y="555" width="45" height="50" as="geometry" />
</mxCell>
<mxCell id="line_lapdb" value="" style="endArrow=none;dashed=1;html=1;rounded=0;strokeWidth=1;" edge="1" parent="1" source="ll_lapdb_bot" target="ll_lapdb_top">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Messages -->
<mxCell id="dm1" value="Pilih filter cabang &amp; bulan, klik Tampilkan" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="95" y="140" as="sourcePoint" /><mxPoint x="290" y="140" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="dm2" value="filterLaporan(cabang_id, periode) / route GET /laporan" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="290" y="170" as="sourcePoint" /><mxPoint x="482" y="170" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="dm3" value="cekHakAkses(role, cabang_id)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="0.2" y="-15" relative="1" as="geometry"><mxPoint x="482" y="195" as="sourcePoint" /><mxPoint x="482" y="220" as="targetPoint" />
    <Array as="points"><mxPoint x="525" y="195" /><mxPoint x="525" y="220" /></Array><mxPoint as="offset" />
  </mxGeometry>
</mxCell>
<mxCell id="dm4" value="getRekapKeuangan(cabang_id, periode)" style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="482" y="250" as="sourcePoint" /><mxPoint x="682" y="250" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="dm5" value="SELECT SUM(total_harga), SUM(jumlah_bayar)..." style="endArrow=block;html=1;rounded=0;strokeWidth=1.5;endFill=1;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="682" y="280" as="sourcePoint" /><mxPoint x="872" y="280" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="dm6" value="return (rekapitulasi_data)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="872" y="310" as="sourcePoint" /><mxPoint x="482" y="310" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>
<mxCell id="dm7" value="return (view_laporan, data_rekap, grafik)" style="endArrow=open;dashed=1;html=1;rounded=0;strokeWidth=1.5;endFill=0;" edge="1" parent="1">
  <mxGeometry x="-0.05" y="-12" relative="1" as="geometry"><mxPoint x="482" y="360" as="sourcePoint" /><mxPoint x="290" y="360" as="targetPoint" /><mxPoint as="offset" /></mxGeometry>
</mxCell>

<!-- Caption -->
<mxCell id="caption_fig16" value="&lt;b&gt;Gambar 16. Sequence Diagram Fitur Dashboard dan Rekap Laporan (PC-006)&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=13;" vertex="1" parent="1">
  <mxGeometry x="300" y="630" width="490" height="30" as="geometry" />
</mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

#### Penjelasan Gambar 16. Sequence Diagram Fitur Dashboard dan Rekap Laporan:
Gambar 16 memodelkan pengolahan data intelijen bisnis workshop PrintCraft. Pengguna memilih parameter periode dan cabang di antarmuka laporan. Controller menjalankan kalkulasi matematis terhadap seluruh transaksi yang tersimpan di basis data, lalu memvisualisasikan hasilnya dalam bentuk ringkasan keuangan dan grafik performa workshop.

---
*Dokumen ini disusun untuk memenuhi kelengkapan Tugas 5 TPDB Sistem Informasi Workshop PrintCraft sesuai standar pedoman dosen dan dokumen SRS.*
