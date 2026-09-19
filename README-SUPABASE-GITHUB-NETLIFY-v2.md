# منصة قرية الحرية — Supabase + GitHub + Netlify v2

## 1) Supabase
1. افتح مشروع Supabase.
2. من SQL Editor شغّل `schema.sql` مرة واحدة.
3. من Authentication > Users أنشئ أول حساب مشرف.
4. بعد إنشاء الحساب افتح Table Editor > profiles، وحدد المستخدم واجعل `is_admin = true` و`active = true`.
5. تأكد من Storage أن bucket `public-assets` موجود.

> المفتاح الموجود في `supabase-config.js` هو Publishable Key فقط. لا تضع Secret/Service Role Key في الواجهة أو GitHub.

## 2) GitHub
ارفع جميع الملفات إلى مستودع `Freedom-Village-Platform` مع الحفاظ على مجلد `supabase/`.

يمكن ربط Supabase مباشرة مع GitHub من Project Settings > Integrations > GitHub Integration. التكامل يستطيع متابعة الفروع وتشغيل migrations عند النشر للإنتاج.

## 3) Netlify
اربط مستودع GitHub نفسه في Netlify.
- Build command: اتركه فارغًا.
- Publish directory: `.`

## 4) GitHub Actions (اختياري لكنه موصى به)
إذا أردت أن يدفع GitHub migrations إلى Supabase تلقائيًا، أضف Secrets التالية للمستودع:
- `SUPABASE_ACCESS_TOKEN`
- `SUPABASE_PROJECT_REF` = `novkheywufddqqoigxqe`
- `SUPABASE_DB_PASSWORD`

لا تضع كلمة مرور قاعدة البيانات أو Secret Key داخل الملفات.

## 5) المستخدمون
الحسابات تُنشأ من Supabase Authentication. عند إنشاء مستخدم جديد ينشأ له profile تلقائيًا بواسطة trigger. تعيين المشرف يتم من جدول `profiles`.

## 6) الاختبار النهائي
- تسجيل الدخول والخروج.
- مستخدم عادي لا يرى الإدارة.
- المشرف يرى الإدارة.
- نشر خبر وحذفه.
- إضافة خدمة/فعالية/طوارئ/دليل وحذفها.
- تحديث مواقيت الصلاة ورفع صورة.
- إرسال طلب من مستخدم وتتبع حالته.
- تغيير حالة الطلب من المشرف.
- رفع شعار المنصة.
- فتح الموقع من جهازين والتأكد من ظهور التغييرات.
