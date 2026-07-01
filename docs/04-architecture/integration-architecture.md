# Integration Architecture

## الهدف
يوثق هذا المستند آلية تكامل EduCore مع الأنظمة والخدمات الخارجية بطريقة آمنة وقابلة للتوسع.

## مبادئ التكامل
- API First.
- Loose Coupling.
- Retry مع Exponential Backoff.
- Idempotency للعمليات الحرجة.
- Timeouts وCircuit Breaker عند الحاجة.

## التكاملات المتوقعة
- بوابات الدفع.
- مزود البريد الإلكتروني.
- مزود الرسائل النصية (SMS).
- Push Notifications.
- Identity Provider (OIDC/OAuth2).
- أنظمة ERP أو LMS مستقبلًا.

## الأنماط
- REST APIs.
- Webhooks.
- Background Jobs للعمليات غير المتزامنة.
- Domain Events للتكامل الداخلي.

## قواعد العمل
- INT-0101: جميع مفاتيح API تخزن في Secret Manager.
- INT-0102: تسجل جميع طلبات التكامل الحساسة في Audit Log.
- INT-0103: يمنع استدعاء الخدمات الخارجية مباشرة من Domain Layer.
- INT-0104: يجب معالجة حالات الفشل وإعادة المحاولة بشكل آمن.
