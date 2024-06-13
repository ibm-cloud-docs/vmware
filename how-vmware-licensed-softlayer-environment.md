---

copyright:
  years: 1994, 2019

lastupdated: "2017-08-09"

keywords: vmware license, VMware Service Provider Program licensing, vspp, esx

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# How is VMware licensed?
{: #how-vmware-licensed}

The licensing approach is tied to your deployment mechanism. You have two ways to deploy VMware:

1. When you deploy ESX from the portal, VMware Service Provider Program licensing (VSPP) automatically enables. On deployment, a default user 'vmadmin' is added to the ESX server for data collection. Do not delete this default user. VSPP charges for RAM that is reserved and used for all “powered on” virtual machines (not “per socket” like a standard host license).


2. When you deploy ESX manually, you can BYOL (bring your own license), so you can apply standard licenses to these hosts. **Note:** BYOL cannot be used for hosts that are deployed through the portal. The VSPP is expected to be enabled.

    * Additionally, a vCenter Server instance is not required for VSPP to work.
