---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 为 VMware 安装 EVault Backup 客户机

要在 VMware 服务器上安装 EVault Backup 客户机，可以通过在目标 ESX 服务器中的 shell 或终端中执行一系列命令来完成。此过程概述在 VMware 服务器上安装 EVault Backup 客户机所需的步骤：
{:shortdesc}

要安装代理程序，请使用以下命令下载 `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` 软件包，并将其复制到目标 ESX 服务器上：

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**注：**必须在目标 ESX 服务器上本地执行以下步骤。

1. 解压缩软件包中的文件。为此，请使用以下命令（其中，“PACKAGENAME”可为“Agent-VMware-ESX-Server-6.71”）：<br/>`tar xvfz PACKAGENAME.tar.gz`
2. 转至在其中解压缩软件包的目录。
3. 运行安装脚本：<br />`# ./install.sh`<br/><br/>
**注：**安装脚本将以交互方式提示您输入配置信息，例如 Web 注册（地址、端口号和认证）和日志文件名。

输入此服务器的 WebCC 用户名。

4. 对于请求 WebCC 用户名的提示，键入 **EVault Backup 用户名**作为输入内容。请参阅[查看 EVault Backup 存储器详细信息](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal)过程，以获取查看 EVault Backup 用户名的指示信息。
5. 对于请求 WebCC 密码的提示，键入“EVault Backup 密码”作为输入内容。
6. 安装完成时，将显示一条完成消息，并且代理程序守护程序将在运行。


其他安装说明：<br/>
如果安装成功，Install.log 将位于安装目录中。<br/>
例如：`/opt/BUAgent/Install.log`

如果安装失败且回滚，安装日志将位于 `<Installation Failure directory> 中。`<br/>
如果安装失败而未回滚，安装日志将位于 `<Installation Kit directory>` 中。<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
请确保连接到 {{site.data.keyword.BluSoftlayer_full}} VPN，以便查看上述链接。有关连接到 IBM Cloud VPN 的更多信息，请参阅[启用对 IBM Cloud 基础架构专用网络的访问](/docs/customer-portal/getting-started.html#enable-private-network)。
