---
layout: post
title: http.HandleFunc, http.HandlerFunc, http.Handle ve http.Handler nedir arasındaki farklar
categories:
- go
---

http.HandleFunc ve http.Handle function olarak kendi arasında, http.HandlerFunc'ı bir tip http.Handler'ı ise bir interface olarak kendi arasında iki guruba ayırabiliriz.

yukarıdaki ifadeleri guruplamamdaki amaç, aslında bir gurubun olmazsa olmaz diğer gurubun ise geliştiricilere kolaylık sağlamak amacı ile oluşturulduğunu göstermekdir.

net/http paketinin kullanımı hakkında örneklere baktığımızda üç farklı şekilde rota tanımlandığını görebiliyoruz.

**1. Yöntem** (Zor olan)

    type IndexHandler struct{}

    func (this IndexHandler) ServeHTTP(rw http.ResponseWriter, req *http.Request) {
        rw.Write([]byte("Hellow World!"))
    }

    func main() {
        http.Handle("/", IndexHandler{})

        http.ListenAndServe(":8000", nil)
    }

**2. Yöntem** (Eh işte orta)

    func indexHandler(rw http.ResponseWriter, req *http.Request) {
        rw.Write([]byte("Hellow World!"))
    }

    func main() {
        http.Handle("/", http.HandlerFunc(indexHandler))

        http.ListenAndServe(":8000", nil)
    }

**3. Yöntem** (Kolay olan)

    func indexHandler(rw http.ResponseWriter, req *http.Request) {
        rw.Write([]byte("Hellow World!"))
    }

    func main() {
        http.HandleFunc("/", indexHandler)

        http.ListenAndServe(":8000", nil)
    }

Nasıl ? sizce üçüncü yöntem çok daha kolay değil mi ? birinci yöntem'de bir struct oluşturacaksın daha sonra ona bir metod ekleyeceksin falan filan... ama üçüncü yöntemde tek bir fonksiyon ile hallediyoruz.

aslında arka plan'da tüm yöntemler 1. yönteme dönüşür!

**http.HandleFunc**

HandleFunc iki değer alan bir fonksiyondur, ilk değer path ikinci değer de bir fonksiyon'dur (http.HandlerFunc tipinde)

    func HandleFunc(pattern string, handler func(ResponseWriter, *Request)) {
        DefaultServeMux.HandleFunc(pattern, handler)
    }

**http.Handle**

handle iki değer alan bir fonksiyondur, ilk değer path ikinci değer de bir http.Handler interface'ine uygun ifadedir.

    func Handle(pattern string, handler Handler) {
            DefaultServeMux.Handle(pattern, handler) 
    }

**http.HandlerFunc** 

HandlerFunc, ServeHTTP adında bir metodu bulunan bir tiptir. bunun var oluş amacı kolay bir şekilde http.Handler interface'ine uygun struct'lar oluşturmakdır.

    type HandlerFunc func(ResponseWriter, *Request)

    func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
        f(w, r)
    }

ikinci yönteme dikkat ederseniz http.Handle() ile rota tanımlamamıza rağmen herhangi bir struct falan oluşturmadık. http.HandlerFunc bizim yerimize oluşturdu çünkü. bunu bir wrapper olarak düşünebilirsiniz. geriye http.Handler interface'ine uygun bir ifade döndürür.

**http.Handler**

http.Handler bir inerface'dir.

    type Handler interface {
        ServeHTTP(ResponseWriter, *Request)
    }