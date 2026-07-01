# Filtering & Sorting

## الهدف
توحيد آليات التصفية والترتيب في جميع واجهات برمجة تطبيقات EduCore لضمان الاتساق وتحسين تجربة الاستخدام والأداء.

## المبادئ
- جميع Endpoints التي تعرض قوائم تدعم التصفية والترتيب.
- يمكن الجمع بين Pagination وFiltering وSorting في نفس الطلب.
- التحقق من الحقول المسموح بها لمنع الاستعلامات غير الصالحة.

## Query Parameters
- filter=<field>:<value>
- sort=<field>
- order=asc|desc
- search=<text>

## أمثلة
- GET /api/v1/students?search=Ahmed
- GET /api/v1/students?filter=grade:5
- GET /api/v1/students?sort=lastName&order=asc
- GET /api/v1/students?page=1&pageSize=20&filter=branch:1&sort=createdAt&order=desc

## قواعد العمل
- FIL-0101: يسمح فقط بالتصفية على الحقول المعرفة مسبقًا.
- FIL-0102: يمنع الترتيب باستخدام حقول غير مفهرسة عند الإمكان.
- FIL-0103: تكون عمليات البحث غير حساسة لحالة الأحرف حيثما كان ذلك مناسبًا.
- FIL-0104: جميع معلمات التصفية غير الصالحة تعيد HTTP 400 مع رسالة واضحة.