---
layout: fandogh
id: images
title: تصاویر در فندق
sidebar_label: تصاویر در فندق
---
سرویس ها در فندق از روی ایمیج ها ساخته می شوند و از طرفی سرویس ها همواره در حال بهبود و تغییر هستند. برای آنکه بتوانیم تاریخچه تغییرات در هر بار 
را در اختیار داشته باشیم  image ها دارای یک شماره نسخه منحصر به فرد می باشند که کاربر در هر بار publish کردن٬ آن را مشخص می کند.
به طور کلی در فندق هر Image معادل یک پروژه است. هر image  دارای یک نام و تعداد دلخواه ورژن می باشد.

>مفهوم Image و ImageVersion تقریبا شبیه به مفهوم Image و Tag در داکر است، که بعدا می‌توانید از روی هر ورژن یک Image به تعداد مورد نیاز سرویس ایجاد کنید.

## ساخت ایمیج‌ها
به طور مثال فرض کنید شما پروژه ای به نام HelloApplication را در پوشه ای در رایانه شخصی خود دارید و حالا قصد دارید که این پروژه را بر روی فندق بارگذاری و اجرا نمایید. ابتدا از طریق CLI به آدرس پوشه مورد نظر میروید.
<br>
![Image Init](/img/docs/image-init.png "Image Init")
<br>
وقتی مطمئن شدید در آدرس مورد نظر هستید٬ از طریق دستور init پروژه خود را برای بارگذاری بر روی سرور فندق آماده میکنید.
```
fandogh image init --name HelloApplication
```
* **name--** یا **n-**
پارامتر name یا n نمایانگر نام پروژه ای می باشد که میخواهید بارگذاری کنید.
<br>

> توجه داشته باشید که شما برای هر پروژه تنها یک بار نیاز دارید که از دستور **init** استفاده کنید و برای بارگذاری تنها نیاز است که هر بار یک شماره  نسخه جدید را **publish** کنید.

هنگامی که شما در CLI دستور init را فراخوانی می‌کنید، سمت سرور فندق یک پروژه جدید با نامی که مشخص کرده‌اید `( در این مثال نام پروژه ما HelloApplication می باشد)` می‌سازد. این پروژه در ابتدا حاوی هیچ ورژنی نبوده و فقط یک نام است که در ادامه از طریق ورژن‌هایی که برای آن می‌سازید می‌توانید سرویس خود را اجرا کنید. 
<br>
![Image Publish](/img/docs/image-publish.png "Image Publish")
<br>
حال برای آنکه محتویات پوشه ای که داخل آن هستیم برای سرورهای فندق ارسال شود از دستور `image publish` استفاده می کنیم.
```
fandogh image publish --version 1.0
```
* **version--** یا **v-**
پارامتر version یا v نمایانگر ورژن پروژه ای می باشد که میخواهید بارگذاری کنید.
<br>

> توجه داشته باشید برای آنکه پروژه شما به درستی publish٬ شود٬ حتما باید در قسمت root directory پروژه خود Dockerfile مربوط به آن پروژه را داشته باشید٬ در غیر این صورت در ادامه با مشکل مواجه خواهید شد.

زمانی که دستور publish را اجرا می‌کنید، CLI محتویات پوشه جاری را با فرمت zip فشرده می‌کند و به عنوان یک ورژن بخصوص که خودتان همانند دستور بالا آن را تعیین کرده اید٬ بر روی سرور فندق بارگذاری می‌کند. فایل فشرده سمت سرور فندق گشوده می‌شود و با استفاده از Dockerfile همراه فایل‌ها یک ایمیج داکر تولید شده و با ورژن مشخص شده تگ می‌خورد و در کتابخانه فندق ذخیره می‌شود. \
هنگام ساخته شدن Docker image از روی محتویات فایل فشرده، لاگ هایی مربوط به ساخت ایمیج تولید می‌شود. این لاگ ها بلافاصله بعد از publish موفق روی ترمینال شما قابل مشاهده خواهد بود، مگر آنکه از طریق d- یا detach به CLI گفته باشید که نیازی به مشاهده لاگ ندارید.
برای آنکه به CLI فندق بگویید که لاگ های ساخت ایمیج را به شما نمایش ندهد می توانید مانند نمونه زیر از پارامتر detach استفاده کنید.
```
fandogh image publish --version 1.0 -d
```
* **detach** یا **d-**
این پارامتر به CLI میگوید که همه کارها را در background انجام دهد تا کاربر بتواند از CLI استفاده کرده و منتظر پایان کار سرور نماند.
<br>

