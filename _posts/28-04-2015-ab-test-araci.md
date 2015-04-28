---
layout: post
title: ab test aracı kullanımı
categories:
- test
---

##AB (ApacheBenchmark)
İsminden de anlaşılacağı üzere, araç Apache firmasınındır.

bu araç, bir web uygulamamısının performansını ölçmek için dizayn edilmiştir.

## Kullanım

    ab -n “toplam istek sayısı” -c “eşzamnlı olarak kaç istek yapılacak”  URL

## Gerçek hayattan örnek,
example.org adresine aynı anda 10 olmak üzere toplamda 100 http isteği gönderelim ve 
aracın çıktısını inceleyelim.

    ab -n 100 -c 10 example.org/

yukarıdaki komutu çalıştırıp kısa bir süre bekledikten sonra aşağıdaki çıktı gibi bir çıktı alacağız.

```
This is ApacheBench, Version 2.3 <$Revision: 1528965 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking example.org (be patient).....done


Server Software:        ECS
Server Hostname:        example.org
Server Port:            80

Document Path:          /
Document Length:        1270 bytes

Concurrency Level:      10
Time taken for tests:   2.593 seconds
Failed requests:        0
Total transferred:      161000 bytes
HTML transferred:       127000 bytes
Requests per second:    38.56 [#/sec] (mean)
Time per request:       259.350 [ms] (mean)
Time per request:       25.935 [ms] (mean, across all concurrent requests)
Transfer rate:          60.62 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:      123  127   2.5    126     134
Processing:   126  129   2.4    128     135
Waiting:      125  129   2.4    128     134
Total:        249  256   4.9    254     269

Percentage of the requests served within a certain time (ms)
  50%    254
  66%    257
  75%    261
  80%    262
  90%    264
  95%    267
  98%    267
  99%    269
 100%    269 (longest request)
 ```

Şimdi önemli olan kısımlara değinelim.

    Time taken for tests:   2.593 seconds

Test toplam kaç saniye sürdü. Yani example.org adresi **2.593** saniyede 100 isteğe cevap vermiş.

    Failed requests:        0

Başarısız olan istek sayısı, 0 gördüğünüz gibi.

    Requests per second:    38.56 [#/sec] (mean)

saniyede yapılan istek sayısı, 38.56 istek yapılmış bir saniyede

    Time per request:       259.350 [ms] (mean)

Bir istek kaç saniye sürmüş (ortalama), 259.350 milisaniye

    Time per request:       25.935 [ms] (mean, across all concurrent requests)

Bir istek kaç saniye sürmüş (ortalama), 25.935 (eş zamanlı istekler dahil değil.)

Neden iki tane `Time per request` çıktısı var, çünkü birincisinde eşzamanlı istekler dahil hesaplanır, ikincisinde dahil değildir.

örneğin, `ab -n 100 -c 1 example.org/` (dikkat edin, eş zamanlı istek yok) şeklinde bir test yaptığımızda iki değer de aynı çıkacaktır.


çok daha ayrıntılı bilgi için [buraya](http://httpd.apache.org/docs/2.2/programs/ab.html) bakabilirsiniz.