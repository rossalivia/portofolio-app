# Aturan Desain: Website Portofolio

Dokumen ini adalah sumber kebenaran visual. Tempatkan di `docs/DESIGN.md` dan rujuk dari `AGENTS.md`.
Jika ada konflik dengan keputusan agen, dokumen ini menang. Jika sebuah situasi belum diatur, pilih opsi yang **lebih tenang dan lebih sedikit**.

---

## 1. Arah Visual

**Nama arah: "Editorial Hangat".**
Terasa seperti majalah desain atau jurnal pribadi yang rapi, bukan template SaaS. Kertas hangat, tinta pekat, satu warna aksen, tipografi yang berkarakter, dan banyak ruang kosong. Kesan yang dituju: **tenang, teliti, dewasa, personal**.

### Tiga prinsip
1. **Tipografi yang memimpin.** Hierarki dibangun dari ukuran, berat, dan jenis huruf, bukan dari kotak, bayangan, atau warna.
2. **Satu aksen, dipakai hemat.** Warna aksen hanya untuk hal yang bisa diklik atau harus diperhatikan.
3. **Struktur terlihat.** Garis tipis (hairline), penomoran bagian, dan grid yang konsisten menggantikan dekorasi.

### Yang ingin dirasakan pengunjung
"Orang ini rapi, punya selera, dan tahu apa yang ia kerjakan", bukan "ini template yang diisi."

---

## 2. Daftar Larangan (Anti-Slop)

Pola berikut **dilarang**. Jika agen menghasilkannya, tolak dan perbaiki.

| Dilarang | Alasan | Gantinya |
|---|---|---|
| Gradien ungu-biru/pink, "aurora", blob blur di latar | Penanda paling jelas desain AI generik | Warna datar, kertas hangat |
| Font Inter, Roboto, Poppins, Arial, system-ui sebagai identitas | Pasaran | Pasangan font di bagian 4 |
| Hero tengah dengan judul besar + dua tombol + gambar mockup | Template | Hero rata kiri, asimetris, editorial |
| Kartu berbayangan tebal, sudut sangat bulat (`rounded-3xl`) di mana-mana | Gaya "kartu SaaS" | Hairline border, radius kecil |
| Glassmorphism, `backdrop-blur` dekoratif | Usang dan berat | Permukaan solid |
| Ikon emoji di judul atau poin (🚀 ✨ 💡) | Tidak profesional | Tanpa ikon, atau ikon garis tipis |
| Ikon dalam lingkaran berwarna di atas tiap kartu fitur | Klise | Penomoran `01`, `02`, teks saja |
| Grid 3 kolom "fitur" berisi ikon + judul + kalimat | Klise | Daftar berbaris dengan garis pemisah |
| Teks "gradient" pada judul | Klise | Warna tinta solid |
| Animasi masuk berlebihan (bounce, flip, parallax berat) | Mengganggu | Fade + geser 8 px, sekali |
| Badge neon, glow, bayangan berwarna | Murahan | Badge garis tipis, netral |
| Tombol ber-gradien atau bayangan berwarna | Klise | Tombol solid datar |
| Statistik palsu atau pengisi ("100+ klien puas") | Tidak jujur | Hanya angka nyata dari data |
| Testimoni/logo fiktif, foto stok orang tersenyum | Tidak jujur | Karya nyata, foto sendiri |
| Salin teks generik: "passionate", "crafting digital experiences", "turning ideas into reality" | Kosong | Kalimat spesifik tentang apa yang dibuat |
| Dekorasi tanpa fungsi (garis bergelombang, partikel, ilustrasi 3D acak) | Noise | Hapus |
| Lebih dari satu warna aksen | Kacau | Satu aksen + netral |
| Tema gelap berupa hitam murni `#000` dengan teks putih murni | Silau, kasar | Tema gelap hangat (bagian 3) |

---

## 3. Warna

Semua warna didefinisikan sebagai token. **Dilarang** memakai kode warna mentah di komponen; gunakan token.

### Palet Terang ("Kertas")

