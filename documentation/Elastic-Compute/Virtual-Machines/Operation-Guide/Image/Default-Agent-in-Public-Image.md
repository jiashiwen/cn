# 官方镜像系统组件
官方镜像中默认安装了下述系统组件，以和对应服务或产品配合提供完备的产品功能和安全监控。建议不要进行卸载或禁止开机运行，否则会导致部分功能缺失。

受系统升级和组件演进的客观因素影响，早期官方镜像中可能未安装以下组件，建议您核查当前系统的安装情况后逐一完成安装。

>提示：
>ifrit可实现JCS-Agent的自动安装和更新，在导入镜像/镜像组件更新场景下，建议您参照下方指导，在确保云主机内cloud-init和QGA已卸载的前提下，直接安装ifrit。安装完成后最多等待10分钟即可完成JCS-Agent的安装或更新。
    

| 组件名称    | 相关进程名称    | 主要功能     | 不安装有何影响    |
| --- | --- | --- | --- |
|   JCS-Agent  | JCSAgentCore <br> MonitorPlugin-‘版本号’  <br>  UpgradePlugin-‘版本号’  | 通用核心组件，配合元数据服务提供密码密钥注入、自定义脚本注入、监控数据上报等功能    |  无法通过京东云控制台或openAPI设置密码、密钥、自定义用户数据，无法获得部分云主机监控数据   |
| Ifrit    |  ifrit-agent <br> ifrit-supervise   |   通用部署插件，实现JCS-Agent的自动升级	  |  无法获得自动升级JCS-Agent的能力，如后续希望使用基于JCS-Agent开发的新功能，需要手动升级JCS-Agent   |
|  Jcloudhids   |jcloudhids <br> jcloudhidsupdate    | 早期安全组件，逐步下线中    | 无须安装   |
| Jdog-Monitor |	jdog-monitor.'版本号'<br>jdog-watchdog<br>jdog-kunlunmirror| 安全核心插件，提供安全防护能力|无法通过“主机安全”产品获得关于云主机的安全隐患及异常行为监测 |

