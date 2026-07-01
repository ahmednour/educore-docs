# Architecture Overview

## الهدف
يوضح هذا المستند الرؤية المعمارية العامة لنظام EduCore والعلاقات بين مكوناته الرئيسية لضمان قابلية التوسع وسهولة الصيانة والاختبار.

## المبادئ المعمارية
- Clean Architecture.
- Domain-Driven Design (DDD).
- Modular Monolith مع إمكانية التحول إلى Microservices مستقبلاً.
- API First.
- Security by Design.
- Cloud Ready.

## الطبقات
1. Presentation Layer
2. Application Layer
3. Domain Layer
4. Infrastructure Layer

## المكونات الرئيسية
- Web Admin Portal
- Parent Portal
- Student Portal
- Teacher Portal
- Flutter Mobile App
- REST API
- Background Workers
- PostgreSQL Database
- Object Storage
- Notification Services

## تدفق الطلبات
Client -> API -> Application -> Domain -> Infrastructure -> Database

## قواعد العمل
- ARC-0101: يمنع وصول طبقة العرض مباشرة إلى قاعدة البيانات.
- ARC-0102: تعتمد جميع الوحدات على Domain Layer فقط.
- ARC-0103: جميع التكاملات الخارجية تمر عبر Infrastructure Layer.
- ARC-0104: يجب أن تكون الوحدات قابلة للاختبار بشكل مستقل.