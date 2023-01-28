# 拷贝参数组
考虑到便利性，如果您想基于当前参数组重新生产一个新的参数组，可通过参数组拷贝实现。

## 注意事项

* 拷贝的参数组无法修改数据库类型和版本。
* 拷贝的参数组，会同步源参数组的参数修改历史记录。

## 操作步骤

1. 登录 [参数组控制台](https://rds-console.jdcloud.com/paramgroup/list)。
2. 在参数组列表页，选择需要拷贝的源参数组，点击 **操作** 的 **拷贝** 按钮，出现拷贝参数组弹出框。
3. 输入参数组名称及备注，点击确定完成参数组拷贝。

    ![截图](https://img1.jcloudcs.com/cms/604bf122-ce51-44f0-9835-c0a7fbf3428220180815094448.png)

## 相关API
拷贝参数组：[copyParameterGroup](https://docs.jdcloud.com/cn/rds/api/copyparametergroup)
