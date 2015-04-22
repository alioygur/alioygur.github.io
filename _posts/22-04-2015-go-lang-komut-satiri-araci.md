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