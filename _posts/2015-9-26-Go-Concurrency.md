---
layout: post
title: Go Concurrency (Google IO 2012)
tags: [Golang]
---

![Go]({{ site.baseurl }}/images/2015091900.jpg "Go")

Concurrency is the key to designing high performance network services. Go's concurrency primitives (goroutines and channels) provide a simple and efficient means of expressing concurrent execution. [In this talk we see how tricky concurrency problems can be solved gracefully with simple Go code.](https://www.youtube.com/watch?v=f6kdp27TYZs)

### Some Notes
- Concurrency is not parallelism
  - Go support concurrency across multiple cpu cores, which is called parallelism
- Example of running the search function to search web,image and video concurrently
  - with no lock, no condition variable and no callbacks
  - with ability to limite maximum wait time, and return the searched result among web, image and video.
- The video used Go's concurrency primitives to convert
  - from slow, sequential and failure sensitive program
  - to fast, concurrent, replicated and robust program
