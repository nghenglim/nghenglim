---
layout: post
title: SaltStack Vagrant Part 1
tags: [Salt, Configuration-Management, Vagrant]
---

![git]({{ site.baseurl }}/images/2016011600.png "git")

### What is SaltStack
- SaltStack software orchestrates the build and ongoing management of any modern infrastructure.
- SaltStack is also the most scalable and flexible configuration management software for event-driven automation of CloudOps, ITOps and DevOps.
- SaltStack is one of the top configuration management framework among Chef, Puppet, Ansible and SaltStack.

### Why SaltStack with Vagrant
- Salt execution routines can be written as plain Python modules. (I am the Python guy)
- SaltStack script for Vagrant will be mostly same for the cloud server
    - Achievement `development server == production server` Unlocked

### Vagrant Folder Structure
```
- salt/
  - root/
    - top.sls
    - webserver.sls
  - minion
- Vagrantfile
```

### Vagrantfile Setup
```ruby
Vagrant.configure("2") do |config|

    # load up the box for centos 6.6
    # This will take long to download the os, hold up there
    # Or go for a coffee
        config.vm.box = "CentOS_7_x64"
    ## For masterless, mount your salt file root
    config.vm.synced_folder "salt/root/", "/srv/salt/"
    config.vm.network "private_network", ip: "10.0.0.201"

    ## Use all the defaults:
    config.vm.provision :salt do |salt|
        salt.bootstrap_options = "-P -c /tmp" # to salve minion_config not copied issue
        salt.masterless = true
        salt.minion_config = "salt/minion"
        salt.run_highstate = true

    end
end
```

### top.sls
```ruby
base:
  '*':
    - webserver
```

### webserver.sls
```ruby
httpd:               # ID declaration
  pkg:                # state declaration
    - installed       # function declaration
  service.running:
    - enable: True
    - require:
        - pkg: httpd
```

### minion
```ruby
file_client: local
```

### Ending
Run `vagrant up` you should get a CentOS_7_x64 box with httpd server installed!

By the end of this article, you should know the basic of how salt work.
