---
layout: fandogh
id: redis-managed-service
title: Redis
sidebar_label: Redis
---


### ![Redis](/img/docs/redis-managed-service.png "Redis")

شاید تا به حال نام پایگاه داده قدرتمند Redis را شنیده باشید.
طبق توضیحات سایت [Redis.io](https://redis.io) ٬ Redis یک پایگاه داده متن‌باز است که با قابلیت ذخیره داده‌ها به صورت in-memory باعث بالا رفتن سرعت ذخیره و بازیابی داده‌ها می‌شود.
برای اینکه بتوانید این سرویس را دیپلوی کنید٬ پارامتر‌های زیر را می‌توانید مشخص کنید:
|کانفیگ|نوع|پیش‌فرض|توضیح|
|---	|---	|---	|---	|
|service_name| string| redis| نامی که برای سرویس مایلید در نظر گرفته شود|
|redis_password| string| None| رمز عبور دیتابیس|
|volume_name| string| None| نام volumeای که به سرویس وصل می شود|

> توجه داشته باشید که سرویس ‌Redis به صورت پیش فرض داده‌های خود را در Memory نگهداری می‌کند و این حالت پایدار نیست٬ زیرا چنانچه service شما تحت هر شرایطی از بین برود و یا restart شود٬ داده‌های شما پاک می‌شود٬ لذا حتما از یک [dedicated volumes](https://docs.fandogh.cloud/docs/dedicated-volume.html)  استفاده نمایید٬تا backup دیتاهای خود را به صورت مستمر ثبت و حفظ کنید.

به عنوان مثال برای دیپلوی کردن یک Redis می‌توانیم به این شکل یک سرویس بسازیم:
```
  fandogh managed-service deploy redis 5.0.3 \
       -c service_name=test-redis \
       -c redis_password=pass123
```
این دستور یک سرویس Redis ایجاد می‌کند که:
* نام سرویس آن test-redis ( یعنی در شبکه داخلی فضانام شما باقی سرویس‌ها از طریق نام test-redis و بر روی پورت 6379 می‌توانند به آن متصل شوند) .
* رمز عبور آن pass123 است.

> **هشدار**

برای استفاده از سرویس Redis باید به ۲ نکته زیر توجه داشته باشید:
*  در صورتی که **رمز عبور** یا **redis_password** را وارد نکنید٬ برای اجرای دستورها دیگر  نیازی به رمز عبور نخواهید داشت ولی با این کار **سرویس را در معرض خطرهای بیرونی زیادی** قرار می‌دهید لذا بهتر است که از رمز عبور معتبری استفاده نمایید.<br>
* برای حفط مسائل امنیتی سرویس Redis به صورت یک [Internal Service](https://docs.fandogh.cloud/docs/services.html#%DB%B2-%D8%B3%D8%B1%D9%88%DB%8C%D8%B3-%D9%87%D8%A7%DB%8C-%D8%AE%D8%A7%D8%B1%D8%AC%DB%8C-%DB%8C%D8%A7-external-service) عمل می‌کند و شما خارج از namespace خود به آن دسترسی ندارید.

### Deploy With Manifest
  

شما همچنین می توانید برای اجرای راحت تر سرویس های مدیریت شده از [مانیفست](https://docs.fandogh.cloud/docs/service-manifest.html) همانند مثال زیر استفاده کنید.

```
kind: ManagedService
name: redis
spec:
  service_name: test-redis
  version: 5.0.3
  parameters:
    - name: redis_password
      value: pass123
    - name: volume_name
      value: YOUR_VOLUME_NAME

  resources:
      memory: 200Mi
```
