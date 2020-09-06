---
layout: post
title: 跳板机ssh开发与调试
tags:
  - howto
  - network
date: 2020-09-02 17:40 +0800
hero: https://source.unsplash.com/collection/430471/
overlay: blue
published: true
---

# 1. ssh免秘钥登录
<!–-break-–>

{% highlight shell %}
cd .ssh
scp id_rsa.pub  <目标机器用户名>@<目标机器ip>:~

#如果没有authorized_keys文件
touch authorized_keys
chmod 600 authorized_keys

cat id_rsa.pub >> authorized_keys
{% endhighlight %}

# 2. 跳板机配置

[参考](https://www.jianshu.com/p/8f262bc444f0)