| Token | Hex | Pemakaian |
|---|---|---|
| `--paper` | `#F6F3EC` | Latar halaman |
| `--paper-raised` | `#FBF9F4` | Permukaan terangkat (kartu, input) |
| `--paper-sunk` | `#ECE8DE` | Latar bagian berselang, blok kode |
| `--ink` | `#17160F` | Teks utama, judul |
| `--ink-soft` | `#4A4739` | Teks sekunder, paragraf panjang |
| `--ink-faint` | `#6F6B5A` | Meta, label, placeholder |
| `--line` | `#D9D4C5` | Garis tipis, pemisah |
| `--line-strong` | `#B9B3A0` | Garis tegas, border input |
| `--accent` | `#D4431F` | Permukaan aksen (tombol utama, penanda) |
| `--accent-ink` | `#B8381A` | Teks/tautan aksen di atas kertas |
| `--accent-wash` | `#F4DCD3` | Latar sorotan lembut |
| `--on-accent` | `#FFF8F3` | Teks di atas `--accent` |

### Palet Gelap ("Arang Hangat")
Bukan hasil membalik warna. Dirancang terpisah.

| Token | Hex | Pemakaian |
|---|---|---|
| `--paper` | `#14130F` | Latar halaman |
| `--paper-raised` | `#1C1B16` | Permukaan terangkat |
| `--paper-sunk` | `#0F0E0B` | Latar bagian berselang |
| `--ink` | `#EEEADF` | Teks utama |
| `--ink-soft` | `#B9B4A3` | Teks sekunder |
| `--ink-faint` | `#8A8574` | Meta, label |
| `--line` | `#2E2C24` | Garis tipis |
| `--line-strong` | `#47443A` | Garis tegas |
| `--accent` | `#FF6A3D` | Permukaan aksen |
| `--accent-ink` | `#FF8A63` | Teks/tautan aksen |
| `--accent-wash` | `#35201A` | Latar sorotan lembut |
| `--on-accent` | `#1A0D08` | Teks di atas aksen |

### Warna status (sangat hemat)
Sukses `#3F7D4E` (gelap: `#6FBF84`), peringatan `#A86A12` (gelap: `#E0A24A`), galat `#B3261E` (gelap: `#FF8A80`). Hanya untuk pesan sistem dan formulir.

### Aturan pemakaian warna
- Proporsi: **±90% netral (paper/ink)**, ±8% garis dan permukaan, **≤2% aksen**.
- Aksen hanya untuk: tombol utama, tautan, indikator aktif, penanda hover, dan satu elemen sorotan per layar.
- Kontras teks wajib **WCAG AA** (4,5:1 teks normal, 3:1 teks besar). Verifikasi dengan pemeriksa kontras sebelum menyetujui; ubah nilai token bila perlu, bukan ditoleransi.
- Teks aksen kecil memakai `--accent-ink`, bukan `--accent`.
- Gambar karya tidak diberi filter warna.

---

## 4. Tipografi

### Pasangan huruf
| Peran | Font | Sumber | Catatan |
|---|---|---|---|
| **Display / judul** | **Instrument Serif** | `next/font/google` | Serif tipis berkarakter, dipakai untuk judul besar dan angka penomoran. Satu berat (Regular) + Italic untuk penekanan |
| **Teks / UI** | **Geist Sans** | `next/font/google` | Bersih, tidak pasaran seperti Inter |
| **Meta / label / kode** | **Geist Mono** | `next/font/google` | Label bagian, tanggal, tech stack, nomor |

Aturan: maksimal **3 keluarga font**, dimuat lewat `next/font` dengan `display: swap` dan subset `latin`. Jangan menambah font lain.

### Skala (mobile → desktop)
| Peran | Font | Ukuran | Line-height | Letter-spacing |
|---|---|---|---|---|
| Display (hero) | Instrument Serif | `clamp(2.75rem, 7vw, 6rem)` | 1.0 | -0.02em |
| H1 halaman | Instrument Serif | `clamp(2.25rem, 5vw, 4rem)` | 1.05 | -0.015em |
| H2 bagian | Instrument Serif | `clamp(1.75rem, 3.5vw, 2.75rem)` | 1.1 | -0.01em |
| H3 | Geist Sans 600 | 1.25rem | 1.3 | -0.005em |
| Isi (body) | Geist Sans 400 | 1rem – 1.0625rem | 1.65 | 0 |
| Kecil | Geist Sans 400 | 0.875rem | 1.55 | 0 |
| Label / meta | Geist Mono 400 | 0.75rem | 1.4 | +0.04em, huruf kapital |

