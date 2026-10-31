# Product Requirement Document (PRD)
## Website Portofolio Profesional dengan CMS Internal

| Atribut | Keterangan |
|---|---|
| Nama Produk | Website Portofolio Profesional + Dashboard Admin (CMS) |
| Pemilik Produk | Livia |
| Versi Dokumen | 1.0 (Draft untuk Pengembangan) |
| Status | Siap Dikembangkan |
| Tech Stack | Next.js (App Router), Node.js, TypeScript, Tailwind CSS, Supabase (PostgreSQL, Auth, Storage), Vercel |
| Bahasa Antarmuka | Bahasa Indonesia (ID) dan Bahasa Inggris (EN) |

---

## Daftar Isi

1. Latar Belakang
2. Tujuan Produk
3. Pengguna dan Peran / Hak Akses
4. Aturan Bisnis / Logika Sistem
5. User Story
6. Alur Status dan Interaksi
7. Spesifikasi Halaman / Menu
8. Data Utama
9. Fitur Nilai Tambah / Lanjutan
10. Kebutuhan Non-Fungsional
11. Kriteria Selesai (Definition of Done)
12. Di Luar Lingkup

---

## 1. Latar Belakang

### 1.1 Gambaran Umum
Portofolio digital adalah representasi profesional utama bagi mahasiswa dan fresh graduate di bidang teknologi. Recruiter, dosen, dan calon kolaborator umumnya hanya meluangkan waktu singkat untuk menilai seseorang, sehingga informasi pendidikan, pengalaman organisasi, kepanitiaan, proyek, sertifikasi, dan dokumentasi kegiatan harus mudah ditemukan, mutakhir, dan meyakinkan.

### 1.2 Masalah pada Portofolio Statis
Portofolio statis (halaman HTML tetap, PDF, atau template tanpa backend) memiliki keterbatasan berikut:

| No | Masalah | Dampak |
|---|---|---|
| 1 | Konten tertanam di kode (hardcoded) | Setiap pembaruan proyek atau sertifikat memerlukan edit kode dan deploy ulang |
| 2 | Tidak ada pencarian dan filter | Recruiter sulit menemukan proyek atau sertifikat yang relevan |
| 3 | Tidak ada jalur kontak terstruktur | Pesan masuk lewat kanal tidak terpusat dan mudah terlewat |
| 4 | Tidak mendukung dua bahasa | Jangkauan ke recruiter internasional terbatas |
| 5 | Tidak ada manajemen draf | Konten setengah jadi tidak bisa disiapkan tanpa tampil ke publik |
| 6 | Tidak ada data kunjungan | Pemilik tidak tahu seberapa efektif portofolionya |
| 7 | SEO dan pratinjau tautan (Open Graph) minim | Tautan tampil kurang menarik saat dibagikan di LinkedIn, WhatsApp, dan lainnya |

### 1.3 Solusi yang Ditawarkan
Website portofolio dinamis berbasis Next.js dan Supabase dengan **CMS internal** (Dashboard Admin) sehingga pemilik dapat mengelola seluruh konten (Full CRUD), mengatur status publikasi (draf/tayang), menyorot proyek unggulan, dan membaca pesan masuk tanpa menyentuh kode. Sisi publik menampilkan konten secara cepat, responsif, ramah SEO, serta mendukung multi-bahasa dan mode gelap/terang.

---

## 2. Tujuan Produk

### 2.1 Tujuan Fungsional
- F-01: Menyajikan seluruh portofolio (Home, Pendidikan, Organisasi, Kepanitiaan, Project, Sertifikasi & Penghargaan, Galeri, Kontak) dalam satu website terpadu.
- F-02: Menyediakan pencarian dan filter pada modul Project dan Sertifikasi & Penghargaan.
- F-03: Menyediakan CMS dengan Full CRUD untuk semua modul data oleh Super Admin.
- F-04: Menyediakan formulir kontak yang tersimpan di database dan memicu notifikasi email.
- F-05: Menyediakan pengaturan status publikasi (draf/tayang) pada konten.
- F-06: Menyediakan pengunduhan CV dalam format PDF.

### 2.2 Tujuan Teknis
- T-01: Arsitektur Next.js App Router dengan TypeScript ketat (`strict: true`).
- T-02: Keamanan data di level database melalui Supabase Auth dan Row Level Security (RLS).
- T-03: Rendering optimal (Server Components, ISR/revalidasi) untuk performa dan SEO.
- T-04: Deployment otomatis di Vercel (CI/CD dari repositori Git) dengan environment variable terpisah untuk development dan production.
- T-05: Skema database ternormalisasi dengan migrasi yang terdokumentasi.

### 2.3 Tujuan Pengalaman Pengguna
- U-01: Pengunjung memahami profil pemilik dalam kurang dari 30 detik dari halaman Home.
- U-02: Navigasi konsisten dan nyaman di perangkat mobile maupun desktop.
- U-03: Pergantian bahasa dan tema berlangsung instan dan preferensi diingat.
- U-04: Admin dapat menambah atau mengubah konten dalam beberapa klik dengan formulir yang jelas dan umpan balik validasi yang informatif.

### 2.4 Indikator Keberhasilan (KPI)

| KPI | Target |
|---|---|
| Skor Lighthouse (Performance, Accessibility, Best Practices, SEO) | ≥ 90 pada halaman publik utama |
| Largest Contentful Paint (LCP) | ≤ 2,5 detik pada koneksi 4G |
| Waktu penambahan satu proyek baru oleh admin | ≤ 3 menit |
| Pesan kontak yang tersimpan dan terkirim notifikasi | 100% (tanpa kehilangan pesan) |
| Konten draf yang bocor ke publik | 0 kasus |

---

## 3. Pengguna dan Peran / Hak Akses

### 3.1 Daftar Peran

| Peran | Deskripsi | Autentikasi |
|---|---|---|
| **Public Visitor (Guest)** | Pengunjung umum, recruiter, dosen, atau kolaborator yang mengakses website tanpa login | Tidak diperlukan |
| **Super Admin** | Pemilik portofolio dengan hak penuh atas seluruh data melalui panel admin terlindungi | Supabase Auth (email + password) |

### 3.2 Matriks Hak Akses

