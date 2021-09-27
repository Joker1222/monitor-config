# Node_Exporter 安装部署

[官方下载地址](https://prometheus.io/download/)

> node_exporter是监控整机性能数据的,没什么特殊配置,解压后直接./run.sh start运行即可,开箱即用! note:建议存放在/opt目录下

~~~bash 
$ cd /opt && wget https://github.com/Joker1222/Personal-Server-Monitor/raw/master/node_exporter/node_exporter-1.0.1.linux-amd64.tgz
$ cd /opt && tar zxvf node_exporter-1.0.1.linux-amd64.tgz && mv node_exporter-1.0.1.linux-amd64 node_exporter
$ cd /opt/node_exporter && ./run.sh start
~~~

