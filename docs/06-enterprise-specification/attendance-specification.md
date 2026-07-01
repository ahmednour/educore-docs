# Attendance Specification

## Overview
تمثل وحدة الحضور والانصراف المسؤول الرئيسي عن تسجيل حضور وغياب الطلاب، وإدارة حالات التأخير والانصراف المبكر، وإصدار التقارير المتعلقة بالالتزام.

## Business Rules
- لا يمكن تسجيل حضور بدون تسجيل فعال للطالب.
- يمنع تسجيل أكثر من حالة حضور لنفس الطالب في نفس الحصة أو اليوم حسب السياسة.
- يجب توثيق سبب الغياب أو التأخير عند الحاجة.
- يحتفظ النظام بسجل تاريخي لجميع التعديلات.

## Functional Requirements
- تسجيل الحضور.
- تسجيل الغياب.
- تسجيل التأخير والانصراف المبكر.
- تعديل السجلات حسب الصلاحيات.
- البحث والتقارير.

## Non-Functional Requirements
- دعم التسجيل السريع للفصول الكبيرة.
- تسجيل العمليات الحساسة في Audit Log.

## Data Model
- Attendance
- Student
- Class
- Session
- AttendanceStatus

## API Contracts
- GET /attendance
- GET /attendance/{id}
- POST /attendance
- PUT /attendance/{id}
- DELETE /attendance/{id}

## UI Requirements
- شاشة تسجيل الحضور.
- سجل الحضور.
- تقارير الحضور.

## Acceptance Criteria
- حفظ السجل بنجاح.
- منع التكرار.
- تطبيق الصلاحيات وقواعد الأعمال.

## Mermaid Diagram
```mermaid
flowchart LR
A[Take Attendance] --> B[Validate]
B --> C[Save Record]
C --> D[Audit Log]
```