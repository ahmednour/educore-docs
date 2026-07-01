# Mobile Architecture

## الهدف
يوثق هذا المستند البنية المعمارية لتطبيق EduCore للأجهزة المحمولة، مع التركيز على القابلية للتوسع، والأداء، والعمل دون اتصال جزئيًا.

## التقنيات المقترحة
- Flutter
- Dart
- Riverpod
- Dio
- Go Router
- Hive
- flutter_secure_storage

## طبقات التطبيق
- Presentation Layer
- Application Layer
- Domain Layer
- Data Layer

## إدارة الحالة
- Riverpod لإدارة الحالة والاعتماديات.
- AsyncValue للتعامل مع البيانات غير المتزامنة.

## التخزين المحلي
- Hive للبيانات المؤقتة.
- Secure Storage للرموز (Tokens) والبيانات الحساسة.

## الاتصال بالشبكة
- Dio مع Interceptors.
- Retry Policy.
- Token Refresh.
- Offline Queue للعمليات القابلة للتأجيل.

## قواعد العمل
- MOB-0101: يمنع تخزين البيانات الحساسة في التخزين غير المشفر.
- MOB-0102: جميع الطلبات تمر عبر طبقة Services موحدة.
- MOB-0103: يدعم التطبيق RTL والوضعين الفاتح والداكن.
- MOB-0104: يجب أن يعمل التطبيق بكفاءة على أنظمة Android وiOS.