---
copyright:
  years: 1994, 2018
lastupdated: "2018-11-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQs: VMware 

## What license level is enabled when you deploy vSphere from the IBM Cloud portal?

Enterprise Plus, the highest vSphere license level.

## How is VMware vSphere 6 licensed?

The licensing approach is tied to your deployment mechanism. You have two ways to deploy VMware 6:

1. When you deploy vSphere from the control portal, VMware Service Provider Program licensing (VSPP) automatically enables. On deployment, a default user "_slvmadmin_" is added to the host for vSphere administration and integration services into the control portal.

2. When you deploy vSphere manually, you can bring your own license and media (BYOL/BYOM). When you BYOL, you can apply your standard licenses to these hosts. **Note:** If you want to use your own VMWare licensing, it is recommended that you order the server with a free OS such as CentOS or as NO OS. Then, install the VMWare OS through IPMI [Virtual ISO](/docs/bare_metal/mount-iso-bare-metal-server.html)

## Can I create an isolated private VMware cloud?

Yes, you can deploy bare metal systems and install any supported hypervisor (including VMware ESX) on these hosts. You can also deploy virtual machines by using the native management tools. By default, systems are deployed in VLANs for segregation and networking components (such as gateways, routers, and firewalls) and are used to create almost any topology.

## How is VMware licensed?

The licensing approach is tied to your deployment mechanism. You have two ways to deploy VMware:

1. When you deploy ESX from the portal, VMware Service Provider Program licensing (VSPP) automatically enables. On deployment, a default user '_vmadmin_' is added to the ESX server for data collection. Do not delete this default user. VSPP charges for RAM that is reserved and used for all “powered on” virtual machines (not “per socket” like a standard host license).

2. When you deploy ESX manually, you can BYOL (bring your own license), so you can apply standard licenses to these hosts. **Note:** BYOL cannot be used for hosts that are deployed through the portal. The VSPP is expected to be enabled.

    * Additionally, a vCenter Server instance is not required for VSPP to work.

## Can I deploy VMware components directly from the IBM Cloud portal?

Yes, you have two options:

1. Select and deploy the ESX hypervisor automatically with a monthly bare metal system. You can also deploy vCenter management automatically with a virtual machine or bare metal system (Windows only).

2. Deploy a bare metal host with a free-operating system, such as CentOS, and manually install ESX by using Remote Console and virtual media access of the host. You can then install vCenter Server manually or deploy the VMware vCenter Server Appliance that operates on Linux.

