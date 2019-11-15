# 容器监控：cAdvisor

Docker是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的Linux/Windows/Mac机器上。容器镜像正成为一个新的标准化软件交付方式。

例如，可以通过以下命令快速在本地启动一个Nginx服务：

```text
docker run -itd nginx
```

为了能够获取到Docker容器的运行状态，用户可以通过Docker的stats命令获取到当前主机上运行容器的统计信息，可以查看容器的CPU利用率、内存使用量、网络IO总量以及磁盘IO总量等信息。

```text
$ docker stats
CONTAINER           CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
9a1648bec3b2        0.30%               196KiB / 3.855GiB     0.00%               828B / 0B           827kB / 0B          1
```

除了使用命令以外，用户还可以通过Docker提供的HTTP API查看容器详细的监控统计信息。

## 使用CAdvisor

CAdvisor是Google开源的一款用于展示和分析容器运行状态的可视化工具。通过在主机上运行CAdvisor用户可以轻松的获取到当前主机上容器的运行统计信息，并以图表的形式向用户展示。

在本地运行CAdvisor也非常简单，直接运行一下命令即可：

```text
docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  google/cadvisor:latest
```

通过访问[http://localhost:8080](http://localhost:8080)可以查看，当前主机上容器的运行状态，如下所示：

![CAdvisor&#x53EF;&#x89C6;&#x5316;&#xFF1A;CPU&#x603B;&#x91CF;](../../../.gitbook/assets/cadvisor-total-usage.png)

CAdvisor是一个简单易用的工具，相比于使用Docker命令行工具，用户不用再登录到服务器中即可以可视化图表的形式查看主机上所有容器的运行状态。

而在多主机的情况下，在所有节点上运行一个CAdvisor再通过各自的UI查看监控信息显然不太方便，同时CAdvisor默认只保存2分钟的监控数据。好消息是CAdvisor已经内置了对Prometheus的支持。访问[http://localhost:8080/metrics](http://localhost:8080/metrics)即可获取到标准的Prometheus监控样本输出:

```text
# HELP cadvisor_version_info A metric with a constant '1' value labeled by kernel version, OS version, docker version, cadvisor version & cadvisor revision.
# TYPE cadvisor_version_info gauge
cadvisor_version_info{cadvisorRevision="1e567c2",cadvisorVersion="v0.28.3",dockerVersion="17.09.1-ce",kernelVersion="4.9.49-moby",osVersion="Alpine Linux v3.4"} 1
# HELP container_cpu_load_average_10s Value of container cpu load average over the last 10 seconds.
# TYPE container_cpu_load_average_10s gauge
container_cpu_load_average_10s{container_label_maintainer="",id="/",image="",name=""} 0
container_cpu_load_average_10s{container_label_maintainer="",id="/docker",image="",name=""} 0
container_cpu_load_average_10s{container_label_maintainer="",id="/docker/15535a1e09b3a307b46d90400423d5b262ec84dc55b91ca9e7dd886f4f764ab3",image="busybox",name="lucid_shaw"} 0
container_cpu_load_average_10s{container_label_maintainer="",id="/docker/46750749b97bae47921d49dccdf9011b503e954312b8cffdec6268c249afa2dd",image="google/cadvisor:latest",name="cadvisor"} 0
container_cpu_load_average_10s{container_label_maintainer="NGINX Docker Maintainers <docker-maint@nginx.com>",id="/docker/f51fd4d4f410965d3a0fd7e9f3250218911c1505e12960fb6dd7b889e75fc114",image="nginx",name="confident_brattain"} 0
```

下面表格中列举了一些CAdvisor中获取到的典型监控指标：

| 指标名称 | 类型 | 含义 |
| :--- | :--- | :--- |
| container\_cpu\_load\_average\_10s | gauge | 过去10秒容器CPU的平均负载 |
| container\_cpu\_usage\_seconds\_total | counter | 容器在每个CPU内核上的累积占用时间 \(单位：秒\) |
| container\_cpu\_system\_seconds\_total | counter | System CPU累积占用时间（单位：秒） |
| container\_cpu\_user\_seconds\_total | counter | User CPU累积占用时间（单位：秒） |
| container\_fs\_usage\_bytes | gauge | 容器中文件系统的使用量\(单位：字节\) |
| container\_fs\_limit\_bytes | gauge | 容器可以使用的文件系统总量\(单位：字节\) |
| container\_fs\_reads\_bytes\_total | counter | 容器累积读取数据的总量\(单位：字节\) |
| container\_fs\_writes\_bytes\_total | counter | 容器累积写入数据的总量\(单位：字节\) |
| container\_memory\_max\_usage\_bytes | gauge | 容器的最大内存使用量（单位：字节） |
| container\_memory\_usage\_bytes | gauge | 容器当前的内存使用量（单位：字节 |
| container\_spec\_memory\_limit\_bytes | gauge | 容器的内存使用量限制 |
| machine\_memory\_bytes | gauge | 当前主机的内存总量 |
| container\_network\_receive\_bytes\_total | counter | 容器网络累积接收数据总量（单位：字节） |
| container\_network\_transmit\_bytes\_total | counter | 容器网络累积传输数据总量（单位：字节） |

## 与Prometheus集成

修改/etc/prometheus/prometheus.yml，将cAdvisor添加监控数据采集任务目标当中：

```yaml
- job_name: cadvisor
  static_configs:
  - targets:
    - localhost:8080
```

启动Prometheus服务:

```text
prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/data/prometheus
```

启动完成后，可以在Prometheus UI中查看到当前所有的Target状态：

![Target](../../../.gitbook/assets/prometheus_targetes_with_cadvisor.png)

当能够正常采集到cAdvisor的样本数据后，可以通过以下表达式计算容器的CPU使用率：

```text
sum(irate(container_cpu_usage_seconds_total{image!=""}[1m])) without (cpu)
```

![&#x5BB9;&#x5668;CPU&#x4F7F;&#x7528;&#x7387;](../../../.gitbook/assets/promql_container_cpu_usage.png)

查询容器内存使用量（单位：字节）:

```text
container_memory_usage_bytes{image!=""}
```

查询容器网络接收量速率（单位：字节/秒）：

```text
sum(rate(container_network_receive_bytes_total{image!=""}[1m])) without (interface)
```

![&#x5BB9;&#x5668;&#x7F51;&#x7EDC;&#x63A5;&#x6536;&#x91CF; &#x5B57;&#x8282;/&#x79D2;](../../../.gitbook/assets/container_network_receive_bytes_total.png)

查询容器网络传输量速率（单位：字节/秒）：

```text
sum(rate(container_network_transmit_bytes_total{image!=""}[1m])) without (interface)
```

![&#x5BB9;&#x5668;&#x7F51;&#x7EDC;&#x4F20;&#x8F93;&#x91CF; &#x5B57;&#x8282;/&#x79D2;](../../../.gitbook/assets/container_network_transmit_bytes_total.png)

查询容器文件系统读取速率（单位：字节/秒）：

```text
sum(rate(container_fs_reads_bytes_total{image!=""}[1m])) without (device)
```

![&#x5BB9;&#x5668;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x8BFB;&#x53D6;&#x901F;&#x7387; &#x5B57;&#x8282;/&#x79D2;](../../../.gitbook/assets/container_fs_reads_bytes_total.png)

查询容器文件系统写入速率（单位：字节/秒）：

```text
sum(rate(container_fs_writes_bytes_total{image!=""}[1m])) without (device)
```

![&#x5BB9;&#x5668;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x5199;&#x5165;&#x901F;&#x7387; &#x5B57;&#x8282;/&#x79D2;](../../../.gitbook/assets/container_fs_writes_bytes_total.png)

