# ADR-010: Backend Framework — NestJS بدل ASP.NET Core

## Status
Accepted (يلغي الاختيار الأصلي لـ ASP.NET Core Web API المذكور سابقًا في 04-architecture/backend-architecture.md)

## Context
كان الاختيار الأولي لطبقة الـ
Backend

هو
ASP.NET Core Web API

مع

Entity Framework Core،

طبقاً لما كان موثق في

04-architecture/backend-architecture.md.

بعد مراجعة الفريق، تقرر التحول لـ
NestJS

كإطار العمل الأساسي للـ
Backend، للحفاظ على توحيد اللغة (TypeScript) بين الـ Frontend المبني على Next.js والـ Backend، وتقليل التنقل بين لغتين مختلفتين (C# و TypeScript) داخل نفس الفريق.

## Decision
- استبدال
ASP.NET Core Web API

بـ

NestJS (Node.js / TypeScript).

- استبدال
Entity Framework Core

بـ

Prisma ORM

(أو

TypeORM

كبديل ثانٍ)

للتعامل مع
schema.md

الموثق مسبقاً، مع بقاء

PostgreSQL

كما هو من غير أي تغيير.

- استبدال
MediatR

بوحدة
CQRS

المدمجة داخل

NestJS

لتطبيق نفس نمط

Commands & Queries

المعتمد سابقاً.

- استبدال
FluentValidation

بـ

class-validator

مع

DTOs،

أو

Zod

عند الحاجة لتوحيد التحقق مع الـ

Frontend.

- استبدال
Background Workers

المعتمدة على

.NET

بـ

BullMQ

(مبني على

Redis).

- مبادئ Clean Architecture و CQRS و Repository Pattern المعتمدة أصلاً في 04-architecture/clean-architecture.md تبقى كما هي بدون تغيير، فقط الأدوات التقنية اللي بتنفذها هي اللي اتغيرت.

- **استضافة قاعدة البيانات:** يُستخدم Supabase كاستضافة مُدارة لقاعدة PostgreSQL (وله ميزة اختيارية بتفعيل Auth الجاهز عنده لتسريع مرحلة MVP إذا لزم). الاتصال من NestJS يتم عبر Connection String قياسي (عبر Prisma) وليس عبر Supabase SDK من طرف الفرونت، حتى تبقى قاعدة البيانات قابلة للنقل لأي استضافة PostgreSQL أخرى مستقبلاً من غير أي تعديل في كود التطبيق. يجب تفعيل Connection Pooling من اليوم الأول عبر Supavisor (المدمج في Supabase) لتفادي اختناق الاتصالات مع زيادة عدد الفروع والمستخدمين المتزامنين، بما يتوافق مع استراتيجية التوسع الموثقة في ADR-008-scalability-strategy.md. منطق الأعمال والـ CQRS والـ Repository Pattern كله يبقى داخل NestJS حصراً، ولا يُعتمد على Row Level Security كبديل لطبقة التطبيق نظراً لتعقيد قواعد العمل الموثقة (مثال: BR-1003، BR-1505، BR-1506).

## Alternatives Considered
- الاستمرار بـ
ASP.NET Core — تم الرفض بناءً على قرار الفريق بعدم العمل بـ ASP.NET.
- Express.js
مباشرة بدون إطار عمل منظم — تم الرفض لأن
NestJS

بيوفر هيكلية جاهزة أقرب لمبادئ

Clean Architecture

المعتمدة، وده بيقلل وقت إعادة بناء الهيكل من الصفر.

- Python (Django/FastAPI) — تم الرفض حفاظًا على توحيد اللغة مع الـ Frontend.

## Consequences
### الإيجابيات
- توحيد اللغة
(TypeScript)

بين الـ

Frontend

والـ

Backend،

وده بيسهّل مشاركة الـ

Types

والـ

Validation Schemas

بين الطبقتين.

- منحنى تعلم أقل لو نفس المطور شغال على الفرونت والباك.
- توفر بيئة
Node.js

الغنية بالمكتبات المفتوحة المصدر.

### السلبيات
- فقدان
Strong Typing

القوي جداً اللي بيوفره

C#

على مستوى الـ

Compiler، رغم إن TypeScript بيقلل الفارق ده جزئيًا.

- إعادة تصميم طبقة
Infrastructure

اللي كانت مبنية على افتراض

Entity Framework Core

تحديداً.

## ملفات تم تحديثها بناءً على هذا القرار
- 04-architecture/backend-architecture.md
- 04-architecture/clean-architecture.md
- 04-architecture/deployment-architecture.md

## References
- NestJS Documentation
- Prisma Documentation
- 09-architecture-decisions/ADR-002-database-strategy.md
