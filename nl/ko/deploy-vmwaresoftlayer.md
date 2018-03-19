---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware 배치에 대한 쿡북 사용

VMware 관리자는 {{site.data.keyword.BluSoftlayer_full}} 엔터프라이즈급 글로벌 클라우드에 배치함으로써 비용 효율적인 하이브리드 클라우드 특성을 빠르게 인지할 수 있습니다. vSphere 워크로드 및 카탈로그를 VMware VM 또는 게스트에 대한 수정 없이 {{site.data.keyword.cloud_notm}} 데이터 센터 내의 VMware vSphere 환경으로 프로비저닝할 수 있습니다. 이러한 배치는 공통 vSphere 하이퍼바이저 및 관리/오케스트레이션 플랫폼을 사용하여 가능합니다. 또한 vSphere 구현을 통해 VMware vCloud Suite의 다른 컴포넌트 즉, vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator 및 NSX를 사용으로 설정할 수 있습니다. 

VMware 쿡북 시리즈의 핵심 목표는 IBM Cloud 인프라 내의 VMware vSphere 환경을 배치하여 vSphere 관리자를 지원하는 것입니다. 쿡북은 vSphere를 관리하는 방법을 교육하기 위한 것이 아닙니다. vSphere 관리에 대한 자세한 정보는 [VMware Education ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}을 참조하십시오.

{{site.data.keyword.cloud_notm}}에는 베어메탈 인스턴스와 네트워크, 백업과 복구 구성요소 및 스토리지를 셀프 서비스 방식으로 이용하기 위한 유연성을 VMware 관리자에게 제공하는 여러 특정 기능이 있습니다. 이러한 구성 요소를 사용하여 온프레미스 vSphere 구현(VMware@Home)을 확장하거나 대체하기 위해 빌드될 수 있는, 완전한 기능적 vSphere 구현을 배치할 수 있습니다.

관리자는 다음 쿡북을 사용할 수 있습니다. 

* [단일 사이트 VMware 환경 빌드](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html): vSphere 관리자로서 내구성(Endurance) 또는 성능(Performance) 블록 스토리지 또는 QuantaStor 사용을 포함하여 환경을 빌드하는 단계를 살펴봅니다. 
* [Migrate vSphere Workloads ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}: vSphere 구현이 IBM Cloud 데이터 센터에 배치된 후 워크로드[가상 머신(VM)]를 VMware로 마이그레이션하는 데 도움을 주기 위한 시나리오가 제시됩니다. 
* [Leverage NSX® ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}: VMware NSX를 활용하여 소프트웨어 정의 네트워킹(SDN) 구성 요소를 VMware@SoftLayer 배치에 제공할 수 있습니다. 
* [Catalogic ECX ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}: 하이브리드 IT 인프라에서 CopyData를 관리하고 분석할 수 있습니다. 인프라는 Catalogic Software 지능형 CopyData 관리 플랫폼, ECX를 사용하고, NetApp Private Storage 및 VMware vSphere 인프라를 사용하여 IBM Cloud 인프라에 배치됩니다. 
* [VMware Back Up ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}: 이 쿡북은 VMware 배치에서 실행 중인 VMware 기반 워크로드(VM)를 백업, 복구 및 아카이브하기 위한 대체 접근 방식에 대해 설명합니다. 
* [VMware Disaster Recovery ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}: 이 쿡북은 VMware를 사용하여 재해 복구(DR) 솔루션을 설정하는 두 가지 유스 케이스에 대해 설명합니다. 첫 번째는 온프레미스 VMware 환경과 연결되며 이를 통해 온프레미스 워크로드를 복구할 수 있습니다. 두 번째는 {{site.data.keyword.cloud_notm}} 데이터 센터에서 VMware 워크로드를 복구하는 유스 케이스입니다. 
* [Vormetric Encryption of VMware ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}: 유스 케이스에서는 VM 데이터를 암호화하여 Vormetric이 VMware 워크로드를 보호하는 방법을 보여줍니다. 
* [Deploy a trusted cloud solution with IBM, VMware, and HyTrust ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}: 하이퍼바이저 및 관리 애플리케이션을 통해 하드웨어에서 신뢰 체인을 작성하기 위해 다양한 아키텍처 요소를 통합할 수 있습니다. 


**참고:** 쿡북은 숙련된 vSphere 관리자를 대상으로 합니다. 포함되어 있는 일부 주제에서는 독자들이 vSphere 및 vCenter를 설치하고 구성하기 위한 기본 배치 스킬을 보유하고 있다고 간주합니다. 
