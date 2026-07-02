# ADR-004: Frontend Architecture

## Status
Accepted

## Context
يحتاج EduCore إلى واجهة أمامية قابلة للتوسع وسهلة الصيانة تدعم الأداء العالي، وإعادة الاستخدام، وتجربة مستخدم متسقة عبر الويب والأجهزة المختلفة.

## Decision
- اعتماد React مع Next.js (App Router) لتطبيق الويب.
- استخدام TypeScript لضمان سلامة الأنواع.
- الاعتماد على Server Components عند الإمكان وتحسين الأداء عبر SSR وStreaming.
- استخدام Design System موحد ومكونات قابلة لإعادة الاستخدام.
- إدارة الحالة باستخدام حلول مناسبة حسب النطاق (مثل React Query للبيانات وZustand للحالة المحلية عند الحاجة).

## Alternatives Considered
- Angular.
- Vue.js.
- React بدون إطار عمل.

## Consequences
### الإيجابيات
- أداء وتجربة مستخدم محسّنة.
- قابلية توسع وصيانة عالية.
- توافق جيد مع SSR وSEO.

### السلبيات
- منحنى تعلم أعلى لبعض مفاهيم Next.js.
- الحاجة إلى إدارة دقيقة للفصل بين Server وClient Components.

## References
- Next.js Documentation
- React Documentation
- TypeScript Handbook