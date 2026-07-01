# Junction Tables

## الهدف
توثيق جداول الربط (Many-to-Many) المستخدمة في EduCore لضمان تصميم مرن وقابل للتوسع.

## الجداول المقترحة

### TeacherSubjects
يربط المدرسين بالمواد التي يمكنهم تدريسها.

الأعمدة:
- Id
- TeacherId
- SubjectId
- CreatedAt

### TeacherGrades
يربط المدرسين بالصفوف الدراسية المسموح لهم بتدريسها.

الأعمدة:
- Id
- TeacherId
- GradeId

### StudentParents
يربط الطلاب بأولياء الأمور مع تحديد صلة القرابة.

الأعمدة:
- Id
- StudentId
- ParentId
- RelationshipType
- IsPrimary

### RolePermissions
يربط الأدوار بالصلاحيات.

الأعمدة:
- RoleId
- PermissionId

## قواعد العمل
- JT-0101: تمنع السجلات المكررة باستخدام Composite Unique Index.
- JT-0102: جميع المفاتيح الخارجية يجب أن تكون مفهرسة.
- JT-0103: تدعم جداول الربط الحذف المنطقي عند الحاجة.
- JT-0104: أي تعديل على جداول الربط يسجل في Audit Log.
