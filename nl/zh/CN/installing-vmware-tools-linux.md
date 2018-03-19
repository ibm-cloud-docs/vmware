---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# 安装 VMware Tools - Linux

VMware Tools 是一种实用程序套件，用于增强虚拟机访客操作系统的性能，并改进虚拟机的管理。在访客操作系统中安装 VMware Tools 至关重要。尽管访客操作系统可以在没有 VMware Tools 的情况下运行，但为此您会失去重要的功能和便利性。

在 Linux、FreeBSD 和 Solaris 访客上，该服务名为 `vmware-guestd`。`vmware-guesd` 服务在访客操作系统中履行以下责任：

* 将消息从主机操作系统传递到访客操作系统。
* 执行操作系统中的命令可在工作站中选择电源操作时，完全关闭或重新启动 Linux、FreeBSD 或 Solaris 系统。
* 使访客操作系统中的时间与主机操作系统中的时间同步。
* 运行脚本以帮助自动执行访客操作系统操作。这些脚本在虚拟机的电源状态更改时运行。

该服务在访客操作系统启动时启动。

要在 Linux 服务器上安装 VMware Tools，请在 vSphere 客户机中右键单击相应的服务器，将鼠标悬停在**访客**上，然后单击**安装/升级 VMware Tools**。

此链接将装载包含 VMware Tools rpm 的虚拟 CD-ROM 驱动器。要在装载虚拟 CD-ROM 驱动器之后安装 VMware Tools，请执行以下步骤：
1. 使用以下命令装载 CD-ROM 驱动器：`mount /dev/cdrom /mnt`
2. 在已装载的目录上使用 `ls /mnt` 命令来验证该文件是否存在并已正确装载。您将看到文件 `VMWareTools-4.0.0-208167.i386.rpm`。 
3. 运行命令 `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm`。
4. 运行以下命令为运行中的内核配置 VMware Tools：`/usr/bin/vmware-config-tools.pl`。**注：**配置更新期间，系统会中途要求您按一次 **ENTER** 键。
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**注：**在安装 VMware Tools 后不必重新启动 VM，但是建议您执行此操作。

如果 VMware Tools 已正确安装，那么 vSphere 客户机界面中将显示“正常”。
