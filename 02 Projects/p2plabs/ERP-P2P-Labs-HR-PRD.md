---
title: ERP P2P Labs — PRD Modul Human Resource
aliases:
  - ERP HR PRD
  - erp.p2plabs.asia
company: P2P Labs
product: ERP P2P Labs
module: Human Resource
document_type: prd
version: 0.9.0
date: 2026-10-22
status: draft-for-founder-review
host: erp.p2plabs.asia
tags:
  - project
  - decision
  - erp
  - hr
  - payroll
related:
  - "[[02 Projects/P2P Labs|P2P Labs]]"
  - "[[p2plabs/P2P-Labs-Brand]]"
  - "[[Home]]"
  - "[[02 Projects/Projects MOC|Projects MOC]]"
---

# ERP P2P Labs — PRD Modul Human Resource

> [!success] Apa dokumen ini
> Spesifikasi modul orang untuk ERP internal P2P Labs. Host yang disepakati: `erp.p2plabs.asia`. Acuan menu: tangkapan layar Mekari Talenta (22 Oktober 2026). Acuan hukum: teks yang masih hidup pada tanggal note ini, disimpan sebagai **aturan berversi**, bukan angka yang diketik mati di kode.

> [!danger] Bukan tiga hal ini
> Bukan klon Talenta. Bukan fitur di situs statis `p2plabs.asia`. Bukan izin untuk memindahkan uang, memotong pajak, atau melapor ke DJP / BPJS tanpa orang yang mengunci angkanya.
>
> Rumus di bawah adalah bahan konfigurasi. Sebelum slip pertama dikunci, seorang manusia membuka teks resmi yang dikutip dan mencocokkan satu karyawan sungguhan dengan hitungan manual.

## 0. Keputusan yang sudah dikunci — 2026-10-22

- Produk internal. Nama: **ERP P2P Labs**. Modul pertama: **Human Resource**.
- Alamat nanti: `erp.p2plabs.asia`. Repo terpisah, proses terpisah, basis data terpisah. Bukan folder di `/var/www/p2plabs.asia`. Bukan bagian dari rsync newsroom.
- Kotak newsroom (`116.206.196.6`, 1 vCPU, 1 GB, nginx statis) tidak menjalankan aplikasi ini.
- Joe mencari VPS yang lebih besar, atau server sendiri. Kandidat yang dia sebut 22 Oktober 2026: PC di rumah, IP statis ISP `103.145.240.52`. Belum dibeli, belum diarahkan DNS-nya. PRD ini tidak membeli apa pun.
- v1 yang menggantikan langganan untuk studio kecil: data karyawan, kontrak, absensi satu kantor, cuti, lembur sederhana, slip gaji yang dikunci manusia, lalu transfer bank manual.
- PPh 21 dan BPJS dihitung, lalu ditinjau orang. Tidak ada potong-otomatis yang langsung dianggap benar.
- Tidak ada auto-pay, virtual account, earned wage, e-Bupot, face recognition, live tracking, ATS, atau LMS di v1.
- Tautan footer situs publik menunggu keputusan terpisah. Jangan dipasang bersama modul ini.

## 1. Masalah

Langganan HR yang sekarang terasa mubazir untuk ukuran studio. Yang benar-benar dipakai: siapa karyawannya, kontraknya sampai kapan, masuk atau tidak, cuti dan izin, lembur, dan slip yang bisa dicek sebelum ditransfer.

Menu Talenta yang difoto jauh lebih lebar dari kebutuhan itu. Sebagian adalah produk mitra (pencairan bank, Klikpajak, outsourcing payroll, mesin sidik jari, liveness). Menyalinnya berarti membangun perusahaan lain di dalam perusahaan sendiri, plus menyimpan data gaji, NIK, dan kesehatan di tempat yang salah.

## 2. Siapa memakai

| Peran | Boleh | Tidak boleh |
|---|---|---|
| Pemilik / admin HR | Data orang, kontrak, jadwal, koreksi absen, setujui cuti dan lembur, jalankan draf gaji, kunci slip, unduh CSV transfer | Mengubah slip yang sudah terkunci. Melihat sandi. Mengirim NIK lewat email |
| Karyawan (ESS) | Clock milik sendiri, ajukan cuti / izin / lembur, lihat saldo cuti, unduh slip milik sendiri, ubah kontak darurat | Melihat gaji orang lain, mengunci payroll, mengubah saldo sendiri |
| Peninjau kedua | Dibuka kalau jumlah orang naik. Menyetujui kunci slip yang disiapkan admin | Mengubah komponen setelah kunci |

v1 boleh satu orang (Joe) sebagai admin, dengan jejak audit. Risikonya: orang yang sama menyusun dan mengunci. Jejak waktu tetap wajib. Peninjau kedua jadi syarat sebelum gaji karyawan di luar pemilik ikut ditransfer rutin.

## 3. Peta menu Talenta

Fase: **v1** dibangun dulu. **Nanti** ada tempatnya di model data, tidak di layar pertama. **Tidak** tidak dibangun sebagai produk. **Mitra** adalah jasa keuangan atau pajak; ERP hanya menyimpan angka untuk manusia, tidak menyalin produknya.

### Kehadiran

| Menu di foto | Fase | Arti di ERP ini |
|---|---|---|
| Absensi online | v1 | Clock masuk dan pulang dari HP, satu kantor. GPS jadi peringatan, bukan pemecatan otomatis |
| Liveness / wajah | Tidak | Tidak ada vendor biometrik. Foto opsional hanya bukti clock, bukan pengenalan wajah |
| Cuti | v1 | Jenis, saldo, ajuan, setuju, tolak |
| Timesheet | v1 tipis | Log clock harian adalah timesheet-nya. Tidak ada kolaborasi proyek antar-tim |
| Lembur | v1 | Ajuan, setuju, hitung PP 35/2021, masuk draf slip |
| Live tracking | Tidak | Tidak melacak posisi karyawan sepanjang hari |
| Portal mesin sidik jari | Tidak | Tidak ada mesin, tidak ada integrasi alat |
| Shift | v1 satu jadwal | Pilih pola 5 hari atau 6 hari. Rotasi, lintas malam, dan multi-cabang nanti |

### Payroll, kompensasi, benefit

