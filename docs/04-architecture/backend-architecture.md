# Backend Architecture

## الهدف
يوثق هذا المستند البنية الخلفية (Backend) لنظام EduCore، مع تحديد المكونات، ومسؤولياتها، وآلية التواصل بينها بما يتوافق مع مبادئ Clean Architecture وDDD.

## التقنيات المقترحة
- ASP.NET Core Web API
- Entity Framework Core
- PostgreSQL
- MediatR (CQRS)
- FluentValidation
- JWT Authentication

## المكونات الرئيسية
- API Controllers
- Application Services
- Commands & Queries
- Domain Models
- Repository Interfaces
- Infrastructure Implementations
- Background Workers

## تدفق الطلب
Client → Controller → Validation → Command/Query → Domain → Repository → Database

## قواعد العمل
- BE-0101: جميع الطلبات تمر عبر طبقة Application.
- BE-0102: يمنع تضمين منطق الأعمال داخل Controllers.
- BE-0103: يتم تنفيذ التحقق باستخدام FluentValidation.
- BE-0104: تعتمد جميع عمليات الوصول للبيانات على Repository Interfaces.
- BE-0105: تستخدم المعاملات (Transactions) للعمليات الحرجة فقط.

## اعتبارات الأداء
- استخدام Async/Await في جميع عمليات الإدخال والإخراج.
- تقليل عدد الاستعلامات باستخدام Projection.
- دعم Caching للبيانات المرجعية.
- مراقبة الأداء باستخدام Logging وMetrics.