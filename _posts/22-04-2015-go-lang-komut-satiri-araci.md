---
layout: post
title: go lang komut satırı aracı
categories:
- go
---

go dili güçlü bir komut satırı aracı ile gelmektedir. şimdi teker teker bu komutların ne işe yaradıklarına bakalım.

terminalinizden (kabuk, shell, artık ne diyorsanız :) `go` komutunu çalıştırdığınızda aşağıdaki gibi bir çıktı alacaksınız.

{% highlight sh %}
➜  alioygur.github.io git:(master) go
Go is a tool for managing Go source code.

Usage:

    go command [arguments]

The commands are:

    build       compile packages and dependencies
    clean       remove object files
    env         print Go environment information
    fix         run go tool fix on packages
    fmt         run gofmt on package sources
    get         download and install packages and dependencies
    install     compile and install packages and dependencies
    list        list packages
    run         compile and run Go program
    test        test packages
    tool        run specified go tool
    version     print Go version
    vet         run go tool vet on packages

Use "go help [command]" for more information about a command.

Additional help topics:

    c           calling between Go and C
    gopath      GOPATH environment variable
    importpath  import path syntax
    packages    description of package lists
    testflag    description of testing flags
    testfunc    description of testing functions

Use "go help [topic]" for more information about that topic.
{% endhighlight %}

bu `go` ya ait alt komutları ve nasıl kullanabileceğimizi kısaca özetlemektedir. Şimdi bakalım,


## go build

Go paketlerini derlemek için kullanılan komuttur. Eğer gerektiği durumlarda bağımlı olan paketleride otomatik derler.

