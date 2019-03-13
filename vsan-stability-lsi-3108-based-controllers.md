---

copyright:
  years: 1994, 2019
lastupdated: "2018-05-18"

keywords: vsan stability

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring vSANs for stability on LSI 3108-based controllers
{: #config-vsan-stability}

To help prevent device-related failures when running vSAN with LSI 3108-series controllers, run the following commands from the ESXi shell:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

**Note:**

* These commands must be run on each ESXi host in the vSAN cluster.
* These commands are immediately effective. No restart is required.
* These commands result in persistent changes and remains configured across restarts.

For more information, see VMware Knowledge Base topic, [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kb.vmware.com/s/article/2144936){: new_window}.