>هر زمان که نیاز داشته باشید می‌توانید از طریق `fandogh image logs` لاگ‌های مربوط به ساخت یک ورژن بخصوص را مشاهده کنید.
```
fandogh image logs --image IMAGE_NAME --version IMAGE_VERSION
```
* **image--** یا **i-**
پارامتر image یا i نمایانگر نام imageای می باشد که میخواهید لاگ های آن را مشاهده کنید.

* **version--** یا **v-**
پارامتر version یا v نمایانگر ورژن imageای می باشد که میخواهید لاگ های آن را مشاهده کنید.


## مدیریت تصاویر
![ CLI Image](/img/docs/cli_image.png "CLI Image")

دستورات مربوط به بخش image فقط محدود به init یا publish و logs نمی باشد. کلیه دستورات مربوط به بخش image در ادامه توضیح داده شده اند.
>شما همچنین می توانید با وارد کردن دستور`fandogh image --help`  در CLI لیست دستورات موجود را مشاهده کنید.

### init
با وارد کردن دستور `fandogh image init --name IMAGE_NAME` شما سمت سرور پروژه ای با نام IMAGE_NAME بر روی فندق میسازید تا بتوانید محتوای پروژه خود را با دستور publish بر روی آن منتقل کنید.

* **name--** یا **n-**
پارامتر name یا n نمایانگر نام پروژه ای می باشد که میخواهید بارگذاری کنید.

### publish
با وارد کردن دستور `fandogh image publish --version IMAGE_VERSION` می توانید پروژه خود را به سرور فندق ارسال کنید.
* **version--** یا **v-**
پارامتر version یا v نمایانگر ورژن پروژه ای می باشد که میخواهید بارگذاری کنید.
* **detach** یا **d-**
این پارامتر به CLI میگوید که همه کارها را در background انجام دهد تا کاربر بتواند از CLI استفاده کرده و منتظر پایان کار سرور نماند.

### logs
با استفاده از دستور `fandogh image logs --image IMAGE_NAME --version IMAGE_VERSION` می توانید لاگ های ساخت image مربوط به هر ورژن از یک image مشخص را مشاهده کنید.

* **image--** یا **i-**
پارامتر image یا i نمایانگر نام imageای می باشد که میخواهید لاگ های آن را مشاهده کنید.

* **version--** یا **v-** :
پارامتر version یا v نمایانگر ورژن imageای می باشد که میخواهید لاگ های آن را مشاهده کنید.

### list
با استفاده از دستور `fandogh image list` می توانید لیست تمام imageهایی که تا به حال ساخته اید را مشاهده کنید.

### delete
با استفاده از دستور `fandogh image delete --image IMAGE_NAME` ٬ image با نام IMAGE_NAME را از پاک کنید.

>  توجه داشته باشید که حذف image منجر به حذف تمام ورژن‌ها و لاگ‌های build آن image خواهد شد.

### versions
با وارد کردن دستور `fandogh image versions --image IMAGE_NAME` لیست ورژن های مربوط به هر image را مشاهده کنید.
* **image--** یا **i-** :
این پارامتر نمایانگر نام imageای می باشد که میخواهید لیست ورژن های آن را مشاهده کنید.
