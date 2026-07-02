# Entity Relationship Model (ERM)

## الهدف
يوضح هذا المستند الكيانات الأساسية في EduCore والعلاقات بينها كنموذج منطقي مستقل عن نوع قاعدة البيانات.

## الكيانات الأساسية
- Branch
- AcademicYear
- Stage
- Grade
- Program
- Classroom
- Subject
- Teacher
- Student
- Parent
- Enrollment
- TeacherAssignment
- Attendance
- Timetable
- Exam
- ExamResult
- Fee
- Invoice
- Payment
- Role
- Permission
- AuditLog
- Notification

## العلاقات الرئيسية
- Branch يمتلك Academic Years.
- Academic Year يحتوي على Classrooms وEnrollments.
- Student يمتلك Enrollments متعددة عبر الأعوام.
- Enrollment يربط Student مع Classroom.
- TeacherAssignment يربط Teacher مع Subject وClassroom.
- Attendance يرتبط بـ Enrollment وTimetable.
- Payments ترتبط بـ Invoice الخاصة بالطالب.

## Schema الفعلي
تفاصيل الأعمدة، الأنواع، المفاتيح الأساسية والخارجية، والفهارس موثقة بالكامل في
schema.md.

هذا الملف يبقى كنموذج منطقي مختصر للعلاقات، بينما
schema.md

هو المرجع القابل للتنفيذ مباشرة.

## ER Diagram
```mermaid
erDiagram
    BRANCH ||--o{ ACADEMIC_YEAR : has
    ACADEMIC_YEAR ||--o{ ENROLLMENT : contains
    STUDENT ||--o{ ENROLLMENT : has
    ENROLLMENT }o--|| CLASSROOM : "belongs to"
    STUDENT }o--o{ PARENT : "linked via student_parents"
    TEACHER ||--o{ TEACHER_ASSIGNMENT : has
    TEACHER_ASSIGNMENT }o--|| SUBJECT : covers
    TEACHER_ASSIGNMENT }o--|| CLASSROOM : "teaches in"
    ENROLLMENT ||--o{ ATTENDANCE : generates
    ENROLLMENT ||--o{ EXAM_RESULT : has
    EXAM ||--o{ EXAM_RESULT : produces
    ENROLLMENT ||--o{ FEE : owes
    FEE ||--o{ INVOICE : "billed via"
    INVOICE ||--o{ PAYMENT : "settled via"
```