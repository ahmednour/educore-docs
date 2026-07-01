# Authentication

## الهدف
توحيد آلية المصادقة في EduCore لجميع تطبيقات الويب والجوال ولوحات الإدارة باستخدام JWT وRefresh Tokens.

## المبادئ
- استخدام HTTPS فقط.
- Access Token قصير العمر.
- Refresh Token طويل العمر وقابل للإبطال.
- دعم تسجيل الخروج من جميع الأجهزة.

## طرق تسجيل الدخول
- اسم المستخدم أو البريد الإلكتروني.
- رقم الجوال (اختياري).
- OTP للعمليات الحساسة.

## قواعد العمل
- AUTH-0101: جميع الطلبات المحمية تتطلب Access Token صالح.
- AUTH-0102: يتم إبطال Refresh Token عند تسجيل الخروج.
- AUTH-0103: يتم تسجيل جميع عمليات تسجيل الدخول في Audit Log.
- AUTH-0104: يدعم النظام المصادقة متعددة العوامل مستقبلاً.

## Endpoints
- POST /api/v1/auth/login
- POST /api/v1/auth/refresh
- POST /api/v1/auth/logout
- GET /api/v1/auth/profile
