---
layout: post
title: golang, pointer kavramı
categories:
- go
---

Aslında **pointer** kavramı her dilde aynıdır ancak biz örneklerde **go** dilini kullanacağız.

pointer, Programlama dillerinde bellek adreslerini saklayan değişkenlere verilen genel isimdir.
pointer olayını iyi kavrarsanız daha iyi kodlar yazabilirsiniz. zira go dilinde pointer sıkça kullanılmaktadır.

şimdi bir değişken tanılayalım ve neler olup bittiğine bir göz atalım.

```
degisken1 := 1
```

şeklinde bir değişken tanımladığımızda, hafızada ona bir yer ayrılır ve 3 sütünda tutulur.

| değişken adı  | değeri    | adresi        |
|-------------- |--------   |------------   |
| degisken1     | 5         | 0x0000ffff    |

şimdi, 2. bir değişken oluşturalım ve ve değer olarak birinci değişkeni verelim.

```
degisken2 := degisken1
```

yukarıdaki örnekte bellekte 2. bir yer ayrıldı ve son durum aşağıdaki gibi oldu.