* [JCS-Agent](default-agent-in-public-image#user-content-1)
* [Ifrit](default-agent-in-public-image#user-content-2)
* [Jdog-Monitor](default-agent-in-public-image#user-content-4)


<div id="user-content-1"></div>

## JCS-Agent
### 组件介绍
JCS-Agent是京东云自研的云主机核心组件，可提供诸如云主机基本信息（密码、密钥）注入、用户数据注入、Windows系统KMS激活、监控数据上报等功能。

2018年8月-12月之间官方镜像陆续升级，完成了JCS-Agent的默认安装，早期官方镜像中存在安装cloud-init和qemu-guest-agent的情况，此类镜像依然具有主机基本信息注入和监控上报功能，但用户数据注入、Windows系统KMS激活及后续新增功能均无法支持，如您当前使用的是早期agent建议您更换为JCS-Agent（如您当前使用的JCS-Agent为低于1.0.728的版本，建议您参照下方操作进行新版本的安装，以便获得Ifrit的自动升级管理功能。

云市场镜像安装JCS-Agent的情况视镜像发布时间（基于何版本的官方镜像制作）和服务商制作情况，如您依赖JCS-Agent提供的某些特殊功能，请咨询云市场确认镜像内agent情况后再行使用。

### 安装准备
#### 卸载冲突软件
***如您使用的镜像为京东云外环境的导入镜像，且导入前已安装了cloud-init或qemu-guest-agent，请务必在完成卸载后再进行安装！***

如果卸载时提示软件未安装，则说明当前系统未做安装，可不用进行后续的配置文件和日志清理。同时建议卸载完成后运行`ps -ef`查看服务是否已清理。

① cloudinit卸载清理：<br>
* CentOS：`rpm -e cloud-init`、`rm -rf /etc/conf/cloud/*`、`rm -rf /var/lib/cloud/*`<br>
* Ubuntu：` apt-get purge cloud-init`  <br>
* Windows：【控制面板】—【程序】，找到Cloudbase-Init，右键点击卸载

② qemu-guest-agent卸载清理：<br>
* CentOS：`rpm -e qemu-guest-agent`、`rm -fr /var/log/qemu-ga` <br>
* Ubuntu：`apt-get purge qemu-guest-agent` <br>
* Windows：【控制面板】—【程序】，找到qemu-guest-agent，右键点击卸载

#### 查看当前软件版本
通过查看监控插件的版本来获悉JCS-Agent版本号。<br>
Linux：`ps -ef|grep MonitorPlugin`<br>
Windows：`wmic process where caption="MonitorPlugin.exe" get caption,commandline /value`

### 安装方式
**（建议您[安装ifrit](default-agent-in-public-image#user-content-2) 后由其自动拉起JCS-Agent，此方式下可跳过下述安装步骤。）**

**Linux：**<br>
1、下载下述安装包和安装脚本，将其下载至同一目录中（比如：/root/jcloud）。<br>
若主机未绑定公网IP需要内网环境下载，请将链接中的bucket地址"bj"和地域参数"cn-north-1"分别替换成主机所在地域的代码："gz","cn-south-1"(华南-广州)、"sq","cn-east-1"(华东-宿迁)、"sh","cn-east-2"(华东-上海)，并将域名中的"s3"改为"s3-internal"。<br>
https://bj-jcs-agent-linux.s3.cn-north-1.jdcloud-oss.com/jcloud-jcs-agent-linux-deploy.py <br>
https://bj-jcs-agent-linux.s3.cn-north-1.jdcloud-oss.com/jcloud-jcs-agent-linux.zip <br>

2、在下载目录执行下述指令，卸载旧版本。（**此步骤用于更新JCS-Agent时操作，如当前未安装可跳过**）<br>
```
python jcloud-jcs-agent-linux-deploy.py uninstall
```

3、在下载目录执行下述指令，安装最新版本。<br>
```
python jcloud-jcs-agent-linux-deploy.py install
```

4、执行`ps -ef`看到JCSAgentCore和MonitorPlugin两个进程即表示安装成功。安装成功后可以删除安装包和安装脚本。

**Windows:**<br>
1、下载安装包、安装脚本和MD5工具，将其下载至同一目录中（比如： C:\jcloud）。<br>
若主机未绑定公网IP需要内网环境下载，请将链接中的地域参数"cn-north-1"替换成主机所在地域的代码："cn-south-1"(华南-广州)、"cn-east-1"(华东-宿迁)、"cn-east-2"(华东-上海)，并将域名中的"s3"改为"s3-internal"。<br>
https://bj-jcs-agent-windows.s3.cn-north-1.jdcloud-oss.com/jcloud-jcs-agent-windows-manual.zip <br>
https://bj-jcs-agent-windows.s3.cn-north-1.jdcloud-oss.com/jcloud-jcs-agent-win-deploy.ps1 <br>
https://bj-jcs-agent-windows.s3.cn-north-1.jdcloud-oss.com/MD5.exe <br>

2、在下载目录使用powershell执行下述指令，卸载旧版本（**此步骤用于更新JCS-Agent时操作，如当前未安装可跳过**）<br>
```
.\jcloud-jcs-agent-win-deploy.ps1 uninstall
```
3、打开powershll，进入安装包所在的目录（C:\jcloud）执行下述命令进行安装
```
.\jcloud-jcs-agent-win-deploy.ps1 install
```

4、执行`ps -ef`命令看到JCSAgentCore和MonitorPlugin两个进程即表示安装成功。安装成功后可以删除安装包、安装脚本和MD5工具。


<div id="user-content-2"></div>

## Ifrit
### 组件介绍
Ifrit是京东云自研的轻量、通用的部署运维工具，可实现对其所管理组件的部署、升级、卸载等管理操作。Ifrit与JCS-Agent配合工作，实现对JCS-Agent的自动化升级。

官方镜像于2019年5月-7月期间陆续升级，完成Ifrit的默认安装。云市场镜像安装情况视镜像发布时间（基于何版本的官方镜像制作）和服务商制作情况，具体请咨询云市场。

### 安装方式
**Linux：** <br>
* 公网/外网环境执行安装：<br>
```
wget -c http://devops-hb.s3.cn-north-1.jdcloud-oss.com/ifrit/ifrit-agent-external-v0.01.465.534ae3d.20190523181914.bin -O installer && sh installer -- -a jcs-agent-core,jcs-agent-script,jcs-agent-monitor /usr/local/share/jcloud/ifrit && rm -f installer
```

* 京东云内网环境执行安装：<br>
```
curl -fsSL http://deploy-code-vpc.jdcloud.com/dl-ifrit-agents/install_jcs | bash
```

**Windows:** <br>
* 公网/外网环境执行安装：<br>
```
($client = new-object System.Net.WebClient) -and ($client.DownloadFile('http://devops-hb.s3.cn-north-1.jdcloud-oss.com/ifrit/ifrit-external-v0.01.461.56ff760.20190517095556.exe', 'c:\ifrit.exe')) -or (Start-Process 'c:\ifrit.exe')
```

* 京东云内网环境执行安装：<br>

① 华北-北京：<br>
```
($client = new-object System.Net.WebClient) -and ($client.DownloadFile('http://devops-hb.s3-internal.cn-north-1.jdcloud-oss.com/ifrit/ifrit-external-v0.01.461.56ff760.20190517095556.exe', 'c:\ifrit.exe')) -or (Start-Process 'c:\ifrit.exe')
```

② 华东-上海：<br>
```
($client = new-object System.Net.WebClient) -and ($client.DownloadFile('http://devops-hd.s3-internal.cn-east-2.jdcloud-oss.com/ifrit/ifrit-external-v0.01.461.56ff760.20190517095556.exe', 'c:\ifrit.exe')) -or (Start-Process 'c:\ifrit.exe')
```

③ 华东-宿迁：<br>
```
($client = new-object System.Net.WebClient) -and ($client.DownloadFile('http://devops-sq.s3-internal.cn-east-1.jdcloud-oss.com/ifrit/ifrit-external-v0.01.461.56ff760.20190517095556.exe', 'c:\ifrit.exe')) -or (Start-Process 'c:\ifrit.exe')
```

④ 华南-广州：<br>
```
($client = new-object System.Net.WebClient) -and ($client.DownloadFile('http://devops.s3-internal.cn-south-1.jdcloud-oss.com/ifrit/ifrit-external-v0.01.461.56ff760.20190517095556.exe', 'c:\ifrit.exe')) -or (Start-Process 'c:\ifrit.exe')
```

在安装向导中单击“下一步”，在配置信息页面中，只需在AGENTS配置中填写：jcs-agent-core-win,jcs-agent-script-win,jcs-agent-monitor-win，其他配置不用填写采用默认值。

![](https://img1.jcloudcs.com/cn/image/vm/ifrit-install-1.png)
![](https://img1.jcloudcs.com/cn/image/vm/ifrit-install-2.png)

暂不支持自定义安装路径，勾选“我同意许可条款和条件”，点击“下一步”。

![](https://img1.jcloudcs.com/cn/image/vm/ifrit-install-3.png)

点击“安装”，完成ifrit安装。

![](https://img1.jcloudcs.com/cn/image/vm/ifrit-install-4.png)
![](https://img1.jcloudcs.com/cn/image/vm/ifrit-install-5.png)



<div id="user-content-4"></div>

## Jdog-Monitor
### 组件介绍
Jdog-Monitor是京东云自研的安全核心组件，是“主机安全”产品所实现的安全监控及防范功能的核心，可提供防暴力破解、异常登陆检测、高危漏洞检测等安全功能。

### 安装方式
**Linux：**<br>

1、下载安装包：（非华北地域主机请绑定公网IP后下载）<br>
https://iaas-cns-download.s3.cn-north-1.jdcloud-oss.com/JdogMonitor/jdog-op-agent-master-7a35746b-0709091136.tar <br>

2、运行以下指令进行安装。<br>
```
mkdir -p /usr/local/share/jcloud/jdog-monitor
tar zxvf jdog-op-agent-master-7a35746b-0709091136.tar -C /usr/local/share/jcloud/jdog-monitor
/usr/local/share/jcloud/jdog-monitor/scripts/jdog_service install
```

**Windows：**<br>
1、下载安装包：（非华北地域主机请绑定公网IP后下载）<br>
https://iaas-cns-download.s3.cn-north-1.jdcloud-oss.com/JdogMonitor/jdog-monitor.exe <br>

2、以管理员(administrator)权限运行jdog-monitor.exe 进行安装。

