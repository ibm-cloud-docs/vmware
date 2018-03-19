---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 通过远程控制台和虚拟介质安装 VMware vSphere ESXi

通过安装介质部署 ESX 的操作在所有版本中都很类似，并且可用于 BYOL（自带许可证）方案。

## 需求
* 有权访问专用网络的虚拟机 (VM) 实例 [例如，随 Windows 或 Linux 一起安装的云计算实例 (VSI)，随支持 Java 的浏览器一起安装的 VSI，以及可通过 vpn.softlayer.com 或公共 IP 访问的 VSI]。VSI 必须位于服务器的智能平台管理接口 (IPMI) 地址所在的专用网络上。
* VMware ESXi VIM 安装程序 ISO 的副本。

<!--## Steps -->

## 连接到 IPMI
1. 将 VMware ISO 上传到在“需求”中指定的 VSI（这些 VSI 应该具有公用 Web 访问权。）
2. 从客户门户网站中收集 IPMI 地址和登录信息。
3. 选择**设备** > **设备列表** > **[服务器]** > **远程管理**选项卡。
4. 使用远程桌面 (RDP) 或远程 X 连接到存储 ESXi 映像的 VSI。
5. 在 RDP 会话中打开 Web 浏览器，然后输入在步骤 2 中收集的 IPMI 地址。
6. 使用也出现在步骤 2 中的凭证（通常是 root 用户凭证）登录到 IPMI 控制台。
* 记下您的 IPMI 用户访问级别。此级别可能是管理员。如果将此级别设置为**操作员**，那么装载远程存储器时可能会遇到问题。如果无法装载介质，请提交支持凭单以升级您的 IPMI 凭证。
7. 确认您位于主页登录页面上，并单击**远程控制** > **控制台重定向** > **启动控制台**。

## 连接 ISO
1. 在基于内核的虚拟机 (KVM) 查看器上，选择**虚拟介质** > **虚拟存储器**。您的操作系统和 Java 版本可能需要您提供访问权才能启动基于 Java 的查看器。
2. 单击“虚拟存储器”窗口中的 **CDROM 和 ISO** 选项卡。对于“逻辑驱动器类型”，选择 **ISO 文件**，然后单击**打开映像**。
3. 转至 ESXi ISO，并单击**确定**。然后，单击**插件**。
4. 在 ISO 插入到会话后，单击**确定**。
* 返回到 IPMI Web 页面，然后单击**远程** > **控制** > **重置服务器** > **执行操作**以重新启动服务器。

### 安装并完成联网配置
1. 安装 ESXi。
* 安装完成后，请确保**拔出** ISO，以便您可以重新启动服务器。
2. 重新启动服务器。
3. 在服务器重新启动后，配置该服务器的 IP 地址。
4. 从设备的“配置”选项卡中收集详细信息。

现在，您可以管理 ESXi 主机。

有关如何设置耐久性或高性能块存储器的更多信息，请参阅[供应和管理块存储器](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)。

有关设置 QuantaStor 的更多信息，请参阅 [QuantaStor 体系结构指南](architecture-guide-quantastor-vmwaresoftlayer.html)。
