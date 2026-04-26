🌸 FlowerDex
สารานุกรมดอกไม้ไทย — ค้นหา สำรวจ และเรียนรู้เกี่ยวกับดอกไม้พื้นถิ่นและดอกไม้นิยมในประเทศไทย

A Thai flower encyclopedia web app powered by Perenual Plant API and Supabase

✨ Features
ฟีเจอร์รายละเอียด🔍 ค้นหาอัจฉริยะรองรับภาษาไทย/อังกฤษ และแก้คำผิดอัตโนมัติ (Levenshtein fuzzy search)🌈 กรองตามสีและฤดูกาลเลือกดูดอกไม้ตามสีหรือช่วงเวลาออกดอก🤖 Autofill จาก Perenual APIกรอกชื่อดอกไม้แล้วดึงข้อมูลครบอัตโนมัติ🌱 ข้อมูลการดูแลการรดน้ำ แสงแดด ดิน อุณหภูมิ (cached)💖 รายการโปรดบันทึกดอกไม้ที่ชืบชอบ (localStorage)🔐 ระบบ Adminเพิ่ม แก้ไข ลบดอกไม้ผ่าน Supabase Auth + RLS

🚀 Quick Start

1. Clone & Install
   bashgit clone <your-repo>
   cd flower-dex
   npm install
2. Setup Supabase
   ดูคู่มือละเอียดใน SUPABASE_SETUP.md
   สรุปย่อ:

สร้าง project ที่ https://supabase.com
รัน SQL schema จากไฟล์ SUPABASE_SETUP.md
สร้าง storage bucket flower-images (public)
สร้าง admin user ใน Authentication → Users

3. Environment Variables
   bashcp .env.example .env.local
   แก้ไขค่าใน .env.local:
   envVITE_SUPABASE_URL=https://xxxxxxxxxxxx.supabase.co
   VITE_SUPABASE_PUBLISHABLE_KEY=eyJ...
   VITE_PERENUAL_API_KEY=sk-... # optional — ใช้สำหรับ Autofill
4. Run
   bashnpm run dev

# เปิด http://localhost:8080

🗂️ Project Structure
src/
├── App.tsx # Root: QueryClient + AuthProvider + Routes
├── context/
│ └── AuthContext.tsx # Supabase auth state (user, signIn, signOut)
├── components/
│ ├── FlowerCard.tsx # การ์ดดอกไม้
│ ├── FlowerModal.tsx # Modal รายละเอียด + care info
│ ├── Navbar.tsx # Nav (แสดง logout เมื่อ login แล้ว)
│ ├── NavLink.tsx # Router NavLink wrapper
│ ├── ProtectedRoute.tsx # Guard /admin → redirect /login
│ └── admin/
│ └── AutofillInput.tsx # Input + Perenual species search
├── data/
│ └── flowers.ts # Type definitions + CATEGORIES + COLOR_LIST
├── hooks/
│ ├── useFlowers.ts # Supabase fetch + Perenual enrichment
│ ├── useFavorites.ts # localStorage favorites
│ └── use-toast.ts
├── lib/
│ ├── perenual.ts # Perenual API integration + autofill logic
│ └── utils.ts # cn() helper
├── pages/
│ ├── Index.tsx # หน้าหลัก + search + filter
│ ├── Favorites.tsx # รายการโปรด
│ ├── Admin.tsx # จัดการดอกไม้ (Protected)
│ ├── Login.tsx # หน้า login admin
│ └── NotFound.tsx
└── utils/
└── search.ts # Fuzzy search + EN→TH translation

🔐 Admin Access

ไปที่ /login หรือคลิก "เข้าสู่ระบบ" ใน Navbar
Login ด้วย email/password ที่สร้างใน Supabase
หลัง login → เมนู "จัดการ" จะปรากฏใน Navbar
ในหน้า Admin สามารถ เพิ่ม / แก้ไข / ลบ ดอกไม้ได้
Logout ผ่านปุ่ม "ออกจากระบบ" ที่มุมขวาบน

🛠️ Scripts
CommandDescriptionnpm run devDevelopment server (port 8080)npm run buildProduction buildnpm run previewPreview production buildnpm run lintESLint checknpm testRun tests (Vitest)

🧰 Tech Stack

Frontend — React + TypeScript + Vite
Styling — Tailwind CSS + shadcn/ui
Database — Supabase (PostgreSQL + RLS)
Auth — Supabase Auth
Plant Data — Perenual Plant API
State — TanStack Query (React Query)
