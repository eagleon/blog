---
layout: post
title: redmine安装手记
categories:
- learn
tags:
- Ruby
- Web
- Linux
- bug
---



##1. 升级ruby：
ruby在CentOS 5上的默认版本是1.8.5. 需要先升级。
首先删除已经安装的Ruby：
{% highlight bash %}
sudo yum erase ruby ruby-libs ruby-mode ruby-rdoc ruby-irb ruby-ri ruby-docs
{% endhighlight %}
安装编译需要的相关工具和包：
{% highlight bash %}
sudo yum install openssl-devel zlib-devel gcc gcc-c++ make autoconf readline-devel curl-devel expat-devel gettext-devel  
{% endhighlight %}
下载Ruby1.9.2安装：
{% highlight bash %}
wget http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-p180.tar.gz  
tar xvf ruby-1.9.2-p180.tar.gz 
./configure --enable-shared --enable-pthread  
make && make install  
{% endhighlight %}
注:ruby升级过程http://ritto.blog.51cto.com/427838/737824  

##2. 安装RubyGems：
1.9.2 已经包含RubyGems，所以不需要安装。但是若是1.8.7等等，则需要安装。
{% highlight bash %}
wget http://rubyforge.org/frs/download.php/74445/rubygems-1.6.2.tgz  
tar zxvf rubygems-1.6.2.tgz   
cd rubygems-1.6.2   
ruby setup.rb  
{% endhighlight %}
注：gem更新 gem update --system

##3. 下载：
{% highlight bash %}
wget http://rubyforge.org/frs/download.php/76134/redmine-2.0.0.tar.gz
{% endhighlight %}

##4. 安装Mysql相关：
（推荐使用http://lnmp.org/ 一键安装包，懒人专用）  
{% highlight bash %}
yum install mysql mysql-devel mysql-server  
chkconfig --levels 235 mysqld on  
/etc/init.d/mysqld start  
{% endhighlight %}

##5. 安装相关包：
{% highlight bash %}
gem install bundler
bundle install --without development test
{% endhighlight %}

##6. config database.yml
Copy config/database.yml.example to config/database.yml and edit this file in order to configure your database settings for "production" environment.

##7. Generate a session store secret.
 rake generate_secret_token
##8. Create the database structure, by running the following command under the application root directory:
RAILS_ENV=production rake db:migrate

##9. Insert default configuration data in database, by running the following command:
RAILS_ENV=production rake redmine:load_default_data

##10.Test the installation by running WEBrick web server:
    ruby script/rails server webrick -e production
##11. Use default administrator account to log in:
login: admin  
password: admin  




##参考：  
1.http://blog.csdn.net/wangxujun163163/article/details/6417894  
2.http://www.cnblogs.com/wuchang/archive/2011/10/04/2199018.html  
3.http://www.redmine.org/projects/redmine/wiki/RedmineInstall  