# ADR-003: API Design

## Status
Accepted

## Context
يحتاج EduCore إلى واجهات برمجية متسقة وسهلة الصيانة تدعم تطبيقات الويب والجوال والتكاملات الخارجية.

## Decision
- اعتماد RESTful APIs كأساس.
- استخدام OpenAPI 3.1 لتوثيق جميع الواجهات.
- تطبيق إصدار للواجهات (API Versioning) عبر المسار مثل `/api/v1`.
- توحيد بنية الطلبات والاستجابات وأكواد الأخطاء.
- دعم Pagination وFiltering وSorting في نقاط النهاية المناسبة.

## Alternatives Considered
- GraphQL كواجهة رئيسية.
- gRPC لجميع الخدمات.
- عدم استخدام إصدار للواجهات.

## Consequences
### الإيجابيات
- سهولة التكامل مع العملاء الخارجيين.
- توثيق قياسي وقابل للتوليد الآلي.
- توافق واسع مع الأدوات والمنصات.

### السلبيات
- قد يتطلب REST عدة طلبات لبعض السيناريوهات المعقدة.
- الحاجة إلى إدارة إصدارات الواجهات مع تطور النظام.

## References
- OpenAPI Specification 3.1
- REST Architectural Style
- RFC 9110 HTTP Semantics