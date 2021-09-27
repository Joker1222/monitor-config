# Grafana 安装部署

[官方安装教程](https://grafana.com/grafana/download)

> 以下演示Debian或CentOS系统的安装方式

~~~bash
$ apt-get install -y adduser libfontconfig1 #安装依赖
$ wget https://dl.grafana.com/oss/release/grafana_7.3.4_amd64.deb
$ dpkg -i grafana_7.3.4_amd64.deb
$ /etc/init.d/grafana-server start  #启动grafana
~~~

**默认端口3000** <br>
打开浏览器验证 <br>
http://IP:3000/ 

![Grafana Show png](../png/GrafanaLoginShow.png)
