# Administration Specification

## Overview
تمثل وحدة الإدارة المسؤول الرئيسي عن إدارة المستخدمين والأدوار والصلاحيات وإعدادات المؤسسة وسجل التدقيق داخل EduCore.

## Business Rules
- لكل مستخدم معرف فريد.
- تعتمد الصلاحيات على الأدوار مع إمكانية إضافة صلاحيات مباشرة عند الحاجة.
- يجب تسجيل جميع العمليات الإدارية في Audit Log.
- يمنع حذف المستخدمين المرتبطين بسجلات تاريخية، ويستخدم التعطيل بدلاً من الحذف.

## Functional Requirements
- إدارة المستخدمين.
- إدارة الأدوار والصلاحيات.
- إدارة الوحدات والصلاحيات الدقيقة.
- مراجعة سجل التدقيق.
- إدارة إعدادات المؤسسة.

## Non-Functional Requirements
- دعم المصادقة متعددة العوامل عند توفرها.
- تسجيل جميع العمليات الحساسة.

## Data Model
- User
- Role
- Permission
- UserRole
- AuditLog

## API Contracts
- GET /admin/users
- POST /admin/users
- PUT /admin/users/{id}
- GET /admin/roles
- POST /admin/roles

## Acceptance Criteria
- إنشاء مستخدم جديد بنجاح.
- تطبيق الصلاحيات بصورة صحيحة.
- تسجيل جميع العمليات الإدارية في Audit Log.