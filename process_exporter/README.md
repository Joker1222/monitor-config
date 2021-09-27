# Process_exporter 安装部署

[官方下载地址](https://github.com/ncabatoff/process-exporter/releases/download/)

> process-exporter是监控某个进程性能数据的,数据源和top命令差不多,解压后需要额外配置下你要监控的进程,按名称匹配即可 note:建议存放在/opt目录下

~~~bash
$ cd /opt/ && wget https://github.com/Joker1222/monitor-config/raw/master/process_exporter/process-exporter-0.7.5.linux-386.tgz
$ cd /opt && tar zxvf process-exporter-0.7.5.linux-386.tgz && mv process-exporter-0.7.5.linux-386 process_exporter
$ cd /opt/process_exporter/ && ./run.sh start
~~~

### 配置简易说明

~~~bash
$ vim /opt/process_exporter/process-name.yaml
process_names:
  - name: "{{.Matches}}" # 每新加一个进程就填这三行
    cmdline:
    - 'loginserver1'     # 这里就是匹配索引了,按照名称匹配!注意,如果启动进程有重名可能导致监控失败

  - name: "{{.Matches}}"
    cmdline:
    - 'gateserver1'
$ cd /opt/process_exporter/ && ./run.sh restart  # 保存后重启
~~~
