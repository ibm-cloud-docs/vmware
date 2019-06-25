---

copyright:
  years: 1994, 2019
lastupdated: "2019-06-24"

keywords: IBM Issued Licenses VMware vSphere 6

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Applying IBM Issued Licenses for VMware vSphere 6
{: #apply-vmware-vsphere-6-licenses}

Many VMware Add On licenses can be purchased directly and stored on the {{site.data.keyword.slportal}}. After a license is purchased, you need to apply the license to your vSphere Hosts by using the following steps.
{:shortdesc}

## Before you begin
* Navigate to your console's device menu. For more information, see [Navigating to devices](/docs/infrastructure/vmware?topic=virtual-servers-navigating-devices).
* Ensure you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/iam?topic=iam-infrapermission#infrapermission) and [Managing device access](/docs/vsi?topic=virtual-servers-managing-device-access).

1. Log in to the [{{site.data.keyword.slportal_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window}.
2. Go to **Devices > Manage > VMware Licenses**.
3. Note the VMware **License Key**.
4. Log in to your vCenter Instances.
5. Go to **Administration > Licensing > Licenses**.
  * From here, you can see what licenses that are applied and apply new licenses.
6. To apply a new license, click the green **plus** [+] sign.
7. Enter your license keys, one per line.
8. Click **Next**.
9. Enter an appropriate **License Name**.
10. Click **Finish**.
