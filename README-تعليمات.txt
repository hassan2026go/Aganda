مفكرتي اليومية - تقدمة ياسر الحسين
=====================================
أولًا: النشر (مجانًا)
1) فك ضغط الملف. 2) افتح app.netlify.com/drop 3) اسحب المجلد كاملًا.
4) أرسل الرابط للعمال. يثبّتونه بزر «📲 تثبيت التطبيق» (آيفون: مشاركة ثم إضافة إلى الشاشة الرئيسية).
بعد أول فتح بالإنترنت يعمل بدون إنترنت.

ثانيًا: تفعيل الحفظ السحابي بالبريد الإلكتروني (اختياري، مجاني)
1) افتح console.firebase.google.com وأنشئ مشروعًا جديدًا.
2) Build > Authentication > Get started > فعّل «Email/Password».
3) Build > Firestore Database > Create database (production mode).
4) من تبويب Rules ضع القواعد التالية ثم Publish:
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
5) Project settings > Your apps > أضف تطبيق ويب (</>) وانسخ firebaseConfig.
6) افتح ملف firebase-config.js والصق القيم مكان null ثم احفظ.
7) أعد رفع المجلد على Netlify.
8) Authentication > Settings > Authorized domains: أضف نطاق موقعك على Netlify إن لم يكن موجودًا.
بعدها يفتح العامل «حسابي» ويدخل بريده وكلمة مرور (حساب جديد)، فتُحفظ بياناته تلقائيًا في السحابة،
ويستعيدها على أي جهاز بنفس البريد.

ملاحظات:
- كل عامل يرى بياناته فقط (القواعد أعلاه تمنع الاطلاع على بيانات غيره).
- عند الاسترجاع تُدمج بيانات السحابة مع بيانات الجهاز دون تكرار.
- عند تعديل أي ملف لاحقًا غيّر رقم النسخة في sw.js (v4 إلى v5).
- يظل النسخ الاحتياطي بالملف أو واتساب متاحًا دائمًا.