### Aturan teks
- Lebar baris paragraf **maksimal 65 karakter** (`max-w-prose`).
- Judul memakai *sentence case*, bukan Title Case atau SEMUA KAPITAL (kapital hanya untuk label mono).
- Penekanan dalam judul memakai **Italic Instrument Serif**, bukan warna atau garis bawah warna-warni.
- Tidak ada teks rata-tengah untuk paragraf. Rata tengah hanya untuk label pendek atau keadaan kosong.
- Angka tanggal dan statistik memakai `font-variant-numeric: tabular-nums`.
- Tautan di dalam teks: warna `--accent-ink`, garis bawah 1 px dengan `text-underline-offset: 3px`, hover menebalkan garis.

---

## 5. Tata Letak dan Spasi

### Grid
- Kontainer maksimum **1200 px**, gutter samping 20 px (mobile), 32 px (tablet), 48 px (desktop).
- Grid **12 kolom** pada desktop, 4 kolom pada mobile. Komposisi **asimetris**: label bagian di kolom 1–3, konten di kolom 4–12.
- Konten teks panjang di kolom sempit (maks. 65ch); jangan meregangkan teks hingga lebar penuh.

### Skala spasi (kelipatan 4 px)
`4 · 8 · 12 · 16 · 24 · 32 · 48 · 64 · 96 · 128`. Jarak antar-bagian halaman: **96 px (mobile 64 px)**. Jangan memakai nilai di luar skala.

### Bentuk
| Elemen | Aturan |
|---|---|
| Radius | `2px` (input, badge), `4px` (kartu, tombol). **Tidak ada** radius > 8 px kecuali avatar bulat |
| Border | 1 px `--line`; fokus/hover `--line-strong` |
| Bayangan | **Tidak dipakai** pada tampilan publik. Elevasi lewat garis dan perbedaan permukaan. Pengecualian: dialog/lightbox boleh memakai satu bayangan lembut |
| Pemisah bagian | Garis tipis penuh lebar + label bagian `01 / Projects` dalam mono |

### Struktur bagian (pola berulang)
```
──────────────────────────────────────────────  (garis tipis)
01 / PROJECTS          Judul bagian dalam serif besar
(mono, kecil)          Satu kalimat pengantar spesifik.
                       [konten]
```
Penomoran bagian konsisten di semua halaman (`01`, `02`, ...). Ini menjadi tanda tangan visual situs.

---

## 6. Komponen

### Tombol
| Varian | Gaya |
|---|---|
| Primer | Latar `--accent`, teks `--on-accent`, radius 4 px, tinggi 44 px, padding 20 px, **tanpa bayangan**. Hover: gelapkan 6%, geser panah `→` 3 px |
| Sekunder | Transparan, border 1 px `--line-strong`, teks `--ink`. Hover: latar `--paper-sunk` |
| Teks/Tautan | Teks `--accent-ink` + garis bawah, ikon panah `↗` untuk tautan eksternal |
Maksimal **satu tombol primer per layar**. Fokus keyboard: outline 2 px `--accent`, offset 3 px.

### Kartu Proyek
- Tanpa bayangan. Border tipis `--line`, latar `--paper-raised`, radius 4 px.
- Gambar rasio **4:3** (konsisten), `object-fit: cover`, tanpa overlay gradien.
- Isi: label mono (kategori · tahun), judul serif/Geist 600, ringkasan maks. 2 baris, daftar tech stack sebagai teks mono dipisah `·` (bukan deretan badge berwarna).
- Hover: border menjadi `--line-strong`, gambar zoom halus 1.02 (200 ms), panah `↗` muncul. Tidak ada kartu yang "melompat" atau berbayang.

### Daftar Baris (Pendidikan, Organisasi, Kepanitiaan, Sertifikat)
Bukan kartu. Gunakan **baris editorial** dengan garis pemisah:
```
2023 — Sekarang │ Universitas Semarang
(mono, kolom 1–3) │ Sistem Informasi (serif/semibold)
                 │ Deskripsi singkat (ink-soft)
```
Linimasa Pendidikan: garis vertikal 1 px `--line` dengan titik 8 px; titik aktif memakai `--accent`.