- Eğer paket  `main` değilde,  bölüm 1.2 deki gibi `mymath` ise, `go build` çalıştığında hiç birşey oluşturulmayacak. Eğer `$GOPATH/pkg` içinde `.a` uzantılı derlemiş haline istiyorsanız,  `go install` komutunu kullanabilirsiniz.
- Eğer paket `main` ise, aynı dizin içinde çalıştırılabilir haline oluşturcaktır. Eğer oluşacak dosyanın `$GOPATH/bin` içinde olmasını istiyorsanız, `go install` ya da `go build -o ${DİZİN_YOLU}/a.exe` olarak çalıştırın.
- Dizinde birden fazla go dosyası varsa, ve sadece birini derlemek istiyorsanız, `go build` komutuna dosya ismini argüman olarak vermelisiniz. Örneğin, `go build a.go`. `go build` argüman almaz ise dizindeki bütüm dosyaları derleyecektir.
- Oluşacak dosyanın isminide önceden belirieyebilirsiniz. Örneğin, `mathapp` projesinde (bölüm 1.2'deki),  `go build -o astaxie.exe` komutu `mathapp.exe` yerine `astaxie.exe` adında bir dosya oluşturacaktır. Öntanımlı isimlendirme ya dizin ismi ya da ilk kaynak kodu içeren dosya ismi olarak seçilmiştir.

( [Go Programlama  Dili Kılavuzu](https://golang.org/ref/spec)'na göre , paket isimleri  `package` anahtar kelimesinden sonra kaynak dosyanın ilk satırına yazılmalıdır. Dizin ismi ile aynı olması zorunlu değildir, çalıştırılabilir dosyanın ismi dizin ismi olacaktır.]) 

- `go build`, `_` ya da `.` ile başlayan dosyaları görmezden gelir.
- Her işletim sistemi için ayrı dosyalar tutmak isterseniz, işletim sistemi ismini ek olarak kullanabilirsiniz. Örneğin, `array.go`'yu farklı sistemler için yazacaksanız. Dosya isimleri aşağıdaki gibi olabilir:
    
    array_linux.go | array_darwin.go | array_windows.go | array_freebsd.go
    
`go build` işletim sisteminize göre derleme işlemini yapacaktır. Örneğin, Linux kullanıyorsanız sadece  array_linux.go derleyip, diğerlerini yoksayacaktır.

## go clean

Derleyici tarafından oluşturulmuş aşağıdaki  dosyaları temizler: 
    
    _obj/            // eski obje klasörü, Makefiles tarafından oluşturulmuş
    _test/           // eksi test klasörü, Makefiles tarafından oluşturulmuş
    _testmain.go     // eski gotest dizini, Makefiles tarafından oluşturulmuş
    test.out         // eski test dizini, Makefiles tarafından oluşturulmuş 
    build.out        // eksi test dizini, Makefiles tarafından oluşturulmuş 
    *.[568ao]        // obje dosyaları,  Makefiles tarafından oluşturulmuş 

    DIR(.exe)        // go build tarafıdan oluşturulmuş
    DIR.test(.exe)   // go test -c tarafından oluşturulmuş
    MAINFILE(.exe)   // go build MAINFILE.go tarafından oluşturulmuş
    
Projelerimi Github'a göndermeden önce genellikle bu komutu çalıştırırım. Yereldeki testler için önemli, ama sürüm takip için gereksiz dosyalar.

## go fmt

Öncede C/C++ ile çalışmış olanlar, hangi kodlama stilinin daha iyi olduğu konusundaki tartışmları biliyordur: K&R-stili ya da ANSI-stili. Go da ise, herkesin kullanmak zorunda olduğu  sadece bir kod stili vardır. Örneğin, açma parantezleri satır sonlarını yazılmalıdır, yeni bir satırda yazılamazlar, eğer bu kurala uymazsanız derleme hatası alacaksınız! Neyse ki, bu kuralları ezberlemek zorunda değilsiniz. `go fmt` bu işi sizin yerinize yapacaktır. Terminalinizde `go fmt <dosya_ismi>.go` komutunu çalıştırmanız yetecektir. Bir çok IDE siz dosyayı kaydettiğinizde otomatik olarak bu komutu çalıştıracaktır. IDE'ler hakkında bir sonraki bölümde daha ayrıntılı bilgi vereceğim.

`gofmt` şeklind değilde  `go fmt -w` şeklinde kullanmanız daha iyi olcaktır. `-w` parametresi formatladıktan sonra değişiklikleri kaydetcektir. `gofmt -w src` ise src altındaki butun dosyaları formatlar.

## go get

Bu komut üçüncü parti paketleri almanızı sağlar. Şuanda; BitBucket, Github, Google Code ve Launchpad desteği sunuyor. Bu komutu çalıştırdığımızda iki şey yapılıyor. Birincisi Go kaynak kodunu indiriyor, ikinci olarakta `go install` komutunu çalıştırıyor. Bu komutu çalıştırmadan önce, gerekli araçları kurudğunuzdan emin olun.

    BitBucket (Mercurial Git)
    Github (git)
    Google Code (Git, Mercurial, Subversion)
    Launchpad (Bazaar)
    
Bu komutu kullanmak için, yukarıdaki araçları kurmuş olmanız lazım. `$PATH` değişkenini ayarlamayıda unutmayın. Bu arada, özel alan adlarınıda destekliyor. `go help remote` komutu ile daha ayrıntılı bilgi edinebilrsiniz.

## go install

Bu komut bütün paketleri derleyip oluşan dosyaları, `$GOPATH/pkg` ya da  `$GOPATH/bin` altına taşır.

## go test

Bu komut  `*_test.go` ile biten dosyaları derleyip çalıştırır, gerekli bilgileri ekrana basar.

    ok   archive/tar   0.011s
    FAIL archive/zip   0.022s
    ok   compress/gzip 0.033s
    ...
    
Öntanımlı olarak bütün test dosyalarını çalıştırır. `go help testflag` komutunu kullanarak daha ayrıntılı bilgi elde edebilirsiniz.

## go doc

Bir çok insan Go için üçüncü parti bir dökümantasyona aracına gerek olamdığını düşünüyor (aslına bakarsanız ben bir tane yazdım bile [CHM](https://github.com/astaxie/godoc)). Go dökümanları yönetmek için çok güçlü bir araca sahip.

Peki bir paketin dökümantasyonuna nasıl bakabiliriz? Örneğin, Eğer bir `builtin` paket hakkında daha fazla bilgi istiyorsanız, `go doc builtin` komutunu işinizi görecektir. Benzer şekilde, `go doc net/http` komutu ile  `http` paketi hakkında bilgi elde edebilirsiniz. Fonksiyonlar hakkında daha ayrıntılı bilgi istiyorsanız, `godoc fmt Printf` ve  `godoc -src fmt Printf` komutları işinizi görecektir(`-src` fonksiyonun kodlarını göstercektir).

`godoc -http=:8080` komutunu çalıştırın, `127.0.0.1:8080` adresine gidin. `golang.org`'ın lokal versiyonunu görmüş olmanız gerekiyor. Sadece standart paketler hakkında değil, `$GOPATH/pkg` altındaki bütün paketler içinde bilgileri bulabilirsiniz. Büyük Çin Güvenlik duvarından dökümantasyonlara erişemeyenler için.

## Diğer komutlar

Go yukarıda bahsettiklerimizden daha fazla komut sunuyor.

    go fix // versiyon yükseltme
    go version // Kulladığınız Go sürümü bilgisi
    go env // Go ile alakalı ortam değişkenleri
    go list // yüklü paketlerin listesi
    go run // paketi geçiçi olarak derleyip çalıştırma 
    
Go komutlarınin kendi dökümantasyonunda daha ayrıntılı bilgi bulabilirsiniz. `go help <komut_ismi>` ile bu bilgilere erişebilirsiniz.

kaynak: [https://github.com/astaxie/build-web-application-with-golang](https://github.com/astaxie/build-web-application-with-golang)