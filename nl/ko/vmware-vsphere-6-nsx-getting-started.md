---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX 시작하기 

NSX는 사용자 인프라에 적용하기 위해 라이센스 부여로 배치됩니다. {{site.data.keyword.BluSoftlayer_full}}는 프로세서별 기준으로 라이센스를 제공합니다(가격 책정은 CPU당 코어 수를 변경하지 않습니다). NSX 라이센스는 NSX 컴포넌트(관리, 제어 또는 데이터 플레인)를 사용하는 모든 서버에 필요합니다. NSX는 추가 네트워킹 기능을 플랫폼에 추가합니다. 온프레미스 프라이빗 클라우드에서 제공자 및 확장을 포함하는 하이브리드 클라우드 환경, 테넌트 세그먼트화 및 시스템 보안을 위한 강력한 오버레이 네트워크를 작성할 수 있습니다.
{:shortdesc}

RESTful API를 통해 자동화 지원 환경에 방화벽, 로드 밸런싱, VPN, NAT 서비스 및 VXLAN 기반 마이크로 세그먼트화를 추가할 수 있습니다. 

## 라이센스 추가
라이센스는 다음 프로세스를 사용하여 서버에 추가됩니다.
1. vSphere Client를 사용하여 vCenter Server에 로그인하십시오.
* **관리** 아래의 **라이센싱**을 클릭하십시오.
* **솔루션**을 클릭하십시오.
* 제품 목록에서 **VMware NSX for vSphere**를 클릭하십시오.
* **라이센스 키** 또는 **새 라이센스 키 입력**을 클릭하십시오.
* **확인**을 클릭하십시오.

## NSX 설치

1. NSX Manager를 배치하십시오.
* NSX Manager를 vCenter Server에 등록하십시오.
* vSphere 웹 클라이언트는 NSX Manager를 통해 NSX Controller 인스턴스를 배치합니다.
* NSX Manager를 사용하여 vSphere 호스트를 준비하여 클러스터에 있는 호스트에 VIB를 설치하십시오.
* NSX Controller가 적용 가능한 모든 호스트에 배치되고 나면 Edge Gateway, 로드 밸런서 및 방화벽과 같은 NSX 컴포넌트를 정의하고 구성하십시오.

## 배치 고려사항

솔루션에 대한 NSX를 사용하려면 표준 컴퓨팅 노드 이외에 추가 vSphere 노드를 사용해야 합니다.

**NSX Manager**<br />
관리 클러스터의 IBM Informix 가상 어플라이언스에는 vCenter와의 1:1 관계가 성립되어 있습니다. 일반 HA vSphere 기능을 권장합니다. NSX Manager에는 스케줄된/온디맨드 백업 기능이 포함되어 있으며 vCenter, 제어기, NSX Edge 리소스 및 ESXi 호스트에 대한 IP 연결이 필요합니다. NSX Manager가 동일한 서브넷/VLAN에 vCenter로 배치되지만 반드시 필요한 것은 아닙니다. 일반 VM 크기는 다음과 같습니다. 

|NSX 릴리스|vCPU|메모리|OS 디스크|
|---|---|---|---|
|6.2 Small|4|12GB|60GB|
|6.2 Default|4|16GB|60GB|
|6.2 Large Scale|4|24GB|60GB|
{: caption="표 1. NSX Manager 일반 VM 크기" caption-side="top"}

**NSX Controller 노드**<br />
NSX Controller 노드는 NSX Manager UI에서 가상 어플라이언스로 배치됩니다. 각 어플라이언스는 일반적으로 NSX Manager로 동일한 서브넷에 있는 별개의 IP 주소를 통해 통신하지만, 필수 요구사항은 아닙니다. 세 개 이상의 제어기 VM을 세 개 이상의 분리된 실제 vSphere 노드에 배치하는 것이 좋습니다. 이러한 작업은 NSX 관리자가 정의하는 작업 분석을 사용하여 활성-활성-활성으로 작동합니다. 노드가 실패하는 경우 남아 있는 제어기에 워크로드를 재분배하기 위해 "다수 원칙" 장애 복구가 발생합니다. NSX는 기본적으로 이 디자인 사례를 강제 실행하지 않습니다. 원시 vSphere 선호도 방지 규칙을 사용하여 둘 이상의 제어기 노드가 동일한 ESXi 서버에서 배치되는 것을 방지합니다. VM당 일반 VM 크기는 다음과 같습니다. 

|Controller VM|vCPU|예약|메모리|OS 디스크|
|---|---|---|---|---|
|3|4|2048Mhz|4GB|20GB|
{: caption="표 2. NSX Controller 일반 VM 크기" caption-side="top"}

**NSX Switch**
업그레이드된 VDS(Virtual Distributed Switch)는 분배된 기능을 구현하기 위해 모든 호스트에 배치됩니다. 

**NSX Edge Services Gateway**<br />
환경에서 필요한 대로 다중 기능 VM 어플라이언스로 배치됩니다. 라우팅 전용은 최대 8개 게이트웨이의 활성 클러스터를 배치할 수 있습니다. 다른 모든 서비스의 경우 활성-대기 배치에서 배치됩니다. VM 환경의 외부에 있는 통신은 NAT 풀, VIP 및 VPN 엔드포인트를 포함시키려면 IBM Cloud 지정 포터블 IP가 필요합니다. 

|게이트웨이 형태|vCPU|메모리|특정 사용법|
|---|---|---|---|
|X-Large|6|8GB|L7 고성능 LB에 적합|
|Quad-Large|4|1GB|고성능 ECMP 및 FW 배치에 적합|
|Large|2|1GB|소형 DC & 단일 서비스|
|Compact|1|512MB|소형 배치, 단일 서비스 사용 또는 PoC|
{: caption="표 3. NSX Edge Services" caption-side="top"}

