# Introduction

慧聪文档



慧聪文档



* [全书组织](introduction.md)

## Part I - Prometheus基础

* [第1章 天降奇兵](parti-prometheus-ji-chu/quickstart/)
  * [Prometheus简介](parti-prometheus-ji-chu/quickstart/why-monitor.md)
  * [初识Prometheus](parti-prometheus-ji-chu/quickstart/prometheus-quick-start/)
    * [安装Prometheus Server](parti-prometheus-ji-chu/quickstart/prometheus-quick-start/install-prometheus-server.md)
    * [使用Node Exporter采集主机数据](parti-prometheus-ji-chu/quickstart/prometheus-quick-start/use-node-exporter.md)
    * [使用PromQL查询监控数据](parti-prometheus-ji-chu/quickstart/prometheus-quick-start/promql_quickstart.md)
    * [监控数据可视化](parti-prometheus-ji-chu/quickstart/prometheus-quick-start/use-grafana-create-dashboard.md)
  * [任务和实例](parti-prometheus-ji-chu/quickstart/prometheus-job-and-instance.md)
  * [Prometheus核心组件](parti-prometheus-ji-chu/quickstart/prometheus-arch.md)
  * [小结](parti-prometheus-ji-chu/quickstart/summary.md)
* [第2章 探索PromQL](parti-prometheus-ji-chu/promql/)
  * [理解时间序列](parti-prometheus-ji-chu/promql/what-is-prometheus-metrics-and-labels.md)
  * [Metrics类型](parti-prometheus-ji-chu/promql/prometheus-metrics-types.md)
  * [初识PromQL](parti-prometheus-ji-chu/promql/prometheus-query-language.md)
  * [PromQL操作符](parti-prometheus-ji-chu/promql/prometheus-promql-operators-v2.md)
  * [PromQL聚合操作](parti-prometheus-ji-chu/promql/prometheus-aggr-ops.md)
  * [PromQL内置函数](parti-prometheus-ji-chu/promql/prometheus-promql-functions.md)
  * [在HTTP API中使用PromQL](parti-prometheus-ji-chu/promql/prometheus-promql-with-http-api.md)
  * [最佳实践：4个黄金指标和USE方法](parti-prometheus-ji-chu/promql/prometheus-promql-best-praticase.md)
  * [小结](parti-prometheus-ji-chu/promql/summary.md)
* [第3章 Prometheus告警处理](parti-prometheus-ji-chu/alert/)
  * [Prometheus告警简介](parti-prometheus-ji-chu/alert/prometheus-alert-manager-overview.md)
  * [自定义Prometheus告警规则](parti-prometheus-ji-chu/alert/prometheus-alert-rule.md)
  * [部署AlertManager](parti-prometheus-ji-chu/alert/install-alert-manager.md)
  * [Alertmanager配置概述](parti-prometheus-ji-chu/alert/alert-manager-config.md)
  * [基于标签的告警处理路由](parti-prometheus-ji-chu/alert/alert-manager-route.md)
  * [使用Receiver接收告警信息](parti-prometheus-ji-chu/alert/alert-manager-use-receiver/)
    * [集成邮件系统](parti-prometheus-ji-chu/alert/alert-manager-use-receiver/alert-with-smtp.md)
    * [集成Slack](parti-prometheus-ji-chu/alert/alert-manager-use-receiver/alert-with-slack.md)
    * [集成企业微信](parti-prometheus-ji-chu/alert/alert-manager-use-receiver/alert-with-wechat.md)
    * [集成钉钉：基于Webhook的扩展](parti-prometheus-ji-chu/alert/alert-manager-use-receiver/alert-manager-extension-with-webhook.md)
  * [告警模板详解](parti-prometheus-ji-chu/alert/alert-template.md)
  * [屏蔽告警通知](parti-prometheus-ji-chu/alert/alert-manager-inhibit.md)
  * [使用Recoding Rules优化性能](parti-prometheus-ji-chu/alert/prometheus-recoding-rules.md)
  * [小结](parti-prometheus-ji-chu/alert/summary.md)

## Part II - Prometheus进阶