| Menu di foto | Fase | Arti di ERP ini |
|---|---|---|
| Hitung gaji | v1 | Draf per orang, baris bisa dicek, lalu kunci |
| Laporan | v1 | Rekap slip terkunci per periode. Bukan dasbor prediksi |
| Pencairan / virtual account | Mitra, tidak dikloning | CSV untuk transfer manual. Tidak ada saldo perusahaan di dalam ERP |
| Slip digital | v1 | PDF di ESS, setelah terkunci |
| AI reimbursement | Nanti, tanpa AI | Kuitansi, nominal, setuju, masuk slip. Tidak ada model yang "membaca" bon |
| Kompensasi | v1 | Komponen slip dikonfigurasi. Struktur dan skala upah menyusul setelah ambang PP 49/2025 dicek |
| Expense / perjalanan | Nanti | Satu alur dengan reimbursement |
| Benefit karyawan | v1 terbatas | Hanya iuran yang memotong atau ditanggung perusahaan di slip |
| Outsourcing payroll | Tidak | Orang internal yang mengunci |
| e-Bupot lewat Coretax | Nanti | Ekspor bukti yang manusia unggah. Tidak ada lapor otomatis |

### Administrasi HR

| Menu di foto | Fase | Arti di ERP ini |
|---|---|---|
| Database karyawan | v1 | Identitas kerja, kontrak aktif, kontak, rekening, status pajak, BPJS |
| ESS | v1 | Layar karyawan di tabel peran |
| Aset dan akses | Nanti | Laptop dan akun tidak menghalangi slip pertama |
| Komunikasi internal | Tidak | Chat tetap di alat yang sudah dipakai |
| Template dokumen | Nanti | Kontrak v1 cukup unggah PDF yang sudah ditandatangani |
| Request dan survei | Tidak di v1 | Cuti, izin, dan lembur sudah berupa request. Survei tidak |
| Onboarding / offboarding | v1 tipis | Ceklis di kontrak: NIK, rekening, BPJS, tanggal mulai, tanggal akhir. Alur tugas lengkap nanti |
| Tugas dan proyek | Tidak | Bukan modul HR |
| Helpdesk HR | Tidak | Permintaan lewat cuti, izin, atau koreksi absen |

### Akuisisi, pengembangan, AI, integrasi

| Menu di foto | Fase | Arti di ERP ini |
|---|---|---|
| Rekrutmen / ATS | Tidak | Lowongan tidak hidup di ERP ini |
| Asesmen kandidat | Tidak | |
| Manpower planning | Tidak | |
| Performance / KPI | Nanti | Catatan periode, bukan nine-box |
| Talent management | Tidak | |
| LMS | Tidak | |
| HR analytics | v1 polos | Jumlah orang, cuti terpakai, jam lembur, total slip terkunci |
| Talenta AI / chatbot | Tidak | |
| Integrasi ERP | v1 adalah modulnya | Tidak ada konektor ke Talenta |
| Tanda tangan digital | Nanti | v1 menyimpan PDF yang ditandatangani di luar sistem |
| Klikpajak | Mitra, tidak dikloning | Sama seperti e-Bupot |

## 4. v1 yang harus selesai sebelum langganan boleh dilepas

1. Admin membuat karyawan dan satu kontrak aktif (PKWT atau PKWTT).
2. Karyawan clock masuk dan pulang. Admin mengoreksi dengan alasan. Jejak lama tetap ada.
3. Karyawan mengajukan cuti atau izin. Saldo bergerak hanya setelah disetujui.
4. Lembur: perintah admin atau ajuan karyawan, persetujuan tercatat, hitung sesuai aturan aktif, masuk draf.
5. Admin menjalankan periode gaji. Setiap baris kelihatan. Admin mengunci. Slip tidak bisa disunting.
6. Karyawan mengunduh slip sendiri. Admin mengunduh CSV rekening dan nominal bersih untuk transfer manual.
7. THR adalah periode terpisah, dengan pengingat H-7 hari raya orang itu, dan kunci sendiri.
8. Akhir PKWT menghitung uang kompensasi sebagai draf. Manusia mengunci sebelum dibayar.
9. Cadangan terenkripsi di luar kotak ERP, dan satu uji pulihkan, selesai sebelum slip sungguhan pertama.

Kalau butir 9 belum, payroll sungguhan tidak dinyalakan.

## 5. Model data

Satu perusahaan dulu. `company_id` tetap ada di setiap tabel supaya cabang kedua tidak memaksa migrasi, tapi layar v1 tidak menampilkan pemilih perusahaan.

### Orang (`person`)

- Nama, nama panggilan, surel kerja, HP, kontak darurat.
- NIK 16 digit. Disimpan terenkripsi. Bukan nama pengguna, bukan isi email, bukan isi log.
- NPWP hanya kalau berbeda dari NIK yang sudah diaktivasi. Cabang memakai NITKU 22 digit, dan itu bukan NPWP. Cek format bukan bukti terdaftar. Tidak ada lookup publik DJP.
- Status PTKP di awal tahun pajak (`TK/0` … `K/3`, plus `K/I/*` kalau penghasilan istri digabung). Perubahan tengah tahun dicatat, tidak mengubah kategori TER tahun berjalan sampai aturan aktif berkata lain.
- Agama atau hari raya untuk THR: Idulfitri, Natal, Nyepi, Waisak, Imlek. Kosong tidak boleh saat THR dihitung.
- Rekening: bank, nomor, nama pemilik. Terenkripsi. Tidak ikut ke CSV kecuali saat unduh transfer.
- Tanggal masuk, status: `calon`, `aktif`, `cuti_panjang_khusus`, `berakhir`.
- Lokasi kerja (kota) karena lantai upah mengikuti tempat orang itu bekerja, bukan alamat PT di akta kalau berbeda.

### Kontrak (`contract`)

- Jenis: `PKWTT` atau `PKWT`.
- PKWT wajib punya tanggal akhir. Sistem mengingatkan 60 dan 30 hari sebelumnya.
- Jabatan, pola waktu kerja (`5x8` atau `6x7`), upah pokok, daftar tunjangan tetap, daftar tunjangan tidak tetap.
- Golongan tanpa lembur hanya kalau tertulis di kontrak **dan** upahnya lebih tinggi (PP 35/2021 Pasal 27). Default: setiap orang tetap dapat lembur. Kosongnya klausul berarti lembur tetap dibayar.
- Status: `draf`, `aktif`, `segera_berakhir`, `berakhir`.
- Satu orang satu kontrak `aktif`.
- File PDF kontrak tersimpan, bukan digenerate di v1.
- Peringatan kalau PKWT kumulatif mendekati 5 tahun. Manusia yang memutuskan perpanjang atau pindah ke PKWTT. Sistem tidak mengalihkannya sendiri.

