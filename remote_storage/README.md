# Prometheus数据化远程持久化存储方案
> 转自：https://yunlzheng.gitbook.io/prometheus-book/part-ii-prometheus-jin-jie/readmd/prometheus-remote-storage

## 使用Influxdb作为Remote Storage
> 步骤： docker启动influxdb --> 获取并启动Prometheus提供的Remote Storage Adapter --> 配置Prometheus远程存储相关内容

1. docker启动influxdb (docker这里默认已经安装好)<br>
~~~bash
$ cd /opt && wget https://raw.githubusercontent.com/Joker1222/Personal-Server-Monitor/master/remote_storage/docker-compose.yml
$ docker-compose up -d
~~~

2.获取并启动Prometheus提供的Remote Storage Adapter
~~~bash
$ cd /opt && wget https://github.com/Joker1222/Personal-Server-Monitor/raw/master/remote_storage/remote_storage_adapter
$ cd /opt && chmod 777 remote_storage_adapter && nohup ./remote_storage_adapter --influxdb-url=http://localhost:8086 --influxdb.username=prom --influxdb.database=prometheus --influxdb.retention-policy=autogen > remote.log &
~~~

3.修改Prometheus配置
~~~vim
remote_write:
  - url: "http://localhost:9201/write"

remote_read:
  - url: "http://localhost:9201/read"
~~~

4.检查结果
~~~bash
$ docker exec -it <CONTAINERID> influx #进入influx容器
$ Connected to http://localhost:8086 version 1.3.5
$ InfluxDB shell version: 1.3.5
> auth
username: prom
password:

> use prometheus
> SHOW MEASUREMENTS  #到这一步有内容就代表成功了
name: measurements
name
----
go_gc_duration_seconds
go_gc_duration_seconds_count
go_gc_duration_seconds_sum
go_goroutines
go_info
go_memstats_alloc_bytes
go_memstats_alloc_bytes_total
go_memstats_buck_hash_sys_bytes
go_memstats_frees_total
go_memstats_gc_cpu_fraction
go_memstats_gc_sys_bytes
go_memstats_heap_alloc_bytes
go_memstats_heap_idle_bytes
~~~

~~~bash
####!!!!!!!!!!!!!!!!!!!!!!!!!! 谨慎一点！别把以前的重要数据给删了
$ cd /opt/prometheus && ./run.sh stop && rm data -rvf #删除本地data文件，然后重启，观察是否能够从influxdb中恢复数据
~~~