| Fitur / Modul | Public Visitor | Super Admin |
|---|:---:|:---:|
| Melihat Home, Pendidikan, Organisasi, Kepanitiaan (status tayang) | ✅ | ✅ |
| Melihat Project, Sertifikasi & Penghargaan, Galeri (status tayang) | ✅ | ✅ |
| Melihat konten berstatus draf | ❌ | ✅ |
| Mencari dan memfilter Project / Sertifikasi | ✅ | ✅ |
| Mengganti bahasa (ID/EN) dan tema (Dark/Light) | ✅ | ✅ |
| Mengunduh CV PDF | ✅ | ✅ |
| Membuka lightbox galeri | ✅ | ✅ |
| Mengirim pesan kontak | ✅ (Create saja) | ✅ |
| Membaca, menandai, dan menghapus pesan masuk | ❌ | ✅ |
| Login ke Dashboard Admin | ❌ | ✅ |
| Create, Read, Update, Delete seluruh modul data | ❌ | ✅ |
| Mengunggah file ke Supabase Storage | ❌ | ✅ |
| Mengatur status publikasi dan `is_featured` | ❌ | ✅ |
| Mengubah profil dan mengganti CV | ❌ | ✅ |
| Melihat statistik kunjungan | Terbatas (angka counter publik) | ✅ (detail) |

### 3.3 Penjelasan Peran

**Public Visitor** hanya dapat membaca data yang berstatus **tayang** dan mengirim pesan kontak. Visitor tidak pernah memiliki akses tulis ke tabel mana pun selain `messages` (insert), dan akses ini dibatasi oleh kebijakan RLS serta validasi server.

**Super Admin** adalah satu-satunya akun yang berwenang. Identitas admin ditentukan di level database (bukan hanya di antarmuka) sehingga pemanggilan API langsung tanpa sesi admin yang sah akan ditolak oleh RLS.

---

## 4. Aturan Bisnis / Logika Sistem

### 4.1 Autentikasi dan Keamanan

| Kode | Aturan |
|---|---|
| BR-01 | Seluruh rute `/admin/*` adalah **Protected Route**. Pengguna tanpa sesi Supabase Auth yang valid dialihkan ke `/admin/login`. Pengecekan dilakukan di `middleware.ts` (sisi server), bukan hanya di sisi klien. |
| BR-02 | Hanya satu akun Super Admin yang diizinkan. Registrasi publik dinonaktifkan di Supabase Auth (*disable signups*); akun dibuat manual melalui dashboard Supabase. |
| BR-03 | Semua tabel mengaktifkan **Row Level Security (RLS)**. Tidak ada tabel yang dibiarkan tanpa kebijakan. |
| BR-04 | Kebijakan RLS baca publik (`SELECT` untuk anon) hanya berlaku pada baris dengan `status = 'published'`. Baris `draft` hanya dapat dibaca oleh Super Admin. |
| BR-05 | Operasi `INSERT`, `UPDATE`, `DELETE` pada semua tabel konten hanya diizinkan untuk Super Admin (dicek berdasarkan `auth.uid()` yang terdaftar pada tabel `profiles` dengan `role = 'super_admin'`). |
| BR-06 | Tabel `messages` mengizinkan `INSERT` oleh anon, tetapi `SELECT`, `UPDATE`, `DELETE` hanya oleh Super Admin. |
| BR-07 | `SUPABASE_SERVICE_ROLE_KEY` hanya digunakan di server (Route Handler / Server Action) dan tidak boleh diekspos ke klien atau diawali `NEXT_PUBLIC_`. |
| BR-08 | Sesi admin kedaluwarsa otomatis setelah periode tidak aktif (default 7 hari, dapat dikonfigurasi) dan tombol Logout menghapus sesi sepenuhnya. |
| BR-09 | Percobaan login gagal berulang dibatasi (rate limit) untuk mencegah brute force. |

### 4.2 Validasi Formulir

| Kode | Aturan |
|---|---|
| BR-10 | Validasi dilakukan di dua lapis: klien (umpan balik cepat) dan server (otoritatif), menggunakan skema yang sama (mis. Zod). |
| BR-11 | Formulir kontak: Nama (2–100 karakter), Email (format valid, maks. 254 karakter), Subjek (3–150 karakter), Pesan (10–2000 karakter). Semua wajib diisi. |
| BR-12 | Formulir kontak dilindungi anti-spam: *honeypot field* tersembunyi dan pembatasan laju (maks. 3 pesan per alamat IP per jam). Pengiriman yang terdeteksi bot ditolak secara senyap. |
| BR-13 | Semua input teks disanitasi untuk mencegah XSS. Konten Rich Text disanitasi (allowlist tag HTML) sebelum disimpan dan sebelum dirender. |
| BR-14 | Field tanggal: `end_date` tidak boleh lebih awal dari `start_date`. Jika `is_current = true`, `end_date` dikosongkan dan ditampilkan sebagai "Sekarang / Present". |
| BR-15 | URL (live demo, repositori, kredensial, sosial media) harus berformat `https://` yang valid. |
| BR-16 | `slug` unik per tabel yang memilikinya (projects), dibuat otomatis dari judul dan dapat disunting; duplikat ditolak dengan pesan jelas. |
| BR-17 | Setiap entri konten wajib memiliki judul/nama dalam minimal satu bahasa; versi bahasa lain bersifat opsional dengan *fallback* ke bahasa utama (lihat BR-40). |

### 4.3 Upload File dan Storage

| Kode | Aturan |
|---|---|
| BR-18 | Hanya Super Admin yang dapat mengunggah file. Kebijakan Storage mengunci operasi tulis hanya untuk admin; baca publik hanya pada bucket publik yang ditentukan. |
| BR-19 | Bucket yang digunakan: `avatars`, `project-images`, `certificates`, `gallery`, `documents` (CV PDF). |
| BR-20 | Tipe gambar yang diizinkan: JPG, PNG, WebP (maks. **2 MB** per file untuk gambar umum, maks. **5 MB** untuk galeri). Tipe lain ditolak berdasarkan MIME type dan ekstensi. |
| BR-21 | Dokumen CV hanya PDF dengan ukuran maks. **5 MB**. |
| BR-22 | Nama file dinormalisasi (huruf kecil, tanpa spasi, diberi awalan UUID/timestamp) untuk mencegah tabrakan dan path traversal. |
| BR-23 | Saat sebuah entri dihapus atau gambarnya diganti, file lama di Storage ikut dihapus agar tidak ada file yatim (*orphan files*). |
| BR-24 | Gambar dioptimalkan melalui `next/image` (format modern, ukuran responsif, *lazy loading*), dan setiap gambar wajib memiliki `alt text`. |

