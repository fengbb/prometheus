# 监控数据可视化

Prometheus UI提供了快速验证PromQL以及临时可视化支持的能力，而在大多数场景下引入监控系统通常还需要构建可以长期使用的监控数据可视化面板（Dashboard）。这时用户可以考虑使用第三方的可视化工具如Grafana，Grafana是一个开源的可视化平台，并且提供了对Prometheus的完整支持。

```text
docker run -d -p 3000:3000 grafana/grafana
```

访问[http://localhost:3000](http://localhost:3000)就可以进入到Grafana的界面中，默认情况下使用账户admin/admin进行登录。在Grafana首页中显示默认的使用向导，包括：安装、添加数据源、创建Dashboard、邀请成员、以及安装应用和插件等主要流程:

![Grafana&#x5411;&#x5BFC;](../../../.gitbook/assets/get_start_with_grafana2.png)

这里将添加Prometheus作为默认的数据源，如下图所示，指定数据源类型为Prometheus并且设置Prometheus的访问地址即可，在配置正确的情况下点击“Add”按钮，会提示连接成功的信息：

![&#x6DFB;&#x52A0;Prometheus&#x4F5C;&#x4E3A;&#x6570;&#x636E;&#x6E90;](../../../.gitbook/assets/add_default_prometheus_datasource.png)

在完成数据源的添加之后就可以在Grafana中创建我们可视化Dashboard了。Grafana提供了对PromQL的完整支持，如下所示，通过Grafana添加Dashboard并且为该Dashboard添加一个类型为“Graph”的面板。 并在该面板的“Metrics”选项下通过PromQL查询需要可视化的数据：

![&#x7B2C;&#x4E00;&#x4E2A;&#x53EF;&#x89C6;&#x5316;&#x9762;&#x677F;](../../../.gitbook/assets/first_grafana_dashboard.png)

点击界面中的保存选项，就创建了我们的第一个可视化Dashboard了。 当然作为开源软件，Grafana社区鼓励用户分享Dashboard通过[https://grafana.com/dashboards](https://grafana.com/dashboards)网站，可以找到大量可直接使用的Dashboard：

![&#x7528;&#x6237;&#x5171;&#x4EAB;&#x7684;Dashboard](../../../.gitbook/assets/grafana_dashboards.png)

Grafana中所有的Dashboard通过JSON进行共享，下载并且导入这些JSON文件，就可以直接使用这些已经定义好的Dashboard：

![Host Stats Dashboard](../../../.gitbook/assets/node_exporter_dashboard.png)