### Badge dan Tag
Teks mono 12 px, border 1 px `--line`, radius 2 px, **tanpa latar berwarna**. Tag aktif pada filter: latar `--ink`, teks `--paper` (inversi, bukan aksen).

### Formulir
- Label di atas input (bukan placeholder sebagai label). Input: latar `--paper-raised`, border 1 px `--line-strong`, radius 2 px, tinggi 44 px.
- Fokus: border `--accent` + ring 2 px `--accent-wash`.
- Galat: border + teks `--error`, pesan di bawah field, singkat dan spesifik ("Email belum valid", bukan "Terjadi kesalahan").

### Navigasi
- Header tipis (64 px), latar `--paper` dengan garis bawah tipis saat di-scroll. **Tanpa blur kaca**.
- Kiri: nama/monogram dalam serif. Kanan: tautan teks, pengalih bahasa `ID / EN` (mono), pengalih tema (ikon matahari/bulan garis tipis).
- Tautan aktif: garis bawah 1 px `--accent`, bukan latar berwarna.
- Mobile: panel penuh layar dengan tautan berukuran besar dalam serif.

### Lightbox Galeri
Latar `--paper-sunk` 96% opak (gelap di tema gelap), foto di tengah, keterangan dalam mono di bawah, kontrol teks minimal (`← →`, `Esc`). Fokus terkunci, dapat dioperasikan keyboard.

### Keadaan Kosong, Memuat, Galat
- Kosong: satu kalimat jujur + satu tindakan ("Belum ada proyek di kategori ini. Reset filter").
- Memuat: skeleton datar `--paper-sunk` tanpa efek shimmer berkilau; boleh denyut opacity pelan.
- 404: judul serif besar, satu kalimat, tautan kembali. Tanpa ilustrasi lucu.

---

## 7. Halaman Kunci

### Hero (Home)
- **Rata kiri**, asimetris. Judul display serif memuat satu kalimat spesifik tentang apa yang kamu bangun; kata kunci ditekankan dengan *italic*.
- Di bawahnya: satu paragraf pendek (≤ 2 kalimat), tautan teks `Lihat project →` dan `Unduh CV ↓`, dan baris meta mono (lokasi, status ketersediaan, tahun).
- Foto: potret dengan rasio 4:5, kolom kanan, tanpa bingkai warna-warni, tanpa blob. Boleh disertai caption mono kecil.
- **Tidak ada** mockup perangkat, gelembung teknologi melayang, atau efek ketik berulang (typewriter).

### Tech Stack
Daftar teks mono dalam grid rapat, dikelompokkan (Frontend / Backend / Tools) dengan label kecil. Tanpa logo berwarna-warni, tanpa bilah persentase kemahiran.

### Statistik Cepat
Angka besar Instrument Serif + label mono, dipisah garis tipis vertikal. Hanya angka nyata dari database.

### Featured Projects
Layout editorial: proyek pertama besar (lebar penuh), sisanya 2 kolom. Bukan carousel.

### Galeri
Grid dengan rasio campuran rapi (masonry sederhana) dan jarak 8 px. Keterangan muncul di lightbox, bukan menimpa foto.

---

## 8. Gerak (Motion)

- Prinsip: gerak menjelaskan perubahan, bukan menghibur.
- Durasi 150–250 ms, easing `cubic-bezier(0.22, 1, 0.36, 1)`.
- Masuk saat scroll: **fade + geser vertikal 8 px, sekali**, per bagian (bukan per huruf atau per kata).
- Hover: perubahan warna/garis, panah bergeser 3 px, gambar zoom 1.02.
- **Wajib** menghormati `prefers-reduced-motion: reduce` (matikan semua transisi non-esensial).
- Dilarang: parallax, cursor kustom, scroll-jacking, animasi tak berujung, loader layar penuh.

---

## 9. Gambar dan Ikon

