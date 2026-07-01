# Authorization

## الهدف
تحديد آلية التفويض (Authorization) للتحكم في الوصول إلى موارد النظام باستخدام نموذج RBAC (Role-Based Access Control).

## المبادئ
- تعتمد جميع الصلاحيات على الأدوار.
- يمكن للمستخدم امتلاك أكثر من دور.
- يتم التحقق من الصلاحيات في كل طلب محمي.
- تدعم الصلاحيات التقييد حسب الفرع (Branch Scope).

## الأدوار الأساسية
- System Administrator
- Branch Manager
- Accountant
- Teacher
- Receptionist
- Parent
- Student

## قواعد العمل
- AUTHZ-0101: يمنع الوصول إلى أي مورد بدون صلاحية مناسبة.
- AUTHZ-0102: يتم تسجيل محاولات الوصول غير المصرح بها في Audit Log.
- AUTHZ-0103: يمكن تطبيق صلاحيات إضافية على مستوى الكيان عند الحاجة.
- AUTHZ-0104: يجب التحقق من الصلاحيات قبل تنفيذ منطق الأعمال.

## أمثلة
- Students.Read
- Students.Create
- Students.Update
- Students.Delete
- Reports.View
- Fees.Manage
- Attendance.Manage
