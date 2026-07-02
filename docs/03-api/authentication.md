# Authentication

## الهدف
توحيد آلية المصادقة في EduCore لجميع تطبيقات الويب والجوال ولوحات الإدارة، طبقاً للقرار المعماري المعتمد في
ADR-001-authentication-strategy.md.

## العلاقة مع ADR-001
هذا المستند يوثق التفاصيل التشغيلية للمصادقة، بينما
ADR-001

هو مصدر الحقيقة للقرار الاستراتيجي. الأساس المعتمد هو
OAuth 2.1

و

OpenID Connect،

ويُستخدم
JWT

كصيغة داخلية لـ

Access Token

ضمن هذا الإطار، وليس كبديل عنه.

## المبادئ
- استخدام HTTPS فقط.
- Access Token قصير العمر، بصيغة JWT.
- Refresh Token طويل العمر وقابل للإبطال.
- دعم تسجيل الخروج من جميع الأجهزة.
- دعم Multi-Factor Authentication (MFA) طبقاً لـ ADR-001.

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
