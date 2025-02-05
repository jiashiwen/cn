# 上传备份并授权
本文档将描述如何将备份文件上传到对象存储OSS中，并设置合适的权限，以便SQL Server 服务可以正确访问备份文件并且将备份导入到云数据库 SQL Server中。

#### 1. 进入对象存储的空间管理页面

进入控制台中的 **对象存储** ，点击 **空间管理**。

![上传备份1](../../../../../../image/RDS/Upload-Backup-V2-1.png)

#### 2. 选择对象存储空间
点击空间名称，进入要上传文件的空间

![上传备份2](../../../../../../image/RDS/Upload-Backup-V2-2.png)

#### 3. 上传文件
选择 **Object管理** 页面，根据需要点击 **上传** 或者 **新建文件夹**

>  注意：控制台上传单个文件大小不超过 5GB，如需上传更大的文件请使用京东云对象存储提供的 [SDK](https://docs.jdcloud.com/cn/object-storage-service/multipart-upload-s3)**

![上传备份3](../../../../../../image/RDS/Upload-Backup-V2-3.png)

#### 4. 备份文件授权

> **建议： 我们建议创建单独的对象存储空间用于上传要导入的备份文件，并给后台系统账号授予整个Bucket的读取权限**

点击进入备份文件所在的空间，选择 **空间设置** ， **添加自定义权限** ，进入权限设置页面

![权限设置1](../../../../../../image/RDS/Grant-File-Privilege-1.png)

- 选择 **自定义用户** ，添加用户ID： **785455908940**。</br>
  >注意：785455908940 这个ID为后台系统ID，不能更改 </font></p>
- 涉及操作勾选 **GetObject** 和 **ListBucket**
- 其他保持不变
- 点击 **确认** 保持设置

![权限设置2](../../../../../../image/RDS/Grant-File-Privilege-2.png)

>注意：不要对该Bucket中 **空间设置** 下的 **静态网站托管** 页面中的任何参数进行设置，否则可能会导致备份文件读取失败
