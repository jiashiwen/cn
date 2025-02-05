# 绑定合作安全组
您可以在实例创建时绑定合作安全组，也可以在实例创建之后单独为实例绑定合作安全组，或者在修改实例的私有网络配置时绑定合作安全组。

## 前提条件及限制
* 实例的每块网卡至少绑定一个、至多绑定五个合作安全组。
* 实例仅允许绑定相同合作私有网络内的合作安全组，即针对实例的网卡，若需要绑定多个合作安全组，则该多个合作安全组需属于同一合作私有网络。

## 操作影响
实例绑定合作安全组后 ，合作安全组的规则对实例立即生效。

## 操作步骤
为已创建的实例绑定合作安全组操作步骤如下：
1. 访问[合作云主机控制台](https://coccns-console.jdcloud.com/host/compute/list)，即进入实例列表页面。或访问[京东云控制台](https://console.jdcloud.com)点击顶部导航栏**合作云产品-合作云主机**进入实例列表页。
2. 选择地域。
3. 在实例列表中选择需要绑定合作安全组的实例，点击名称进入详情页。
4. 点击**安全组Tab-添加**按钮。
5. 在弹出弹窗中，选择一个或多个安全组，点击**确定**。<br>

![image](https://user-images.githubusercontent.com/88134774/198301777-5118d7a6-e982-420b-887a-184e48b5eb90.png)



