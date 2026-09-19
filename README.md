# منصة قرية الحرية — الإصدار النهائي 4.0.0

البنية المعتمدة:
- GitHub: المصدر الرئيسي للكود والإصدارات.
- Supabase: Authentication + PostgreSQL + RLS + Realtime + Storage.
- Netlify أو GitHub Pages: نشر واجهة التطبيق.

## الإعداد مرة واحدة
1. اربط مستودع GitHub الحالي بالمشروع.
2. في Supabase شغّل `supabase/migrations/20260919110000_initial_schema.sql` من SQL Editor إذا لم تكن migration منشورة بعد.
3. فعّل Email/Password من Authentication.
4. أنشئ أول مستخدم من Authentication > Users.
5. بعد إنشاء المستخدم، اجعل `profiles.is_admin = true` و`profiles.active = true` لذلك المستخدم.
6. اربط Netlify بالمستودع إذا أردت النشر التلقائي.

## بعد الإعداد
لا يحتاج المستخدم إلى تنزيل ZIP أو رفع ملفات إلى Supabase. التحديثات البرمجية تكون عبر GitHub، والبيانات عبر Supabase.

> لا تضع أي Secret Key داخل المستودع. مفتاح `sb_publishable_...` مخصص للواجهة مع RLS.
