---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用 VMware vSphere 6 部署及配置 vCenter Server Appliance (vCSA)  

使用下列步驟來部署 VMware vCenter Server Appliance。
{:shortdesc}

**必要條件**
* 已安裝相容瀏覽器的 Windows 系統
  * Internet Explorer/Firefox/Chrome
* 具有足夠資源的「vSphere 主機」，以支援 VMware vCenter Server Appliance
  * 如需必要系統資源的相關資訊，請參閱 [VMware vCenter Server 6.0 Appliance 最低需求 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kb.vmware.com/s/article/2106572){: new_window}。
* vCSA ISO 映像檔
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* 裝載 ISO 的能力
* 具有 IBM Cloud 專用網路存取權的 VPN 階段作業

**部署及配置 vCenter Server Appliance**

1. 裝載 vCenter Server Appliance (vCSA) ISO。
2. 在相容的瀏覽器中開啟 vcsa-setup.html。
3. 檢閱並接受 VMware Client Integration 外掛程式的安裝。
4. 按一下**容許**
5. 按一下**安裝**
6. 檢閱並接受授權合約的條款，然後按**下一步**。
7. 輸入您要安裝 vCSA 之「VMware 主機」的 FQDN 或「專用 IP 位址」以及使用者名稱和密碼。按**下一步**。
8. 按一下**是**，以接受憑證警告。
9. 輸入適當的「應用裝置名稱」及「OS 密碼」，然後按**下一步**。
10. 針對部署類型，選取「使用 Embedded Platform Service 控制器安裝 vCenter Server」，然後按**下一步**。
11. 按一下「建立 SSO 網域」，然後按**下一步**。<!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. 選擇「應用裝置大小」，然後按**下一步**。
13. 選取資料儲存庫，然後按**下一步**。
14. 選取「使用內嵌資料庫 (PostgreSQL)」，然後按**下一步*。
15. 輸入下列資訊，以設定網路配置：
  1. 網路
  * IP 位址系列
  * 網路類型
  * 網址
  * 系統名稱
  * 子網路遮罩
  * 網路閘道
  * 網路 DNS 伺服器
      * 如需相關資訊，請參閱[何謂本端 DNS 解析器](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-)。
  * 配置時間同步
  * 按**下一步**
16. 檢閱設定，然後按一下**完成**。即已佈建您的 vCSA 實例。

