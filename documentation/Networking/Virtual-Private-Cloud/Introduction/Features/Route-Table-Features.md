# 路由表

## 基本概念

路由表是一系列路由规则的集合，用于控制私有网络中子网的流量流出路径。京东云共有两种类型的路由表：默认路由表和自定义路由表。随私有网络创建时自动创建的路由表为默认路由表，您自主创建的路由表为自定义路由表。每个子网都必须关联一张路由表且只能关联一张路由表，每张路由表可以关联多个子网，配额请参考[使用限制](../Restrictions.md)。

### 默认路由表

随私有网络创建时自动创建的路由表为默认路由表，默认路由表不可删除，默认路由表占用路由表的1个配额。默认路由表默认有两条路由策略：

- 用于VPC内网访问的Local规则，不支持编辑或删除；
- 用于Internet访问的Internet规则；支持编辑或删除
可在默认路由表上增加安全组规则。



### 自定义路由表

- 由用户主动创建的路由表为自定义路由表。自定义路由表默认有一条路由策略：用于VPC内网访问的Local规则；
- 已关联子网的自定义路由表不可删除；
- 自定义路由表的路由策略可编辑、可增加、可删除，默认的Local路由策略不可编辑、不可删除。


### 路由策略

路由表由一系列路由策略组成，路由策略用来控制子网中数据包的路由途径。每条路由策略包含三个参数：路由策略由路由的目的端、下一跳类型和下一跳地址组成，
|属性|说明|示例|
|:--------|:--------|:--------|
|目的端|目的网段描述（仅支持网段格式，如果希望目的端为单个 IP，可设置掩码为`32`（如：IPv4：`192.168.10.10/32`，IPv6:`2002::/128`），目的端若为路由表所在VPC内的网段时，则该条路由策略将被Local规则覆盖，数据包将按Local规则进行路由|10.0.1.41/24|
|下一跳类型|私有网络流量的出口，如Internet、云主机、VPC对等连接、NAT网关、[边界网关](https://docs.jdcloud.com/cn/direct-connection/border-gateway-features)、弹性网卡|Internet|
|下一跳|基于下一跳类型的下一跳路由实例|云主机实例、Internet|
|路由类型|包括静态路由和动态路由|默认为静态路由|

> 路由表支持弹性网卡功能处于灰度中，目前支持华东-上海地域，如需使用请提[工单申请](https://ticket.jdcloud.com/applyorder/submit)。

其中Internet用于公网访问，通过公网IP进行Internet通信的实例必须配置该条路由，云主机可作为公网网关使用，详见访问Internet，从控制台自定义的路由类型均为静态路由。
 

## 使用限制

- 所有路由表均包含一条默认 Local 路由策略，表示私有网络内网互通。其路由规则为 [ Local，Local，Local ]，该路由规则不可修改、不可删除。
- 每张路由表可以关联同一个VPC中的多个子网，每个子网能关联且只能关联一张路由表。您可以在子网侧更改关联的路由表，也能在路由表侧更改关联子网。
- 相同属性子网包含两种情况：
  a.相同地域的标准子网；
  b.相同地域关联相同边缘可用区的边缘子网；

- 路由表只能关联相同属性的子网，关联的子网都是标准子网或者都是相同[边缘可用区](../Region-Az.md)的边缘子网，不允许关联不同属性的子网；已关联标准子网的路由表，不能再关联边缘子网，已关联边缘子网的路由表，不能再关联标准子网，也不能关联不同边缘可用区的边缘子网。


## 路由传播

  路由传播是通过手动配置方式之外获取的路由规则，如通过内部工作机制将不同网关实体（如VPC路由表所在的路由网关、边界网关）的路由表项信息进行同步、自动更新到达或者经由彼此转发业务的路由信息。VPC路由表支持两种路由类型：动态传播路由与静态路由。静态路由策略可编辑，动态传播路由不可编辑、可查看。

**VPC路由表和边界网关路由表之间可实现双向路由动态传播**：

**边界网关-->VPC方向的路由传播**：当VPC路由表配置路由传播时，选择路由传播的源边界网关与填写路由传播范围。传播关系创建后，系统将自动把该边界网关有效路由表中、路由前缀在传播范围内的特定路由规则自动添加VPC路由表内，并且下一跳指向与该VPC创建传播关系的边界网关；

**VPC-->边界网关方向的路由传播**：当基于BGW创建VPC接口时，如果传播VPC网段选择“VPC全部网段”或者“指定子网网段”时，即为路由自动传播方式。边界网关路由表会依据配置的子网范围，自动添加或者删除到达相关子网的路由表项，路由前缀为子网网段、下一跳为连接指定VPC和边界网关的VPC接口。

### **路由策略优先级**

- 京东云VPC路由表优先级优先级范围为1~256，数值越小，路由优先级别越高。京东云VPC路由表的静态路由优先级缺省为100，传播路由优先级缺省为120。

- 当路由表中存在多条路由策略时，路由优先级由高至低分别为： Local路由>>最长前缀（掩码最长的前缀）匹配>>同样长度前缀、路由类型不同，则静态路由优于动态传播路由
    
- 同样长度前缀、路由类型相同(如同为传播路由、或同为静态路由)，则为等价路由，目前仅传播路由支持等价路由。

例如：私有网络内一云主机绑定了弹性 IP，同时又在关联了 NAT 网关的子网内（路由表中设置了该子网访问 Internet 流量的下一跳是 NAT 网关），那么该云主机访问 Internet 的流量会全部通过 NAT 网关实现，因为最精确路由的优先级高于公网 IP。

## 相关参考

- [配置路由表](../../Operation-Guide/Route-Table-Configuration.md)
- [使用限制](../Restrictions.md)
- [常见问题](../../FAQ/FAQ.md)
