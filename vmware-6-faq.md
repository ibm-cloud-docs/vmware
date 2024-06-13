---

copyright:
  years: 1994, 2019
lastupdated: "2017-11-22"

keywords: vmware 6 faq

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# VMware 6 FAQ
{: #vmware-6-faq}

## What license level is enabled when you deploy vSphere from the IBM Cloud portal?

Enterprise Plus, the highest vSphere license level.

## How is VMware vSphere 6 licensed?

The licensing approach is tied to your deployment mechanism. You have two ways to deploy VMware 6:
1. When you deploy vSphere from the control portal, VMware Service Provider Program licensing (VSPP) automatically enables. On deployment, a default user "slvmadmin" is added to the Host for vSphere administration and integration services into the control portal.
2. When you deploy vSphere manually, you can bring your own license and media (BYOL/BYOM), which allows you to apply your standard licenses to these hosts. **Note:** If you want to use your own VMWare licensing, it is recommended that you order the server with a free OS such as CentOS or as NO OS. Then, install the VMWare OS through IPMI [Virtual ISO](/bare-metal?topic=bare-metal-mounting-an-iso-on-a-bare-metal-server)


## vSAN stability on LSI 3108-based controllers

To help prevent device-related failures that is running vSAN with LSI 3108-series controllers, run the following commands from the ESXi shell:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

**Note:**
   * These commands must be run on each ESXi host in the vSAN cluster.
   * These commands are immediately effective. No restart is required.
   * These commands result in persistent changes and remain configured across restarts.

For more information, see VMware's [KB article 2144936](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2144936).


## Can I create my isolated private VMware cloud?

Yes, you can deploy bare metal systems and install any supported hypervisor (including VMware ESX) on these hosts. You can also deploy virtual machines by using the native management tools. By default, systems are deployed in VLANs for segregation and networking components (such as gateways, routers, and firewalls) and are used to create almost any topology.

