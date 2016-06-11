---
layout: post
title: Lubuntu to replace Window
tags: [Lubuntu]
---

![lubuntu]({{ site.baseurl }}/images/2016061100.png "lubuntu")

### Why Lubuntu
As a developer, you must have heard of ubuntu. FYI, Lubuntu is a light weight version of Ubuntu. Using Lubuntu, you can have more control on your PC.

### Advantage for replacing Windows for Lubuntu
- Combination of Windows 7 with command line feeling
- Directly use docker container to run application instead of virtualbox, which provide a higher speed.
- Faster speed for most of the program, for example android-studio. This might be due to less backend application run in Windows (And it is hard to disable those application).
- More control on the system and more debug message can be seen.

### Disadvantage for using Lubuntu
- Most gaming software run natively in windows, the worst things is I have installed lubuntu xenial 16.04LTS version and they have dropped support for my AMD RADEON graphic card model,
- The UI is not as beautiful as Windows

### Some bug Fix
- Fix no sound

~~~
install restrict-ubuntu
~~~
- Fix frequent crash in dell inspiron graphic card: upgrade from kernel 4.4 to kernel 4.6
- Local Support: go to start > Preferences > Language Support
- Unable to start docker: sudo docker daemon -D -s vfs

### Some example
- Run this blog locally

~~~bash
cd /e/nghenglim.github.io/ # contain the repo
sudo docker run -d -v "$PWD:/src" -p 4000:4000 grahamc/jekyll serve -H 0.0.0.0
~~~

### Conclusion
If graphic card is not supported by Lubuntu, the best setup will be dual boot Lubuntu and Windows. Play games and watch movie in Windows, however do development in Lubuntu.
