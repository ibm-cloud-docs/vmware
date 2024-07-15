---

copyright:
  years: 1994, 2024
lastupdated: "2024-07-15"

keywords: vsan stability

subcollection: vmware

---

{{site.data.keyword.cloud}}

# Configuring vSANs for stability on LSI 3108-based controllers
{: #config-vsan-stability}

To help prevent device-related failures when you run vSAN with LSI 3108-series controllers, run the following commands from the ESXi shell:

   `esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`

   `esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

* You must run these commands on each ESXi host in the vSAN cluster.
* These commands are immediately effective. No restart is required.
* These commands result in persistent changes and remains configured across restarts.
