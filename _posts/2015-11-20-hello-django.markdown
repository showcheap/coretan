---
layout: post
title:  "Hello Django!!"
date:   2015-11-29 20:14:00 +0700
categories: cerita
---

Saya lagi tertarik belajar Python/Django, salah satu web framework populer saat ini. Framework ini juga digunakan oleh Instagram loh. 

Persyaratan
===========
1. Terinstall python
2. Terinstall pip, virtualenv
3. Basic command shell (bash/linux terminal)

Configure Environment
=====================
Pertama kita menuju folder yang akan kita gunakan untuk membuat aplikasi django. Kemudian buat python virtual environtmen dengan perintah `virtualenv .` atau bisa juga dengan `virtualenv namafolder` ex: `virtualenv env`.

Output :
{% highlight bash %}
~/Dev/Django/django-blog » virtualenv .
New python executable in ./bin/python
Installing setuptools, pip, wheel...done.
{% endhighlight %}

Activate it :
`source bin/activate`

Install Django
==============

`pip install django`

Output:

{% highlight bash %}
Collecting django
  Using cached Django-1.8.7-py2.py3-none-any.whl
Installing collected packages: django
Successfully installed django-1.8.7
{% endhighlight %}

Create Project
==============

`django-admin startproject myblog`

`cd myblog`

Start your Django Projecet
==========================
`python manage.py runserver`

Output:
{% highlight bash %}
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

November 29, 2015 - 13:28:45
Django version 1.8.7, using settings 'myblog.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
{% endhighlight %}
