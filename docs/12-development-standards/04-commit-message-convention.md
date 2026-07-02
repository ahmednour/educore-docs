# Commit Message Convention

## الهدف
تحديد صيغة موحدة لرسائل الـ Commit في EduCore لتحسين قابلية التتبع والقراءة وإدارة الإصدارات.

## الصيغة
```
<type>(<scope>): <ملخص مختصر>
```

## الأنواع الشائعة
- feat
- fix
- docs
- refactor
- test
- chore
- ci
- perf
- build

## الإرشادات
- استخدام صيغة الأمر المباشر (Imperative Mood).
- إبقاء الملخص مختصرًا.
- الإشارة إلى رقم المهمة (Issue) عند الحاجة.
- وصف التغييرات الجذرية (Breaking Changes) في نص الـ Commit عند الحاجة.

## أمثلة
- feat(auth): add password reset flow
- fix(api): handle expired access tokens
- docs(readme): update setup instructions

## معايير النجاح
- التزام جميع الـ Commits بالاصطلاح المتفق عليه.
- بقاء سجل الـ Commits واضحًا وقابلًا للبحث.
