# Exam Specification

## Overview
توثق هذه الوحدة إدارة الاختبارات والنتائج داخل EduCore، وتشمل إنشاء الاختبارات، جدولة المواعيد، إدخال الدرجات، واعتماد النتائج.

## Business Rules
- يرتبط كل اختبار بمادة وسنة دراسية.
- لا تقبل درجة أعلى من الحد الأقصى.
- تعتمد النتائج قبل نشرها.

## Functional Requirements
- إنشاء اختبار.
- إدارة الجدول.
- إدخال الدرجات.
- اعتماد النتائج.
- إصدار التقارير.

## Data Model
- Exam
- Grade
- Subject
- Student

## API Contracts
- GET /exams
- POST /exams
- PUT /exams/{id}
- DELETE /exams/{id}

## Acceptance Criteria
- إنشاء اختبار بنجاح.
- التحقق من الدرجات.
- احترام الصلاحيات.