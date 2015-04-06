---
layout: post
title: PSR - PHP standart önerileri 
categories:
- php
---

Php gelişticisi iseniz php ile kod yazarken birşeyin birden fazla yolu olduğunu biliyorsunuzdur. Bu ilk bakışta kulağa hoş geliyor olabilir. Ancak birşeyin birden fazla yolu varsa buda beraberinde bir "standardizasyon" problemini getiriyor.

___

**Örneğin;**

- Kendi yazdığımız kitapliklarimizi gelecekteki projelerimize dahil etmekte sıkıntı yaşayabiliyoruz.
- Gönüllü gelistiricilerin yazdiklari kitaplıkları projemize dahil etmekte sıkıntı yaşayabiliyoruz.
- Veya A Framework ünün X sınıfını B frameworküne entegre etmekte sıkıntı yaşayabiliyoruz..

Hadi tüm bu dez avantajları bir kenara bırakalım. Ve değişik bir pencereden bakalım. Bana bu problemler "Açık Kaynak" ekosistemine biraz aykırı gibi geldi. Hani Ali yazacak paylaşacak, Veli isterse bunu kullanabilecekti?

Neyseki PHP cephesindeki öncu gelistiriciler bunun farkına vardılar ve "PHP-FIG" (PHP Framework Interop Group) çatısı altında PSR (PHP Standards Recommendation/PHP Standartlar Önerileri), ı hazırladılar.

**Standartları Kim belirliyor?**  
Herkes! Bu standartları bir proje olarak düşünebilirsiniz. Ki zaten proje [buradan](https://github.com/php-fig/fig-standards) ulaşabilirsiniz.

Akış şu şekilde oluyor. 

1. Fikir ortaya atılıyor,
2. Oylamaya sunuluyor,
3. Kabul edilenler standartlaşıyor.

Sizde bu konudaki fikirlerinizi sunabilir, Oy kullanabilir veya Tartışmalara katılabilirsiniz.

**PHP-FIG Nedir?**  
PHP Framework Interoperability Group, Sözkonusu standarları yayınlayan topluluktur.

**Bu Standartlar Nelerdir?**  
Su anda standartlar PSR-0, PSR-1, PSR-2 ve PSR-3 olmak üzere 4 guruba ayrılmış bulunmaktadır. Şimdi bunları tek tek inceleyelim.

- **PSR-0 (Otomatik Yükleyici Standartları)** [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)
- **PSR-1 (Temel Kodlama Standartları)** [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
- **PSR-2 (Kodlama Stili Rehberi)** [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
- **PSR-3 (Loglama Arabirimi)** [PSR-3](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md)

*Başlıkların yanında bulunan linklere tıklayarak standartların içeriğini görebilirsiniz.*

[http://www.php-fig.org](http://www.php-fig.org)