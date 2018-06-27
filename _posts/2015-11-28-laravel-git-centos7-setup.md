---
layout: post
title: Laravel Git CentOS 7 Setup
tags: [PHP]
---

![Laravel]({{ site.baseurl }}/images/2015112800.jpg "Laravel")

### Laravel
Laravel currently is the most popular PHP framework. With the news that PHP 7 is going to release on December the 3th, I'll expect a spike in usage of laravel usage. PHP 7 is definitely the best tool for developing web application quickly.

### Setup
The below setup will be using Apache + Laravel approach, as nginx + PHP-FPM seems to have potential memory leak problem.

at your remote server

~~~ bash
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum install httpd php56w php56w-mysqlnd mariadb-server php56w-mcrypt php56w-dom php56w-mbstring
curl  -k -sS https://getcomposer.org/installer | php

mv composer.phar /usr/local/bin/composer

composer create-project laravel/laravel=5.1 /var/www/laravel --prefer-dist

sudo vim /vagrant/provisioner_utils/laravel.conf
  NameVirtualHost *:80
  <VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName your.localhost.com
    ServerAlias your.localhost.com
    DocumentRoot /var/www/laravel/public/
    <Directory /var/www/laravel>
    	AllowOverride All
    </Directory>
  </VirtualHost>

cd /var
mkdir repo && cd repo
mkdir site.git && cd site.git
git init --bare

cat > post-receive
#!/bin/sh
git --work-tree=/var/www/laravel --git-dir=/var/repo/site.git checkout -f
~~~

at your local desktop

~~~ bash
git init
git remote add live ssh://username@your.localhost.com/var/repo/site.git
git add .
git commit -m "Initial commit"
git push live master
~~~

### Conclusion
With this setup, we can easily test our code inside our VM.
