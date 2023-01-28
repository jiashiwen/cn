# 限制说明

您可以快速创建并使用应用负载均衡，但使用中有部分约束条件需要注意。


| 资源	| 限制	| 例外申请方式 |
| :- | :- | :- |
|单地域下应用负载均衡实例	|5个	|工单|
|一个应用负载均衡下的监听器	|20个	|工单|
|一个应用负载均衡下的后端服务	|20个	|工单|
|一个应用负载均衡下的虚拟服务器组	|20个|	工单|
|一个虚拟服务器组内的实例	|100个|	工单|
|一个应用负载均衡下的转发规则组	|50个|	工单|
|一个转发规则组内的转发规则	|50个|	工单|
|一条转发规则可以配置的扩展动作数	|10个|	工单|
|一个应用负载均衡可绑定的安全组|4个|	无|
|一个监听器绑定的扩展证书项(不包括默认证书项)|25个|	工单|


## 相关参考

- [产品概述](../Introduction/Product-Overview.md)
- [价格总览](../Pricing/Price-Overview.md)
- [创建实例](../Getting-Started/Create-Instance.md)
- [虚拟服务器组管理](../Operation-Guide/TargetGroup-Management.md)
- [监听器管理](../Operation-Guide/Listener-Management.md)
- [管理后端服务与查看服务实例健康状态](../Operation-Guide/Backend-Management.md)
- [查看监控信息](../Operation-Guide/Monitoring.md)
