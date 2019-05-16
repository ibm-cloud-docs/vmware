---

copyright:
  years: 1994, 2019
lastupdated: "2019-05-16"

keywords: order vmware license, {{site.data.keyword.BluSoftlayer_full}}, {{site.data.keyword.slportal}}

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Ordering VMware Licenses
{: #ordering-vmware-license}

VMware administrators understand that they can quickly realize the cost-effective hybrid cloud characteristics by deploying into {{site.data.keyword.BluSoftlayer_full}}. One of the characteristics is that vSphere workloads and catalogs are provisioned onto VMware vSphere environments within {{site.data.keyword.cloud_notm}} data centers without modification to VMware VMs or guests. Using a common vSphere hypervisor and management/orchestration platform makes these deployments possible.
{:shortdesc}

vSphere implementation also enables the use of other components. Table 1 contains a list of VMware products that are available to order through the {{site.data.keyword.slportal}}. Pricing information can be found under www.ibm.com/cloud/vmware.

|Product Name|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware vRealize Network Insight (1, 2, or 4 CPU)|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="Table 1. VMware products available in the Customer Portal" caption-side="top"}

Use the following steps to order licenses for the VMware products that are listed in Table 1:
1. Log in to the [{{site.data.keyword.slportal_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window}.
2. Click **Devices > Managed > VMware Licenses > Order VMware licenses**.
3. Click the drop-down list under **Add License...** to list the VMware products and number of CPUs for the licenses that you want to order.
  * **Note:** VMware vSphere Enterprise Plus (ESXi 6.0) is not ordered through this process. It is ordered as a requested OS when you order your bare metal server.
4. You can see the price of the VMware product that you selected on the far right of the screen.
5. Click **Continue** to order the licenses or you can click **Add License** to add more licenses.
  * After you click **Continue**, you are taken back to the **VMware Licenses** page, which displays your VMware products and license keys.
6. Download the **Install Files** from the link that is provided. You need to have an SSL connection to the IBM Cloud Private network to access the download page.
7. Download the correct VMware products and manually install them into your vSphere environment.