### Jadwal (`schedule`)

- Satu jadwal kantor di v1: hari kerja, jam masuk, jam pulang, toleransi terlambat (menit), titik kantor, radius peringatan meter.
- Hari libur nasional diimpor sebagai tanggal, sumber dan tahun tercatat. Bukan scrape diam-diam setiap malam tanpa versi.

### Absensi (`attendance_day` + `attendance_event`)

- Event: `in`, `out`, sumber `phone` atau `admin`, waktu perangkat, waktu server, koordinat, jarak dari kantor, di dalam radius atau tidak.
- Hari: `lengkap`, `kurang`, `terkoreksi`, `cuti`, `izin`, `sakit`, `libur`, `off`, `alpha`.
- Koreksi menambah event baru. Event lama tidak dihapus.
- Di luar radius tetap tercatat, dengan badge. Tidak menolak clock. Kerja dari rumah adalah keputusan jadwal, bukan pelanggaran otomatis.

### Cuti (`leave_type`, `leave_balance`, `leave_request`)

- Jenis membawa: bayar atau tidak, memotong saldo atau tidak, butuh lampiran atau tidak, plafond hari, dasar aturan.
- Saldo per orang per tahun: dapat, terpakai, menunggu, sisa.
- Ajuan: `draf`, `diajukan`, `disetujui`, `ditolak`, `dibatalkan`.
- Saldo berkurang saat disetujui, bukan saat diajukan. Batal setelah setuju mengembalikan saldo kalau tanggal itu belum masuk slip terkunci.
- Cuti bersama tidak memotong cuti tahunan kecuali aturan perusahaan yang tersimpan berkata demikian.

### Lembur (`overtime_request`)

- Tanggal, jam mulai, jam selesai, istirahat di tengah, alasan.
- Status: `diajukan`, `disetujui`, `ditolak`, `dihitung`, `masuk_draf`, `terbayar`.
- Persetujuan menyimpan siapa, kapan, dan kanal (`app`). Itu cukup sebagai persetujuan digital Pasal 28.
- Menit di bawah kelipatan yang ditentukan aturan dibulatkan sesuai versi aturan, dan cara bulatnya tertulis di slip.

### Penggajian

- `pay_component`: kode, nama, jenis (`earning`, `deduction`, `employer_info`), kena pajak atau tidak, masuk dasar BPJS atau tidak, masuk dasar lembur atau tidak.
- `pay_run`: jenis `bulanan`, `thr`, `kompensasi_pkwt`, `penyesuaian`. Periode. Status `draf`, `ditinjau`, `terkunci`.
- `pay_slip`: satu per orang per run. Bruto, dasar lembur, dasar BPJS, dasar TER, potongan, bersih, jejak versi aturan.
- `pay_slip_line`: komponen, kuantitas, tarif, jumlah, rumus yang kepakai (teks), bukan hanya angka jadi.
- Slip `terkunci` tidak punya operasi update. Salah hitung diselesaikan dengan run `penyesuaian` yang menunjuk slip lama.
- CSV transfer lahir hanya dari slip terkunci: nama rekening, bank, nomor, nominal bersih. Tidak memuat NIK.

## 6. Alur

### Clock

1. Karyawan menekan masuk. Server mencatat waktu Jakarta dan jarak ke kantor.
2. Pulang sama.
3. Hari tanpa clock tetap `kurang` sampai ada cuti, izin, libur, atau koreksi.
4. Admin yang mengisi koreksi menulis alasan. Karyawan melihat koreksi itu di hari yang sama.

### Cuti dan izin

1. Karyawan memilih jenis dan tanggal. Sistem menolak kalau sisa tidak cukup untuk jenis yang memotong saldo.
2. Admin setuju atau tolak, dengan catatan.
3. Hari yang disetujui tidak lagi `kurang`.
4. Izin tidak berbayar tidak memotong cuti tahunan dan tidak menciptakan upah.

### Lembur

1. Ada ajuan atau perintah, lalu persetujuan sebelum hitung.
2. Jam di hari kerja biasa yang membuat total lewat 4 jam sehari atau 18 jam seminggu ditandai. Manusia yang memutuskan tetap menyetujui atau memotong. Lembur di istirahat mingguan dan hari libur resmi tidak masuk plafon 4/18 itu (Pasal 26 ayat 2).
3. Kalau satu hari lembur 4 jam atau lebih, slip internal menandai kewajiban makan dan minum minimal 1.400 kkal. Itu bukan uang. Tidak ada baris "uang makan lembur" otomatis (Pasal 29).
4. Hasil hitung masuk draf periode. Belum terbayar sebelum slip terkunci.

### Gaji bulan

1. Admin memilih bulan. Sistem menyusun draf dari kontrak aktif, absensi, cuti tidak berbayar, lembur disetujui, komponen tetap, dan aturan yang berlaku di tanggal periode.
2. Tiap orang satu layar: earning, potongan karyawan, iuran perusahaan (informasi, tidak mengurangi bersih), bersih.
3. Admin menandai ditinjau, lalu mengunci. Kunci meminta ketik ulang periode.
4. Setelah kunci, PDF slip tersedia untuk orang itu. CSV transfer tersedia untuk admin.
5. Transfer terjadi di aplikasi bank, di luar ERP. ERP tidak menyimpan bukti mutasi sebagai "sudah dibayar" kecuali admin mengetik tanggal transfer dengan tangan.

### THR

Periode sendiri. Dasar upah sesuai Permenaker 6/2016 (upah bersih tanpa tunjangan, atau pokok + tunjangan tetap — ikuti struktur yang tersimpan di kontrak). Masa kerja 12 bulan atau lebih = 1 bulan upah. Satu bulan sampai di bawah 12 bulan = masa kerja / 12 × 1 bulan upah. Di bawah 1 bulan = tidak dapat. Dibayar rupiah, paling lambat 7 hari sebelum hari raya orang itu. Terlambat: hitung denda 5% sebagai peringatan; THR-nya tetap terutang. Denda tidak menambahkan dirinya sendiri ke slip tanpa keputusan admin.

