# Backend Architecture

## الهدف
يوثق هذا المستند البنية الخلفية (Backend) لنظام EduCore، مع تحديد المكونات، ومسؤولياتها، وآلية التواصل بينها بما يتوافق مع مبادئ Clean Architecture وDDD.

## التقنيات المقترحة
- NestJS (Node.js / TypeScript)
- Prisma ORM أو TypeORM
- PostgreSQL
- CQRS Module (المدمج في NestJS، بديل MediatR)
- class-validator / Zod
- Passport.js (JWT Strategy + OAuth 2.1)

## المكونات الرئيسية
- Controllers (NestJS)
- Application Services / Use Cases
- Commands & Queries (CQRS)
- Domain Models / Entities
- Repository Interfaces
- Infrastructure Implementations (Prisma/TypeORM)
- Background Workers (BullMQ)

## تدفق الطلب
Client → Controller → Validation Pipe → Command/Query Handler → Domain → Repository → Database

## قواعد العمل
- BE-0101: جميع الطلبات تمر عبر طبقة Application.
- BE-0102: يمنع تضمين منطق الأعمال داخل Controllers.
- BE-0103: يتم تنفيذ التحقق باستخدام class-validator أو Zod DTOs.
- BE-0104: تعتمد جميع عمليات الوصول للبيانات على Repository Interfaces.
- BE-0105: تستخدم المعاملات (Transactions) للعمليات الحرجة فقط.

## اعتبارات الأداء
- استخدام async/await في جميع عمليات الإدخال والإخراج.
- تقليل عدد الاستعلامات باستخدام Select/Include محددة بدقة.
- دعم Caching للبيانات المرجعية عبر Redis.
- مراقبة الأداء باستخدام Logging وMetrics.