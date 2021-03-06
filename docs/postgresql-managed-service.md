---
layout: fandogh
id: postgresql-managed-service
title: PostgreSQL + Adminer
sidebar_label: PostgreSQL + Adminer
---
### ![Postgresql + Adminer](/img/docs/postgresql-adminer.png "Postgresql + Adminer")

Postgresql یک ORDBMS معروف و پرطرفدار است که می‌توانید به سادگی به عنوان یک managed-service روی Namespace خود دیپلوی کنید.
هنگام دیپلوی کردن Postgresql پارامتر‌های زیر را می‌توانید مشخص کنید:
|کانفیگ|نوع|پیش‌فرض|توضیح|
|---	|---	|---	|---	|
|service_name| string| postgresql| نامی که برای سرویس مایلید در نظر گرفته شود|
|adminer_enabled|boolean | true | فعال یا غیرفعال بودن Adminer
|postgres_password| string| postgres| رمز عبور دیتابیس|
|volume_name| string| None| نام volumeای که به سرویس وصل می شود|

> توجه داشته باشید که اگر میخواهید سرعت I/O در سرویس دیتابیس شما بیشتر شود٬ می‌توانید از volume‌ها استفاده کنید و نام آن را به صورت `c volume_name=VOLUME_NAME-` موقع ساخت Managed Service در cli وارد نمایید. ( VOLUME_NAME نام volume‌ای است که موقع ساخت آن تعیین کرده‌اید).
> 
به عنوان مثال برای دیپلوی کردن یک Postgresql می‌توانیم به این شکل یک سرویس بسازیم:
```
  fandogh managed-service deploy postgresql 10.4 \
       -c service_name=test-dbms \
       -c adminer_enabled=false \
       -c postgres_password=test123
```
این دستور یک سرویس Postgresql ایجاد می‌کند که:
* نام سرویس آن test-dbms ( یعنی در شبکه داخلی فضانام شما باقی سرویس‌ها از طریق نام test-dbms می‌توانند به آن متصل شوند) .
* رمز عبور آن test123 است.
*  Adminer هم در آن غیر‌فعال شده است.

### Deploy With Manifest
 
شما همچنین می توانید برای اجرای راحت تر سرویس های مدیریت شده از [مانیفست](https://docs.fandogh.cloud/docs/service-manifest.html) همانند مثال زیر استفاده کنید.

```
kind: ManagedService
name: db
spec:
  service_name: postgresql
  version: 10.4
  parameters:
    - name: phpmyadmin_enabled
      value: true
    - name: mysql_root_password
      value: some_long_unpredictable_string
    - name: volume_name
      value: YOUR_VOLUME_NAME

  resources:
      memory: 600Mi
```
