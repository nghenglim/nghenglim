---
layout: post
title: Loopback for NodeJS
tags: [NodeJS]
---

![loopback]({{ site.baseurl }}/images/2016070900.png "Loopback")

### What is Loopback
In a nutshell, loopback is a NodeJS framework for building rest API server

### Loopback for Full-Stack Web Development
- Frontend: Loopback has a first class support using AngularJS 1. It comes with `lb-ng` tools which auto generate angular service which you might find it handy.
- Backend: Build in swagger support, switchable database at model level and easy-to-create script such as database migration.

### Advantage Of Loopback
- [Well Documented](https://docs.strongloop.com/display/LB/LoopBack), including Android SDK, iOS SDK and Xamarin SDK.
- IBM and the StrongLoop team are committed to maintaining and improving the LoopBack open-source project

### Disadvantage Of Loopback
- No first class support of promise yet - as in discussed in this [thread](https://github.com/strongloop/loopback/issues/418)
- Postgres datasource is still lack of some feature - might have to write raw query to get the job done.
- Rumor is Google is ditching Angular 1. Therefore there could be a hard time to upgrade to Angular 2 for Loopback.

### Words of Thought
Recently I have been using Loopback a lot in my web project or as mobile application's backend server. Personally I think it is the best NodeJS framework among those I had tried - expressJS, sailsJS and meteorJs.

If you are choosing a NodeJS framework for your new project, you might as well give it a try!
