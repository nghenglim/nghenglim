---
layout: post
title: Real time chat with Mongodb Express AngularJS Node.js
tags: [Mongodb, AngularJS, NodeJS]
---

![MEAN STACK]({{ site.baseurl }}/images/2015062700.jpg "MEAN STACK")

What I am going to write about is a real time chat proof of concept which I have done in 2014. It is now at
[Github](https://github.com/nghenglim/nodejslim). A demo can be found at [http://nodejslim.herokuapp.com/](http://nodejslim.herokuapp.com)

### MEAN Stack

MEAN stack is a software bundle with [Mongodb](https://www.mongodb.org/), [Express](http://expressjs.com/),
[AngularJS](https://angularjs.org/) and [NodeJS](https://nodejs.org/).

### What this Repo do.

- It uses Node.js -- a web server that use a event-driven, non-blocking I/O model that makes it lightweight and efficient.
- To make use of this non blocking attributes, we use an asynchronous non-blocking nosql database MongoDB.
  - FYI, mysql and postgresql still have no good asynchronous support at this point of time.
  - As a real time chat system, it has to store many data, a relational database will be too hard to scale and also to partition it easily.
- To setup this server quickly while maintaining a good architecture, we use express as a web framework for Node.js.
- For the frontend, we use AngularJS as Javascript MVC framework. Everything will serve restfully from Node.js to AngularJS.

### Some comment

- Node.JS is using ECMAScript 5(current javascript syntax), therefore the code is not so clean. With the future ECMAScript 6 become mainstream,
I believe that it will be easier to code for nodeJS.
- Need to make sure everything is asynchronous, and use promise when needed.
