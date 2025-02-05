
# 创建集群

**创建Kubernetes集群操作说明**

 1. 创建集群时默认创建一个工作节点组；
 2. 工作节点组基于高可用组创建，工作节点将在对应的高可用组内均匀分布，以降低单个可用区出现物理故障时对您业务的影响；
 3. 管理节点CIDR不可与工作节点CIDR重叠；
 4. 工作节点CIDR在已选择的私有网络内分配，请尽量选择一个新建的私有网络部署Kubernetes集群;
 5. 对于Kubernetes集群自动创建的相关资源如云主机、云硬盘、弹性公网IP、负载均衡，还请不要对单个资源的产品进行删除、修改名称等操作。

**创建集群步骤**

   具体还请参考[创建Kubernetes集群](https://docs.jdcloud.com/cn/jcs-for-kubernetes/create-to-cluster)。
   

**创建Serverless集群步骤**

  具体还请参考[创建Serverless集群](https://docs.jdcloud.com/cn/jcs-for-kubernetes/create-serverless-cluster)。
