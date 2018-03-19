---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQ: VMware 

## IBM Cloud 포털에서 vSphere를 배치할 때 사용하도록 설정되는 라이센스 레벨은 무엇입니까?

vSphere 최고 라이센스 레벨인 Enterprise Plus입니다.

## VMware vSphere 6 라이센스는 어떻게 얻습니까?

라이센싱 접근 방식은 배치 메커니즘과 연결되어 있습니다. VMware 6를 배치하는 두 가지 방법이 있습니다.

1. 제어 포털에서 vSphere를 배치하는 경우 자동으로 VSPP(VMware Service Provider Program) 라이센싱이 사용으로 설정됩니다. 배치 시 기본 사용자 "slvmadmin"은 제어 포털에 있는 vSphere 관리 및 통합 서비스의 호스트에 추가됩니다. 

2. vSphere를 수동으로 배치하는 경우 고유 라이센스 및 미디어를 사용(BYOL/BYOM)할 수 있으며 사용자는 표준 라이센스를 이러한 호스트에 적용할 수 있습니다. **참고:** 고유 VMWare 라이센싱을 사용하려는 경우 OS가 없거나, CentOS와 같은 무료 OS가 설치된 서버를 주문하는 것이 좋습니다. 그런 다음 IPMI [가상 ISO](../bare_metal/mount-iso-bare-metal-server.html)를 통해 VMWare OS를 설치하십시오. 

## 격리된 개인용 VMware 클라우드를 작성할 수 있습니까?

네, 베어메탈 시스템을 배치하고, 지원되는 하이퍼바이저(VMware ESX 포함)를 이 호스트에 설치할 수 있습니다. 기본 관리 도구를 사용하여 가상 머신을 배치할 수도 있습니다. 기본적으로 시스템은 (게이트웨이, 라우터 및 방화벽과 같은) 분리 및 네트워킹 컴포넌트에 대한 VLAN에 배치되며 대부분의 토폴로지를 작성하는 데 사용됩니다. 

## VMware 라이센스는 어떻게 얻습니까?

라이센싱 접근 방식은 배치 메커니즘과 연결되어 있습니다. VMware를 배치하는 두 가지 방법이 있습니다.

1. 포털에서 ESX를 배치하는 경우 자동으로 VSPP(VMware Service Provider Program) 라이센싱이 사용으로 설정됩니다. 배치 시 기본 사용자 'vmadmin'은 데이터 콜렉션을 위한 ESX Server에 추가됩니다. 이 기본 사용자를 삭제하지 마십시오. VSPP에서는 “전원이 켜진” 모든 가상 머신을 위해 예약되고 사용되는 RAM에 대한 비용을 청구합니다(표준 호스트 라이센스와 같은 “소켓 기준”이 아님). 

2. ESX를 수동으로 배치하는 경우 기존에 보유한 고유 라이센스를 사용(BYOL)할 수 있으므로 표준 라이센스를 이러한 호스트에 적용할 수 있습니다. **참고:** BYOL은 포털을 통해 배치되는 호스트에는 사용할 수 없습니다. VSPP가 사용될 것으로 예상됩니다. 

    * 또한 VSPP가 작동하는 데 vCenter Server 인스턴스는 필요하지 않습니다.

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## IBM Cloud 포털에서 직접 VMware 컴포넌트를 배치할 수 있습니까?

네, 두 가지 옵션이 있습니다.

1. 월별 베어메탈 시스템을 사용하여 자동으로 ESX 하이퍼바이저를 선택하고 배치합니다<!-- (Figure 2)-->. 또한 가상 머신 또는 베어메탈 시스템을 사용하여 vCenter 관리를 자동으로 배치할 수 있습니다(Windows 전용).

2. CentOS와 같은 무료 운영 체제가 포함된 베어메탈 호스트를 배치하고 그 뒤에 원격 콘솔 및 호스트의 가상 미디어 액세스 권한을 사용하여 ESX를 수동으로 설치합니다. 그런 다음 vCenter Server를 수동으로 설치하거나 Linux에서 작동하는 VMware vCenter Server 어플라이언스를 배치할 수 있습니다. 

