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