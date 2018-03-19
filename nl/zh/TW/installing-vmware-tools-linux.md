---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# 安裝 VMware Tools - Linux

VMware Tools 是一套公用程式，可加強虛擬機器訪客作業系統的效能，並改善虛擬機器的管理。在訪客作業系統中安裝 VMware Tools 十分重要。雖然訪客作業系統不需要 VMware Tools 也可以執行，但您會失去重要功能及便利性。

在 Linux、FreeBSD 及 Solaris 訪客作業系統上，服務命名為 `vmware-guestd`。`vmware-guestd` 服務會在訪客作業系統內履行下列職責：

* 將訊息從主機作業系統傳遞至訪客作業系統。
* 在工作站中選取電源作業時，請在作業系統中執行指令，以完全關閉或重新啟動 Linux、FreeBSD 或 Solaris 系統。
* 將訪客作業系統中的時間與主機作業系統中的時間同步化。
* 執行 Script，以協助自動執行訪客作業系統作業。虛擬機器的電源狀態變更時，就會執行 Script。

服務會在訪客作業系統啟動時啟動。

若要在 Linux 伺服器上安裝 VMware Tools，請用滑鼠右鍵按一下 vSphere Client 中的適當伺服器，並將游標移至**訪客**上方，然後按一下**安裝/升級 VMware Tools**。

此鏈結會裝載包含 VMware Tools RPM 的虛擬 CD-ROM 光碟機。若要在裝載虛擬 CD-ROM 光碟機之後安裝工具，請遵循下列步驟：
1. 使用下列指令來裝載 CD-ROM 光碟機：`mount /dev/cdrom /mnt`
2. 在所裝載的目錄上使用 `ls /mnt` 指令，驗證檔案已存在並且已正確裝載。您將會看到 `VMWareTools-4.0.0-208167.i386.rpm` 檔案。 
3. 執行 `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm` 指令。
4. 執行下列指令，以配置執行中核心的 VMware Tools：`/usr/bin/vmware-config-tools.pl`。**附註：**在配置更新期間，系統會要求您中途按一次 **ENTER**。
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**附註：**您不需要在安裝 VMware Tools 之後重新啟動 VM，但建議您這麼做。

如果已正確安裝 VMware Tools，則會在 vSphere Client 介面內顯示「正常」。
