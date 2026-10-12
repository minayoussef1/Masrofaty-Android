# مصروفاتي 💰

تطبيق ويب خفيف (ملف واحد) لتتبع المصروفات والدخل والسلف والديون والفواتير وأهداف الادخار.
يشتغل بدون إنترنت، وبياناته بتتخزن على جهاز المستخدم بس.

## هيكل المشروع
```
www/                 ← التطبيق نفسه (ده اللي بيتنشر)
  index.html         ← كل الكود (HTML + CSS + JS)
  sw.js              ← الشغل بدون إنترنت (Service Worker)
  manifest.webmanifest  ← بيخلي الموقع يتثبت كتطبيق
  icon-192.png / icon-512.png
.github/workflows/pages.yml  ← نشر تلقائي على GitHub Pages
capacitor.config.json        ← للمرحلة اللي بتحوّله فيها لتطبيق أندرويد أصلي (اختياري)
```

## 1) الرفع على GitHub
1. اعمل حساب على github.com، ثم **New repository** باسم `masrofaty` (Public).
2. من صفحة الريبو اختار **uploading an existing file** وارفع كل محتويات المجلد
   (مع الحفاظ على مجلد `www` ومجلد `.github`). أو من الطرفية:
   ```
   git init
   git add .
   git commit -m "first version"
   git branch -M main
   git remote add origin https://github.com/USERNAME/masrofaty.git
   git push -u origin main
   ```
3. **Settings → Pages → Source: GitHub Actions**.
4. بعد دقيقة هتلاقي الرابط: `https://USERNAME.github.io/masrofaty/`

## 2) التثبيت على الموبايل
افتح الرابط في **Chrome** ثم ⋮ ← **Install app / Add to Home screen**.
(على iPhone: Safari ← Share ← Add to Home Screen).

## 3) نسخة APK
- **الأسهل (يدعم نسخ Google Drive):** افتح **pwabuilder.com**، الصق رابط GitHub Pages،
  اضغط Start ثم **Package for stores → Android**، وحمّل الملف الجاهز.
  احتفظ بملف التوقيع (keystore) في مكان آمن، هتحتاجه لكل تحديث.
- **لو عايز إشعارات تذكير بتشتغل والتطبيق مقفول (أصلي):**
  ```
  npm i @capacitor/core @capacitor/cli @capacitor/android @capacitor/local-notifications
  npx cap add android
  npx cap sync
  npx cap open android      # يفتح Android Studio ← Build ← Build APK
  ```
  تنبيه: تسجيل دخول Google داخل WebView الأصلي ممكن يتحجب، فنسخ Drive الأفضل معاه نسخة PWABuilder.

## 4) تفعيل النسخ الاحتياطي على Google Drive
1. ادخل **console.cloud.google.com** ← New Project.
2. **APIs & Services → Library** ← فعّل **Google Drive API**.
3. **OAuth consent screen** ← External ← اكتب اسم التطبيق وإيميلك.
   أضف الـ scope: `.../auth/drive.appdata` (ده من النوع non-sensitive).
4. **Credentials → Create credentials → OAuth client ID → Web application**.
   في **Authorized JavaScript origins** حط: `https://USERNAME.github.io`
5. انسخ الـ **Client ID** والصقه من داخل التطبيق: الإعدادات ← النسخ الاحتياطي ← Google Drive،
   أو ضعه في الثابت `GCLIENT` داخل `www/index.html` فيشتغل لكل المستخدمين.
6. وأنت جاهز للنشر للناس: من OAuth consent screen غيّر الحالة إلى **In production**.

النسخة بتتحفظ في مجلد خاص بالتطبيق على درايف (مش ظاهر في ملفاتك)، والنسخ التلقائي
بيتم مرة كل 24 ساعة عند فتح التطبيق.

## 5) تحديث التطبيق
عدّل `www/index.html` ← commit و push ← بيتنشر لوحده.
**مهم:** غيّر رقم النسخة في `www/sw.js` (`masrofaty-v2` ← `v3`) عشان الناس يشوفوا التحديث.

## 6) ملاحظات
- البيانات على جهاز المستخدم فقط؛ خد نسخة احتياطية من وقت للتاني.
- القفل بالرقم السري حماية بسيطة وليس تشفيرًا قويًا.
