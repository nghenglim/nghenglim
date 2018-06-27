---
layout: post
title: Goroutine
tags: [Golang]
---

![Go]({{ site.baseurl }}/images/2015091900.jpg "Go")

A goroutine is a lightweight thread managed by the Go runtime to support concurrency. It is considered a better mechanism than nodejs event event loop or normal thread.

### Goroutine vs Java thread
Quoting from [this blog](http://tleyden.github.io/blog/2014/10/30/goroutines-vs-threads/)

- On Java you can run 1000’s or tens of 1000’s threads. On Go you can run hundreds of thousands or millions of goroutines.
- Java threads map directly to OS threads, and are relatively heavyweight. Part of the reason they are heavyweight is their rather large fixed stack size. This caps the number of them you can run in a single VM due to the increasing memory overhead.
- Go OTOH has a segmented stack that grows as needed. They are “Green threads”, which means the Go runtime does the scheduling, not the OS. The runtime multiplexes the goroutines onto real OS threads, the number of which is controlled by GOMAXPROCS. Typically you’ll want to set this to the number of cores on your system, to maximize potential parellelism.

### Example of goroutine
The example can be found at [gobyexample](https://gobyexample.com/goroutines). The how it work internally can refer to this
["example"](http://www.goinggo.net/2015/02/scheduler-tracing-in-go.html).

To summarise, golang achieve concurrency with the implementation of goroutine and [channel](https://gobyexample.com/channels). Goroutine acts as task worker while channel let them achieve "[Share Memory By Communicating](https://golang.org/doc/codewalk/sharemem/)".

### Advantage of goroutine
- No callback hell, example at [stackoverflow](http://stackoverflow.com/a/23709882)

  ~~~ js
  //nodejs
  doSomething1(arg1, arg2, function() {
    doSomething2(arg1, arg2, function() {
      doSomething3(function() {
        // done
      });
    });
  });
  somethingElse();
  ~~~
  ~~~ go
  //golang
  go func() {
    doSomething1(arg1, arg2)
    doSomething2(arg1, arg2)
    doSomething3()
    // done
  }()
  somethingElse()
  ~~~
- Faster startup time and light weight than threads = run more, run faster
