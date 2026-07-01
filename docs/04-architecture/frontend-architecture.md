# Frontend Architecture

## الهدف
يوثق هذا المستند البنية الأمامية (Frontend) لنظام EduCore لضمان قابلية التوسع، وسهولة الصيانة، وإعادة استخدام المكونات عبر بوابات النظام.

## التقنيات المقترحة
- Next.js (App Router)
- React
- TypeScript
- Tailwind CSS
- TanStack Query
- Zustand
- React Hook Form
- Zod

## الهيكل العام
- app/
- components/
- features/
- shared/
- services/
- hooks/
- lib/
- types/

## المبادئ
- Feature-Based Architecture.
- Server Components حيثما أمكن.
- فصل مكونات العرض عن منطق الأعمال.
- Design System موحد.
- دعم RTL وi18n.

## إدارة الحالة
- Server State باستخدام TanStack Query.
- Client State باستخدام Zustand.
- Forms باستخدام React Hook Form.

## قواعد العمل
- FE-0101: يمنع استدعاء API مباشرة من مكونات العرض عند وجود Service Layer.
- FE-0102: جميع النماذج تستخدم تحققًا موحدًا.
- FE-0103: جميع الشاشات تدعم Responsive Design.
- FE-0104: تلتزم جميع الواجهات بمعايير WCAG 2.2 AA قدر الإمكان.