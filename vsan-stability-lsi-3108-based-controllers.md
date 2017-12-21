---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuring vSANs for stability on LSI 3108-based controllers

To help prevent device-related failures when running vSAN with LSI 3108-series controllers, run the following commands from the ESXi shell:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

Please note:

* These commands must be run on each ESXi host in the vSAN cluster.
* These commands are immediately effective. No reboot is required.
* These commands result in persistent changes and remains configured across reboots.

For more information, see VMware Knowledge Base topic, [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kb.vmware.com/s/article/2144936){: new_window}.
