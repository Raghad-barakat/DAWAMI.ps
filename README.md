# نظام تسجيل الدوام | Employee Attendance System

نظام دوام مرن للشركات مع:
- تسجيل الدوام عبر QR Code
- التحقق من الموقع الجغرافي (GPS)
- حساب الراتب حسب أيام الشهر
- أيام العيد (أول يوم ثابت 8 ساعات، الباقي ×1.5)
- طلبات الإجازة السنوية
- لوحة تحكم الأدمن

## 🚀 التشغيل

### 1. Supabase Setup
1. أنشئ مشروع جديد على [Supabase](https://supabase.com)
2. اذهب إلى SQL Editor ← New query
3. انسخ محتوى `supabase/migrations/001_schema.sql` والصقه وشغله
4. اذهب إلى Authentication ← Settings ← Signup/Login
5. شغل "Enable Email confirmations" (اختياري)
6. أنشئ حساب أدمن يدوياً من Authentication ← Users ← Add user

### 2. Local Setup
```bash
# Clone repo
git clone https://github.com/yourusername/attendance-system.git
cd attendance-system

# Install dependencies
npm install

# Create .env.local
cp .env.example .env.local
# عدل المفاتيح من Supabase Dashboard ← Settings ← API

# Run dev server
npm run dev
```

### 3. Deploy on Vercel
```bash
npm i -g vercel
vercel --prod
```

## 📁 Structure
```
src/
  app/
    page.tsx          # Login
    employee/page.tsx # Employee dashboard
    admin/page.tsx    # Admin dashboard
  lib/supabase.ts     # All DB functions
  types/index.ts      # TypeScript types
supabase/
  migrations/001_schema.sql
```

## 🔐 Auth
- **الأدمن**: Supabase Auth (Email + Password)
- **الموظف**: QR Code / Employee ID (بدون كلمة مرور)

## 📍 Location
- يتم التحقق من GPS عند تسجيل الدخول
- الأدمن يحدد موقع المكتب ونطاق المسموح به (متر)

## 💰 Salary Calculation
- 28 يوم → الراتب ÷ 192
- 30 يوم → الراتب ÷ 208
- 31 يوم → الراتب ÷ 216
- العيد: أول يوم = 8 ساعات ثابت، الباقي = ساعات العمل × 1.5
