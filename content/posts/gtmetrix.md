---
author: Yahya
category:
  - web
  - آموزش
  - برنامه-نویسی
  - برنامه‌نویسی
date: "2016-12-24T14:51:08+00:00"
guid: http://ysarbabi.ir/blog/?p=228
summary: چند روز پیش که کمی حوصله‌ام سر رفته بود و 1-2 ساعت وقت داشتم، تصمیم گرفتم صفحه اول (home، index یا هرچی..) سایت خودم [theyahya.com](http://theyahya.com/) را دوباره بنویسیم. و در انتهای این فرآیند که معمولا کارهای مرتب‌سازی کد و بهینه‌سازی‌ها را انجام می‌دهم. مسلما یکی از ابزارهایی که استفاده می‌کنم سایت [gtmetrix](https://gtmetrix.com/) است. از آنجایی که همیشه تا حد معقولی از بهینه‌سازی را طبق gtmetrix انجام می‌دهم، که خب روش منطقی هم همین است. ولی اینبار تصمیم گرفتم که به انتهای حد بهینه‌سازی نائل شوم و مصمم شدم که بالاترین رتبه را کسب کنم!‌ که خب نتیجه‌ای رضایت‌بخشی حاصل شد و تصمیم گرفتم که در مورد این فرآیند اینجا هم بنویسم و تقریبا تمام مراحل را در [گیت‌هاب](https://github.com/theyahya/aggressive-performance-gtmetrix) هم کامیت کردم و از مرحله هم یک [release دادم](https://github.com/theyahya/aggressive-performance-gtmetrix/releases) که مرور کد کاملا راحت‌تر شود.
tag:
  - web
  - آموزش
  - برنامه-نویسی
title: بهینه‌سازی شدید با gtmetrix
url: /aggressive-performance-gtmetrix/

---
چند روز پیش که کمی حوصله‌ام سر رفته بود و 1-2 ساعت وقت داشتم، تصمیم گرفتم صفحه اول (home، index یا هرچی..) سایت خودم [theyahya.com](http://theyahya.com/) را دوباره بنویسیم. و در انتهای این فرآیند که معمولا کارهای مرتب‌سازی کد و بهینه‌سازی‌ها را انجام می‌دهم. مسلما یکی از ابزارهایی که استفاده می‌کنم سایت [gtmetrix](https://gtmetrix.com/) است. از آنجایی که همیشه تا حد معقولی از بهینه‌سازی را طبق gtmetrix انجام می‌دهم، که خب روش منطقی هم همین است. ولی اینبار تصمیم گرفتم که به انتهای حد بهینه‌سازی نائل شوم و مصمم شدم که بالاترین رتبه را کسب کنم!‌ که خب نتیجه‌ای رضایت‌بخشی حاصل شد و تصمیم گرفتم که در مورد این فرآیند اینجا هم بنویسم و تقریبا تمام مراحل را در [گیت‌هاب](https://github.com/theyahya/aggressive-performance-gtmetrix) هم کامیت کردم و از مرحله هم یک [release دادم](https://github.com/theyahya/aggressive-performance-gtmetrix/releases) که مرور کد کاملا راحت‌تر شود.

ساختار معقول یک صفحه‌ی ساده معمولا چنین چیزی هست:

```default
├── avatar.jpg
├── bg.png
├── index.html
├── style.less
└── style.min.css

```

و نتیجه‌ی حاصل شده از این ساختار در تست gtmetrix هم چیزی‌ست شبیه تصویر پایین:

[![](/wp-content/uploads/2016/12/gtmetrix_v1_0_0.png)](/blog/wp-content/uploads/2016/12/gtmetrix_v1_0_0.png)

و اگر نگاهی به waterfall بیاندازیم، و بخواهیم سریع برویم سراغ مشکلات اصلی! همانطور که در تصویر زیر پیداست، ۳ فایل مشخص شده مربوط به فونت‌هایی‌ست که از [fonts.google.com](https://fonts.google.com/) گرفته می‌شوند.

[![](/wp-content/uploads/2016/12/waterfall_v1_0_0.png)](/blog/wp-content/uploads/2016/12/waterfall_v1_0_0.png)

که نتیجه‌ی کد:

```default
@import url('https://fonts.googleapis.com/css?family=Cormorant+Garamond:300,400');
```

است که ابتدای فایل [styleام](https://github.com/theyahya/aggressive-performance-gtmetrix/blob/247baba638061b27b3d886b101753a6e16046e91/style.less) نوشته‌ام تا بتوانم از فونت Cormorant Garamond استفاده کنم. خط بالا در واقع [یک css است](https://fonts.googleapis.com/css?family=Cormorant+Garamond:300,400) که فایل‌های font را لود می‌کند. حالا ما می‌توانیم بجای ایمپورت کردم این css، خود آن را (محتویات آن را ) کپی کرده و به ابتدای styleمان اضافه کنیم. ولی ما پا را از این هم فراتر می‌گذاریم و نسخه‌ی latin با وزن 300 را دانلود می‌کنیم.  که نتیجه فایلی با نام _iEjm9hVxcattz37Y8gZwVbq2HNNMYxbOC04F0CNdzo8.woff2_ است. حالا با دستور زیر در ابونتو آن را به کد base64 تبدیل می‌کنیم:

```default
base64 iEjm9hVxcattz37Y8gZwVbq2HNNMYxbOC04F0CNdzo8.woff2
```

نکته: سایت‌هایی نیز برای اینکار وجود دارد، که اگر از ویندوز استفاده می‌کنیم می‌توانید فایل‌تان را در آنها آپلود کنید و کد base۶۴ را دریافت کنید.

حالا به ابتدای فایل style کد زیر را بجای ایمپورت قبلی می‌گذاریم و مسلما کد base64 فونت را هم قرار می‌دهیم که من بخاطر طولانی بودنش اینجا نگذاشته‌ام.

```default
@font-face {
  font-family: 'Cormorant Garamond';
  font-style: normal;
  font-weight: 300;
  src: local('Cormorant Garamond Light'), local('CormorantGaramond-Light'), url(data:application/x-font-woff;charset=utf-8;base64,محل کد base64) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2212, U+2215, U+E0FF, U+EFFD, U+F000;
}
```

و [این جا](https://github.com/theyahya/aggressive-performance-gtmetrix/commit/5c03818d9b076afc1cf34a579b6d9793c469412a) می‌تونید دقیقا ببینید که چه اتفاقی افتاده و در تصویر زیر هم بهبود وضعیت gtmetrix به وضوح پیداست :)

[![](/wp-content/uploads/2016/12/gtmetrix_v2_0_0.png)](/blog/wp-content/uploads/2016/12/gtmetrix_v2_0_0.png)

حالا باید چنین کاری را با فایل‌های bg.png و avatar.jpg که برای faveicon استفاده می‌شه انجام بدیم و علاوه برآن؛ کل فایل style.min.css را هم کپی کنیم و داخل تکل style توی head فایل index.html قرار بدیم. و در نتیجه تنها فایل [index.html](https://github.com/theyahya/aggressive-performance-gtmetrix/blob/d848544542651b19435020953cd5c8cb3c81dbd9/index.html) برایمان باقی می‌ماند و در نتیجه تعداد requestهایمان هم به 1 کاهش پیدا می‌کند و حالا فقط با minify کردن فایل index.html می‌توانیم به [نسخه‌ی نهایی برسیم](https://github.com/theyahya/aggressive-performance-gtmetrix) و نتیجه‌ی کارمان چیزی شبیه تصویر زیر خواهد بود:

[![](/wp-content/uploads/2016/12/gtmetrix_v5_0_0.png)](/blog/wp-content/uploads/2016/12/gtmetrix_v5_0_0.png)

حالا اگر از سرور‌های آپاچی یا مشابه آن استفاده کینم، می‌توانیم با کمی خلاقیت در htaccess همین تک فایل index.html را هم سمت کاربر cache کنیم و نتیجه‌ای که کاربر دریافت می‌کند را بسیار سریع‌تر کنیم.