* [第4章 Exporter详解](part-ii-prometheus-jin-jie/exporter/)
  * [Exporter是什么](part-ii-prometheus-jin-jie/exporter/what-is-prometheus-exporter.md)
  * [常用Exporter](part-ii-prometheus-jin-jie/exporter/commonly-eporter-usage/)
    * [容器监控：cAdvisor](part-ii-prometheus-jin-jie/exporter/commonly-eporter-usage/use-prometheus-monitor-container.md)
    * [监控MySQL运行状态：MySQLD Exporter](part-ii-prometheus-jin-jie/exporter/commonly-eporter-usage/use-promethues-monitor-mysql.md)
    * [网络探测：Blackbox Exporter](part-ii-prometheus-jin-jie/exporter/commonly-eporter-usage/install_blackbox_exporter.md)
  * [使用Java自定义Exporter](part-ii-prometheus-jin-jie/exporter/custom_exporter_with_java/)
    * [使用Client Java构建Exporter程序](part-ii-prometheus-jin-jie/exporter/custom_exporter_with_java/client_library_java.md)
    * [在应用中内置Prometheus支持](part-ii-prometheus-jin-jie/exporter/custom_exporter_with_java/custom_app_support_prometheus.md)
  * [小结](part-ii-prometheus-jin-jie/exporter/summary.md)
* [第5章 数据与可视化](part-ii-prometheus-jin-jie/grafana/)
  * [使用Console Template](part-ii-prometheus-jin-jie/grafana/use-console-template.md)
  * [Grafana的基本概念](part-ii-prometheus-jin-jie/grafana/grafana-intro.md)
  * [Grafana与数据可视化](part-ii-prometheus-jin-jie/grafana/grafana-panels/)
    * [变化趋势：Graph面板](part-ii-prometheus-jin-jie/grafana/grafana-panels/use_graph_panel.md)
    * [分布统计：Heatmap面板](part-ii-prometheus-jin-jie/grafana/grafana-panels/use_heatmap_panel.md)
    * [当前状态：SingleStat面板](part-ii-prometheus-jin-jie/grafana/grafana-panels/use_singlestat_panel.md)
  * [模板化Dashboard](part-ii-prometheus-jin-jie/grafana/templating.md)
  * [小结](part-ii-prometheus-jin-jie/grafana/summary.md)
* [第6章 集群与高可用](part-ii-prometheus-jin-jie/readmd/)
  * [本地存储](part-ii-prometheus-jin-jie/readmd/prometheus-local-storage.md)
  * [远程存储](part-ii-prometheus-jin-jie/readmd/prometheus-remote-storage.md)
  * [联邦集群](part-ii-prometheus-jin-jie/readmd/scale-prometheus-with-federation.md)
  * [Prometheus高可用](part-ii-prometheus-jin-jie/readmd/prometheus-and-high-availability.md)
  * [Alertmanager高可用](part-ii-prometheus-jin-jie/readmd/alertmanager-high-availability.md)
  * [小结](part-ii-prometheus-jin-jie/readmd/summary.md)
* [第7章 Prometheus服务发现](part-ii-prometheus-jin-jie/sd/)
  * [Prometheus与服务发现](part-ii-prometheus-jin-jie/sd/why-need-service-discovery.md)
  * [基于文件的服务发现](part-ii-prometheus-jin-jie/sd/service-discovery-with-file.md)
  * [基于Consul的服务发现](part-ii-prometheus-jin-jie/sd/service-discovery-with-consul.md)
  * [服务发现与Relabel](part-ii-prometheus-jin-jie/sd/service-discovery-with-relabel.md)
  * [小结](part-ii-prometheus-jin-jie/sd/summary.md)

## Part III - Prometheus实战

* [第8章 监控Kubernetes](part-iii-prometheus-shi-zhan/readmd/)
  * [初识Kubernetes](part-iii-prometheus-shi-zhan/readmd/kubernetes-with-minikube.md)
  * [部署Prometheus](part-iii-prometheus-shi-zhan/readmd/deploy-prometheus-in-kubernetes.md)
  * [Kubernetes下的服务发现](part-iii-prometheus-shi-zhan/readmd/service-discovery-with-kubernetes.md)
  * [监控Kubernetes集群](part-iii-prometheus-shi-zhan/readmd/use-prometheus-monitor-kubernetes.md)
  * [基于Prometheus的弹性伸缩](part-iii-prometheus-shi-zhan/readmd/hap-with-prometheus.md)
  * [小结](part-iii-prometheus-shi-zhan/readmd/summary.md)
* [第9章 Prometheus Operator](part-iii-prometheus-shi-zhan/operator/)
  * [什么是Prometheus Operator](part-iii-prometheus-shi-zhan/operator/what-is-prometheus-operator.md)
  * [使用Operator管理Prometheus](part-iii-prometheus-shi-zhan/operator/use-operator-manage-prometheus.md)
  * [使用Operator管理监控配置](part-iii-prometheus-shi-zhan/operator/use-operator-manage-monitor.md)
  * [在Prometheus Operator中使用自定义配置](part-iii-prometheus-shi-zhan/operator/use-custom-configuration-in-operator.md)
  * [小结](part-iii-prometheus-shi-zhan/operator/summary.md)
* [参考资料](part-iii-prometheus-shi-zhan/references.md)

