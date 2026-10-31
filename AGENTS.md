# Aturan Proyek: Website Portofolio + CMS

Sumber kebenaran: docs/PRD.md. Jika ada konflik, PRD menang. Jika PRD ambigu, tanyakan dulu.

## Stack
Next.js (App Router), TypeScript strict, Tailwind CSS, Supabase (PostgreSQL, Auth, Storage), deploy Vercel.

## Aturan Kode
- TypeScript strict, dilarang `any` tanpa alasan tertulis.
- Gunakan Server Components secara default; Client Components hanya bila perlu interaksi.
- Validasi input dengan Zod di klien DAN server (skema dibagi).
- Akses data lewat helper di `src/lib/supabase/` (client, server, middleware). Jangan buat klien Supabase ad hoc.
- SUPABASE_SERVICE_ROLE_KEY hanya di server, tidak pernah diawali NEXT_PUBLIC_.
- Keamanan ditegakkan di database (RLS), bukan hanya UI.
- Sanitasi semua HTML rich text sebelum simpan dan render.
- Semua teks UI lewat kamus i18n (ID/EN), tidak ada string hardcoded di komponen.
- Semua gambar via next/image dengan alt text.
- Semua rute /admin/* wajib noindex dan dilindungi middleware.
- Migrasi SQL disimpan berversi di supabase/migrations/.