- Foto asli lebih baik dari ilustrasi. Gunakan tangkapan layar proyek yang bersih (tanpa bingkai perangkat palsu).
- Rasio konsisten per konteks (proyek 4:3, potret 4:5, galeri bebas dalam grid).
- Ikon: **lucide-react**, `strokeWidth={1.5}`, ukuran 16/20 px, warna mengikuti teks. Dipakai hanya jika membantu (tema, panah, sosial media). Tidak ada ikon dekoratif.
- Semua gambar punya `alt` yang deskriptif, dan placeholder `blur` berwarna `--paper-sunk`.

---

## 10. Suara dan Salin Teks (Copy)

| Prinsip | Contoh baik | Contoh buruk |
|---|---|---|
| Spesifik | "Membangun aplikasi ERP distribusi dengan Next.js dan Supabase." | "Passionate developer crafting digital experiences." |
| Orang pertama, langsung | "Saya mahasiswa Sistem Informasi yang suka merapikan alur kerja yang berantakan." | "Seorang individu yang berdedikasi tinggi…" |
| Singkat | Kalimat ≤ 20 kata | Paragraf pembuka berlapis |
| Jujur | "Proyek kuliah, belum dipakai pengguna nyata." | "Solusi inovatif kelas enterprise." |
| Tanpa klise | Hindari: *passionate, innovative, cutting-edge, seamless, leverage, journey* | |

- Bahasa Indonesia: baku-santai, bukan kaku, tanpa campuran Inggris yang tidak perlu. Bahasa Inggris: sederhana dan setara bobotnya, bukan terjemahan mentah.
- Tombol berupa kata kerja: "Lihat project", "Kirim pesan", "Unduh CV".
- Tanpa tanda seru berlebihan, tanpa emoji.

---

## 11. Panel Admin

Admin adalah alat kerja, bukan pajangan. Tetap satu keluarga visual, tetapi **lebih padat dan netral**.
- Pakai token yang sama, tetapi aksen lebih hemat (hanya tombol primer dan fokus).
- Font: Geist Sans untuk semua; Instrument Serif hanya untuk judul halaman.
- Tabel rapat: tinggi baris 44 px, garis tipis, tanpa zebra mencolok, aksi per baris berupa ikon garis dengan tooltip.
- Status: teks mono kecil dengan titik 6 px (`Draf` abu, `Tayang` hijau), bukan pil berwarna cerah.
- Formulir dua kolom di desktop; tab ID/EN jelas; tombol "Simpan Draf" (sekunder) dan "Simpan & Publikasikan" (primer).
- Dialog konfirmasi hapus: teks spesifik ("Hapus proyek 'ERP Distribusi'? Tindakan ini tidak bisa dibatalkan.") dan tombol hapus berwarna galat.

---

## 12. Implementasi Token (Tailwind v4)

Letakkan di `src/app/globals.css`. Sesuaikan jika proyek memakai Tailwind v3 (pindahkan ke `tailwind.config`).

```css
@import "tailwindcss";

@theme {
  --font-display: var(--font-instrument-serif), ui-serif, Georgia, serif;
  --font-sans: var(--font-geist-sans), ui-sans-serif, sans-serif;
  --font-mono: var(--font-geist-mono), ui-monospace, monospace;

  --color-paper: var(--paper);
  --color-paper-raised: var(--paper-raised);
  --color-paper-sunk: var(--paper-sunk);
  --color-ink: var(--ink);
  --color-ink-soft: var(--ink-soft);
  --color-ink-faint: var(--ink-faint);
  --color-line: var(--line);
  --color-line-strong: var(--line-strong);
  --color-accent: var(--accent);
  --color-accent-ink: var(--accent-ink);
  --color-accent-wash: var(--accent-wash);
  --color-on-accent: var(--on-accent);

  --radius-sm: 2px;
  --radius-md: 4px;
}

:root {
  --paper: #F6F3EC;  --paper-raised: #FBF9F4;  --paper-sunk: #ECE8DE;
  --ink: #17160F;    --ink-soft: #4A4739;      --ink-faint: #6F6B5A;
  --line: #D9D4C5;   --line-strong: #B9B3A0;
  --accent: #D4431F; --accent-ink: #B8381A;    --accent-wash: #F4DCD3;
  --on-accent: #FFF8F3;
}

.dark {
  --paper: #14130F;  --paper-raised: #1C1B16;  --paper-sunk: #0F0E0B;
  --ink: #EEEADF;    --ink-soft: #B9B4A3;      --ink-faint: #8A8574;
  --line: #2E2C24;   --line-strong: #47443A;
  --accent: #FF6A3D; --accent-ink: #FF8A63;    --accent-wash: #35201A;
  --on-accent: #1A0D08;
}

html { background: var(--paper); color: var(--ink); }
body { font-family: var(--font-sans); font-size: 1rem; line-height: 1.65; }

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation: none !important; transition: none !important; scroll-behavior: auto !important; }
}
```

