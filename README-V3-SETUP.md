# منصة قرية الحرية — Supabase + GitHub + Netlify v3

هذه النسخة تستخدم Supabase Auth + PostgreSQL + Realtime + Storage، مع GitHub كمصدر للكود وNetlify للنشر.

## 1) Supabase

المشروع: `novkheywufddqqoigxqe`

في Supabase → SQL Editor نفّذ الملف:
`supabase/migrations/20260919110000_initial_schema.sql`

إذا كانت القاعدة قد نُفذت سابقاً، لا تعِد تنفيذ migration على قاعدة تحتوي بيانات إنتاجية إلا بعد أخذ نسخة احتياطية ومراجعة التغييرات.

## 2) إنشاء المشرف

Supabase → Authentication → Users → Add user.

بعد إنشاء المستخدم سيُنشأ سجل `profiles` تلقائياً بواسطة trigger.
في Table Editor → profiles عدّل:
- `is_admin = true`
- `active = true`

## 3) GitHub

ارفع محتويات المشروع إلى المستودع:
`Freedom-Village-Platform`
والفرع الرئيسي `main`.

يمكن ربط Supabase بالمستودع من Project Settings → Integrations → GitHub Integration. توضع مجلدات `supabase/` في جذر المستودع.

## 4) Netlify

اربط Netlify بمستودع GitHub نفسه، واجعل النشر من `main`.
هذا المشروع static/PWA ولا يحتاج إلى خادم Node لتشغيل الواجهة.

## 5) GitHub Actions لـ Supabase

الملف `.github/workflows/supabase-deploy.yml` يدفع migrations عند تغيير `supabase/**`.
أضف Secrets التالية في GitHub:
- `SUPABASE_ACCESS_TOKEN`
- `SUPABASE_PROJECT_REF` = `novkheywufddqqoigxqe`
- `SUPABASE_DB_PASSWORD`

لا تضع Secret Key أو كلمة مرور قاعدة البيانات في ملفات المشروع.

## 6) اختبار نهائي

اختبر بالترتيب:
1. تسجيل دخول المشرف.
2. ظهور لوحة الإدارة للمشرف فقط.
3. إنشاء مستخدم عادي.
4. منع المستخدم العادي من وظائف الإدارة بواسطة RLS.
5. إنشاء خبر/خدمة/فعالية.
6. إرسال طلب من مستخدم عادي.
7. رؤية المستخدم لطلباته فقط.
8. رؤية المشرف لجميع الطلبات.
9. تغيير حالة الطلب.
10. رفع صورة مواقيت الصلاة.
11. رفع شعار المنصة.
12. فتح التطبيق من جهاز Android ثانٍ والتأكد من المزامنة.
13. تسجيل الخروج وإعادة الدخول.
14. اختبار التحديث بعد نشر نسخة جديدة.
