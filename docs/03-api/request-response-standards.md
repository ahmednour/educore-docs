# Request & Response Standards

## الهدف
توحيد شكل الطلبات والاستجابات في جميع واجهات برمجة تطبيقات EduCore لضمان الاتساق وسهولة التكامل.

## المبادئ
- جميع الطلبات والاستجابات تستخدم JSON.
- استخدام UTF-8.
- جميع التواريخ بصيغة ISO 8601.
- جميع المعرفات من نوع UUID.

## نموذج النجاح
```json
{
  "success": true,
  "data": {},
  "message": "Operation completed successfully",
  "traceId": "uuid"
}
```

## نموذج الخطأ
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed"
  },
  "traceId": "uuid"
}
```

## قواعد العمل
- API-0101: يجب أن تتضمن جميع الاستجابات TraceId.
- API-0102: يجب استخدام أكواد HTTP القياسية.
- API-0103: لا يتم إرجاع Stack Trace أو تفاصيل داخلية.
- API-0104: تكون رسائل الخطأ قابلة للترجمة.