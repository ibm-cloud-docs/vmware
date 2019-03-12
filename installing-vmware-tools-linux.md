---

copyright:
  years: 1994, 2019
lastupdated: "2017-08-07"

keywords: install vmware linux tools, linux

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Installing VMware Tools - Linux
{: #install-vmware-linux-tools}

VMware Tools is a suite of utilities that enhances the performance of the virtual machine’s guest operating system and improves management of the virtual machine. Installing VMware Tools in the guest operating system is vital. Although the guest operating system can run without VMware Tools, you lose important functionality and convenience.

The service is named `vmware-guestd` on Linux, FreeBSD, and Solaris guests. The `vmware-guestd` service performs the following duties within the guest operating system:

* Passes messages from the host operating system to the guest operating system.
* Executes commands in the operating system to cleanly shut down or restart a Linux, FreeBSD, or Solaris system when you select power operations in Workstation.
* Synchronizes the time in the guest operating system with the time in the host operating system.
* Runs scripts that help automate guest operating system operations. The scripts run when the virtual machine’s power state changes.

The service starts when the guest operating system starts.

To install VMware tools on a Linux server, right-click the appropriate server in your vSphere client, hover over **Guest** and click **Install/Upgrade VMware Tools**.

This link mounts a virtual CD-ROM drive that contains the VMware tools rpm. To install the tools after you mount the virtual CD-ROM drive follow these steps:
1. Mount the CD-ROM drive by using the command: `mount /dev/cdrom /mnt`
2. Verify that the file exists and is mounted correctly by using the `ls /mnt` command on the mounted directory. You will see the file `VMWareTools-4.0.0-208167.i386.rpm`. 
3. Run the command `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm`.
4. Run the following command to configure VMware Tools for the running kernel: `/usr/bin/vmware-config-tools.pl`. **Note:** You are asked to press **ENTER** once midway during the configuration updates.
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**Note:** It is not necessary to restart the VM after you install the VMware tools however, it is recommended.

If the VMware tools installed correctly, “OK” is displayed within your vSphere Client interface.