Pemuatan font (`src/app/layout.tsx`):
```ts
import { Instrument_Serif, Geist, Geist_Mono } from "next/font/google";

const display = Instrument_Serif({ subsets: ["latin"], weight: "400", style: ["normal", "italic"], variable: "--font-instrument-serif", display: "swap" });
const sans = Geist({ subsets: ["latin"], variable: "--font-geist-sans", display: "swap" });
const mono = Geist_Mono({ subsets: ["latin"], variable: "--font-geist-mono", display: "swap" });
// <html className={`${display.variable} ${sans.variable} ${mono.variable}`}>
```

---

## 13. Daftar Periksa Desain (sebelum setiap commit UI)

- [ ] Tidak ada item dari Daftar Larangan (bagian 2).
- [ ] Hanya token warna yang dipakai; tidak ada hex mentah di komponen.
- [ ] Aksen ≤ 2% area layar; satu tombol primer per layar.
- [ ] Hanya 3 keluarga font; judul serif, meta mono, isi Geist.
- [ ] Paragraf ≤ 65 karakter per baris, tidak rata tengah.
- [ ] Tidak ada bayangan pada kartu publik; radius ≤ 4 px.
- [ ] Penomoran bagian dan garis tipis konsisten.
- [ ] Kontras AA di tema terang **dan** gelap (dicek, bukan dikira).
- [ ] Tema gelap terlihat dirancang, bukan inversi.
- [ ] Diuji di lebar 320, 375, 768, 1024, 1440 px tanpa overflow.
- [ ] `prefers-reduced-motion` dihormati; navigasi keyboard dan fokus terlihat.
- [ ] Salin teks spesifik, jujur, tanpa klise dan emoji.
- [ ] Semua gambar punya `alt`; tidak ada gambar stok generik.

---

## 14. Prompt Penerapan untuk Antigravity

Gunakan pada **Fase 3** (menggantikan arah visual yang diusulkan agen), dan ulangi singkat di fase UI berikutnya.

```text
Baca docs/DESIGN.md sampai selesai. Dokumen ini adalah sumber kebenaran visual dan mengalahkan preferensi gayamu sendiri.

Tugas:
1. Terapkan token warna (terang dan gelap), skala tipografi, radius, dan spasi dari DESIGN.md ke globals.css dan konfigurasi Tailwind persis seperti bagian 12. Muat Instrument Serif, Geist, dan Geist Mono lewat next/font.
2. Bangun komponen dasar sesuai bagian 6: Button (primer/sekunder/teks), Badge/Tag, Input/Textarea/Select, Card proyek, baris editorial (untuk pendidikan/organisasi/kepanitiaan/sertifikat), Header, Footer, SectionHeading (dengan penomoran 01 / LABEL), EmptyState, Skeleton.
3. Jangan memakai gradien, glassmorphism, bayangan pada kartu, ikon emoji, ikon dalam lingkaran berwarna, font selain tiga yang ditetapkan, atau warna hex mentah di komponen.
4. Hormati prefers-reduced-motion dan WCAG AA di kedua tema.
5. Setelah selesai, jalankan Daftar Periksa Desain (bagian 13) terhadap hasilmu dan laporkan butir mana yang lulus atau gagal. Perbaiki yang gagal sebelum melapor.
Jika ada situasi yang tidak diatur DESIGN.md, pilih opsi yang lebih tenang dan lebih sedikit, lalu catat keputusan itu.
```

Tambahkan satu baris ke `AGENTS.md`:
```markdown
- Semua keputusan visual mengikuti docs/DESIGN.md. Hindari pola pada Daftar Larangan (Anti-Slop).
```
