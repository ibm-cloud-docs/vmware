---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# VMware Tools 설치 - Linux

VMware Tools는 가상 머신의 게스트 운영 체제에 대한 성능을 강화하고 가상 머신의 관리를 향상시키는 유틸리티 스위트입니다. VMware Tools를 게스트 운영 체제에 설치하는 것은 필수적입니다. VMware Tools 없이 게스트 운영 체제를 실행할 수 있지만 중요한 기능과 편의성을 잃게 됩니다. 

서비스는 Linux, FreeBSD 및 Solaris 게스트에서 `vmware-guestd`로 이름이 지정됩니다. `vmware-guestd` 서비스는 게스트 운영 체제 내에서 다음 작업을 수행합니다. 

* 호스트 운영 체제에서 게스트 운영 체제로 메시지를 전달합니다.
* 워크스테이션에서 파워 오퍼레이션을 선택하는 경우 Linux, FreeBSD  또는 Solaris 시스템을 완전히 종료하기 위해 운영 체제에서 명령을 실행합니다.
* 게스트 운영 체제의 시간을 호스트 운영 체제의 시간과 동기화합니다.
* 게스트 운영 체제 오퍼레이션을 자동화하도록 도와주는 스크립트를 실행합니다. 가상 머신의 전원 상태가 변경되는 경우 스크립트를 실행합니다.

게스트 운영 체제를 시작하면 서비스가 시작됩니다.

Linux 서버에 VMware tools를 설치하려면 vSphere 클라이언트의 해당 서버를 마우스 오른쪽 단추로 클릭하고 **게스트** 위로 마우스를 가져가서 **VMware Tools 설치/업그레이드**를 클릭하십시오.

이 링크는 VMware tools rpm을 포함하는 가상 CD-ROM 드라이브를 마운트합니다. 가상 CD-ROM 드라이브를 마운트한 후에 도구를 설치하려면 다음 단계를 수행하십시오.
1. `mount /dev/cdrom /mnt` 명령을 사용하여 CD-ROM 드라이브를 마운트하십시오.
2. 마운트된 디렉토리에서 `ls /mnt` 명령을 사용하여, 파일이 있고 올바르게 마운트되었는지 확인하십시오. `VMWareTools-4.0.0-208167.i386.rpm` 파일이 표시됩니다. 
3. `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm` 명령을 실행하십시오.
4. `/usr/bin/vmware-config-tools.pl` 명령을 실행하여 실행 중인 커널에 대해 VMware Tools를 구성하십시오. **참고:** 구성 업데이트 중에 한 번 **ENTER**를 누르도록 요청됩니다. 
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**참고:** VMware Tools를 설치한 후 VM을 다시 시작해야 하는 것은 아니지만, 권장됩니다. 

VMware Tools를 올바르게 설치한 경우 vSphere 클라이언트 인터페이스 내에 “확인”이 표시됩니다. 
