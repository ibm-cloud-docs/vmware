---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 시작하기 

다음 단계에 따라 vSphere 6를 시작하십시오.

## 환경 및 구성에 대한 이해

VMware 솔루션을 최적화하려면, VMware vSphere 환경에 대해 사설 네트워크 VLAN 및 공용(필요하지 않은 경우 선택적, 공용 포트를 사용 안함으로 설정할 수 있음)을 사용하는 것이 좋습니다. 이 프로비저닝 프로파일은 다음의 계층 2 세그먼트 트래픽 경계를 고려합니다. 

|예제 VLAN ID|설명|유형|추가 세부사항|
|---|---|---|---|
|VLAN1 - **1101**|관리, VxLAN|개인용 BCR|태그가 지정되지 않은 Native VLAN 및 원래 Native VLAN(VMWare 호스트가 주문 시 배치됨)|
|VLAN4 - **2200**|공용 인터넷 액세스 DMZ|공용 FCR|태그가 지정되지 않은 Native VLAN 및 원래 Native VLAN(VMWare 호스트가 주문 시 배치됨)|
{: caption="표 1. 사설 및 공용 VLAN 예제" caption-side="top"}

## vSphere Server 주문하기
1. [{{site.data.keyword.slportal_full}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}에 로그인하십시오.
2. **계정 > 주문하기**를 클릭하십시오.
3. **베어메탈 서버** 섹션에서 **월별**을 클릭하십시오.
4. 서버를 선택하십시오. 최소 요구사항은 VMware 지원 문서를 참조하십시오.
  * 다음은 서버가 예로 선택됩니다. **참고:** 비부착 듀얼 공용 및 사설 업링크를 보유하는 것이 중복성에 대한 요구사항입니다. VLAN을 작성한 데이터 센터에 비부착 업링크가 있는지 확인하십시오. 
  * 용량 클러스터(수량: 2)
    * 서버 구성: '듀얼 프로세서 멀티 코어 서버' 섹션에서 Intel Xeon v3 서버 선택
    * 소프트웨어: OS = vSphere Enterprise Plus 6
    * OS 스토리지: 2 x 1TB SATA (RAID 1로 구성됨)
    * 데이터 스토리지: 2TB SATA 또는 1.2TB SSD 또는 내구성(Endurance)/성능(Performance)  NFS SAN Storage 주문 권장
      * 다른 스토리지 유형에 관심이 있는 경우 [VMware System과 사용할 스토리지](select-storage-option-use-vmware.html)를 참조하십시오. 
      * 업링크 포트 속도: 1Gbps 듀얼 공용 및 사설 네트워크(비부착)
        * VMware vSAN 솔루션에 10Gbps 업링크를 권장합니다.
5. 새 IBM Cloud 데이터 센터에 새 배치를 작성 중인 경우 6단계를 진행하십시오. 기존 데이터 센터에 대한 확장 또는 배치의 경우에는 선호하는 백엔드 BCR VLAN + 프론트엔드 FCR VLAN을 선택하십시오. 예를 들어, 백엔드 BCR VLAN은 1101이고 프론트엔드 FCR VLAN은 2200입니다. **참고:** 새 배치이거나 새 DC로의 새 배치인 경우 백엔드 BCR 및 프론트엔드 FCR VLAN은 서버 주문 시 작성됩니다. 
6. **호스트 이름** 및 **도메인**을 입력하십시오.
7. 주문을 검토하고 **주문 완료**를 클릭하여 프로비저닝 프로세스를 시작하십시오. 

## vCenter Server 주문하기

vCenter는 Windows Server에 대한 추가 기능입니다. 이 구성은 최대 20개의 vSphere 호스트까지 확장됩니다. 대규모 구현의 경우 vCSA(vCenter Server Appliance)의 배치는 vSphere 클러스터로 직접 [vCSA(vCenter Server Appliance) 배치 및 구성](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)하는 것이 좋습니다. 

다음 단계에 따라 설치된 vCenter로 가상 서버를 주문하십시오. 

1. {{site.data.keyword.slportal_short}}에 로그인하십시오. 
2. **계정 > 주문하기**를 클릭하십시오.
3. 가상 서버 아래에서 **월별** 베어메탈 또는 공용/개인용 노드 VSI(Virtual Server Instance) 중 하나를 주문하십시오. 
  1. SoftLayer VSI(Virtual Server Instance)가 vCenter 6.0에 대한 자격을 얻으려면, 최소 **4 x 2.0 GHz 코어** 및 **RAM 4GB**에서 배치해야 합니다. 
  2. vCenter 배치 권장사항 목록은 [VMware vCenter Server&trade; 6.0 Deployment Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}를 참조하십시오.
4. 다음 정보를 입력하십시오. 
  * 권장되는 최소 서버 구성 기준
    * vCPU 코어 구성: 4 x 2.0 GHz 코어
    * RAM 구성: 12GB RAM
    * 소프트웨어: OS = Windows Server 2012 R2 Standard Edition(64비트)
    * OS 특정 추가 기능: vCenter 6
    * 첫 번째 디스크: 1 x 100GB (SAN)
    * 두 번째 디스크: 1 x 50GB (SAN)
    * 업링크 포트 속도: 1Gbps 공용 및 사설 네트워크 업링크

5. 새 IBM Cloud 데이터 센터로의 새 배치인 경우 아래 6단계를 진행하십시오. 이 배치가 기존 데이터 센터로의 확장 또는 배치인 경우 선호하는 백엔드 BCR VLAN + 프론트엔드 FCR VLAN을 선택하십시오. 예제에서 백엔드 BCR VLAN은 1101이고 프론트엔드 FCR VLAN은 2200입니다. (새 배치이거나 새 DC로의 새 배치인 경우 백엔드 BCR 및 프론트엔드 FCR VLAN은 서버 주문 시 작성됩니다.) 
6. **호스트 이름** 및 **도메인**을 입력하십시오.
7. 주문을 검토하고 **주문 완료**를 클릭하여 프로비저닝 프로세스를 시작하십시오. 

## 포터블 공용 및 사설 서브넷/IP 주소 주문

**참고:** VLAN이 완전히 프로비저닝되지 않은 경우 진행하지 마십시오.

서브넷은 VMware 게스트 가상 머신(VM) 및 VMware 호스트 커널 기반 트래픽의 주소 지정에 사용됩니다. 

1. 제어 포털에서 **네트워크 > IP 관리 > 서브넷**을 클릭하십시오.
2. 화면의 오른쪽 상단에서 **IP 주소 주문**을 클릭하십시오.
3. **포터블 사설**을 선택하십시오.
4. 적합한 VLAN을 선택하십시오(예: bcr01.wdc04: 1101)
5. **계속**을 클릭하십시오.
6. **IP 주소 주문** 양식을 완성하십시오.
7. 화면의 오른쪽 상단에서 **IP 주소 주문**을 클릭하십시오.
8. **주문하기**를 클릭하십시오.
9. 적용 가능한 각 VLAN에 대해 이 프로세스를 수행하십시오(예: 1101, 2200)
  1. VLAN에 대한 자세한 정보는 [VLAN 시작하기](/docs/infrastructure/vlans/getting-started.html)를 참조하십시오.

|서브넷 유형|서브넷 크기|바인딩 VLAN|vSphere 호스트 사용|
|---|---|---|---|
|포터블 - 개인용|/27 32 주소|**1101**|관리 VM|
|포터블 - 개인용|/27 32 주소|**1101**|iSCSI 및 vMotion에 대한 VM 커널 포트|
|포터블 - 개인용|/27 32 주소|**1101**|게스트 VM에 대한 개인용 IP|
|포터블 - 공용|/27 32 주소|**2200**|게스트 VM에 대한 공용 IP(선택사항)|
{: caption="표 2. 서브넷" caption-side="top"}

### 선택사항 – vSphere 호스트에서 공용 인터페이스 사용 안함

vSphere 공용 인터페이스를 사용하지 않는 경우 보안을 위해 사용 안함으로 설정할 수 있습니다. 

1. 제어 포털에서 **디바이스 > 디바이스 목록**을 클릭하십시오.
2. vSphere 호스트의 이름을 클릭하십시오.
3. 구성 표를 클릭하고 네트워크 섹션까지 아래로 스크롤하십시오.
4. 모든 호스트에 대해 적용 가능한 각 vSphere 호스트 eth1 및 eth3 쌍에 대해 **연결 끊기**를 선택하십시오. 

[{{site.data.keyword.slapi_full}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window}을 통해서도 수행할 수 있습니다. 

## vSphere 데이터 센터 클러스터 작성 및 구성 <!-- create and configure should be separate tasks-->

이제 vCenter Server에 로그인하고 vSphere 클러스터를 구성할 수 있습니다. 

1. 제어 포털에서 **디바이스 > 디바이스 목록**을 클릭하십시오.
2. vCenter 디바이스를 찾아서 이름을 클릭하십시오.
3. **디바이스 세부사항** 화면을 서버의 **네트워크** 섹션까지 아래로 스크롤하고 **개인용 IP 주소**를 기록해 두십시오.
4. **디바이스 세부사항** 화면을 아래로 스크롤하여 Windows OS 및 vCenter 소프트웨어에 대한 **비밀번호**를 둘 다 기록해 두십시오.
5. Microsoft 원격 데스크탑(RDP) 세션을 열고 공용 IP 주소를 통해 vCenter Server에 연결하십시오.
6. 4단계에서 확인한 비밀번호를 사용하여 로그인하십시오. **참고:** vCenter에 액세스하는 데 개인용 IP 주소가 사용되는 경우 IBM Cloud에 대한 활성 VPN 연결이 준비되어 있어야 합니다. VPN 액세스에 대한 자세한 정보는 [IBM Cloud 인프라 사설 네트워크에 대한 액세스 사용](/docs/customer-portal/getting-started.html#enable-private-network)을 참조하십시오.
7. 일반적인 [vSphere Client ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window}를 다운로드하고 설치하거나 `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/` 링크를 통해 vSphere 웹 클라이언트를 사용하십시오.
8. 3 및 4단계에서 확인한 IP 주소와 비밀번호를 사용하여 vCenter에 로그인하십시오. 
9. 왼쪽 분할창에서 vCenter 서버 이름을 마우스 오른쪽 단추로 클릭하고 **새 데이터 센터**를 선택하십시오.
10. 데이터 센터에 대한 적합한 이름을 입력하십시오.
11. 데이터 센터를 마우스 오른쪽 단추로 클릭하고 **새 클러스터**를 선택하십시오.
12. 클러스터 이름을 입력하십시오. 이때 클러스터 기능인 vSphere HA 또는 vSphere DRS를 켜지 마십시오.
13. **다음**을 클릭하십시오.
14. **EVC**를 사용 안함 상태로 두고 **다음**을 클릭하십시오.
15. _가상 머신과 동일한 디렉토리에 스왑 파일 기본 저장_을 승인하고 **다음**을 클릭하십시오.
16. **완료**를 클릭하여 클러스터를 완료하십시오.
17. 방금 작성한 새 클러스터를 마우스 오른쪽 단추로 클릭하고 **호스트 추가**를 선택하십시오.
18. vSphere 호스트 중 하나의 IP 주소 또는 호스트 이름을 입력하고 **사용자 이름** 필드에 **Root**를 입력하고 **비밀번호** 필드에 호스트에 대한 비밀번호를 입력하십시오. 
19. 호스트 요약, 라이센스 지정, 록다운 모드 화면까지 **다음**을 클릭하고 **완료**를 클릭하여 클러스터에 호스트 추가를 완료하십시오. 
20. 클러스터에 있는 각 vSphere 호스트에 18 및 19단계를 반복하십시오. 완료하고 나면 새 클러스터 아래 각 vSphere 호스트가 표시됩니다. 

### vSphere 호스트를 위한 기본 네트워크 구성 요소 구성

다음 단계에 따라 클러스터에 있는 vSphere 호스트에 대한 기본 구성 요소를 구성하십시오.

1. 첫 번째 vSphere 호스트를 선택하고 **구성** 탭을 클릭하십시오. 
2. **하드웨어** 섹션 아래에서 **네트워킹**을 선택하십시오. 이미 vmnic0이 포함된 vSwitch0이 있는 경우 vSwitch0 옆에 있는 **특성**을 클릭하십시오. 
3. **vSwitch 특성** 창에서 **네트워크 어댑터**를 선택하고 **추가** 단추를 클릭하십시오.
4. vmnic2를 선택하여 vSwitch0에 추가하고 **다음**을 클릭하십시오.
5. 두 vmnics 모두 **활성 어댑터**인지 확인하고 **다음**을 클릭하십시오.
6. **완료**를 클릭하십시오.
7. **포트** 탭을 클릭하여 vSwitch가 강조표시되어 있는지 확인하고 **편집**을 클릭하십시오.
8. **일반** 탭을 클릭하고 **MTU**를 9000으로 변경하십시오(점보 프레임).
9. **NIC 팀 구성** 탭을 클릭하고 로드 밸런싱을 **IP 기반 라우트** 해시로 변경하고 **확인**을 클릭하십시오.
10. 1단계에서 8단계를 사용하여 클러스터의 다른 vSphere 호스트에 대한 vmnics를 구성하십시오. 

이제 포트 그룹을 vMotion에 추가해야 합니다. 그룹을 VSS(Virtual Standard Switch) 또는 VDS(Virtual Distributed Switch)로 작성할 수 있습니다. 아래 예에 대해 VSS 스위치를 작성하게 됩니다. 

1. **구성** 탭을 선택하고 **네트워킹**을 선택하십시오.
2. vSwitch0의 **특성...**을 클릭하십시오.
3. **추가...**를 클릭하여 포트 그룹을 작성하십시오.
4. **VMkernel**을 선택하고 **다음**을 클릭하십시오.
5. 다음 정보를 사용하여 포트 그룹 특성을 채우십시오.
  * **네트워크 레이블:** 포트 그룹에 대한 적절한 이름
  * **VLAN ID(선택사항):** vMotion 트래픽의 VLAN ID(예의 경우 1101). VLAN ID를 통해 VMware가 특정 VLAN에 대한 트래픽에 태그를 지정할 수 있습니다. 
  * **vMotion에 이 포트 그룹 사용**을 선택하십시오.
6. **다음**을 클릭하십시오.
7. VLAN에 대한 **포터블 IP 주소**를 입력하십시오. SoftLayer 포털 **네트워크 > IP 관리 > VLAN**에서 포트 IP 주소를 가져올 수 있습니다. 올바른 VLAN을 선택하면 **서브넷** 아래 포터블 IP 주소 범위가 표시됩니다. 사용 가능한 포터블 IP 주소가 없거나 현재 풀이 고갈된 경우 '사설 서브넷/IP 주소 주문' 섹션의 단계를 따라 추가 포터블 IP 주소를 주문하십시오.
8. **다음**을 클릭한 후 **완료**를 클릭하여 완료하십시오.

다음 단계에 따라 VM 데이터 트래픽을 위한 포트 그룹을 작성하십시오.

1. vSwitch0의 **특성...**을 클릭하고 **추가, 가상 머신**을 선택하십시오.
2. 다음 정보를 사용하여 **포트 그룹 특성**을 채우십시오.
  * **네트워크 레이블:** 포트 그룹의 이름을 입력하십시오(예: VM Data)
  * **VLAN ID(선택사항):** VLAN ID를 입력하십시오. 예에서는 1101이 사용되었습니다. VLAN ID를 통해 VMware가 VLAN에 대한 트래픽에 태그를 지정할 수 있습니다. 

### 선택사항 - 추가 기능 VMware 라이센스 설치(NSX, vRealize, vSAN 등)

이제 VMware 환경이 설정되고 추가 구성, 게스트 VM 또는 VMware 추가 기능을 계속 배치할 준비가 되었습니다. VMware 추가 기능에 대한 라이센스는 IBM Cloud 제어 포털을 통해 구매할 수 있으며 vCenter 콘솔에서 추가할 수 있습니다. VMware 추가 기능 라이센스 주문 및 관리에 대한 자세한 정보는 [VMware vSphere 6 라이센스 주문 및 관리](vmware-vsphere-6-ordering-and-managing-licenses.html)를 참조하십시오.

## 다음 단계
이제 IBM Cloud 데이터 센터에서 실행 중인 기본 단일 사이트 VMware 환경이 준비되었습니다. 기본 구성에는 로컬 데이터 저장소만 있으며 VMware DRS, HA, 스토리지 DRS 및 방화벽과 같은 기능을 포함하지 않은 간소화된 구성이 가능합니다. 

자세한 정보는 [FAQ: VMware](vmware-faq.html)를 참조하십시오. 
