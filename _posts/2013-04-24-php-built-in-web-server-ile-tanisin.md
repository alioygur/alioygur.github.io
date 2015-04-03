---
layout: post
title: Php built-in web server ile tanisin 
---

Php 5.4 ile birlikte gelen yeni ozellik olan "built-in web server" tukceye sanirim "tumlesik web sunucusu" olarak cevirebiliriz. Biz gelistiricilerin cok isine yarayacak.

**Nedir &amp; Ne ise yarar?**

Tipki Nginx veya Apache gibi bir web sunucusudur.

Oncesinde  yerel makinenizde web uygulamasi gelistirirken nginx veya apache tarzinda bir web sunucusuna ihtiyac duyardik ve her uygulamamiz icin bir virtual host tanimlardik.

Php built in web server geldikten sonra bunlara ihtiyacimiz kalmadi. Bu zaten onlarin yaptigi isi yapiyor.

*Unutmayin, bu sadece development altinda kullanabileceginiz bir web server dur. Prodaction uygulamalarda kullanilmasi tavsiye edilmez.*

**Kullanim**

Kullanimi oldukca basittir.
    
    # bulundugunuz klasoru kok klasor varsayarak web server baslatilir.
    php -S localhost:8000
    
    # -t parametresi ile belirtiginiz klasoru kok klasor varsayarak web server baslatilir.
    php -S localhost:8000 -t /path/to
    
    # Ayrica IP veya degisik portlarda belirtebilirsiniz
    php -S 192.168.0.1:8001

Daha detayli bilgi icin [buraya](http://php.net/manual/en/features.commandline.webserver.php) bakabilirsiniz.