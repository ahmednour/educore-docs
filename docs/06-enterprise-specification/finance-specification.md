# Finance Specification

## Overview
تمثل وحدة الشؤون المالية المسؤول الرئيسي عن إدارة الرسوم الدراسية، والمدفوعات، والاستردادات، والخصومات، والتقارير المالية داخل EduCore.

## Business Rules
- لكل عملية مالية معرف فريد.
- يمنع تسجيل دفعة سالبة.
- يتم تحديث الرصيد تلقائياً بعد كل عملية.
- يحتفظ النظام بسجل تدقيق لجميع العمليات المالية.

## Functional Requirements
- إنشاء الرسوم.
- تسجيل المدفوعات.
- إدارة الخصومات والاستردادات.
- إصدار الإيصالات.
- التقارير المالية.

## Non-Functional Requirements
- ضمان سلامة المعاملات المالية.
- تسجيل جميع العمليات الحساسة في Audit Log.

## Data Model
- Invoice
- Payment
- Discount
- Refund
- StudentAccount

## API Contracts
- GET /finance/invoices
- POST /finance/payments
- GET /finance/payments/{id}
- PUT /finance/payments/{id}

## Acceptance Criteria
- تسجيل دفعة صحيحة.
- تحديث الرصيد تلقائياً.
- احترام الصلاحيات وقواعد الأعمال.