### 4.4 Project, Featured, dan Filter

| Kode | Aturan |
|---|---|
| BR-25 | Kolom `is_featured` (boolean) menentukan apakah proyek muncul pada bagian "Featured Projects" di Home. |
| BR-26 | Jumlah maksimum proyek featured adalah **6**. Jika admin mencoba menandai proyek ketujuh, sistem menolak dan menampilkan daftar proyek featured saat ini untuk dilepas. |
| BR-27 | Hanya proyek berstatus `published` yang dapat tampil di Featured. Jika proyek featured diubah ke `draft`, ia otomatis hilang dari Home namun flag `is_featured` tetap tersimpan. |
| BR-28 | Urutan Featured mengikuti kolom `sort_order` (ascending), lalu `created_at` (descending) sebagai pembeda. |
| BR-29 | Kategori Project berasal dari daftar terkontrol: Web App, Mobile, AI/CV, UI/UX, Data, Lainnya. Satu proyek memiliki tepat satu kategori utama dan boleh memiliki banyak tag tech stack. |
| BR-30 | Filter dan pencarian bersifat gabungan (AND): kata kunci (judul, deskripsi, tech stack) + kategori + tech stack. Hasil kosong menampilkan *empty state* dengan tombol "Reset Filter". |
| BR-31 | Pencarian tidak sensitif huruf besar-kecil dan berjalan dengan *debounce* 300 ms. State filter disimpan di URL (query string) agar dapat dibagikan dan bertahan saat refresh. |
| BR-32 | Sertifikasi & Penghargaan memiliki `type` (`certificate` / `award`) dan `issuer`. Filter tersedia berdasarkan penerbit (issuer) dan jenis. Daftar issuer di filter dihasilkan dinamis dari data tayang. |
| BR-33 | Urutan default Sertifikasi, Pendidikan, Organisasi, dan Kepanitiaan: periode terbaru lebih dulu. |

### 4.5 Pesan Kontak

| Kode | Aturan |
|---|---|
| BR-34 | Pesan yang berhasil divalidasi disimpan ke tabel `messages` dengan status awal `unread`. |
| BR-35 | Setelah penyimpanan, sistem memicu notifikasi email ke pemilik. Kegagalan email **tidak** membatalkan penyimpanan pesan; kegagalan dicatat dan pesan tetap tersedia di inbox admin. |
| BR-36 | Visitor menerima konfirmasi tampilan ("Pesan terkirim") tanpa mengetahui detail internal. Formulir dikosongkan setelah sukses dan tombol kirim dinonaktifkan selama proses (mencegah *double submit*). |
| BR-37 | Pesan tidak dapat diubah isinya oleh siapa pun; admin hanya dapat mengubah status (`unread`, `read`, `archived`) atau menghapus. |

### 4.6 Konten Publik, Bahasa, dan SEO

| Kode | Aturan |
|---|---|
| BR-38 | Halaman publik tidak pernah menampilkan data draf, baik melalui UI, API, maupun cache. |
| BR-39 | Perubahan konten oleh admin memicu revalidasi (on-demand ISR) pada halaman terkait agar pembaruan tampil tanpa deploy ulang. |
| BR-40 | Konten dwibahasa disimpan pada kolom berpasangan (`*_id`, `*_en`). Jika versi EN kosong, sistem menampilkan versi ID sebagai *fallback*, dan sebaliknya. |
| BR-41 | Bahasa ditentukan oleh segmen rute (`/id`, `/en`); bahasa default mengikuti preferensi browser pada kunjungan pertama, lalu diingat melalui cookie. |
| BR-42 | Semua halaman admin mengirim `noindex, nofollow` (meta robots dan header `X-Robots-Tag`) dan dikecualikan di `robots.txt`. |
| BR-43 | Setiap halaman publik memiliki `title`, `description`, `canonical`, dan tag Open Graph/Twitter yang dihasilkan dinamis dari data. |

### 4.7 Visitor Counter

| Kode | Aturan |
|---|---|
| BR-44 | Satu kunjungan unik dihitung per sesi browser (cookie/localStorage) per 24 jam; refresh tidak menambah hitungan. |
| BR-45 | Kunjungan dari akun admin yang sedang login dan dari bot yang dikenali tidak dihitung. |
| BR-46 | Tidak menyimpan data pribadi (IP mentah). Jika diperlukan deduplikasi, gunakan hash dengan *salt* harian. |

---

## 5. User Story

### 5.1 Sudut Pandang Public Visitor

| Kode | Sebagai | Saya ingin | Agar | Aturan Terkait |
|---|---|---|---|---|
| US-01 | Visitor | Melihat Home dengan hero, ringkasan tech stack, statistik, dan Featured Projects | Memahami profil pemilik dengan cepat | BR-25 s.d. BR-28, BR-38 |
| US-02 | Visitor | Melihat linimasa pendidikan formal dan informal | Mengetahui latar belakang akademik | BR-14, BR-33, BR-38 |
| US-03 | Visitor | Melihat pengalaman organisasi (nama, jabatan, periode, kontribusi) | Menilai kepemimpinan dan kerja tim | BR-14, BR-33 |
| US-04 | Visitor | Melihat pengalaman kepanitiaan (peran/divisi, periode, tanggung jawab) | Menilai pengalaman penyelenggaraan acara | BR-14, BR-33 |
| US-05 | Visitor | Menelusuri daftar proyek dan membuka detailnya | Menilai kualitas karya | BR-29 |
| US-06 | Visitor | Mencari dan memfilter proyek berdasarkan kategori dan tech stack | Menemukan proyek yang relevan | BR-30, BR-31 |
| US-07 | Visitor | Membuka link live demo dan repositori GitHub proyek | Memverifikasi karya secara langsung | BR-15 |
| US-08 | Visitor | Melihat sertifikasi dan penghargaan dengan filter issuer dan jenis | Memverifikasi kompetensi dan prestasi | BR-32 |
| US-09 | Visitor | Membuka link kredensial sertifikat | Memvalidasi keaslian sertifikat | BR-15 |
| US-10 | Visitor | Melihat galeri grid dan memperbesar foto lewat lightbox dengan keterangan | Melihat dokumentasi kegiatan | BR-24 |
| US-11 | Visitor | Mengirim pesan lewat formulir kontak | Menghubungi pemilik | BR-11, BR-12, BR-34 s.d. BR-36 |
| US-12 | Visitor | Membuka tautan sosial media dan GitHub | Menjangkau pemilik di kanal lain | BR-15 |
| US-13 | Visitor | Mengunduh CV dalam format PDF | Menyimpan profil untuk keperluan rekrutmen | BR-21 |
| US-14 | Visitor | Mengganti bahasa ID/EN | Membaca dalam bahasa yang saya pahami | BR-40, BR-41 |
| US-15 | Visitor | Mengganti tema Dark/Light | Menyesuaikan kenyamanan visual | NFR-12 |
| US-16 | Visitor | Melihat visitor counter | Mengetahui popularitas website | BR-44 s.d. BR-46 |
| US-17 | Visitor | Membagikan tautan halaman dengan pratinjau yang menarik | Tampil profesional di media sosial | BR-43 |

