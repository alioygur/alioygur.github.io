---
layout: post
title: scp, secure copy
categories:
- linux
- bash
---

#scp nedir?

iki lokasyon arasında dosya transfer eder

- Dosya transferi ssh üzerinden yapılır.
- dosya transferleri ssh üzerinden yapıldığı için ssh kadar güvenlidir.
- aslında `cp` komutu ile hemen hemen aynıdır, sadece transfer ağ üzerinden gerçekleşir.

___

## Basit kullanım örnekleri

**lokalde bulunan bir dosyayı uzaktaki sunucuya kopyalama.**

    scp lokaldekidosya.txt root@example.com:/tmp/
    
**uzak sunucuda bulunan bir dosyayı lokale kopyalama**

    scp root@example.com:/tmp/uzaktakidosya ./
    
**lokalde bulunan bir klasörü uzaktaki sunucuya kopyalama**

    scp -r lokalklasor/ root@example.com:/tmp/

## Bazı önemli ayarlar

- `-P` Port, default ssh portu 22 dir. ancak siz bazı sebeplerden dolayı bunu değiştirmiş olabilirsiniz.
- `-p` Preserves modification, dosya modunu koru. son değişitirilme tarihi vs.
- `-q` Quiet mode, yani sessiz mod. ilerleme çubuğunu falan kapatır.
- `-r` Recursively copy entire directories, yinelemeli olarak gönder. klasör veya iç içe klasör gönderilirken bu ayar kullanılmalı.  
- `-v` Verbose mode, yani hata ayıklama modunu açar.

## İpuçları

- uzak sunucu yerine IP de yazabilirsiniz.
- path belirtirken başına / koymazsanız bağlandığınız kullanıcının home dizisini referans alır. yani root@example.com:path/to -> root@example.com:/root/path/to anlamına gelir.
- kopyalama yaparken ilk lokasyon kaynak olarak, ikinci lokasyon hedef olarak kabül edilir. yani `scp sourcePath destinationPath`