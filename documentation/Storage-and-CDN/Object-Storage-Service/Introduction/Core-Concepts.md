# 核心概念

在您使用对象存储产品之前，请先阅读对象存储相关基础概念，文中详细介绍了Bucket、Object的创建命名规则以及Region、Endpoint、AccessKey等定义，这些可以帮助您更好地理解和使用OSS。

|英文|中文|说明|
| - | - | - |
|Bucket|存储空间|Bucket是对象存储中数据的基本组织单位，所有的数据都必须在某一个Bucket中，Bucket的名称全局唯一,全局指OSS支持的各个地域。如果您创建了某个名称的Bucket，其他用户将无法再创建同名的Bucket|
|Object|对象或者文件|Object是京东对象存储中的基本实体，在本帮助文档中Object、对象、文件均表示相同的意义，对象由键(Key)，数据(Data)和元数据(Metadata)三部分组成|
|Endpoint|OSS访问域名|京东云对象存储为每个Bucket默认分配了一个外网访问域名和一个内网访问域名|
|Region|地域或者数据中心|存储集群所处地域，目前支持：华北-北京、华南-广州、华东-宿迁、华东-上海，四个数据中心|
|Accesskey|AccessKeyId和AccessKeySecret的统称|AccessKeyId与AccessKeySecret是用户访问京东对象存储的身份标识，用户申请并开通京东云产品的使用资格后，即可登录用户中心创建AccessKeyId和AccessKeySecret|
|Put Object|简单上传|用户使用API中的Put Object方法上传单个Object，适用在任何一次HTTP请求交互即可完成上传的场景，比如小文件的上传|
|Multipart Upload|分片上传|除了通过PUT Object以外，OSS提供的另外一种上传模式——Multipart Upload用户如果在上传前无法确定上传文件大小，或上传较大文件且需要支持断点上传时，使用Multipart Upload上传模式|
|Get Object|下载|用于获取单个Object|
|Object Meta|文件元数据|一组键值(Key-Value)的组合，分为系统预定义元数据(System-DefinedMetadata)和用户自定义元数据(User-Defined Metadata)两部分，用来描述文件信息，如长度，类型等|
|Data|文件数据|用户上传的文本、多媒体、二进制等任何类型的数据|
|Key|文件名|Object的唯一名称标识，如test.jpg|
|Storage Class|存储类型|OSS提供标准存储（STANDARD）、低频存储（STANDARD-IA）、归档存储（GLACIER）、低冗余存储（REDUCED_REDUNDANCY）四种存储类型，全面覆盖从热到冷的各种存储场景|
