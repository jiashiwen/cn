# 性能监控

## 概述

云物理服务器产品性能监控服务，支持不同监控维度，目前需要用户手动安装agent到已创建成功的实例，然后才能开始收集到用户的监控数据，以图标的方式更清晰的展示，让用户实时掌握资源的使用情况。<br/>
Windows系统实例暂不支持性能监控功能。<br/>

## 监控项

目前提供的监控项：CPU使用率、内存使用率、内存使用量、磁盘使用率、磁盘使用量、磁盘读流量、磁盘写流量、磁盘读IOPS、磁盘写IOPS、网卡进流量、网卡出流量、网络进包量、网络出包量、CPU平均负载1min、CPU平均负载5min、CPU平均负载15min、TCP总连接数、TCP正常连接数、总进程数。

## 监控数据说明

监控数据采集周期为1分钟；<br/>
统计周期默认支持1小时、6小时、12小时、1天、3天、7天及14天，此外还支持您设置统计周期，周期最长支持30天；<br/>
不同统计周期不同监控项会做对应的聚合；<br/>

## 安装Agent

curl [http://jdcps-proxy.jdcloud.com/agent/download/jdcps-agent-v2.0.0.bin](http://jdcps-proxy.jdcloud.com/agent/download/jdcps-agent-v2.0.0.bin) -O <br/>
chmod +x jdcps-agent-v2.0.0.bin<br/>
sudo ./jdcps-agent-v2.0.0.bin<br/>

说明：基础网络实例安装前准备工作如下：<br/>
基础网络实例增加路由<br/>
1、确定内网Gateway地址 route -n <br/>
查询eth0对应的Gateway地址（eg：10.123.0.1）<br/>
2、将监控流量引导到内网网关<br/>
route add -net 100.66.1.0 netmask 255.255.255.0 gw {机器内网网关地址}<br/>

## 卸载Agent

service jdcpsd stop <br/>
chkconfig --del jdcpsd <br/>
/bin/rm -f /etc/init.d/jdcpsd <br/>

## 监控数据说明

1、进入云物理服务器列表页，选择实例列表->基础网络实例/私有网络实例，选择所需要查看的实例，点击安装“监控插件”，按照如上描述操作，可安装成功，即可获取监控数据；<br/>
2、点击实例列表中的实例名称，进入资源信息页面，即可查看“Agent状态”。<br/>
3、点击实例列表中的监控图标，进入性能监控页面，即可查看服务器性能监控指标。<br/>



