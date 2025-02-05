# 使用限制

### 公有云平台支持
迁移源平台目前支持以下公有云：
- 阿里云
- 华为云
- 京东云

迁移目标平台目前支持：
-  京东云

### 资源自动发现及导入
目前可支持以下常用资源的自动发现及导入：
- 服务器：云服务器
- 数据库：MySQL，PostgreSQL，MongoDB，Redis
- 对象存储：存储桶（Bucket）

### 文档上传
- 文件大小：不超过 50 MB
- 文件类型：支持  .pdf, .docx, .doc, .xlsx, .xls, .pptx, .ppt, .png, .svg, .vsdx, .vsd, .xmind

### OSS 迁移
- 支持的最大单文件大小为 19.5 TB。
- 文件名不能超过 1022 字节，且不得包含回车、换行等不可见字符。
- 从云厂商迁移对象存储服务（兼容 S3），仅支持源 Bucket 权限为公有读，否则将导致迁移失败。
- 迁移限速：当前固定为 200 MB/s 。
