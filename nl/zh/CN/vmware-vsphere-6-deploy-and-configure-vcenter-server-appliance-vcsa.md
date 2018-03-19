---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用 VMware vSphere 6 部署和配置 vCenter Server Appliance (vCSA)  

使用以下步骤来部署 VMware vCenter Server Appliance。
{:shortdesc}

**先决条件**
* 安装了兼容浏览器的 Windows 系统
  * Internet Explorer/Firefox/Chrome
* 具有足够资源支持 VMware vCenter Server Appliance 的 vSphere 主机
  * 在关必需系统资源的更多信息，请参阅 [Minimum requirements for the VMware vCenter Server 6.0 Appliance ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kb.vmware.com/s/article/2106572){: new_window}。
* vCSA ISO 映像
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* 装载 ISO 的功能
* 有权访问 IBM Cloud 专用网络的 VPN 会话

**部署和配置 vCenter Server Appliance**

1. 装载 vCenter Server Appliance (vCSA) ISO。
2. 在兼容的浏览器中打开 vcsa-setup.html。
3. 查看并接受 VMware Client 集成插件的安装。
4. 单击**允许**。
5. 单击**安装**。
6. 查看并接受许可协议的条款，然后单击**下一步**。
7. 输入要安装 vCSA 的 VMware 主机的 FQDN 或专用 IP 地址以及用户名和密码。单击**下一步**。
8. 单击**是**以接受证书警告。
9. 输入相应的“设备名称”和“操作系统密码”，然后单击**下一步**。
10. 对于部署类型，选择“使用嵌入式 Platform Services Controller 安装 vCenter Server”，然后单击**下一步**。
11. 单击“创建 SSO 域”，然后单击**下一步**。<!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. 选择“设备大小”，然后单击**下一步**。
13. 选择数据存储器，然后单击**下一步**。
14. 选择“使用嵌入式数据库 (PostgreSQL)”，然后单击 **下一步*。
15. 通过输入以下信息来设置网络配置：
  1. 网络
  * IP 地址系列
  * 网络类型
  * 网络地址
  * 系统名称
  * 子网掩码
  * 网关
  * 网络 DNS 服务器
      * 有关更多信息，请参阅[什么是本地 DNS 解析器](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-)。
  * 配置时间同步
  * 单击**下一步**
16. 复查设置，然后单击**完成**。您的 vCSA 实例已供应。

