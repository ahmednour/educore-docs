# Observability

## الهدف
يوثق هذا المستند استراتيجية المراقبة (Observability) في EduCore لضمان اكتشاف المشكلات مبكرًا، وتحليل الأداء، وتسريع التحقيق في الأعطال.

## المكونات
- Structured Logging.
- Metrics.
- Distributed Tracing.
- Health Checks.
- Dashboards.
- Alerting.

## المبادئ
- تضمين TraceId وCorrelationId في جميع الطلبات.
- تسجيل الأحداث المهمة فقط مع تجنب البيانات الحساسة.
- جمع مؤشرات الأداء الرئيسية للتطبيق وقاعدة البيانات.
- مراقبة الخدمات الخارجية ووقت الاستجابة.

## المقاييس الأساسية
- Request Rate
- Error Rate
- Response Time
- Database Query Duration
- Cache Hit Ratio
- Queue Length
- Background Job Failures

## قواعد العمل
- OBS-0101: يمنع تسجيل كلمات المرور أو الرموز السرية في السجلات.
- OBS-0102: جميع الخدمات توفر Health Check Endpoint.
- OBS-0103: يتم إرسال تنبيهات عند تجاوز الحدود الحرجة.
- OBS-0104: يجب الاحتفاظ بالسجلات وفق سياسة الاحتفاظ المعتمدة.