Orang yang sedang cuti dan masih punya hubungan kerja tetap masuk run THR.

### Akhir PKWT

Saat kontrak berakhir, draf kompensasi terbit. Belum tercampur ke gaji bulan kecuali admin memindahkannya dengan sadar. Rumus di bagian 7. Usaha mikro dan kecil bisa menyepakati angka lain; cek dulu apakah P2P masuk pengecualian itu sebelum rumus penuh dikunci.

## 7. Mesin aturan

Setiap rumus hidup di baris `rule_version`: kode, berlaku mulai, berlaku sampai, kutipan, isi JSON, siapa yang mengesahkan. Kalkulator menolak jalan kalau tidak ada versi aktif. Mengganti undang-undang berarti baris baru, bukan edit baris lama. Slip terkunci menyimpan id versi yang dipakai.

**Jangan menyalin angka 3 jam / 14 jam.** Itu plafon Kepmenakertrans 102/MEN/VI/2004. Blog HR, termasuk tulisan yang masih beredar di 2026, masih mengutipnya. Pasal 26 PP 35/2021 yang hidup: paling lama **4 jam sehari dan 18 jam seminggu**.

### 7.1 Waktu kerja normal

PP 35/2021, definisi waktu kerja lembur, masih tampil di salinan JDIH:

- 6 hari seminggu: 7 jam sehari dan 40 jam seminggu.
- 5 hari seminggu: 8 jam sehari dan 40 jam seminggu.

P2P belum memilih. Sebelum dipilih, lembur hari libur tidak boleh dihitung, karena tabel pengalinya berbeda.

### 7.2 Upah sejam

Pasal 32:

- Upah sejam = 1/173 × upah sebulan yang menjadi dasar.
- Komponen hanya pokok + tunjangan tetap: dasar = 100% dari jumlah itu.
- Ada tunjangan tidak tetap, dan pokok + tunjangan tetap **lebih kecil dari 75%** upah keseluruhan: dasar dinaikkan menjadi 75% upah keseluruhan.
- Kalau pokok + tunjangan tetap sudah 75% atau lebih, dasar tetap jumlah keduanya, bukan seluruh slip. Lembur, THR, dan bonus tidak masuk dasar ini.

Pasal 33 ayat (3): untuk upah harian, kalau upah sebulan hasil konversi di bawah upah minimum wilayah tempat orang bekerja, dasar lembur memakai upah minimum itu. Untuk karyawan bulanan, kalau dasar Pasal 32 jatuh di bawah UM wilayah kerja, sistem **memperingatkan**, tidak mengangkat angkanya diam-diam, sampai ayatnya ditempel di versi aturan.

Konversi upah harian ke bulanan, kalau nanti ada: ×25 untuk pola 6 hari, dan faktor pola 5 hari diambil dari ayat yang sama saat dikode. Jangan menebak 21 atau 22.

### 7.3 Pengali lembur

Pasal 31, dicocokkan ke salinan PDF JDIH BPK (bukan ke tabel blog yang memotong jam ke-12):

| Situasi | Jam | Pengali |
|---|---|---|
| Hari kerja biasa | Jam pertama | 1,5× |
| Hari kerja biasa | Jam berikutnya | 2× |
| Istirahat mingguan atau libur resmi, pola 5 hari | Jam 1–8 | 2× |
| Pola 5 hari, hari yang sama | Jam 9 | 3× |
| Pola 5 hari, hari yang sama | Jam 10, 11, dan 12 | 4× |
| Istirahat atau libur, pola 6 hari | Jam 1–7 | 2× |
| Pola 6 hari | Jam 8 | 3× |
| Pola 6 hari | Jam 9, 10, dan 11 | 4× |
| Libur resmi jatuh di hari kerja terpendek, pola 6 hari | Jam 1–5 | 2× |
| Hari terpendek itu | Jam 6 | 3× |
| Hari terpendek itu | Jam 7, 8, dan 9 | 4× |

Beberapa kalkulator publik berhenti di "jam 10–11" untuk pola 5 hari dan tidak menyebut jam 12. Teks salinan pemerintah yang dibaca untuk note ini menyebut jam kedua belas. Versi aturan menyalin tabel dari PDF, lalu uji vektor di bagian 8 wajib lulus.

### 7.4 Makan lembur

Pasal 29 ayat (1) huruf c dan ayat (2): lembur 4 jam atau lebih mewajibkan makanan dan minuman paling sedikit 1.400 kkal. Tidak boleh diganti uang. Sistem hanya menandai. Tidak membuat komponen rupiah.

### 7.5 Cuti

- Cuti tahunan: sedikitnya 12 hari kerja setelah 12 bulan terus-menerus. Dasar: Pasal 79 UU 13/2003 sebagaimana diubah UU 6/2023. Sebelum genap 12 bulan, saldo tetap 0 kecuali Joe menulis kebijakan prorata. Prorata bukan hak undang-undang.
- Cuti panjang (istirahat panjang 2 bulan di tahun ke-7 dan ke-8) bukan hak otomatis lagi setelah UU 6/2023. PP 35/2021 menyerahkannya ke perjanjian, peraturan perusahaan, atau PKB untuk perusahaan tertentu. Putusan MK sempat mengubah kata "dapat" menjadi "memberikan" pada ayat perusahaan tertentu; rinciannya tetap butuh aturan perusahaan. Jangan mengode 2 bulan.
- Cuti bersama tidak mengurangi saldo tahunan kecuali aturan perusahaan berkata begitu.
- Sakit panjang: Pasal 93 punya persentase upah (empat bulan pertama penuh, lalu turun). v1 tidak memotong upah sakit otomatis. Ada peringatan "cek Pasal 93 sebelum mengurangi".
- Cuti haid, melahirkan, dan gugur ada di katalog jenis sejak hari pertama, supaya tidak perlu migrasi. Jumlah hari dan upahnya diisi dari ayat yang ditempel, bukan dari ingatan. Admin yang menyetujui.

### 7.6 Kompensasi PKWT

Pasal 15–16 PP 35/2021, diringkas dari penjelasan JDIH Kemenaker yang dikutip pers dan dari teks yang beredar. Tempel ayat penuh ke versi aturan sebelum dipakai:

