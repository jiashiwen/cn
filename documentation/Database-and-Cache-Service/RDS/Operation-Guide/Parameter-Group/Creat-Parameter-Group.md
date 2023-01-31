# 创建参数组
云数据库 MySQL/Percona/MariaDB/PostgreSQL 在创建的时候，需要指定一个参数组，作为数据库引擎的启动配置。新建的数据库，根据其创建时候选择的数据库类型和版本，系统会初始化一套系统默认的参数列表。如果您需要自定义参数的运行值，可以参考 [修改参数](Modify-Parameter-Group.md)

## 注意事项
* 每一个地域最多可以创建 20 个参数组。
* 不同数据库类型和版本的参数组的默认参数列表是不一样的。
* 云数据库 MySQL/Percona/MariaDB/PostgreSQL 选择绑定的参数组，两者的数据库类型和版本必须一致。

## 操作步骤
1. 登录 [参数组控制台](https://rds-console.jdcloud.com/paramgroup/list)
2. 在参数组列表页，点击 **创建** 按钮，进入 **创建参数组** 弹出框
3. 弹出框参数说明如下：
   |参数|说明|
   |--|--|
   |数据库类型|选择需要创建参数组的数据库类型|
   |数据库版本|选择参数组所归属的数据库版本|
   |名称|参数组的名称，长度不超过32个字符|
   |描述|对于参数组的描述，长度不超过64个字符|
    > 注意：不同实例参数略有不同，因此参数组需与实例类型及版本对应。
   
    ![截图](../../../image/RDS/create-parameter-group.png)

4.单击 **确定** 按钮，创建参数组成功，返回到参数组列表页。

## 相关API
创建参数组：[createParameterGroup](https://docs.jdcloud.com/cn/rds/api/createparametergroup)
查看参数列表：[describeParameterGroups
](https://docs.jdcloud.com/cn/rds/api/describeparametergroups)