### 5.2 Sudut Pandang Super Admin

| Kode | Sebagai | Saya ingin | Agar | Aturan Terkait |
|---|---|---|---|---|
| US-18 | Admin | Login aman ke dashboard | Hanya saya yang dapat mengelola konten | BR-01, BR-02, BR-08, BR-09 |
| US-19 | Admin | Logout dan sesi dihentikan | Akun aman di perangkat bersama | BR-08 |
| US-20 | Admin | Melihat ringkasan dashboard (jumlah konten, pesan belum dibaca, kunjungan) | Memantau kondisi portofolio | BR-44 |
| US-21 | Admin | Mengelola profil (nama, headline, bio, foto, sosial media, CV) | Informasi pribadi selalu mutakhir | BR-19 s.d. BR-23 |
| US-22 | Admin | Full CRUD Pendidikan | Memelihara riwayat pendidikan | BR-10, BR-14, BR-17 |
| US-23 | Admin | Full CRUD Organisasi | Memelihara pengalaman organisasi | BR-10, BR-14 |
| US-24 | Admin | Full CRUD Kepanitiaan | Memelihara pengalaman kepanitiaan | BR-10, BR-14 |
| US-25 | Admin | Full CRUD Project termasuk kategori, tech stack, link, dan gambar | Memamerkan karya terbaru | BR-15, BR-16, BR-20, BR-29 |
| US-26 | Admin | Menandai proyek sebagai Featured dan mengatur urutannya | Menyorot karya terbaik di Home | BR-25 s.d. BR-28 |
| US-27 | Admin | Full CRUD Sertifikasi & Penghargaan dengan upload gambar | Memelihara bukti kompetensi | BR-15, BR-20, BR-32 |
| US-28 | Admin | Full CRUD Galeri (unggah, keterangan, hapus) | Memelihara dokumentasi kegiatan | BR-20, BR-23 |
| US-29 | Admin | Mengubah status konten antara draf dan tayang | Menyiapkan konten tanpa tampil ke publik | BR-04, BR-38, BR-39 |
| US-30 | Admin | Menulis deskripsi dengan Rich Text Editor | Memformat konten tanpa menulis HTML | BR-13 |
| US-31 | Admin | Mengisi konten dalam versi ID dan EN | Menjangkau pengunjung dua bahasa | BR-17, BR-40 |
| US-32 | Admin | Membaca, memfilter, menandai dibaca/arsip, dan menghapus pesan masuk | Mengelola komunikasi dengan efisien | BR-06, BR-37 |
| US-33 | Admin | Menerima notifikasi email saat ada pesan baru | Tidak melewatkan peluang | BR-35 |
| US-34 | Admin | Pratinjau konten draf sebelum ditayangkan | Memastikan tampilan benar | BR-04 |
| US-35 | Admin | Konfirmasi sebelum menghapus data | Mencegah penghapusan tidak sengaja | BR-23 |

---

## 6. Alur Status dan Interaksi

### 6.1 Alur Status Publikasi Konten (Admin)

Berlaku untuk: Education, Organization, Committee, Project, Certificate/Award, Gallery.

```
[Buat Baru] ──► DRAFT ──(Publikasikan)──► PUBLISHED
                  ▲                          │
                  └────(Tarik ke Draf)───────┘
                  │                          │
               (Hapus)                    (Hapus)
                  ▼                          ▼
              [DIHAPUS]                  [DIHAPUS]
```

| Status | Terlihat oleh Publik | Terlihat oleh Admin | Transisi yang Diizinkan |
|---|:---:|:---:|---|
| `draft` | ❌ | ✅ | → `published`, → dihapus |
| `published` | ✅ | ✅ | → `draft`, → dihapus |

Aturan transisi:
- Entri baru otomatis berstatus `draft` sampai admin menekan "Publikasikan".
- Saat `published`, kolom `published_at` terisi; saat ditarik ke draf, entri langsung hilang dari publik (revalidasi cache dipicu, BR-39).
- Penghapusan bersifat permanen dan selalu didahului dialog konfirmasi (US-35); file terkait di Storage ikut dihapus (BR-23).
- Perubahan `is_featured` mengikuti BR-26 dan BR-27.

### 6.2 Alur Pembuatan / Pengeditan Konten oleh Admin

1. Admin login (`/admin/login`) → sesi valid → diarahkan ke `/admin`.
2. Memilih modul dari sidebar → melihat tabel daftar (cari, urutkan, filter status).
3. Menekan "Tambah" atau ikon edit → formulir (tab ID/EN, Rich Text Editor, upload gambar).
4. Validasi klien + server (BR-10) → jika gagal, pesan kesalahan per field.
5. Simpan sebagai Draf atau Simpan & Publikasikan.
6. Sistem menyimpan data, memicu revalidasi halaman terkait, dan menampilkan *toast* sukses.

### 6.3 Alur Pengiriman Pesan Kontak (Visitor)

```
Visitor isi formulir
   │
   ▼
Validasi klien ──gagal──► tampilkan pesan error per field
   │ lolos
   ▼
Kirim ke server ──► Cek honeypot & rate limit ──gagal──► tolak (pesan umum)
   │ lolos
   ▼
Validasi server ──gagal──► kembalikan error
   │ lolos
   ▼
INSERT ke `messages` (status: unread)
   │
   ├──► Kirim email notifikasi (gagal → dicatat, tidak membatalkan)
   ▼
Tampilkan "Pesan terkirim" + reset formulir
```