- Hak muncul setelah masa kerja paling sedikit 1 bulan terus-menerus. Dibayar saat PKWT berakhir. Perpanjangan: kompensasi periode lama saat periode lama berakhir, periode baru saat periode baru berakhir.
- 12 bulan terus-menerus = 1 bulan upah.
- Selain itu, termasuk lebih dari 12 bulan = masa kerja / 12 × 1 bulan upah.
- Dasar: pokok + tunjangan tetap. Kalau struktur tidak memakai keduanya: upah tanpa tunjangan. Kalau pokok + tunjangan tidak tetap: pokok saja.
- TKA disebut dikecualikan di penjelasan sekunder. Cek Pasal 15 sebelum menyalakan pengecualian itu.
- Usaha mikro dan kecil dapat menyepakati besaran. Cek skala usaha P2P. Jangan menganggap rumus penuh wajib kalau pengecualiannya kena.

### 7.7 THR

Permenaker 6/2016:

- Wajib setelah masa kerja 1 bulan terus-menerus, untuk PKWT maupun PKWTT.
- 12 bulan atau lebih = 1 bulan upah. Di bawah itu = masa kerja / 12 × 1 bulan upah.
- Upah sebulan = upah tanpa tunjangan (clean wages), atau pokok + tunjangan tetap. Bukan UMP, kecuali UMP memang upah orang itu.
- Paling lambat 7 hari sebelum hari raya keagamaan pekerja. Bentuknya uang rupiah.
- Terlambat: denda 5% dari total THR sejak lewat batas, dan kewajiban THR tidak hilang.

### 7.8 Upah minimum

Angka yang dipakai hanya kalau orangnya bekerja di DKI Jakarta.

| | |
|---|---|
| UMP DKI 2026 | Rp5.729.876 per bulan |
| Berlaku | 1 Januari 2026 |
| UMP 2025 | Rp5.396.761 |
| Kenaikan yang diumumkan | 6,17% atau Rp333.115 |
| Acuan kebijakan | PP 49/2025 tentang Pengupahan, alfa 0,75 |
| Diumumkan | Gubernur DKI, 24 Desember 2025 (Kompas, Antara, Tirto, CNN) |

Selisih aritmetika: 5.729.876 − 5.396.761 = 333.115. Satu berita menulis 333.135; itu salah hitung, bukan angka lain. Nomor Keputusan Gubernur belum ditempel di note ini. Simpan PDF-nya di versi aturan saat Joe punya. Jangan memakai Rp5.396.761 sebagai lantai 2026. DKI pada praktiknya tidak punya UMK terpisah; tetap cek kota tempat orang bekerja. THR, insentif, dan bonus tidak dihitung untuk memenuhi upah minimum.

PP 49/2025 juga memuat struktur dan skala upah. Ambang siapa yang wajib membuatnya belum dikunci di note ini. Bukan penghalang v1. Jangan mengarang ambang "10 orang" atau angka lain.

### 7.9 BPJS

Dasar iuran bulanan pada praktiknya pokok + tunjangan tetap, yaitu upah yang dilaporkan, bukan seluruh slip. Lembur dan THR tidak otomatis masuk dasar bulan itu. Konfirmasi definisi upah di portal sebelum dikode.

Iuran peserta penerima upah, belum berubah tarifnya per sumber Oktober 2026:

| Program | Perusahaan | Karyawan | Plafon upah | Dasar |
|---|---|---|---|---|
| JHT | 3,7% | 2% | Tidak ada | PP 46/2015 |
| JP | 2% | 1% | Rp11.086.300 sejak 1 Maret 2026 (sebelumnya Rp10.547.400) | PP 45/2015 Pasal 28–29. Plafon diubah tiap Maret |
| JKK | 0,24% / 0,54% / 0,89% / 1,27% / 1,74% menurut risiko | 0 | Tidak ada | PP 44/2015, risiko diubah PP 82/2019 |
| JKM | 0,30% | 0 | Tidak ada | PP 44/2015 |
| JKP | Tidak dipotong dari karyawan | 0 | Upah max Rp5.000.000 untuk manfaat | PP 6/2025 mengubah PP 37/2021 |
| Kesehatan | 4% | 1% | Rp12.000.000 | Perpres 82/2018 diubah Perpres 59/2024 Pasal 32. Per 10 Oktober 2026 sumber berita masih memakai plafon ini |

Kelas JKK di atas adalah angka yang dipakai kalkulator dan ringkasan PP. Kelas sungguhan P2P ada di sertifikat risiko, bukan dipilih supaya iurannya kecil. Default sistem: kosong, dan payroll menolak kunci kalau kelas belum diisi.

JKP sejak PP 6/2025 (7 Februari 2025): iuran program 0,36% dari upah, terdiri dari 0,22% pemerintah pusat dan 0,14% rekomposisi dari JKK. Rekomposisi JKM 0,10% yang lama dihapus. Portal kadang menampilkan JKK 0,10%–1,60% karena 0,14 poin sudah dialihkan. **Jangan menambahkan 0,14% di atas 0,24%.** Uang perusahaan untuk potongan itu tetap sebesar tarif JKK penuh. Karyawan tidak menanggung JKK, JKM, atau JKP.

Usaha kecil tidak selalu wajib JP, usaha mikro bisa hanya JKK dan JKM (Perpres 109/2013). Cek skala sebelum JP dinyalakan untuk semua orang.

Keluarga tambahan (anak ke-4 dan seterusnya, orang tua, mertua) kesehatan 1% ditanggung peserta. Mati secara default. Nyalakan per orang.

Jatuh tempo yang umum dipakai: Kesehatan tanggal 10, Ketenagakerjaan tanggal 15 bulan berikutnya. Konfirmasi di portal, lalu simpan di kalender. v1 tidak membayar iuran. v1 menunjukkan angka dan tanggal.

### 7.10 PPh 21

Masih TER. PP 58/2023 dan PMK 168/PMK.03/2023, berlaku 1 Januari 2024, status JDIH masih berlaku. Sumber 2026 tidak menunjukkan tarif baru.

