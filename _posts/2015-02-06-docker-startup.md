---
layout: post
title: Docker入门使用
categories:
- learn
tags:
- docker
- git
- 虚拟机
- 云
---

> 进度：50%

##序
Docker 虚拟化
   

##1.安装docker和fig
docker安装Linux内核需要3.8以上，Ubuntu 12.04等需要升级后才可以安装。
{% highlight bash %}
sudo sh -c "echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
sudo apt-get update
sudo apt-get install linux-image-generic-lts-raring linux-headers-generic-lts-raring
sudo apt-get install lxc-docker
sudo apt-get install python-pip
sudo pip install -U fig
{% endhighlight %}
重启系统：更新内核后，需要重启。

终端中输入docker，打印出docker的命令列表：  
{% highlight bash %}
Commands:
    attach    Attach to a running container
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    cp        Copy files/folders from a container's filesystem to the host path
    create    Create a new container
    diff      Inspect changes on a container's filesystem
    events    Get real time events from the server
    exec      Run a command in a running container
    export    Stream the contents of a container as a tar archive
    history   Show the history of an image
    images    List images
    import    Create a new filesystem image from the contents of a tarball
    info      Display system-wide information
    inspect   Return low-level information on a container
    kill      Kill a running container
    load      Load an image from a tar archive
    login     Register or log in to a Docker registry server
    logout    Log out from a Docker registry server
    logs      Fetch the logs of a container
    port      Lookup the public-facing port that is NAT-ed to PRIVATE_PORT
    pause     Pause all processes within a container
    ps        List containers
    pull      Pull an image or a repository from a Docker registry server
    push      Push an image or a repository to a Docker registry server
    restart   Restart a running container
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    save      Save an image to a tar archive
    search    Search for an image on the Docker Hub
    start     Start a stopped container
    stop      Stop a running container
    tag       Tag an image into a repository
    top       Lookup the running processes of a container
    unpause   Unpause a paused container
    version   Show the Docker version information
    wait      Block until a container stops, then print its exit code
{% endhighlight %}

##2. 配置系统参数

{% highlight bash %}
#0) 把ubuntu用户添加docker分组下，不然每次使用docker命令都要sudo，很麻烦
sudo gpasswd -a ubuntu docker

#如果fig up的时候出现：
$ fig up
Couldn't connect to Docker daemon at http:/ - is it running?

If it's at a non-standard location, specify the URL with the DOCKER_HOST environment variable.
#则按照下面步骤配置一下

#1) Change the DOCKER_OPTS in /etc/default/docker to:
DOCKER_OPTS="-H tcp://127.0.0.1:4243 -H unix:///var/run/docker.sock"

#2) Restart docker
sudo restart docker

#3) Make sure that docker is running on localhost:4243 
$ netstat -ant  |grep 4243
tcp        0      0 127.0.0.1:4243          0.0.0.0:*               LISTEN

#4) Set DOCKER_HOST (.bashrc)
export DOCKER_HOST=tcp://localhost:4243


{% endhighlight %}


##3. 拉取镜像
使用docker images可以查看现在所有的可用image

下载Ubuntu镜像
{% highlight bash %}
sudo docker pull ubuntu
sudo docker run ubuntu /bin/echo hello world
{% endhighlight %}

##4. 使用fig
使用Flask配合Redis配合测试：


> requirements.txt
{% highlight python %}
flask
redis
{% endhighlight %}

> app.py
{% highlight python %}
from flask import Flask
from redis import Redis
import os
app = Flask(__name__)
redis = Redis(host='redis', port=6379)

@app.route('/')
def hello():
    redis.incr('hits')
    return 'Hello World! I have been seen %s times.' % redis.get('hits')

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True)
We define our Python dependencies in a fi
{% endhighlight %}


> Dockerfile
{% highlight bash %}
FROM python:2.7
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
{% endhighlight %}

> fig.yml
{% highlight bash %}
web:
  build: .
  command: python app.py
  ports:
   - "5000:5000"
  volumes:
   - .:/code
  links:
   - redis
redis:
  image: redis
{% endhighlight %}


开启：fig up 查看是否成功   
![fig up](/media/image/2015-2-6-fig-up.png)  

![查看5000端口](/media/image/2015-2-6-5000.png)  


fig up -d 以daemon 的方式启动，在后台运行。   
fig ps 查看现在运行的情况   
fig stop 停止    


##Ref:
[Docker实践3：fig搭建mediawiki](http://blog.csdn.net/lincyang/article/details/43451043)   
[利用Docker构建开发环境](http://tech.uc.cn/?p=2726)      
[Docker镜像文件（images）的存储结构](http://liubin.org/2014/03/10/about-docker-images-storage/)   
[Docker教程中文版本](http://www.widuu.com/docker/index.html)   
[Docker中文指南](http://www.widuu.com/chinese_docker/)   
[Docker使用基本教程](http://docker.widuu.com/)   
[Docker学习笔记之一，搭建一个JAVA Tomcat运行环境](http://www.blogjava.net/yongboy/archive/2013/12/12/407498.html)   