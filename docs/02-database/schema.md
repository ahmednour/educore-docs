# Schema — التصميم الفعلي لقاعدة البيانات

## الهدف
هذا الملف يحل محل الفراغ المذكور سابقاً في
entity-relationship-model.md

ويوثق
Schema

فعلي قابل للتنفيذ مباشرة على
PostgreSQL

طبقاً للقرار
ADR-002-database-strategy.md.

## قواعد عامة على كل الجداول
كل جدول تشغيلي في هذا المستند يحتوي إلزامياً على الأعمدة التالية
(غير مكررة أدناه اختصاراً):

| العمود | النوع | ملاحظات |
|---|---|---|
| id | UUID | PRIMARY KEY، افتراضي gen_random_uuid() |
| branch_id | UUID | FK → branches.id، إلزامي طبقاً لـ MB-0101 |
| created_at | TIMESTAMPTZ | NOT NULL DEFAULT now() |
| updated_at | TIMESTAMPTZ | NOT NULL DEFAULT now() |
| created_by | UUID | FK → users.id |
| updated_by | UUID | FK → users.id، NULLABLE |
| is_deleted | BOOLEAN | NOT NULL DEFAULT false — Soft Delete طبقاً لـ PP-004 |
| deleted_at | TIMESTAMPTZ | NULLABLE |

> جداول التهيئة العامة فقط
(branches، roles، permissions)

مستثناة من

branch_id.

---

## users
جدول أساسي مستقل عن الفروع
(لا يحتوي branch_id مباشرة، لأن المستخدم قد يصل لأكثر من فرع عبر user_roles).

| العمود | النوع | ملاحظات |
|---|---|---|
| id | UUID | PRIMARY KEY |
| username | VARCHAR(100) | UNIQUE NOT NULL |
| email | VARCHAR(150) | UNIQUE NULLABLE |
| phone | VARCHAR(20) | UNIQUE NULLABLE |
| password_hash | TEXT | NOT NULL |
| status | VARCHAR(20) | Active / Suspended / Locked |
| last_login_at | TIMESTAMPTZ | NULLABLE |
| mfa_enabled | BOOLEAN | DEFAULT false — طبقاً لـ ADR-001 |
| created_at | TIMESTAMPTZ | NOT NULL DEFAULT now() |
| updated_at | TIMESTAMPTZ | NOT NULL DEFAULT now() |

> هذا الجدول هو المرجع الفعلي لكل الإشارات إلى users.id المذكورة في باقي الجداول
(created_by، updated_by، teachers.user_id، parents.user_id، audit_logs.user_id).

## branches
| العمود | النوع | ملاحظات |
|---|---|---|
| name_ar | VARCHAR(200) | NOT NULL |
| name_en | VARCHAR(200) | NOT NULL |
| code | VARCHAR(20) | UNIQUE NOT NULL |
| status | VARCHAR(20) | Active / Inactive |

## academic_years
| العمود | النوع | ملاحظات |
|---|---|---|
| name | VARCHAR(50) | مثال: 2026-2027 |
| start_date | DATE | NOT NULL |
| end_date | DATE | NOT NULL |
| status | VARCHAR(20) | Draft / Active / Archived |

**Index:** UNIQUE (branch_id, name)

## programs
| العمود | النوع | ملاحظات |
|---|---|---|
| name_ar | VARCHAR(150) | NOT NULL |
| name_en | VARCHAR(150) | NOT NULL |
| code | VARCHAR(20) | UNIQUE |

## stages
| العمود | النوع | ملاحظات |
|---|---|---|
| program_id | UUID | FK → programs.id |
| name_ar | VARCHAR(100) | NOT NULL |
| sort_order | SMALLINT | لترتيب العرض |

## grades
| العمود | النوع | ملاحظات |
|---|---|---|
| stage_id | UUID | FK → stages.id |
| name_ar | VARCHAR(100) | NOT NULL |
| sort_order | SMALLINT | |