- Januari–November (atau masa selain masa terakhir): PPh = penghasilan bruto bulan itu × tarif TER.
- Masa terakhir (Desember, atau bulan keluar): PPh masa itu = PPh setahun tarif Pasal 17 − PPh yang sudah dipotong di masa sebelumnya. Hasil boleh negatif. Negatif berarti perusahaan mengembalikan kelebihan potong di slip, bukan menghilangkan barisnya.
- Bruto bulan TER memasukkan yang dibayar bulan itu: gaji, tunjangan, lembur, bonus, THR. Bulan THR memang bisa loncat ke golongan tarif yang lebih tinggi. Jangan menghitung TER hanya dari gaji pokok.
- Desember bukan "bruto Desember × TER".

Kategori, dikunci ke contoh penjelasan PP 58 yang menempatkan K/0 di kategori A, dan ke ringkasan yang konsisten dengan itu (bukan ke blog yang memindahkan K/0):

| Kategori | Status |
|---|---|
| A | TK/0, TK/1, K/0 |
| B | TK/2, TK/3, K/1, K/2 |
| C | K/3, dan status penghasilan istri digabung K/I/0 sampai K/I/3 |

Satu blog 2026 (ekoin.co) menaruh K/0 di B dan K/2 di C. Itu tidak dipakai. Mesin tidak mengetik ulang puluhan bracket dari blog. Isi lampiran PMK 168 diimpor sebagai data versi aturan. Satu sel yang boleh jadi uji, karena disebut berasal dari contoh penjelasan PP 58: K/0, bruto Rp10.000.000, masuk kategori A, tarif 2% pada golongan sampai Rp10.050.000. Cocokkan sel itu ke lampiran sebelum dipercaya.

PTKP tahunan, PMK 101/PMK.010/2016, belum tergantikan di sumber yang dibaca:

- Diri sendiri Rp54.000.000.
- Tambahan kawin Rp4.500.000.
- Tambahan tanggungan Rp4.500.000, paling banyak 3.
- Penghasilan istri digabung menambah Rp54.000.000.

Jadi TK/0 = 54jt, K/0 = 58,5jt, K/1 = 63jt, K/2 = 67,5jt, K/3 = 72jt. Status yang dipakai adalah keadaan awal tahun pajak.

Tarif Pasal 17 UU HPP 7/2021 untuk rekonsiliasi:

| PKP setahun | Tarif |
|---|---|
| sampai Rp60.000.000 | 5% |
| di atas itu sampai Rp250.000.000 | 15% |
| di atas itu sampai Rp500.000.000 | 25% |
| di atas itu sampai Rp5.000.000.000 | 30% |
| di atas Rp5.000.000.000 | 35% |

Pengurang di hitungan setahun, sebelum PTKP: biaya jabatan 5% dengan batas Rp6.000.000 setahun, iuran pensiun dan iuran JHT yang dibayar pekerja, zakat yang dibayar lewat pemberi kerja kalau ada. Daftar persisnya ditempel dari PMK 168. Iuran perusahaan bukan pengurang PKP karyawan. Premi yang dibayar perusahaan bisa menjadi penghasilan kena pajak dalam sebagian kasus; v1 tidak gross-up otomatis. Kalau slip lama P2P memakai metode gross-up, itu keputusan terbuka di bagian 11, bukan default.

e-Bupot: masa Januari–November berbentuk BPMP, Desember berbentuk BPA1, diunggah ke Coretax (`coretaxdjp.pajak.go.id`). v1 tidak membuat XML dan tidak mengunggah.

Identitas: sejak 1 Juli 2024 dan Coretax 1 Januari 2025, identitas pajak orang pribadi penduduk yang sudah diaktivasi adalah NIK 16 digit (PMK 136/2023). Badan memakai NPWP 16 digit. NITKU 22 digit identitas cabang, bukan NPWP.

### 7.11 Undang-undang baru, jangan dijadikan rumus

DPR menyetujui RUU Pelindungan Ketenagakerjaan menjadi undang-undang pada 6 Oktober 2026, 23 bab, 313 pasal, menindaklanjuti putusan MK 168/PUU-XXI/2023. Dirjen PHI dan Jamsos, Indah Anggoro Putri, mengatakan masa transisi satu tahun sejak ditetapkan dan diundangkan, dan aturan pengupahan baru diperkirakan baru dipakai untuk UMP 2028 (CNBC Indonesia, 6 Oktober 2026).

Sampai teks di Lembaran Negara dipakai dan tanggal berlaku-nya lewat, mesin tetap pada PP 35/2021, Permenaker 6/2016, dan PP 49/2025. Jangan mengisi tabel pesangon, lembur, atau PKWT dari draf RUU atau dari ringkasan media.

Pesangon, uang penghargaan masa kerja, dan uang penggantian hak tidak dihitung otomatis di v1. Alasan berakhirnya hubungan kerja disimpan. Modul nanti memuat tabel PP 35 sebagai versi aturan, tetap dengan kunci manusia, karena UU baru ini tepat mengenai tabel itu.

## 8. Vektor uji

Semua vektor ini hipotetis. Lulus di unit test sebelum ada data orang sungguhan. Pembulatan default: rupiah bulat, 0,5 ke atas, dan cara itu tertulis di slip. Kalau portal BPJS membulatkan lain, versi aturan yang diganti, bukan tes yang diam-diam diubah.

**Lembur hari kerja.** Dasar sebulan Rp8.650.000. Upah sejam = 8.650.000 / 173 = Rp50.000. Dua jam di hari biasa = 1,5 × 50.000 + 2 × 50.000 = Rp175.000.

**Dasar 75%.** Pokok 2.800.000, tunjangan tetap 400.000, tunjangan tidak tetap 3.720.000, total 6.920.000. Pokok + tetap = 3.200.000 = 46,2% dari total, di bawah 75%. Dasar = 0,75 × 6.920.000 = 5.190.000. Upah sejam = 5.190.000 / 173 = Rp30.000. Memakai 3.200.000 adalah salah.

**Hari libur, pola 5 hari, 12 jam.** Upah sejam Rp50.000. Jam 1–8 = 8 × 2 × 50.000 = 800.000. Jam 9 = 3 × 50.000 = 150.000. Jam 10–12 = 3 × 4 × 50.000 = 600.000. Jumlah = Rp1.550.000. Tes ini gagal kalau kode berhenti di jam 11.

**THR 8 bulan.** Dasar Rp8.000.000. 8/12 × 8.000.000 = Rp5.333.333,33 → Rp5.333.333 dengan pembulatan default, selama versi aturan tidak memilih cara lain. Masa kerja 20 hari = 0.

