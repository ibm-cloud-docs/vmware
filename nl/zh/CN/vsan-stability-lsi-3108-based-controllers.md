---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 配置 vSAN 以实现基于 LSI 3108 的控制器的稳定性

为了帮助阻止在运行使用 LSI 3108 系列控制器的 vSAN 时发生与设备相关的故障，请从 ESXi shell 运行以下命令：

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

请注意：

* 这些命令必须在 vSAN 集群中的每个 ESXi 主机上运行。
* 这些命令将立即生效。无需重新引导。
* 这些命令会导致持久更改，在重新引导后保持已配置状态。

有关更多信息，请参阅 VMware Knowledge Base 主题 [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kb.vmware.com/s/article/2144936){: new_window}。
