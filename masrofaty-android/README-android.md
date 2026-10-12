# مصروفاتي - تشغيل على الأندرويد

الروابط (تيليجرام، يوتيوب، واتساب، الإيميل) بتفتح جوه تطبيقاتها على الموبايل من خلال Capacitor.

## الخطوات (مرة واحدة)

1. ثبّت Node.js.
2. من المجلد ده شغّل:

   npm install @capacitor/core @capacitor/cli @capacitor/android @capacitor/app-launcher @capacitor/filesystem @capacitor/share

3. أضف أندرويد وانسخ الملفات:

   npx cap add android
   npx cap sync android

4. افتح المشروع في Android Studio:

   npx cap open android

5. من القائمة: Build > Build APK(s).

## ملاحظات

- حفظ الملفات (تصدير Excel والنسخة الاحتياطية) بيفتح قائمة المشاركة في الموبايل، واختار منها "Save to Files" أو Drive أو أي تطبيق تاني. ده مش محتاج أي صلاحية للذاكرة.
- الإنترنت مطلوب بس لفتح تيليجرام/واتساب/يوتيوب ولنسخ Google Drive الاحتياطي. باقي التطبيق بيشتغل من غير نت.

- لو الرابط اتفتح في المتصفح بدل التطبيق، اتأكد إن تطبيق تيليجرام/يوتيوب/واتساب متثبت على الموبايل.
- بعد أي تعديل على `www/index.html` شغّل `npx cap sync android` قبل ما تبني الـ APK.