**Kompensasi PKWT 12 bulan.** Dasar pokok + tetap Rp8.000.000. Kompensasi = Rp8.000.000. Masa 7 bulan = 7/12 × 8.000.000.

**PPh, contoh penjelasan.** K/0, bruto Rp10.000.000 tiap bulan, iuran pensiun karyawan Rp100.000 per bulan. Kategori A. Kalau sel lampiran memang 2%: potongan Jan–Nov Rp200.000 per bulan. Bruto setahun 120.000.000. Biaya jabatan 6.000.000. Iuran pensiun 1.200.000. Neto 112.800.000. PTKP 58.500.000. PKP 54.300.000. Pajak setahun 5% = 2.715.000. Desember = 2.715.000 − 2.200.000 = Rp515.000. Kalau sel 2% tidak ada di lampiran, vektor ini diganti, kategorinya tidak.

**BPJS pada upah Rp8.000.000, JKK risiko sangat rendah 0,24%, JP di bawah plafon, kesehatan di bawah plafon.** Karyawan: JHT 160.000 + JP 80.000 + kesehatan 80.000 = 320.000. Perusahaan: JHT 296.000 + JP 160.000 + JKK 19.200 + JKM 24.000 + kesehatan 320.000 = 819.200. JKP tidak menambah potongan karyawan dan tidak ditambahkan lagi di atas JKK.

**JP di atas plafon.** Upah Rp20.000.000 pada Maret 2026 atau sesudahnya: dasar JP = 11.086.300, bukan 20.000.000. JHT tetap dari 20.000.000. Kesehatan dari 12.000.000.

## 9. Data pribadi dan arsip

NIK, rekening, kesehatan, dan slip adalah data pribadi spesifik (UU 27/2022 PDP; masa transisi undang-undang itu sudah lewat 17 Oktober 2024).

Buku, catatan, dan dokumen perpajakan disimpan 10 tahun di Indonesia (UU KUP Pasal 28). Dua kewajiban itu tidak saling menghapus.

- Permintaan hapus akun tidak menghapus slip, bukti potong, atau jurnal yang menjadi dokumen pajak.
- Yang boleh disembunyikan dari layar sehari-hari: NIK utuh, nomor rekening, lampiran kesehatan. Admin membukanya dengan tindakan yang tercatat.
- Akses "siapa membuka slip siapa, kapan" tersimpan.
- Cadangan ikut terenkripsi dan ikut aturan 10 tahun untuk dokumen payroll.
- Tidak ada NIK di newsroom, di chat bot, di analitik, atau di nama file.

## 10. Kotak dan batasnya

Joe yang memilih mesin. PRD hanya memasang lantai supaya pilihannya tidak jatuh lagi ke kotak 1 GB.

| | Newsroom, jangan dipakai | ERP |
|---|---|---|
| Peran | Situs statis `p2plabs.asia` | Aplikasi + Postgres |
| Ukuran yang sudah ada | 1 vCPU, 1 GB | Paling kecil yang masuk akal untuk di bawah 50 orang: 2 vCPU, 4 GB RAM. 8 GB lebih longgar |
| Disk | — | 40 GB atau lebih, untuk PDF slip dan ruang cadangan |
| Zona waktu | — | Asia/Jakarta |
| DNS | A `@` tetap ke newsroom | A `erp` hanya ke mesin baru |
| Deploy | rsync newsroom | Tidak ikut skrip rsync situs |
| Rahasia | — | Tidak masuk repo situs, tidak masuk note ini |

### Kandidat mesin: PC rumah + IP statis

Joe menyebut IP statis rumah `103.145.240.52` pada 22 Oktober 2026. Whois blok `103.145.240.0/24`: CV Candra Putra Mada (Mada Hoster), status assigned portable, diumumkan lewat AS132641 (PT Netciti Persada). Ini bukan `116.206.196.6` dan bukan `76.13.198.28`.

Kalau PC-nya jadi mesin ERP:

- DNS yang berubah hanya A `erp` → `103.145.240.52`. A `@` untuk `p2plabs.asia` tetap ke newsroom.
- Router rumah meneruskan port 443 ke PC itu. Port lain, termasuk 5432 dan SSH publik, tidak diteruskan.
- Alamat WAN di modem harus benar-benar `103.145.240.52`. Kalau yang tampil `192.168…` atau `100.64…`, IP publiknya masih di radio ISP dan port-forward di router rumah tidak sampai.
- PC ini mesin terpisah, nyala terus, RAM 16 GB, SSD, LAN kabel, UPS, disk terenkripsi. Bukan laptop kerja harian.
- Jaringan keluarga tidak boleh mencapai Postgres. Aplikasi hanya lewat nginx di PC itu.
- IP ini tercatat di note karena Joe yang memberinya. Jangan ditulis di situs, di repo newsroom, atau di nama file publik.

Login wajib. `noindex`. Tidak ada halaman publik. Cadangan harian terenkripsi ke mesin atau object storage **lain**, dan satu kali pulihkan dicoba sebelum slip pertama. Postgres dan aplikasi boleh satu mesin di v1. Tidak wajib Docker.

Sertifikat HTTPS untuk `erp.p2plabs.asia` terpisah dari sertifikat apex. Jangan menumpang berkas nginx situs berita.

## 11. Yang masih harus Joe isi

Tanpa ini, bangun aplikasi hanya menghasilkan form kosong.

- [ ] Jumlah orang yang masuk v1, termasuk founder yang digaji atau tidak.
- [ ] Kota tempat mereka bekerja. UMP Jakarta di note ini salah dipakai kalau kantornya bukan Jakarta.
- [ ] Pola waktu: 5 hari × 8 jam, atau 6 hari × 7 jam, plus jam masuk dan pulang.
- [ ] Siapa admin HR. Perlu peninjau kedua atau belum.
- [ ] Ada PKWT atau semuanya PKWTT. Skala usaha untuk pengecualian kompensasi dan untuk wajib-tidaknya JP.
- [ ] Kelas risiko JKK di sertifikat BPJS.
- [ ] Komponen slip yang dipakai sekarang: pokok, tunjangan tetap mana, tunjangan tidak tetap mana, gross atau nett, gross-up atau tidak.
- [ ] Jenis cuti di luar cuti tahunan yang sudah dijanjikan ke orang.
- [ ] Cuti bersama memotong saldo atau tidak.
- [ ] Aturan kerja dari rumah: bebas, atau hanya hari tertentu.
- [ ] Hari raya masing-masing orang untuk THR.
- [ ] Siapa yang mentransfer bank setelah CSV terunduh.
- [ ] PDF Keputusan Gubernur UMP 2026, lampiran PMK 168, dan sertifikat risiko, untuk ditempel sebagai versi aturan.
- [ ] Teks Lembaran Negara UU Pelindungan Ketenagakerjaan, saat terbit, sebelum ada perubahan rumus.

