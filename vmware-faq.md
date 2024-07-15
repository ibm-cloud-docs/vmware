---

copyright:
  years: 1994, 2024
lastupdated: "2024-07-15"

keywords: faq

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# FAQs: VMware
{: #vmware-faq}

## How is VMware licensed?
{: #how-vmware-licensed}
{: faq}

When you deploy ESX through the {{site.data.keyword.cloud}} catalog, VMware Service Provider Program licensing (VSPP) automatically enables. On deployment, a default user 'ibmvmadmin' is added to the ESX server for data collection. Do not delete this default user. VSPP charges for RAM that is reserved and used for all “powered on” virtual machines (not “per socket” like a standard host license).

## How is VMware vSphere licensed?
{: #how-is-vsphere-licensed}
{: faq}

When you deploy vSphere, VMware Service Provider Program licensing (VSPP) is automatically enabled. On deployment, a default user 'ibmvmadmin' is added to the Host for vSphere administration and integration services.

## What license level is enabled when you deploy vSphere from the {{site.data.keyword.cloud}} catalog?
{: #what-license-level-is-enabled}
{: faq}

Enterprise Plus, the highest vSphere license level.

## Can I create an isolated private VMware cloud?
{: #can-i-create-isolated-private-vmware-cloud}
{: faq}

Yes, you can deploy bare metal systems and install any supported hypervisor (including VMware ESX) on these hosts. You can also deploy virtual machines by using the default management tools. By default, systems are deployed in VLANs for segmentation and networking components (such as gateways, routers, and firewalls) and are used to create almost any topology.

## Can I deploy VMware components directly from the {{site.data.keyword.cloud}} catalog?
{: #can-i-deploy-vmware-components}
{: faq}

Yes, you have two options:

1. Select and deploy the ESX hypervisor automatically with a monthly bare metal system. You can also deploy vCenter management automatically with a virtual machine or bare metal system (Windows only).

1. Deploy a bare metal host with a free-operating system, such as CentOS, and then install ESX manually by using Remote Console and virtual media access of the host. You can then install vCenter Server manually or deploy the VMware vCenter Server Appliance that operates on Linux.
