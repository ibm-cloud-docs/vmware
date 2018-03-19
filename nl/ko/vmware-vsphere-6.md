---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware 라이센싱 옵션 

VMware 관리자는 {{site.data.keyword.BluSoftlayer_full}} 엔터프라이즈급 글로벌 클라우드에 배치하여 비용 효율적인 하이브리드 클라우드 특성을 빠르게 인지할 수 있습니다. 주요한 {{site.data.keyword.BluSoftlayer_notm}} 차별화 요소는 vSphere 워크로드와 카탈로그를 VMware VM 또는 게스트 수정 없이 {{site.data.keyword.BluSoftlayer_notm}} 데이터 센터 내의 VMware vSpheres 환경에 프로비저닝할 수 있는 것입니다. 이러한 배치는 공통 vSphere 하이퍼바이저 및 관리/오케스트레이션 플랫폼을 사용하여 가능합니다. 

vSphere 6 Enterprise Plus 라이센스를 제공할 뿐만 아니라 {{site.data.keyword.BluSoftlayer_notm}}는 vCenter, NSX, vRealize, vSAN 및 SRM(Site Recovery Manager)에 대한 월별 라이센싱을 제공합니다.

## VMware vSphere

**사용 목적:** 실제 단일 서버에 여러 가상 서버를 구축하기 위해 프로세서, 메모리, 스토리지 및 네트워킹 리소스를 추출하는 단일 베어메탈 서버 가상화 OS 플랫폼입니다. 프라이빗 클라우드를 작성하기 위해 여러 개의 실제 서버를 함께 클러스터할 수 있습니다. 

**사용자 인터페이스:** vCenter Client, VMware API 및 VMware CLI

**기능:**
* vMotion 라이브 마이그레이션
* 고가용성
* 결함 허용
* 복제
* Nvidia GRID vGPU 가상화
* 워크로드 용량 최적화
* DRS(Distributed Resources Scheduler)
* 씬 프로비저닝
* 네트워크 I/O 제어

## VMware vCenter

**사용 목적:** 각 vSphere 호스트 내에서 컴퓨팅 리소스의 관리를 중앙 집중화합니다. vSphere 호스트는 개별적으로 관리할 수 있지만 vCenter 제어 아래 호스트를 배치하면 다음 기능을 사용할 수 있습니다.

**사용자 인터페이스:** 웹 클라이언트, 씩 클라이언트, VMware API 및 VMware CLI

**기능:**
* 관리 vSphere 호스트 및 게스트 가상 머신 내의 모든 측면에 대한 중앙 집중식 제어 및 가시성을 제공합니다. 
* 컴퓨팅 네트워크 및 스토리지 관리를 위한 vCenter 웹 클라이언트를 통한 인터페이스 보기의 단일 분할창을 제공합니다.
* 사전 최적화. vSphere 호스트 사이에 최대 효율성을 위해 리소스의 할당 및 최적화를 사용하도록 설정합니다.
* NSX, vRealize, vSAN 및 SRM(Site Recovery Manager)과 같은 기타 통합 추가 기능 및 서비스를 위한 확장 관리 기능.
* 모니터링, 경보 및 스케줄링. 클라우드 관리자는 vCenter 웹 클라이언트 내에서 이벤트 및 경보를 볼 수 있으며 스케줄된 조치를 구성할 수 있습니다.
* 자동화 엔진. vCenter는 vSphere API 웹 인터페이스를 통해 제공되는 태스크를 수행하는 엔진입니다. VMware vRealize Automation 및 vRealize Orchestration은 VMware API를 통해 vCenter 조치를 유도하는 애플리케이션 예입니다.

## VMware NSX

**사용 목적:** NSX는 클라우드 플랫폼 오퍼레이션을 지원하는 데 필수적인 SDN(Software-Defined Network) 기능을 제공합니다. 

**사용자 인터페이스:** vCenter Client, VMware API 및 VMware CLI

**기능:**
* 로드 밸런싱
* 방화벽
* 라우팅
* 논리 스위치
* VPN
* VxLAN 세그먼트화/터널 엔드포인트

## VMware vRealize

**사용 목적:** VMware vRealize 스위트는 이기종 하이브리드 클라우드를 관리하는 데 사용할 수 있는 엔터프라이즈급 클라우드 관리 플랫폼입니다. 

**사용자 인터페이스:** vCenter Client, VMware API 및 VMware CLI

**라이센스 모델:** 월별 프로세서 기준

**기능:**
* vRealize Automation: 개인화된 인프라, 애플리케이션 및 사용자 정의 IT 서비스의 자동화된 제공
* vRealize Operations: 지능형 상태, 성능, 용량 및 구성 관리 오케스트레이션
* vRealize Log Insight: 실시간 로그 관리 및 로그 분석

## VMware vSAN

**사용 목적:** VMware vSAN은 vSAN 클러스터의 모든 호스트에 액세스할 수 있는 비공유 스토리지 디바이스로 집계되고 풀링될 각 vSphere 호스트의 로컬 스토리지 드라이브를 사용으로 설정하는 분배된 스토리지 기술입니다. 

**사용자 인터페이스:** vCenter Client, VMware API 및 VMware CLI

**기능:**
* 분산 호스트 기반 스토리지
* 비공유 아키텍처
* 최대 64개 노드로 확장
* 짧은 대기 시간
* 구성 가능한 결함 허용

## VMware SRM(Site Recovery Manager)

**사용 목적:** VMware SRM(Site Recovery Manager)은 프라이빗 클라우드 환경에 있는 사이트 전체에서 애플리케이션 가용성 및 모바일을 사용 가능하도록 설정합니다. 가상 머신의 캡슐화 및 격리를 충분히 활용하면 Site Recovery Manager에서 복구 시간 목표(RTO)를 충족시키도록 재해 복구를 쉽게 자동화할 수 있습니다. 또한 SRM은 비즈니스 연속성 플랜과 연관되는 비용을 줄이고 가상 환경 복구에 대한 낮은 위험의 예측 가능한 결과를 달성하도록 도움을 줍니다. 

**사용자 인터페이스:** vCenter Client, VMware API 및 VMware CLI

**기능:**
* 중단 없는 복구 테스트
* 자동화된 오케스트레이션 워크플로우
* 네트워크 및 보안 설정의 자동 복구
* 사용자 정의 자동화에 대한 확장성
* 오케스트라식 vCenter 간 vMotion
* 중앙 집중식 복구 플랜
* 정책 기반 관리