### 6.4 Status Pesan Masuk (Admin)

```
UNREAD ──(dibuka/ditandai)──► READ ──(arsipkan)──► ARCHIVED
   ▲                            │                      │
   └──────(tandai belum dibaca)─┘                      │
UNREAD / READ / ARCHIVED ──(hapus + konfirmasi)──► DIHAPUS
```

| Status | Arti | Tampilan di Inbox |
|---|---|---|
| `unread` | Pesan baru, belum dibuka | Tebal + lencana jumlah di sidebar |
| `read` | Sudah dibuka admin | Normal |
| `archived` | Disimpan, disembunyikan dari daftar utama | Tab "Arsip" |

---

## 7. Spesifikasi Halaman / Menu

### 7.1 Ringkasan Peta Halaman

| No | Halaman | Rute | Akses | Keterangan |
|---|---|---|---|---|
| 1 | Home / Landing | `/[lang]` | Publik | Ringkasan profil dan sorotan |
| 2 | Pendidikan | `/[lang]/education` | Publik | Linimasa |
| 3 | Organisasi | `/[lang]/organization` | Publik | Daftar pengalaman organisasi |
| 4 | Kepanitiaan | `/[lang]/committee` | Publik | Daftar pengalaman kepanitiaan |
| 5 | Project | `/[lang]/projects` | Publik | Daftar + pencarian + filter |
| 6 | Detail Project | `/[lang]/projects/[slug]` | Publik | Detail proyek |
| 7 | Sertifikasi & Penghargaan | `/[lang]/certificates` | Publik | Daftar + filter |
| 8 | Galeri | `/[lang]/gallery` | Publik | Grid + lightbox |
| 9 | Kontak | `/[lang]/contact` | Publik | Formulir + sosial media |
| 10 | Login Admin | `/admin/login` | Publik (khusus admin) | Autentikasi |
| 11 | Dashboard Admin | `/admin` | Super Admin | Ringkasan |
| 12 | Kelola Profil | `/admin/profile` | Super Admin | Profil dan CV |
| 13 | Kelola Pendidikan | `/admin/educations` | Super Admin | CRUD |
| 14 | Kelola Organisasi | `/admin/organizations` | Super Admin | CRUD |
| 15 | Kelola Kepanitiaan | `/admin/committees` | Super Admin | CRUD |
| 16 | Kelola Project | `/admin/projects` | Super Admin | CRUD + featured |
| 17 | Kelola Sertifikasi | `/admin/certificates` | Super Admin | CRUD |
| 18 | Kelola Galeri | `/admin/galleries` | Super Admin | CRUD + upload |
| 19 | Inbox Pesan | `/admin/messages` | Super Admin | Manajemen pesan |
| 20 | Halaman 404 / Error | otomatis | Publik | Halaman galat ramah |

### 7.2 Halaman Publik

#### 7.2.1 Home / Landing
- **Hero section:** foto profil, nama, headline profesional, kalimat singkat, tombol CTA ("Lihat Project", "Hubungi Saya") dan tombol **Download CV**.
- **Ringkasan Tech Stack:** deretan ikon/badge teknologi (Next.js, TypeScript, Tailwind CSS, Supabase, dsb.) yang diambil dari data profil.
- **Quick Statistics:** angka ringkas (jumlah proyek, sertifikat, organisasi, kepanitiaan) dihitung otomatis dari data tayang.
- **Featured Projects:** kartu proyek dengan `is_featured = true` (maks. 6) dengan tombol "Lihat Semua Project".
- **Visitor Counter:** menampilkan total kunjungan unik.
- Header navigasi (sticky), pengalih bahasa, pengalih tema, dan footer.

#### 7.2.2 Pendidikan
- Linimasa vertikal (kronologis menurun): institusi, jenjang/jurusan, periode, nilai/IPK (opsional), deskripsi singkat.
- Pembeda visual antara pendidikan **formal** dan **informal** (bootcamp, kursus panjang) melalui lencana tipe.

#### 7.2.3 Organisasi
- Kartu: nama organisasi, jabatan, periode aktif (atau "Sekarang"), deskripsi kontribusi (rich text), logo opsional.

#### 7.2.4 Kepanitiaan
- Kartu: nama acara, peran/divisi, periode, ringkasan tanggung jawab, tautan dokumentasi opsional.

#### 7.2.5 Project
- Bilah pencarian, filter kategori (Web App, Mobile, AI/CV, UI/UX, dst.), filter tech stack, dan tombol reset.
- Kartu proyek: thumbnail, judul, ringkasan, badge kategori, badge tech stack, tombol **Live Demo** dan **GitHub**.
- Halaman detail: galeri gambar, deskripsi lengkap (rich text), peran, tech stack, tautan, dan proyek terkait.
- Paginasi atau *load more* (12 item per halaman).

#### 7.2.6 Sertifikasi & Penghargaan
- Satu wadah gabungan dengan tab/filter jenis (Semua, Sertifikat, Penghargaan) dan filter penerbit (issuer).
- Kartu: gambar/thumbnail, judul, issuer, tanggal terbit, tanggal kedaluwarsa (opsional), tombol **Lihat Kredensial**.

#### 7.2.7 Galeri
- Grid foto responsif (masonry atau seragam) dengan *lazy loading*.
- **Lightbox:** klik untuk memperbesar, navigasi kiri/kanan (tombol dan keyboard), tutup dengan Esc, tampilkan keterangan acara dan tanggal.

#### 7.2.8 Kontak
- Formulir: Nama, Email, Subjek, Pesan (BR-11), tombol kirim dengan status *loading*, pesan sukses/gagal.
- Tautan sosial media: GitHub, LinkedIn, Instagram, email.
- Pernyataan privasi singkat terkait penggunaan data pesan.

### 7.3 Halaman Admin

#### 7.3.1 Login Admin
- Form email + password, pesan galat generik ("Email atau password salah"), pembatasan percobaan (BR-09).

