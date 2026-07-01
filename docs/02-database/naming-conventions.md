# Database Naming Conventions

## الهدف
توحيد أسلوب تسمية الجداول والأعمدة والمفاتيح والفهارس داخل قاعدة بيانات EduCore لضمان الوضوح وسهولة الصيانة.

## الجداول
- أسماء الجداول بصيغة المفرد (Student, Teacher, Enrollment).
- استخدام PascalCase للأسماء المنطقية.

## الأعمدة
- Primary Key: Id (UUID).
- Foreign Keys: <Entity>NameId مثل StudentId وTeacherId.
- CreatedAt, UpdatedAt, DeletedAt.
- CreatedBy, UpdatedBy.

## الفهارس
- IX_<Table>_<Column>
- UQ_<Table>_<Column>
- FK_<Child>_<Parent>

## القيود
- PK_<Table>
- CK_<Table>_<Rule>

## قواعد عامة
- استخدام UUID لجميع المفاتيح الأساسية.
- دعم Soft Delete في جميع الجداول.
- عدم استخدام الأسماء المختصرة غير الواضحة.
- الحفاظ على اتساق التسمية في جميع الوحدات.