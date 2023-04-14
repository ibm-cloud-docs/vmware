---

copyright:
  years: 1994, 2023
lastupdated: "2023-04-11"

keywords: order vmware license

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Ordering VMware licenses
{: #ordering-vmware-license}

VMware&reg; administrators understand that they can quickly realize the cost-effective hybrid cloud characteristics by deploying into {{site.data.keyword.BluSoftlayer_full}}. One of the characteristics is that vSphere workloads and catalogs are provisioned onto VMware vSphere environments within {{site.data.keyword.cloud_notm}} data centers without modification to VMware VMs or guests. Using a common vSphere hypervisor and management and orchestration platform makes these deployments possible.
{: shortdesc}

vSphere implementation also enables the use of other components. Table 1 contains a list of VMware products that are available to order through the {{site.data.keyword.cloud_notm}} catalog. For more information about pricing, see [IBM Cloud for VMware Solutions](https://www.ibm.com/cloud/vmware).

|Product name| Version |
|---|---|
| Aria Log Insight | |
| | Advanced |
| | Automation Advanced|
| | Automation Enterprise|
| | Enterprise Plus|
| | Operations Enterprise Edition|
| | Network Insight|
| NSX-T| |
| | Advanced Load Balancer|
| | Data Center SP Base|
| | Data Center SP Professional|
| | Data Center SP Advanced|
| | Data Center SP Enterprise Plus|
| vCenter | Server Standard |
| vSAN | |
| | Standard Tier 1 (0 - 20 TB)|
| | Standard Tier 2 (21 - 64 TB)|
|  | Standard Tier 3 (65 - 124 TB)|
|  | Advanced Tier 1 |
|  | Advanced Tier 2 |
|  | Advanced Tier 3 |
|  | Enterprise Tier 1 |
|  | Enterprise Tier 2 |
|  | Enterprise Tier 3 |
{: caption="Table 1. VMware products that are available in the {{site.data.keyword.cloud}} catalog" caption-side="top"}

## Before you begin
{: #before-you-begin-vmware-order}
* Go to your console's device menu. For more information, see [Navigating to devices](/docs/bare-metal?topic=virtual-servers-navigating-devices).
* Make sure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/account?topic=account-infrapermission#infrapermission) and [Managing device access](/docs/virtual-servers?topic=virtual-servers-managing-device-access).

## Ordering VMWare licenses
{: #order-vmware-licenses}

Use the following steps to order licenses for the VMware products that are listed in Table 1.

1. Click **Devices > Managed > VMware licenses > Order VMware licenses**.
2. Click the drop-down list under **Add license...** to list the VMware products and number of CPUs for the licenses that you want to order.

   VMware vSphere Enterprise Plus (ESXi) is not ordered through this process. It is ordered as a requested OS when you order your bare metal server.
   {: note}

3. You can see the price of the VMware product that you selected on the far right of the screen.
4. Click **Continue** to order the licenses or you can click **Add license** to add more licenses. After you click **Continue**, you are taken back to the **VMware licenses** page, which displays your VMware products and license keys.
5. Download the **Install files** from the provided link. You need to have an SSL connection to the {{site.data.keyword.cloud}} private network to access the download page.
6. Download the correct VMware products and manually install them into your vSphere environment.