## classrooms
| العمود | النوع | ملاحظات |
|---|---|---|
| grade_id | UUID | FK → grades.id |
| academic_year_id | UUID | FK → academic_years.id |
| name | VARCHAR(50) | مثال: 3A |
| capacity | SMALLINT | NOT NULL، يُستخدم في BR-1003 |

**Index:** UNIQUE (grade_id, academic_year_id, name)

## subjects
| العمود | النوع | ملاحظات |
|---|---|---|
| name_ar | VARCHAR(150) | NOT NULL |
| code | VARCHAR(20) | UNIQUE |

## teachers
| العمود | النوع | ملاحظات |
|---|---|---|
| user_id | UUID | FK → users.id، UNIQUE |
| employee_no | VARCHAR(30) | UNIQUE NOT NULL |
| full_name_ar | VARCHAR(200) | NOT NULL |
| full_name_en | VARCHAR(200) | |
| status | VARCHAR(20) | Active / Suspended / Terminated — طبقاً لـ BR-0704 لا يوجد حذف فعلي |

## teacher_assignments
| العمود | النوع | ملاحظات |
|---|---|---|
| teacher_id | UUID | FK → teachers.id |
| subject_id | UUID | FK → subjects.id |
| classroom_id | UUID | FK → classrooms.id |
| academic_year_id | UUID | FK → academic_years.id |

**Index:** UNIQUE (teacher_id, subject_id, classroom_id, academic_year_id)

## students
| العمود | النوع | ملاحظات |
|---|---|---|
| reference_no | VARCHAR(30) | UNIQUE NOT NULL — BR-0801 |
| full_name_ar | VARCHAR(200) | NOT NULL |
| full_name_en | VARCHAR(200) | |
| birth_date | DATE | NOT NULL |
| gender | VARCHAR(10) | |
| nationality | VARCHAR(100) | |
| national_id | VARCHAR(30) | UNIQUE NULLABLE |
| photo_url | TEXT | |
| status | VARCHAR(20) | Active / Suspended / Withdrawn / Graduated |

## parents
| العمود | النوع | ملاحظات |
|---|---|---|
| user_id | UUID | FK → users.id، NULLABLE |
| full_name_ar | VARCHAR(200) | NOT NULL |
| phone | VARCHAR(20) | UNIQUE NOT NULL |
| email | VARCHAR(150) | NULLABLE |
| status | VARCHAR(20) | Active / Inactive — BR-0903، لا يوجد حذف فعلي |

## student_parents (Junction Table)
| العمود | النوع | ملاحظات |
|---|---|---|
| student_id | UUID | FK → students.id |
| parent_id | UUID | FK → parents.id |
| relationship | VARCHAR(30) | Father / Mother / LegalGuardian |
| is_primary | BOOLEAN | DEFAULT false |

**Index:** UNIQUE (student_id, parent_id)

## enrollments
| العمود | النوع | ملاحظات |
|---|---|---|
| student_id | UUID | FK → students.id |
| academic_year_id | UUID | FK → academic_years.id |
| program_id | UUID | FK → programs.id |
| stage_id | UUID | FK → stages.id |
| grade_id | UUID | FK → grades.id |
| classroom_id | UUID | FK → classrooms.id |
| enrollment_date | DATE | NOT NULL |
| status | VARCHAR(20) | Draft / Active / Suspended / Withdrawn / Completed |

**Index:** UNIQUE (student_id, academic_year_id) WHERE status IN ('Active','Draft') — يفرض BR-1001 على مستوى قاعدة البيانات وليس منطق التطبيق فقط

## attendance
| العمود | النوع | ملاحظات |
|---|---|---|
| enrollment_id | UUID | FK → enrollments.id |
| timetable_id | UUID | FK → timetables.id |
| date | DATE | NOT NULL |
| status | VARCHAR(15) | Present / Absent / Late / Excused |

**Index:** UNIQUE (enrollment_id, timetable_id, date)

