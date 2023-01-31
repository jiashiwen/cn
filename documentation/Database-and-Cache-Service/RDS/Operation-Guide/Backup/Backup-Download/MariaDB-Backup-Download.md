# MariaDB 备份下载
当您想获取云数据库 MariaDB 实例的备份数据的时候，京东云提供了内网地址，外网地址供用户自行下载。

## 注意事项
* 内网地址，外网地址是有有效期的，如果超过了有效期地址会失效，需要点击下载按钮，才能生成下载弹出框，才能获取新地址。

## 下载数据备份
1. 登录 [云数据库 RDS 控制台](https://rds-console.jdcloud.com/database)。
2. 选择需要进行备份数据下载的目标实例，点击目标实例的名称，进入到实例详情页。
3. 选择 **备份管理** 标签，选择你要下载的备份数据，点击 **操作** 这一列的 **下载**。
4. 备份下载弹出框参数说明：
    * 地址有效期：内网地址，外网地址支持自定义有效期时间，超过设置的有效期时间后，相应的地址就会失效无法下载，最短可以支持 1 秒，最长不超过 24 小时。
    * 内网地址：提供内网访问的域名，比如可以通过和数据库实例在同一个 VPC 或者子网内的云主机访问这个地址，从而来下载备份数据。
    * 外网地址：提供公网访问的域名，可以通过互联网下载备份数据，下载速度受限于公网的网络带宽，所以如果你的公网网络带宽太小，并且备份文件太大的话，下载时间会比较长。
    * 点击 **本地下载** 按钮，直接通过浏览器的方式，下载备份数据。
    * 点击 **取消** 按钮，取消备份下载。

![backup](../../../../../../image/RDS/backup_download.jpg)

## 下载日志备份
1. 登录 [云数据库 RDS 控制台](https://rds-console.jdcloud.com/database)。
2. 选择需要进行备份数据下载的目标实例，点击目标实例的名称，进入到实例详情页。
3. 选择 **备份管理** 标签，切换至 **binlog** tab页，点击**操作**列的**下载**。

## 相关问题
1. 如何使用下载的备份文件？
您可以将本地盘实例下载的备份文件恢复至自建数据库，具体请参见[将备份恢复到自建MySQL](https://docs.jdcloud.com/cn/rds/restore-backup-to-self-built-mysql-database)。

## 相关API
下载数据备份：[describeBackupDownloadURL](https://docs.jdcloud.com/cn/rds/api/describebackupdownloadurl)
下载日志备份：[describeBinlogDownloadURL](https://docs.jdcloud.com/cn/rds/api/describebinlogdownloadurl)

