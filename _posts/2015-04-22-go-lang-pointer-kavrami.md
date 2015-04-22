---
layout: post
title: go lang pointer kavramı
categories:
- go
---

pointer yani işaretçiler, sadece go diline özel değildir, dinamik veya statik olsun çoğu dillerde vardır. örneğin PHP.

kod yazarken, tanımladığınız bütün değerler(değişkenler, sınıflar, vs.), bellek'te, "adı, değeri, ve adresi" şeklinde kabaca 3 sütün'da tutulur.

Pointer demek, bir değişkenin veya değerin bellek adresi demektir. bellek adresi "0x0000ffff" gibi, hexadecimal(onaltılık tabanda) bir değerdir.

Pointer'ların ne olduğu hakkında hiç bilgisi olmayanlar, [wiki](http://tr.wikipedia.org/wiki/%C4%B0%C5%9Faret%C3%A7iler) sayfasına bakabilirler. zira biz pointer'ların kendisi ile değil de, go dilinde nasıl kullanabileceğimiz ile ilgileneceğiz.

pointer'ları kullanırken **"*"** ve **"&"** karekterlerini sıkça kullanırız.

**"&"** bize bir değerin bellek adresini döndürür. **"*"** ise tam tersidir. yani bir bellek adresinin değerini döndürür.

örnek ile görelim,

    package main

    import "fmt"

    var adi string = "Ali"
    // buraya dikkat etmeniz gerekiyor. biz bu değişkenin tipini string değil de *string olarak
    // belirttik. yani diyoruz ki, bu değişkenin değeri bir "string değerin bellek adresi" olacaktır.
    var adiPointer *string = &adi

    func main() {
        fmt.Println("değişkenin değeri: ", adi)
        fmt.Println("değişkenin bellek adresi: ", adiPointer)
        fmt.Println("bellek adresinin değeri: ", *adiPointer)

        // iki değişken de arka planda aynı adresi işaret ettikleri için
        // birini değiştirirseniz diğeride değişecektir.

        *adiPointer = "Veli"

        fmt.Println("adi değişkeninin değeri: ", adi)
        fmt.Println("adiPointer değişkeninin değeri: ", *adiPointer)
    }

bu kodun çıktısı, aşağıdaki gibi'dir.

    değişkenin değeri:  Ali
    değişkenin bellek adresi:  0x1b4730
    bellek adresinin değeri:  Ali
    adi değişkeninin değeri:  Veli
    adiPointer değişkeninin değeri:  Veli

inanmazsanız [buradan](http://play.golang.org/p/MiCA-rbmQB) bakabilirsiniz :)