## 12. Selesai artinya

- [ ] Sepuluh vektor di bagian 8 lulus, termasuk jam ke-12 hari libur pola 5 hari dan plafon JP/kesehatan.
- [ ] Tidak ada jalur yang mengubah slip terkunci.
- [ ] CSV transfer tidak berisi NIK.
- [ ] Karyawan A tidak bisa membuka slip karyawan B (uji dengan dua akun).
- [ ] Clock di luar radius tetap tersimpan dan bertanda, tidak ditolak.
- [ ] Cuti bersama tidak mengurangi saldo sampai aturan perusahaan diset.
- [ ] Lembur 4 jam memunculkan tanda 1.400 kkal dan tidak memunculkan rupiah.
- [ ] Plafon 4 jam / 18 jam tidak memakan jam hari libur.
- [ ] Golongan tanpa lembur tidak aktif kalau klausulnya kosong.
- [ ] THR memakai hari raya orang itu, bukan satu tanggal perusahaan.
- [ ] Kompensasi PKWT tidak tercampur ke gaji bulan tanpa tindakan admin.
- [ ] Cadangan terpulihkan ke mesin kosong, dicoba, dicatat tanggalnya.
- [ ] `erp.p2plabs.asia` tidak mengarah ke `116.206.196.6`.
- [ ] Situs `p2plabs.asia` tidak mendapat tautan, env, atau tabel milik ERP.

## 13. Sumber yang dibaca untuk versi 0.9

Dibaca 22 Oktober 2026. Kutipan ayat yang dipakai di mesin harus dari PDF-nya, bukan dari baris ini.

- PP 35/2021. JDIH BPK: https://peraturan.bpk.go.id/Details/161904/pp-no-35-tahun-2021. Pasal 15–16 kompensasi, Pasal 26 plafon, Pasal 27 jabatan tanpa lembur, Pasal 28 perintah dan persetujuan, Pasal 29 makan 1.400 kkal, Pasal 31 pengali, Pasal 32 dasar 1/173 dan 75%, Pasal 33 lantai upah minimum untuk upah harian. Salinan PDF BPK dibuka untuk Pasal 26, 31, dan 32.
- PP 49/2025 tentang Pengupahan, sebagai kebijakan upah yang dirujuk pengumuman UMP.
- Permenaker 6/2016 tentang THR Keagamaan. Pasal 2, 3, 5 ayat (4), 6, dan 10.
- UU 13/2003 Pasal 79 sebagaimana diubah UU 6/2023, untuk cuti tahunan 12 hari kerja dan hilangnya cuti panjang sebagai hak otomatis. PP 35 untuk istirahat panjang perusahaan tertentu.
- UMP DKI 2026 Rp5.729.876. Liputan 24 Desember 2025: Kompas, Antara, Tirto, CNN Indonesia, Bisnis. Selisih yang benar terhadap UMP 2025 adalah Rp333.115.
- PMK 168/PMK.03/2023, JDIH status berlaku, dan PP 58/2023 untuk TER. PTKP: PMK 101/PMK.010/2016. Tarif Pasal 17: UU 7/2021 (HPP).
- Identitas pajak: PMK 136/2023, NIK 16 digit, Coretax sejak 1 Januari 2025.
- BPJS Kesehatan plafon Rp12.000.000: Perpres 59/2024 mengubah Perpres 82/2018 Pasal 32. Berita 10 Oktober 2026 menyatakan iuran PPU belum berubah.
- JP plafon Rp11.086.300 sejak 1 Maret 2026, dari Rp10.547.400. JHT 3,7% + 2%, JKM 0,30%, JKK lima kelas 0,24–1,74.
- JKP: PP 6/2025 (7 Februari 2025) mengubah PP 37/2021. Iuran 0,36% = 0,22% pemerintah + 0,14% dari JKK. Plafon manfaat Rp5.000.000. Manfaat uang 60% hingga 6 bulan tidak dihitung di payroll.
- Retensi pajak 10 tahun: UU KUP Pasal 28. PDP: UU 27/2022.
- UU Pelindungan Ketenagakerjaan: persetujuan paripurna DPR 6 Oktober 2026. Masa transisi disebut satu tahun setelah diundangkan (CNBC Indonesia, keterangan Dirjen Indah Anggoro Putri). Bukan dasar hitung versi ini.
- Kepmenakertrans 102/MEN/VI/2004 tidak dipakai. Jangan menghidupkan kembali plafon 3 jam / 14 jam dari blog.

## 14. Log

### 2026-10-22

- Joe minta PRD matang di Obsidian sebelum membeli VPS besar atau memakai server sendiri. Menu yang difoto adalah peta Talenta, bukan daftar fitur yang disalin.
- Diputuskan: modul HR internal di `erp.p2plabs.asia`, di luar kotak 1 GB, v1 orang–kontrak–absen–cuti–lembur–slip terkunci, transfer manual.
- IP statis rumah yang disebut Joe: `103.145.240.52` (blok Mada Hoster / CV Candra Putra Mada). Kandidat A record `erp`. Belum diarahkan. Newsroom tidak pindah ke sana.
- Riset aturan di bagian 13. Selisih sumber yang disengaja dibiarkan tertulis: kategori TER K/0, tampilan portal JKK 0,10–1,60 versus tarif 0,24–1,74, jam lembur ke-12, nomor Kepgub UMP yang belum ditempel, dan UU ketenagakerjaan baru yang belum jadi dasar hitung.
- Kode lokal jalan di folder saudara situs, `erp-p2p-labs`, login `http://127.0.0.1:8766/masuk/`. Belum ada repo GitHub. Belum di-deploy. Bukan di kotak newsroom.

## Tautan

- [[02 Projects/P2P Labs|P2P Labs]]
- [[p2plabs/P2P-Labs-Brand]]
- [[02 Projects/Projects MOC|Projects MOC]]
- [[Home]]
