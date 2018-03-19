---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 订购 VMware 许可证

VMware 管理员很清楚，自己可以通过部署到 {{site.data.keyword.BluSoftlayer_full}}，快速实现具有成本效益的混合云特征。其中一个特征是，vSphere 工作负载和目录供应到 {{site.data.keyword.cloud_notm}} 数据中心内的 VMware vSphere 环境，而无需修改 VMware VM 或访客。通过使用公共 vSphere 系统管理程序和管理/编排平台，可以实现这些部署。
{:shortdesc}

vSphere 实现还支持使用其他组件。表 1 包含可通过 {{site.data.keyword.slportal}} 订购的 VMware 产品的列表。定价信息可在 [IBM Cloud for VMware Solutions](http://www.softlayer.com/vmware-solutions) 下找到。

|产品名称|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="表 1. 客户门户网站中提供的 VMware 产品" caption-side="top"}

使用以下步骤来订购表 1 中所列 VMware 产品的许可证：
1. 登录到 [{{site.data.keyword.slportal_short}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window}。
2. 单击**设备 > 受管 > VMware 许可证**。
3. 单击右上角的**订购 VMware 许可证**。
4. 单击**添加许可证...** 下的下拉列表，以针对要订购的许可证列出 VMware 产品和 CPU 数量。
  * **注：**VMware vSphere Enterprise Plus (ESXi 6.0) 不通过此过程订购。它在您订购裸机服务器时，作为请求的操作系统进行订购。
5. 您可以在屏幕最右侧看到所选 VMware 产品的价格。
6. 单击**继续**以订购许可证，或者可以单击**添加许可证**以添加更多许可证。
  * 单击**继续**后，将返回到 **VMware 许可证**页面，其中显示相应的 VMware 产品和许可证密钥。
7. 从提供的链接下载**安装文件**。您需要具有与 IBM Cloud 专用网络的 SSL 连接才能访问下载页面。
8. 下载正确的 VMware 产品，然后将其手动安装到 vSphere 环境中。