## timetables
| العمود | النوع | ملاحظات |
|---|---|---|
| classroom_id | UUID | FK → classrooms.id |
| subject_id | UUID | FK → subjects.id |
| teacher_id | UUID | FK → teachers.id |
| day_of_week | SMALLINT | 1-7 |
| start_time | TIME | NOT NULL |
| end_time | TIME | NOT NULL |

## exams
| العمود | النوع | ملاحظات |
|---|---|---|
| subject_id | UUID | FK → subjects.id |
| academic_year_id | UUID | FK → academic_years.id |
| name | VARCHAR(150) | NOT NULL |
| max_score | NUMERIC(6,2) | NOT NULL |
| status | VARCHAR(20) | Draft / Published / ResultsApproved — يحكم BR-1404 |

## exam_results
| العمود | النوع | ملاحظات |
|---|---|---|
| exam_id | UUID | FK → exams.id |
| enrollment_id | UUID | FK → enrollments.id |
| score | NUMERIC(6,2) | NOT NULL |

**Index:** UNIQUE (exam_id, enrollment_id)

## fees
| العمود | النوع | ملاحظات |
|---|---|---|
| enrollment_id | UUID | FK → enrollments.id — BR-1501 |
| fee_type | VARCHAR(50) | Tuition / Transport / Books ... |
| amount | NUMERIC(12,2) | NOT NULL |
| due_date | DATE | NOT NULL |

## invoices
| العمود | النوع | ملاحظات |
|---|---|---|
| enrollment_id | UUID | FK → enrollments.id |
| total_amount | NUMERIC(12,2) | NOT NULL |
| status | VARCHAR(20) | Draft / Issued / PartiallyPaid / Paid / Cancelled |

## payments
| العمود | النوع | ملاحظات |
|---|---|---|
| invoice_id | UUID | FK → invoices.id |
| amount | NUMERIC(12,2) | NOT NULL، مجموعها لا يتجاوز invoices.total_amount — BR-1503 |
| method | VARCHAR(30) | Cash / Card / BankTransfer |
| paid_at | TIMESTAMPTZ | NOT NULL |
| reversed | BOOLEAN | DEFAULT false — يُستخدم بدل الحذف طبقاً لـ BR-1505 |

## discounts
يمثل الإعفاء أو المنحة المذكورة في
01-business/fees-and-payments.md

ولم تكن موثقة سابقاً كجدول فعلي.

| العمود | النوع | ملاحظات |
|---|---|---|
| student_id | UUID | FK → students.id |
| academic_year_id | UUID | FK → academic_years.id |
| type | VARCHAR(30) | Discount / Scholarship |
| value_type | VARCHAR(10) | Percentage / Fixed |
| value | NUMERIC(12,2) | NOT NULL |
| reason | VARCHAR(200) | |
| approved_by | UUID | FK → users.id |

## roles / permissions / role_permissions / user_roles
تصميم RBAC قياسي:
- roles (id, name, branch_scoped BOOLEAN)
- permissions (id, code UNIQUE — مثال: Students.Read)
- role_permissions (role_id, permission_id)
- user_roles (user_id, role_id, branch_id NULLABLE)

## audit_logs
| العمود | النوع | ملاحظات |
|---|---|---|
| user_id | UUID | FK → users.id |
| entity_name | VARCHAR(100) | NOT NULL |
| entity_id | UUID | NOT NULL |
| action | VARCHAR(20) | Create / Update / Delete / Approve |
| old_value | JSONB | NULLABLE |
| new_value | JSONB | NULLABLE |
| occurred_at | TIMESTAMPTZ | NOT NULL DEFAULT now() |

**Index:** (entity_name, entity_id), (occurred_at) — طبقاً لـ indexing-strategy.md

---

## ملاحظة على الفجوة السابقة
كانت الوثيقة السابقة
(entity-relationship-model.md)

تنص على تأجيل بناء

Schema

الفعلي. هذا الملف يغلق هذه الفجوة بالكامل، ويجب اعتباره

Source of Truth

الرسمي لبنية قاعدة البيانات بدلاً من الوصف النظري فقط.