#### 7.3.2 Dashboard
- Kartu ringkasan: total entri per modul, pesan belum dibaca, total kunjungan.
- Daftar aktivitas terbaru (pesan terakhir, konten terakhir diubah).
- Pintasan cepat "Tambah Project", "Lihat Pesan".

#### 7.3.3 Halaman Kelola Modul (pola umum)
- Tabel dengan pencarian, filter status (Draf/Tayang), pengurutan, dan paginasi.
- Aksi per baris: Edit, Publikasikan/Tarik, Hapus (dengan konfirmasi).
- Formulir tambah/ubah: tab bahasa ID/EN, Rich Text Editor, upload gambar dengan pratinjau, pemilih tanggal, tombol "Simpan Draf" dan "Simpan & Publikasikan".
- Khusus Project: toggle `is_featured`, pengatur `sort_order`, pemilih kategori, input tag tech stack.
- Khusus Galeri: unggah banyak gambar sekaligus (*multi-upload*) dan atur keterangan per foto.

#### 7.3.4 Inbox Pesan
- Daftar pesan dengan penanda status, pencarian, filter (Semua/Belum dibaca/Arsip).
- Panel detail: nama, email (tombol "Balas via email"), subjek, isi, waktu kirim.
- Aksi: tandai dibaca/belum, arsipkan, hapus.

---

## 8. Data Utama

Database: **Supabase PostgreSQL**. Seluruh tabel mengaktifkan RLS (BR-03). Kolom umum pada tabel konten: `id` (UUID, PK), `status` (`draft`/`published`), `sort_order` (int), `created_at`, `updated_at`, `published_at`.

### 8.1 Ringkasan Tabel

| Tabel | Fungsi | Relasi Utama |
|---|---|---|
| `profiles` | Profil pemilik dan penanda peran admin | 1:1 dengan `auth.users` |
| `educations` | Riwayat pendidikan formal/informal | — |
| `organizations` | Pengalaman organisasi | — |
| `committees` | Pengalaman kepanitiaan | — |
| `projects` | Portofolio karya | — |
| `certificates` | Sertifikat dan penghargaan | — |
| `galleries` | Dokumentasi visual | opsional ke `committees`/`organizations` |
| `messages` | Pesan kontak masuk | — |

### 8.2 Struktur Kolom

**`profiles`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| id | UUID (PK, FK → auth.users.id) | Identitas pengguna |
| role | text | `super_admin` (dasar kebijakan RLS) |
| full_name | text | Nama lengkap |
| headline_id / headline_en | text | Judul profesional |
| bio_id / bio_en | text (rich) | Biografi |
| avatar_url | text | Foto profil |
| email_public | text | Email yang ditampilkan |
| github_url, linkedin_url, instagram_url | text | Tautan sosial |
| cv_url_id / cv_url_en | text | Berkas CV per bahasa |
| tech_stack | text[] / jsonb | Ringkasan tech stack di Home |
| location | text | Domisili |
| updated_at | timestamptz | — |

**`educations`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| institution | text | Nama institusi |
| education_type | text | `formal` / `informal` |
| degree_id / degree_en | text | Jenjang/program |
| field_of_study | text | Jurusan/bidang |
| start_date, end_date | date | Periode |
| is_current | boolean | Masih berjalan |
| gpa | numeric (nullable) | Nilai/IPK |
| description_id / description_en | text (rich) | Deskripsi |
| logo_url | text | Logo institusi |

**`organizations`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| name | text | Nama organisasi |
| position_id / position_en | text | Jabatan |
| start_date, end_date, is_current | date/boolean | Periode aktif |
| description_id / description_en | text (rich) | Kontribusi |
| logo_url | text | Logo |

**`committees`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| event_name | text | Nama acara |
| role_id / role_en | text | Peran/divisi |
| organizer | text | Penyelenggara |
| start_date, end_date | date | Periode |
| description_id / description_en | text (rich) | Ringkasan tanggung jawab |
| documentation_url | text | Tautan dokumentasi (opsional) |

**`projects`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| title_id / title_en | text | Judul |
| slug | text (unik) | URL ramah SEO |
| summary_id / summary_en | text | Ringkasan |
| description_id / description_en | text (rich) | Deskripsi lengkap |
| category | text | Web App / Mobile / AI-CV / UI-UX / Data / Lainnya |
| tech_stack | text[] | Teknologi yang digunakan |
| thumbnail_url | text | Gambar utama |
| images | text[] | Gambar tambahan |
| live_demo_url | text | Link demo |
| repo_url | text | Link GitHub |
| is_featured | boolean | Tampil di Home (maks. 6) |
| year | int | Tahun pengerjaan |

**`certificates`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| title_id / title_en | text | Nama sertifikat/penghargaan |
| type | text | `certificate` / `award` |
| issuer | text | Penerbit/penyelenggara |
| issued_date | date | Tanggal terbit |
| expiry_date | date (nullable) | Kedaluwarsa |
| credential_id | text | ID kredensial |
| credential_url | text | Tautan verifikasi |
| image_url | text | Gambar sertifikat |
| description_id / description_en | text | Deskripsi singkat |

**`galleries`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| image_url | text | Berkas foto |
| caption_id / caption_en | text | Keterangan acara |
| event_date | date | Tanggal kegiatan |
| alt_text | text | Teks alternatif aksesibilitas |
| related_type / related_id | text/UUID | Tautan opsional ke organisasi/kepanitiaan |

**`messages`**

| Kolom | Tipe | Keterangan |
|---|---|---|
| id | UUID (PK) | — |
| name | text | Nama pengirim |
| email | text | Email pengirim |
| subject | text | Subjek |
| message | text | Isi pesan |
| status | text | `unread` / `read` / `archived` |
| created_at | timestamptz | Waktu kirim |
| ip_hash | text | Hash IP untuk rate limit (opsional) |

*Tabel pendukung (opsional):* `site_visits` (`id`, `visitor_hash`, `visited_at`) untuk Visitor Counter.

### 8.3 Ringkasan Kebijakan RLS

| Tabel | anon (publik) | authenticated (Super Admin) |
|---|---|---|
| profiles | SELECT (kolom publik saja) | SELECT, UPDATE |
| educations, organizations, committees, projects, certificates, galleries | SELECT where `status='published'` | SELECT, INSERT, UPDATE, DELETE |
| messages | INSERT saja | SELECT, UPDATE, DELETE |
| site_visits | INSERT saja (via fungsi server) | SELECT |

