---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在 LSI 3108 型控制器上配置 vSAN 以取得穩定性

為了在搭配執行 vSAN 與 LSI 3108 系列控制器時協助防止裝置相關故障，請從 ESXi Shell 執行下列指令：

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

請注意：

* 這些指令必須在 vSAN 叢集的每一個 ESXi 主機上執行。
* 這些指令會立即生效。不需要重新開機。
* 這些指令會導致持續性變更，並在重新開機之後保持配置。

如需相關資訊，請參閱 VMware 知識庫主題：[根據 LSI 3108 晶片組之控制器的必要 vSAN 及 ESXi 配置 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kb.vmware.com/s/article/2144936){: new_window}。
