# Indexing Strategy

## الهدف
تحديد سياسة موحدة لإنشاء الفهارس في قاعدة بيانات EduCore لتحقيق أفضل أداء لعمليات البحث، والتقارير، والربط بين الجداول.

## المبادئ
- إنشاء فهارس للأعمدة المستخدمة بكثرة في البحث والربط.
- تجنب الفهارس غير الضرورية التي تؤثر على أداء الكتابة.
- مراجعة الفهارس دوريًا بناءً على إحصائيات الاستخدام.

## أنواع الفهارس
- Primary Key Index
- Unique Index
- Composite Index
- Covering Index (عند الحاجة)

## أمثلة
- Student(Id)
- Student(NationalId)
- Enrollment(StudentId, AcademicYearId)
- Attendance(ClassroomId, AttendanceDate)
- Payment(InvoiceId)

## قواعد العمل
- IDX-0101: جميع المفاتيح الخارجية يجب أن تمتلك فهرسًا.
- IDX-0102: الحقول الفريدة يجب أن تستخدم Unique Index.
- IDX-0103: تتم مراجعة الفهارس عند كل إصدار رئيسي للنظام.
