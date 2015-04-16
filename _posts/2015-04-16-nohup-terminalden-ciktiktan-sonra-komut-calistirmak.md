---
layout: post
title: nohup, terminalden çıktıktan sonra komut çalıştırmak
categories:
- linux
- bash
---

Çoğu zaman ssh ile uzak sunuculara bağlanmak zorunda kalır, ve o sunucuda 
bir takım komutlar çalıştırır çıkarız.

Çıkış yaptığımız anda (ssh bağlantısını kestiğimizde) çalıştırdığımız bütün komutlar 
eğer hala çalışıyor ise öldürülür. (kill process )

Nadiren de olsa bazen biz çıksak dahi çalıştırdığımız komutların ölmemesini isteyebiliriz. işte bu durumda imdadımıza `nohup` komutu yetişmekte.

`nohup komut-adi &`

yukarıdaki komut, `komut-adi` adındaki komutu çalıştırıp arka plana atacak, siz ssh bağlantısını kapatsanız bile çalıştırdığınız komut ölmeyecektir.

**Bonus**

mevcut oturumda çalışmakta olan komutları görmek için aşağıdaki komutu kullanabilirsiniz.

`jobs -l`

