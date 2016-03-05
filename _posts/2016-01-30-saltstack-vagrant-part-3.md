---
layout: post
title: SaltStack Vagrant Part 3
tags: [Salt, Configuration-Management, Vagrant]
---

![saltStack]({{ site.baseurl }}/images/2016011600.png "saltStack")

Last week we talked about how to make use pillar to create users in our master-less salt server. Today will be about how to use salt-formula and grains. [All SaltStack Article](http://nghenglim.github.io/tags/#Salt-ref)

### What is Salt Formulas
Formulas are pre-written Salt States. All official Salt Formulas are found as separate Git repositories in the "saltstack-formulas" organization on GitHub: [https://github.com/saltstack-formulas](https://github.com/saltstack-formulas)

### Objective
This week objective will be installing NodeJS 5.4.0 from binary with salt formula.

The standard way of installing salt-formula can be found at [https://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html](https://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html). However, I will use my own way here.

### Server Structure
~~~ ruby
# vagrant sync folder
config.vm.synced_folder "salt/root/", "/srv/salt/"
config.vm.synced_folder "salt/pillar/", "/srv/pillar/"
~~~ 

~~~ ruby
- /srv/
  - pillar/  # Unlike state tree, pillar data is only available for the targeted minion specified by the matcher type.
  - salt/  # All the configuration for the minion to run
    - node/ # node formula folder
~~~ 

### Svn Export from Github
My favourite Github hack: (replacing tree/master with trunk)

~~~ bash
cd salt/root
svn export https://github.com/saltstack-formulas/node-formula/trunk/node
~~~ 

~~~ ruby
#salt/root.top.sls
base:
  '*':
    - node
~~~ 

~~~ ruby
# pillar/node/init.sls
node:
  version: 5.4.0
  checksum: f037e2734f52b9de63e6d4a4e80756477b843e6f106e0be05591a16b71ec2bd0
  install_from_binary: True
~~~ 

~~~ ruby
# pillar/top.sls
base:
  '*':
    - node
~~~ 

If you try `salt-call --local state.highstate` you probably will get an error now. Why?

### Grains
Salt comes with an interface to derive information about the underlying system. This is called the grains interface, because it presents salt with grains of information. Grains are collected for the operating system, domain name, IP address, kernel, OS type, memory, and many other system properties.

As of the time I'm writing, [https://github.com/saltstack-formulas/node-formula/blob/master/node/map.jinja](https://github.com/saltstack-formulas/node-formula/blob/master/node/map.jinja) line 19-28 is missing CentOS config for the grains.os (most of saltstack formula comes with Ubuntu), so add Centos config

~~~ ruby
'Centos': {
    'node_pkg': 'nodejs',
    'npm_pkg': 'nodejs' if pillar_get('node:install_from_ppa') else 'npm',
},
~~~ 

How to see my os value is grains? Just run the script below can look for os, for me the value is CentOS
~~~ ruby
sudo salt-call --local grains.items
~~~ 

Grains can be customized in minion config file or at `/etc/salt/grains`, however normally using its default value is enough.

### End Result
It should successfully install node version `5.4.0` and verify against checksum `f037e2734f52b9de6......`.

Now run `salt-call --local state.highstate` and run `node -v` to verify, it should output `v5.4.0`.

### This is it
So the basic concept of saltstack to work with masterless vagrant should be covered from part 1 to part 3. After knowing the basic concept it should be relatively easy to google search for salt related article and create a salt script that fits your need.
