# Website Portofolio Profesional + CMS Internal

Website portofolio digital dinamis dengan sistem manajemen konten internal (CMS) berbasis Next.js (App Router), TypeScript, Tailwind CSS, dan Supabase.

---

## 🚀 Tech Stack

- **Framework**: [Next.js](https://nextjs.org/) (App Router, React 19)
- **Language**: [TypeScript](https://www.typescriptlang.org/) (Strict mode)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **Backend / Database**: [Supabase](https://supabase.com/) (PostgreSQL, Row Level Security, Auth, Storage)
- **Internationalization (i18n)**: [next-intl](https://next-intl-docs.vercel.app/) (ID / EN)
- **Theming**: [next-themes](https://github.com/pacocoursey/next-themes) (Light / Dark mode)
- **Form & Validation**: [React Hook Form](https://react-hook-form.com/) + [Zod](https://zod.dev/)
- **UI Components & Icons**: [Lucide React](https://lucide.dev/), [Sonner](https://sonner.emilkowal.ski/)
- **Deployment**: [Vercel](https://vercel.com/)

---

## 📁 Struktur Direktori

```text
portofolio-app/
├── docs/                      # Dokumentasi produk & spesifikasi
│   └── PRD.md                 # Product Requirement Document (PRD)
├── public/                    # Aset statis publik
├── src/
│   ├── app/                   # Next.js App Router
│   ├── components/            # Komponen React (ui, common, layout)
│   ├── lib/                   # Utilitas & Supabase client helpers
│   │   └── supabase/          # client.ts, server.ts, middleware.ts
│   ├── messages/              # Kamus terjemahan i18n (id.json, en.json)
│   ├── schemas/               # Skema validasi Zod (shared client & server)
│   └── types/                 # Definisi tipe TypeScript & skema database
├── supabase/
│   └── migrations/            # Berkas migrasi database SQL berversi
├── .env.example               # Contoh konfigurasi variabel lingkungan
├── AGENTS.md                  # Aturan pengembangan agen AI
└── DESIGN.md                  # Pedoman desain visual ("Editorial Hangat")
```

---

## 🛠️ Memulai Pengembangan Lokal

### Prasyarat

- [Node.js](https://nodejs.org/) v18.18+ atau v20+
- [npm](https://www.npmjs.com/)

### 1. Klon Repositori & Instal Dependensi

```bash
git clone <url-repositori>
cd portofolio-app
npm install
```

### 2. Konfigurasi Variabel Lingkungan

Salin berkas `.env.example` ke `.env.local`:

```bash
cp .env.example .env.local
```

Buka `.env.local` dan lengkapi konfigurasi berikut:

```env
NEXT_PUBLIC_SUPABASE_URL=https://<your-project-id>.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=<your-anon-key>
SUPABASE_SERVICE_ROLE_KEY=<your-service-role-key>

RESEND_API_KEY=re_<your_resend_api_key>
CONTACT_NOTIFY_EMAIL=admin@example.com

NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

> **Catatan Keamanan**: Berkas `.env.local` tidak boleh dicommit ke Git. `SUPABASE_SERVICE_ROLE_KEY` hanya digunakan di sisi server.

### 3. Jalankan Server Pengembangan

```bash
npm run dev
```

Buka [http://localhost:3000](http://localhost:3000) di browser Anda.

---

## 📜 Skrip yang Tersedia

- `npm run dev` — Menjalankan server pengembangan lokal.
- `npm run build` — Membangun aplikasi untuk produksi.
- `npm run start` — Menjalankan aplikasi hasil produksi.
- `npm run lint` — Memeriksa kualitas kode dengan ESLint.
- `npm run typecheck` — Memeriksa tipe data dengan TypeScript compiler (`tsc --noEmit`).
- `npm run format` — Memformat kode dengan Prettier.
- `npm run format:check` — Memeriksa format kode tanpa mengubah berkas.

---

## 📖 Dokumentasi Terkait

- [docs/PRD.md](docs/PRD.md) — Dokumen spesifikasi kebutuhan produk.
- [DESIGN.md](DESIGN.md) — Panduan desain visual, palet warna, tipografi, dan token desain.
- [AGENTS.md](AGENTS.md) — Aturan arsitektur dan konvensi kode untuk agen AI.
