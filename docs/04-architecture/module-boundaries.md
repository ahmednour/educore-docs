# Module Boundaries

## الهدف
تحديد حدود الوحدات (Modules) داخل EduCore لضمان فصل المسؤوليات وتقليل الترابط ودعم التطوير المتوازي.

## الوحدات الأساسية
- Identity
- Academic
- Students
- Teachers
- Parents
- Enrollment
- Attendance
- Timetable
- Exams
- Finance
- Reports
- Notifications
- Administration

## قواعد التصميم
- لكل وحدة مسؤولية واضحة.
- لا يسمح بالوصول المباشر إلى بيانات وحدة أخرى.
- يتم التكامل بين الوحدات عبر Application Services أو Domain Events.
- تمتلك كل وحدة نماذجها وقواعد أعمالها الخاصة.

## الاعتماد بين الوحدات
- تعتمد Finance على Enrollment.
- تعتمد Attendance على Enrollment وTimetable.
- تعتمد Reports على جميع الوحدات للقراءة فقط.
- تعتمد Notifications على Domain Events.

## قواعد العمل
- MOD-0101: يمنع إنشاء مراجع دائرية بين الوحدات.
- MOD-0102: كل وحدة قابلة للاختبار بشكل مستقل.
- MOD-0103: يمنع مشاركة منطق الأعمال بين الوحدات إلا من خلال واجهات واضحة.
- MOD-0104: يجب توثيق أي اعتماد جديد بين الوحدات.