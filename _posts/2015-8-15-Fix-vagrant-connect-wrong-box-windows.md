---
layout: post
title: Fix vagrant connect to wrong box - Windows
tags: [Vagrant]
---

![Vagrant]({{ site.baseurl }}/images/2015081500.png "Vagrant")

### Scenario
So there is a strange behavior in using vagrant for my work. That is when I start vagrant before starting vmware, it will not find the correct path to the vagrant box and thus create a new VM.

The reason behind this is because my default drive is C drive, and when I join company network, it will mount a Z drive to my laptop and thus my home drive become Z drive. So when I open vmware, vagrant will found my virtualbox which is in C drive, however without open it it will assume my vmware is in Z drive and thus unable to find the VM.

So now the vagrant point to the wrong VM, how can I get back the previous vagrant box? Because rerun the vagrant setup will need about 30 mins like that and there are some database data inside my VM. Therefore, the solution is to let the vagrant to point back the correct file.

### Scripts
~~~ bash
cd "C:\Program Files\Oracle\VirtualBox"
VBoxManage.exe list vms
"vagrant_box" {d055f9f7-6b67-4080-a4b0-2b4f149cac4d}

touch vagrant/tools/.vagrant/machines/default/virtualbox/id
~~~

Paste the above id d055f9f7-6b67-4080-a4b0-2b4f149cac4d inside the id file that just created, then vagrant up, and this should solve the issue.

It is refering to this [Github issue](https://github.com/mitchellh/vagrant/issues/1755)
