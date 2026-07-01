# Error Handling

## الهدف
توحيد آلية معالجة الأخطاء في واجهات برمجة تطبيقات EduCore لضمان تجربة متسقة للمطورين وسهولة تتبع المشكلات.

## المبادئ
- استخدام أكواد HTTP القياسية.
- إرجاع بنية خطأ موحدة.
- تضمين TraceId في جميع الأخطاء.
- عدم كشف تفاصيل داخلية أو Stack Trace.

## أكواد الأخطاء
- VALIDATION_ERROR
- AUTHENTICATION_FAILED
- AUTHORIZATION_DENIED
- RESOURCE_NOT_FOUND
- CONFLICT
- RATE_LIMIT_EXCEEDED
- INTERNAL_SERVER_ERROR

## قواعد العمل
- ERR-0101: جميع الأخطاء تُسجل في نظام المراقبة.
- ERR-0102: رسائل الأخطاء قابلة للترجمة.
- ERR-0103: الأخطاء غير المتوقعة تُرجع HTTP 500.
- ERR-0104: أخطاء التحقق تُرجع HTTP 400 مع تفاصيل الحقول المتأثرة.
