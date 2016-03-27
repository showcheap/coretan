---
layout: post
title:  "Cara Setup Jekyll di Fedora"
date:   2016-03-27 11:17:00 +0700
categories: catatan
---

## Persiapan
Untuk dapat menggunakan jekyll di komputer kamu, harus menyiapkan beberapa list software seperti di bawah ini.

1. **Ruby**, Yes, kita butuh ruby karena jekyll di tulis menggunakan bahasa pemrograman ruby.
2. **Ruby Gems**, Semacam installernya ruby (Mungkin mirip composer, pip, etc.)
3. **Jekyll**, dan jekyll itu sendiri.

## Installasi
Pada catatan kali ini saya menggunakan Linux Fedora 23 Workstation Edition (64bit). Jadi installernya menggunakan `dnf` yak.

`sudo dnf install rubygems ruby-devel -y`

Tunggu sampai proses download selesai. Dan lanjutkan dengan perintah di bawah ini untuk menginstall jekyll.

`sudo gem install jekyll`

Tampilanya kurang lebih seperti di bawah ini.

```
Building native extensions.  This could take a while...
Successfully installed ffi-1.9.10
Fetching: rb-inotify-0.9.7.gem (100%)
Successfully installed rb-inotify-0.9.7
Fetching: listen-3.0.6.gem (100%)
Successfully installed listen-3.0.6
Fetching: jekyll-watch-1.3.1.gem (100%)
Successfully installed jekyll-watch-1.3.1
Fetching: kramdown-1.10.0.gem (100%)
Successfully installed kramdown-1.10.0
Fetching: liquid-3.0.6.gem (100%)
Successfully installed liquid-3.0.6
Fetching: mercenary-0.3.5.gem (100%)
Successfully installed mercenary-0.3.5
Fetching: rouge-1.10.1.gem (100%)
Successfully installed rouge-1.10.1
Fetching: safe_yaml-1.0.4.gem (100%)
Successfully installed safe_yaml-1.0.4
Fetching: jekyll-3.1.2.gem (100%)
Successfully installed jekyll-3.1.2
Parsing documentation for ffi-1.9.10
Installing ri documentation for ffi-1.9.10
Parsing documentation for rb-inotify-0.9.7
Installing ri documentation for rb-inotify-0.9.7
Parsing documentation for listen-3.0.6
Installing ri documentation for listen-3.0.6
Parsing documentation for jekyll-watch-1.3.1
Installing ri documentation for jekyll-watch-1.3.1
Parsing documentation for kramdown-1.10.0
Installing ri documentation for kramdown-1.10.0
Parsing documentation for liquid-3.0.6
Installing ri documentation for liquid-3.0.6
Parsing documentation for mercenary-0.3.5
Installing ri documentation for mercenary-0.3.5
Parsing documentation for rouge-1.10.1
Installing ri documentation for rouge-1.10.1
Parsing documentation for safe_yaml-1.0.4
Installing ri documentation for safe_yaml-1.0.4
Parsing documentation for jekyll-3.1.2
Installing ri documentation for jekyll-3.1.2
Done installing documentation for ffi, rb-inotify, listen, jekyll-watch, kramdown, liquid, mercenary, rouge, safe_yaml, jekyll after 21 seconds
10 gems installed
```

Yes, sampai di sini kita sudah bisa membuat jekyll di komputer kita. Apa itu jekyll?? **Lha embuh**