### 8.4 Storage Buckets

| Bucket | Akses Baca | Akses Tulis | Batas |
|---|---|---|---|
| avatars | Publik | Admin | 2 MB |
| project-images | Publik | Admin | 2 MB |
| certificates | Publik | Admin | 2 MB |
| gallery | Publik | Admin | 5 MB |
| documents | Publik (CV) | Admin | 5 MB (PDF) |

---

## 9. Fitur Nilai Tambah / Lanjutan

| Kode | Fitur | Deskripsi | Aturan Utama |
|---|---|---|---|
| VA-01 | **Multi-Bahasa ID/EN** | Rute berprefiks bahasa, kamus terjemahan UI (mis. `next-intl`), konten dinamis dwibahasa dari database. Pengalih bahasa di header. | BR-40, BR-41; atribut `lang` HTML dan tag `hreflang` disetel benar |
| VA-02 | **Dark / Light Mode** | Pengalih tema dengan opsi Sistem/Terang/Gelap, preferensi disimpan, tanpa *flash* tema salah saat muat (mis. `next-themes`). | Rasio kontras memenuhi WCAG AA di kedua tema |
| VA-03 | **Download CV PDF** | Tombol unduh di Home dan Kontak; berkas diambil dari Storage, versi ID/EN mengikuti bahasa aktif. Admin dapat mengganti CV tanpa deploy. | BR-21; jumlah unduhan dapat dicatat (opsional) |
| VA-04 | **Visitor Counter / Analytics** | Penghitung kunjungan unik di Home. Analitik detail (halaman populer, negara, perangkat) via Vercel Analytics atau Plausible, tanpa data pribadi. | BR-44 s.d. BR-46 |
| VA-05 | **Rich Text Editor (Admin)** | Editor (mis. TipTap) untuk deskripsi: heading, tebal/miring, daftar, tautan, kutipan, blok kode. | Output disanitasi (BR-13); gambar sisipan tunduk pada BR-20 |
| VA-06 | **Pratinjau Draf** | Admin dapat melihat tampilan publik dari konten draf. | Hanya sesi admin; BR-38 tetap berlaku untuk publik |
| VA-07 | **Notifikasi Email** | Email otomatis ke pemilik saat pesan baru masuk (mis. Resend/SMTP). | BR-35 |

---

## 10. Kebutuhan Non-Fungsional

### 10.1 Performa

| Kode | Kebutuhan | Target |
|---|---|---|
| NFR-01 | Largest Contentful Paint (LCP) | ≤ 2,5 detik (4G, mobile) |
| NFR-02 | Interaction to Next Paint (INP) | ≤ 200 ms |
| NFR-03 | Cumulative Layout Shift (CLS) | ≤ 0,1 |
| NFR-04 | Time to First Byte (TTFB) halaman publik | ≤ 600 ms (didukung cache/ISR dan CDN Vercel) |
| NFR-05 | Ukuran JavaScript awal halaman publik | ≤ 200 KB (gzip) di luar gambar |
| NFR-06 | Skor Lighthouse halaman publik | ≥ 90 pada semua kategori |
| NFR-07 | Optimasi aset | `next/image`, font via `next/font`, *code splitting*, *lazy loading* untuk galeri dan lightbox |

### 10.2 SEO dan Open Graph

| Kode | Kebutuhan |
|---|---|
| NFR-08 | Metadata dinamis lewat Metadata API Next.js: `title`, `description`, `canonical`, dan `alternates.languages` untuk ID/EN. |
| NFR-09 | **Open Graph dan Twitter Card dinamis:** `og:title`, `og:description`, `og:image` (gambar OG otomatis via `opengraph-image` atau thumbnail proyek), `og:type`, `og:locale`. Halaman detail proyek memiliki OG sendiri. |
| NFR-10 | `sitemap.xml` dan `robots.txt` dibuat otomatis; sitemap memuat halaman publik dan detail proyek tayang. |
| NFR-11 | Data terstruktur JSON-LD (`Person` di Home, `CreativeWork`/`SoftwareSourceCode` di detail proyek). |
| NFR-12 | **Seluruh rute `/admin/*` bertanda `noindex, nofollow`** dan di-*disallow* pada robots.txt (BR-42). |

### 10.3 Responsif dan Aksesibilitas

| Kode | Kebutuhan |
|---|---|
| NFR-13 | Desain **mobile-first** dengan *breakpoint* Tailwind (sm 640, md 768, lg 1024, xl 1280); diuji pada lebar 320 px hingga 1920 px. |
| NFR-14 | Target sentuh minimal 44×44 px; navigasi mobile berupa menu hamburger/drawer. |
| NFR-15 | Aksesibilitas WCAG 2.1 AA: HTML semantik, navigasi keyboard penuh (termasuk lightbox), *focus ring* jelas, `alt text`, label formulir, dan dukungan `prefers-reduced-motion`. |
| NFR-16 | Kompatibilitas browser: dua versi terbaru Chrome, Edge, Firefox, Safari (desktop dan mobile). |

### 10.4 Keamanan

