# Clean Architecture

## الهدف
تحديد أسلوب Clean Architecture المعتمد في EduCore لضمان فصل المسؤوليات، وسهولة الاختبار، وقابلية التوسع، وتقليل الترابط بين الوحدات.

## الطبقات

### 1. Presentation Layer
- Web Admin
- Parent Portal
- Student Portal
- Teacher Portal
- Flutter Mobile App
- REST Controllers

### 2. Application Layer
- Use Cases
- Commands
- Queries
- DTOs
- Validation
- Application Services

### 3. Domain Layer
- Entities
- Value Objects
- Aggregates
- Domain Services
- Domain Events
- Repository Interfaces
- Business Rules

### 4. Infrastructure Layer
- PostgreSQL
- Entity Framework Core
- File Storage
- Email Provider
- SMS Provider
- Push Notifications
- Background Jobs
- External Integrations

## قواعد الاعتماد
- تعتمد Presentation على Application فقط.
- تعتمد Application على Domain فقط.
- لا يعتمد Domain على أي طبقة أخرى.
- تعتمد Infrastructure على Domain لتنفيذ العقود (Interfaces).

## قواعد العمل
- CA-0101: يمنع وصول Presentation مباشرة إلى قاعدة البيانات.
- CA-0102: جميع منطق الأعمال يوجد داخل Domain وApplication.
- CA-0103: يمنع استخدام Infrastructure داخل Domain.
- CA-0104: جميع الوحدات يجب أن تكون قابلة للاختبار باستخدام Dependency Injection.