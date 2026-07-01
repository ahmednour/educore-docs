# Pagination

## الهدف
توحيد آلية تقسيم النتائج (Pagination) في جميع واجهات برمجة تطبيقات EduCore لتحسين الأداء وتقليل حجم البيانات المنقولة.

## المبادئ
- جميع نقاط النهاية التي تعرض قوائم تدعم Pagination.
- استخدام Page Number وPage Size كآلية افتراضية.
- تحديد حد أقصى لحجم الصفحة لمنع الطلبات الكبيرة.

## Query Parameters
- page = رقم الصفحة (يبدأ من 1).
- pageSize = عدد العناصر في الصفحة.
- sort = ترتيب النتائج.

## نموذج الاستجابة
```json
{
  "success": true,
  "data": [],
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "totalItems": 250,
    "totalPages": 13,
    "hasNext": true,
    "hasPrevious": false
  },
  "traceId": "uuid"
}
```

## قواعد العمل
- PAG-0101: الحد الأقصى لـ pageSize هو 100.
- PAG-0102: القيم غير الصالحة تعيد HTTP 400.
- PAG-0103: يجب أن تكون جميع القوائم قابلة للترتيب والتصفية مع Pagination.
