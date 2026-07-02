# Enrollment Specification

## Overview
تمثل وحدة التسجيل (Enrollment) المسؤول الرئيسي عن تسجيل الطلاب في السنوات الدراسية والفصول والبرامج، مع ضمان تطبيق جميع قواعد القبول والتسجيل.

## Business Rules
- لا يمكن إنشاء تسجيل بدون طالب وسنة دراسية.
- يمنع وجود تسجيلين نشطين للطالب في نفس السنة الدراسية.
- يجب التحقق من الطاقة الاستيعابية للفصل قبل التسجيل.
- يحتفظ النظام بسجل تاريخي لجميع عمليات التسجيل والنقل.

## Functional Requirements
- إنشاء تسجيل جديد.
- نقل الطالب بين الفصول.
- إنهاء التسجيل أو الانسحاب.
- البحث والتصفية.
- عرض سجل التسجيل.

## Non-Functional Requirements
- تنفيذ العمليات داخل معاملات (Transactions).
- تسجيل جميع العمليات الحساسة في Audit Log.

## Data Model
- Enrollment
- Student
- AcademicYear
- Classroom

## API Contracts
- GET /enrollments
- GET /enrollments/{id}
- POST /enrollments
- PUT /enrollments/{id}
- DELETE /enrollments/{id} — لا يحذف السجل، يحوّل الحالة إلى Withdrawn طبقاً لـ BR-1004

## UI Requirements
- قائمة التسجيلات.
- صفحة تفاصيل التسجيل.
- نموذج إنشاء وتعديل.

## Acceptance Criteria
- إنشاء تسجيل صالح.
- منع التسجيل المكرر.
- احترام الصلاحيات وقواعد الأعمال.

## Mermaid Diagram
```mermaid
flowchart LR
A[Create Enrollment] --> B[Validate Rules]
B --> C[Check Capacity]
C --> D[Save]
D --> E[Audit Log]
```