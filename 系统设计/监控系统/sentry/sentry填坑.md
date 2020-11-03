sentry踩坑记

无法发送邮件

安装之后，配置告警，触发告警并邮件，发现邮件没有正常收到，查看smtp设置如下图所示，发现都是未设置。

![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=f5b24299dde95bd5d06e9a03c449342a_8f118824ce50c961_boxk4A7HENqM7SDNP0vbRfhZRIg_E6e9w0XO1srvFD17psjc2OajJA2lv4LQ)

此时需要在 sentry/config.yml 中做配置。

期间遇到了问题如下：

1. 端口配置错误
2. 没有开启smtp服务
3. 密码错误

我们以后遇到类似问题可以先写下简单的脚本验证远程服务是否正常

```
#coding: utf-8  
import smtplib
from email.mime.text import MIMEText
from email.header import Header
sender = 'tuqifei111@126.com'
receiver = 'tuqifei111@126.com'
subject = 'python email test'
smtpserver = 'smtp.126.com:25'
username = 'tuqifei111@126.com'
password = 'xxxx'
msg = MIMEText( 'Hello Python', 'text', 'utf-8' )
msg['Subject'] = Header( subject, 'utf-8' )
smtp = smtplib.SMTP()
smtp.connect( smtpserver )
smtp.login( username, password )
smtp.sendmail( sender, receiver, msg.as_string() )
smtp.quit()
```

然后 上面的脚本跑通了，但是依旧无法由sentry 发送邮件，报的错误是和dns解析有关的，然后进入对应的容器 sentry_onpremise_smtp_1 去看下dns解析是否由问题。

进入容器后，执行ping

```
bash: ping: command not found
```

然而 居然没有 ping 命令

想装 apt-get install ,也报 temporary failure resolving '[deb.debian.org](http://deb.debian.org)'

后来通过查询下面的网址解决了，原因就是没有dnsserver，配置了了下，发现也没有好

https://askubuntu.com/questions/91543/apt-get-update-fails-to-fetch-files-temporary-failure-resolving-error

最后的解决办法：

修改 宿主机中的 /etc/systemd/resolved.conf  的 dns

```
[Resolve]
DNS=8.8.8.8
```

最后测试成功！