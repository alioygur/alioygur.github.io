---
layout: post
title: go lang, tersine mühendislik, net/http
categories:
- go
---

bence bir şeyin nasıl çalıştığını öğrenmenin en iyi yolu, içini açıp bakmaktır. o yüzden bugün biz `go` dilinin en güçlü paketlerinden olan **net/http** paketini inceleyeceğiz.

bu paket, **node.js**'in [http](https://nodejs.org/api/http.html) paketine veya **python**'un [httplib](https://docs.python.org/2/library/httplib.html) paketine benzer. bununla güçlü bir web server oluşturabilir, gelen istekleri (request) leri yanıtlayabilirsiniz (response).

Öncelikle çok basit bir şekilde bu paketi nasıl kullanabileceğimize bakalım.

    package main

    import (
        "net/http"
    )

    func IndexHandler(rw http.ResponseWriter, req *http.Request) {
        rw.Write([]byte("Hellow World!"))
    }
    func main() {
        http.HandleFunc("/", IndexHandler)

        http.ListenAndServe(":8000", nil)
    }

Yukarıda 8000. portu dinleyen bir web server oluşturduk, "/" diye bir rota belirledik ve bu rotaya karşılık gelen bir fonksiyon atadık.

yukarıdaki kodu `gon run dosyaadi` şeklinde çalıştırdıktan sonra tarayıcımızdan **http://localhost:8000** yazdığımızda "Hello World" yazısı ile karşılacağız.

devam edecek...
