---

copyright:
  years: 1994, 2019
lastupdated: "2019-08-21"

keywords: netApp licenses, add license, netApp ONTAP select, order netapp license

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Ordering NetApp Licenses
{: #order-netapp-licenses}

To use NetApp ONTAP Select, you must install it on a VMWare vSphere 6.x server.
NetApp ONTAP Select is only available on bare metal servers that are provisioned for monthly billing.

 Two offerings for NetApp ONTAP Select are available:
* Standard - uses SATA drives
* Premium - uses Flash SSD drives

## Before you begin
{: #before-you-begin-netapp-order}
* Navigate to your console's device menu. For more information, see [Navigating to devices](/docs/virtual-servers?topic=virtual-servers-navigating-devices).
* Make sure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/account?topic=account-infrapermission#infrapermission) and [Managing device access](/virtual-servers?topic=virtual-servers-managing-device-access).

Use the following steps to order licenses for the NetApp products.
1. Click **Devices > Manage > NetApp Licenses**.
2. Click **Order NetApp licenses**.
3. Click the drop-down list under **Add License...** to list the NetApp products and number of CPUs for the licenses that you want to order.
4. You can see the price of the NetApp product that you selected on the far right of the screen.
5. Click **Add License** to add more licenses.
6. After you are finished adding licenses, click **Continue**.
7. Review your order on the Confirm Order screen.
8. Read the Master Service Agreement and enable the checkbox to indicate your agreement.
9. Click **Place Order**. The **NetApp Licenses** page is displayed, which shows your NetApp products and license keys.
10. Click **Download Netapp Software**. You need to have an SSL connection to the IBM Cloud private network to access the download page.
11. Download the correct NetApp products and manually install them into your environment.
