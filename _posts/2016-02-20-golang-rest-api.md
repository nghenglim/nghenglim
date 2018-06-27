---
layout: post
title: Golang Rest API
tags: [GoLang]
---

![Gin]({{ site.baseurl }}/images/2016022000.png "Gin")

### Installation on Golang
We will use gvm to install go for the current user. Note that we need to use go1.4 to compile go1.5 because go1.5 use go itself as compiler, therefore it need to have go installed.

Note that gvm is mainly for development use, IMHO using tar install or docker is a better way for production server.

~~~ bash
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
gvm install go1.4
gvm use go1.4
gvm install go1.6
gvm use go1.6 --default
~~~

### Gin-Gonic/Gin
Gin is a web framework written in Go (Golang). It features a martini-like API with much better performance, up to 40 times faster thanks to httprouter. If you need performance and good productivity, you will love Gin.

~~~
go get github.com/gin-gonic/gin
~~~

~~~ go
#~/golang/server.go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // listen and server on 0.0.0.0:8080
}
~~~

and execute it with `go run server.go`, access localhost:8080/ping and you should be able to see `{"message":"pong"}`

### Live Reloading with codegangsta/gin
However for development, it is important to have compile on files changed function. There is a package there for go. Note that do not start any app on proxy port that is used by gin (default 3000) and the application port.

Running below code will autostart the go app.

~~~ bash
go get github.com/codegangsta/gin
cd ~/golang/
gin -i -a 8080
~~~

now change the code without terminating gin

~~~ bash
#~/golang/server.go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong pong",
        })
    })
    r.Run() // listen and server on 0.0.0.0:8080
}
~~~

access to localhost:8080/ping and you should be able to see `{"message":"pong pong"}`

### This is It
With this, we have successfully setup a simple golang rest api server. Golang is a promising solution to give both near C performance + dynamic language development speed + goroutine.
