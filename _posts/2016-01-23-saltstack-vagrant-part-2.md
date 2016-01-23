---
layout: post
title: SaltStack Vagrant Part 2
tags: [Salt, Configuration-Management, Vagrant]
---

![saltStack]({{ site.baseurl }}/images/2016011600.png "saltStack")

Last week we talked about creating a simple httpd service when we spin up our vagrant VM. This week I will continue to talk more about Salt.

### Inside The Vagrant Virtual Machine
Salt run in `/srv/` folder in our VM. Therefore our folder structure in virtual machine will look like this.

```
- /srv/
  - pillar/  # Unlike state tree, pillar data is only available for the targeted minion specified by the matcher type.
  - salt/  # All the configuration for the minion to run
- /etc/salt/
    - minion  #minion configuration
    - master  #master configuration
```

### Running in Master-less vs Master mode
- Master-less mode

```
salt-call --local state.highstate
```
- Master mode: salt-minion need to accept the salt-key first

```
salt '*' state.highstate
```

For running vagrant, we use master-less mode, the different between master mode and master-less mode shouldn't be large.

### Objective
To create user(s) base on pillar files, uninstall httpd and install nginx

### Coding
- Vagrantfile: mount the desired folder to your VM

```
config.vm.synced_folder "salt/root/", "/srv/salt/"
config.vm.synced_folder "salt/pillar/", "/srv/pillar/"
```
- /srv/pillar/users/init.sls: Sensitive user data

```
users:
    henglim.ng:
        uid: 1000
        fullname: Heng Lim Ng
        groups:
            - wheel
```
- /srv/pillar/top.sls: Include any new pillar data here

```
base:
  '*':
    - users
```
- /srv/salt/top.sls: the list of action we want to perform in env 'base', according to our objective

```
base:
  '*':
    - httpd.absent
    - user.top
    - nginx.init
```
- /srv/salt/user/top.sls: make use of our pillar users

```
{% raw %}
{% for username, user in pillar.get('users', {}).items() %}
{{username}}:
  user.present:
    - fullname: {{user.fullname}}
    - shell: /bin/bash
    - home: /home/{{username}}
    - groups: {{user.groups}}
{% endfor %}
{% endraw %}
```
- /srv/salt/httpd/absent.sls: make sure we uninstalled the httpd that we have installed

```
httpd:               # ID declaration
  pkg.removed: []

/var/www/html/index.html:
  file.absent: []
```
- /srv/salt/nginx/init.sls: yum search for `nginx`, if found, install `nginx` and enable it.

```
nginx:               # ID declaration
  pkg.installed: []
  service.running:
    - enable: True
```

### To Be Continue
In this post I mainly described how to make use of pillar to manage our VM user, uninstalling and installing of services using yum packages. Stay tuned for the SaltStack Vagrant Part 3.