| Kode | Kebutuhan |
|---|---|
| NFR-17 | **Autentikasi dan otorisasi di level database:** semua akses data ditegakkan oleh RLS Supabase; tidak bergantung pada penyembunyian UI. |
| NFR-18 | Middleware Next.js memvalidasi sesi pada semua rute admin; Server Actions/Route Handler admin memverifikasi ulang peran. |
| NFR-19 | Seluruh lalu lintas melalui HTTPS (HSTS aktif). |
| NFR-20 | Header keamanan: `Content-Security-Policy`, `X-Frame-Options`/`frame-ancestors`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`. |
| NFR-21 | Rahasia (service role key, kunci email) hanya di environment variable Vercel server-side; tidak masuk repositori. |
| NFR-22 | Perlindungan XSS, CSRF (Server Actions), dan injeksi SQL (kueri berparameter via klien Supabase). |
| NFR-23 | Pembatasan laju pada login dan formulir kontak (BR-09, BR-12). |
| NFR-24 | Pencadangan: *backup* database Supabase terjadwal dan ekspor berkala data konten. |

### 10.5 Keandalan dan Pemeliharaan

| Kode | Kebutuhan |
|---|---|
| NFR-25 | Ketersediaan target ≥ 99,5% (bergantung SLA Vercel dan Supabase). |
| NFR-26 | Penanganan galat: halaman 404/500 kustom, *error boundary*, dan pencatatan galat (mis. Sentry atau log Vercel). |
| NFR-27 | Kode TypeScript ketat, lint (ESLint) dan format (Prettier) wajib lulus sebelum merge. |
| NFR-28 | Migrasi skema disimpan sebagai berkas SQL berversi di repositori. |
| NFR-29 | Lingkungan terpisah: Development (lokal), Preview (branch Vercel), Production. |

---

## 11. Kriteria Selesai (Definition of Done)

Fitur dinyatakan siap rilis jika seluruh butir berikut lulus.

### 11.1 Fitur Publik
- [ ] Home menampilkan hero, tech stack, statistik, Featured Projects (maks. 6), tombol CV, dan visitor counter dengan data nyata.
- [ ] Halaman Pendidikan, Organisasi, dan Kepanitiaan tampil kronologis dan hanya memuat entri berstatus tayang.
- [ ] Pencarian dan filter Project (kategori + tech stack + kata kunci) berfungsi, tersimpan di URL, dan *empty state* muncul bila tidak ada hasil.
- [ ] Filter Sertifikasi & Penghargaan berdasarkan issuer dan jenis berfungsi; tautan kredensial terbuka benar.
- [ ] Galeri menampilkan grid; lightbox dapat dibuka, ditutup (klik/Esc), dan dinavigasi (tombol/keyboard) dengan keterangan tampil.
- [ ] Formulir kontak: validasi benar, data tersimpan di `messages`, email notifikasi terkirim, *double submit* tercegah, honeypot dan rate limit aktif.
- [ ] Pengalih bahasa ID/EN mengubah seluruh UI dan konten, dengan *fallback* bekerja.
- [ ] Dark/Light mode berfungsi, tersimpan, dan tanpa *flash* tema.
- [ ] Download CV mengunduh PDF yang benar sesuai bahasa.

### 11.2 Fitur Admin
- [ ] Login berhasil dengan kredensial benar dan gagal dengan pesan generik bila salah; rate limit login aktif.
- [ ] Mengakses `/admin/*` tanpa sesi selalu dialihkan ke login.
- [ ] Full CRUD berfungsi pada semua modul: Education, Organization, Committee, Project, Certificate/Award, Gallery.
- [ ] Alur draf ↔ tayang bekerja; draf tidak pernah terlihat publik; revalidasi menampilkan perubahan tanpa deploy.
- [ ] Batas featured (maks. 6) ditegakkan dan `sort_order` memengaruhi urutan di Home.
- [ ] Upload file menolak tipe/ukuran tidak sesuai; file lama terhapus saat entri dihapus/diganti.
- [ ] Rich Text Editor menyimpan dan merender konten dengan benar; HTML berbahaya ter-sanitasi.
- [ ] Inbox pesan: baca, tandai, arsipkan, hapus (dengan konfirmasi) berfungsi.

### 11.3 Keamanan
- [ ] RLS aktif di semua tabel; pengujian dengan klien anon membuktikan: tidak bisa membaca draf, tidak bisa menulis ke tabel konten, tidak bisa membaca `messages`.
- [ ] Pengujian akun non-admin (jika ada akun uji) ditolak pada operasi tulis.
- [ ] Service role key tidak ditemukan pada bundel klien.
- [ ] Header keamanan terpasang; halaman admin mengirim `noindex`.

### 11.4 Kualitas dan Performa
- [ ] Lighthouse ≥ 90 (Performance, Accessibility, Best Practices, SEO) pada Home, Projects, dan Contact (mobile).
- [ ] Core Web Vitals memenuhi NFR-01 s.d. NFR-03.
- [ ] Tag OG tervalidasi melalui pratinjau tautan (LinkedIn/WhatsApp/Facebook Debugger) untuk Home dan satu detail proyek.
- [ ] `sitemap.xml` dan `robots.txt` benar.
- [ ] Tampilan diuji pada lebar 320, 375, 768, 1024, dan 1440 px tanpa *overflow* horizontal.
- [ ] Navigasi keyboard dan pembaca layar dasar lulus pada alur utama.

### 11.5 Rilis
- [ ] Build produksi tanpa galat TypeScript/ESLint.
- [ ] Environment variable produksi terpasang di Vercel; domain dan HTTPS aktif.
- [ ] Konten awal (profil, minimal 3 proyek, pendidikan, sertifikat, galeri) sudah diisi dan berstatus tayang.
- [ ] Akun Super Admin dibuat, registrasi publik dinonaktifkan, dan backup database dikonfirmasi.
- [ ] Dokumentasi README (setup lokal, skema, deploy) tersedia.

---

## 12. Di Luar Lingkup

Hal-hal berikut **tidak** dikerjakan pada versi 1.0:

| No | Item | Catatan |
|---|---|---|
| 1 | Multi-admin / manajemen pengguna dan peran tambahan | Hanya satu Super Admin |
| 2 | Registrasi, login, atau profil untuk pengunjung | Pengunjung selalu anonim |
| 3 | Komentar, *like*, atau fitur sosial pada proyek | — |
| 4 | Blog / artikel dan sistem tag artikel | Dapat dipertimbangkan di versi berikutnya |
| 5 | Pembalasan pesan langsung dari dalam dashboard | Balasan lewat klien email eksternal |
| 6 | Aplikasi mobile native | Cukup web responsif/PWA dasar tidak termasuk |
| 7 | Pembuatan CV otomatis dari data database | CV diunggah manual sebagai PDF |
| 8 | Bahasa selain ID dan EN | — |
| 9 | Pembayaran, e-commerce, atau layanan berlangganan | — |
| 10 | Riwayat versi konten (*version history*) dan alur persetujuan multi-tahap | Hanya status draf/tayang |
| 11 | Dashboard analitik kustom yang mendalam | Memakai alat analitik pihak ketiga |
| 12 | Integrasi otomatis dengan LinkedIn/GitHub (sinkronisasi repositori) | Data diinput manual |
| 13 | Mode *offline* penuh | — |

---

### Catatan Revisi

| Versi | Tanggal | Perubahan | Penulis |
|---|---|---|---|
| 1.0 | 31 Oktober 2026 | Draf awal PRD lengkap | Livia |
