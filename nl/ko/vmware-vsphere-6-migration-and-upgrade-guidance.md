---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  VMware vSphere 6로 마이그레이션 및 업그레이드

VMware 관리 콘솔 분할창을 사용하여 VMware 클라우드 환경을 {{site.data.keyword.BluSoftlayer_full}} 데이터 센터에 빠르고 쉽게 확장하거나 이동시킬 수 있습니다. vSphere 워크로드를 마이그레이션 및 업그레이드하려면 안내서 대로 다음 단계를 사용하십시오.
{:shortdesc}

1. 데이터를 수집하십시오.
2. 기존의 아키텍처를 검토하십시오.
  1. 리소스 활용도(CPU/메모리/스토리지).
  2. 성장율을 추적하고 예상합니다.
  3. 다가오는 미래 프로젝트를 식별하십시오.
  4. 지정된 VLAN/서브넷/ETC가 배치되었는지 확인하십시오(제어 포털에서 사용 가능).
  5. 솔루션에 대한 사용에서 자체 정의 RFC1918 (사설) 서브넷을 찾으십시오. 
3. VMWare 6 문서를 검토하고 VMWare 커뮤니티에 가입하십시오. 
  1. [VMware vSphere documentation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://communities.vmware.com/welcome){: new_window}
4. VMWare 6를 지원하도록 관리 팀의 교육을 업데이트하십시오.
5. 새 아키텍처를 계획하고 설계하십시오.
6. 규제 준수를 기반으로 하는 [Data center ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window}를 선택하십시오. IBM Cloud 영업 팀과 협업하여 제품/서비스의 가용성에 따라 후보 위치를 세분화하십시오. 
7. 필수 VLAN 및 서브넷을 정의하십시오(포터블 공용 IP 및 사설 IP).
8. vSphere Server를 설계하십시오. 
  1. 현재 IBM Cloud 서버 카탈로그를 검토하십시오. 이중 업링크, 이중 전원 공급 장치 및 로컬(부트) 디스크용 RAID-1과 함께 Intel Xeon v3 Server를 권장합니다. 
  2. VMWare를 사용하는 대부분의 고객은 N+1 하드 용량 상한(모든 VM을 (유지보수/장애/등을 위해) 제거된 단일 노드와 함께 문제 없이 서버에 할당할 수 있음)을 준수합니다. 
  3. 많은 고객들은 짧은 컴퓨팅 전환 시간으로 인해 표준 값인 60-75%와 비교하여 더 높은 "소프트 상한"인 80%('n' 서버 구성에서 80% 용량)를 원합니다. 
  4. 외부 공급업체의 vSphere 게스트에 대해 외부 OS 라이센싱(예: Microsoft, Red Hat)이 필요할 수 있습니다. 
  5. [Performance Best Practices for VMware vSphere 6.0 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}를 검토하십시오. 
9. vCenter Server를 설계하십시오. 
  1. 일반적으로 중간 규모의 VSI(Virtual Server Instance)가 소형 환경(8 vCPU + 16GB RAM)의 시작점입니다. 반면, 베어메탈은 대형 환경에 사용됩니다. 
  2. vCenter를 VSI Windows 가상 머신에 OS 추가 기능 또는 어플라이언스로 배치할 수 있습니다. 
    1. 참조 링크:
        * [vCenter Server 6.0 requirements for installation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server Performance and Best Practices ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [VMware vSphere 6로 vCSA(vCenter Server Appliance) 배치 및 구성 ](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. VMWare 이외의 서버: 필요하거나 적절하게 계획할 수 있는 VMWare 이외의 서버(가상 또는 베어메탈)를 식별하고 계획하십시오. 
11. 스토리지:
  1. 환경에 대한 스토리지 플랜을 개발하십시오. 가상화를 위한 스냅샷 영역이 있는 내구성(Endurance) 2 IOPS/GB가 처음 스토리지 플랜으로 적절하지만 가상 데이터베이스 또는 다른 고성능 애플리케이션이 사용되는 경우에는 4 IOPS/GB 티어가 더 적합합니다. 일반적으로 NFS 스토리지를 권장합니다.   
  2. 선택사항 매트릭스는 [VMware 시스템과 사용할 스토리지](select-storage-option-use-vmware.html)에서 찾을 수 있습니다.
  3. 스냅샷 공간은 일반적으로 특정 시점의 복원에 대한 보조 수단으로 사용됩니다. 프로세스가 매우 효율적이고 쉽게 확장할 수 있으므로 10%에서 시작하는 것이 좋습니다. 
12. 백업:
  1. 기존 백업 전략이 작동하는지 확인하십시오. 백업 전략이 없는 경우에는 작성해야 합니다. 
  2. 고유 백업 솔루션을 사용할 수 있습니다. vSphere Enterprise Plus 라이센싱에 포함되어 있는 백업 기능을 사용할 수 있습니다(VEEAM과 같이 최적화된 써드파티 솔루션 또는 일반적인 IBM Cloud r1soft 백업). 
13. 마이그레이션 전략을 개발하십시오.
  1. [Best practices to install or upgrade to ESXi 6.0 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kb.vmware.com/s/article/2109712){: new_window}를 검토하십시오.
  2. 기존의 DNS 및/또는 IP 구성을 검토하고 필요에 따라 TTL을 줄이십시오. 
  3. 소스 호스트, 대상 호스트, 소스 IP, 대상 IP 및 연관된 DNS 항목을 포함하도록 VM에 대한 플랜을 개발하십시오. 
  4. 대부분의 시나리오에서는 VM별 VM(VM-by-VM) 마이그레이션을 수행한 후에 공용 및 사설 네트워크 구성을 업데이트하는 것이 좋습니다. 이전 버전에서 새 버전으로 이동하는 경우 일반적으로 VM을 종료하고 환경 간에 _분리/연결_을 수행하여 간단히 "복사 및 배송"하는 것이 좋습니다. 위치 간에 이동 중이라면 장거리 vMotion이 가능합니다. 
  5. 환경 검증을 위한 테스트 플랜을 개발하십시오. 
  6. 사용자와 변경/유지보수 창을 조정하십시오. 개별 VM 유지보수 창은 문제점 해결을 위한 시간 뿐만 아니라 데이터 전송, VM 구성, DNS 변경 및 전파를 설명할 수 있습니다. 
14. 새 환경을 배치하십시오.
  1. [VMware vSphere 6을 시작하십시오](vmware-vsphere-6-getting-started.html).
  2. 새 vSphere 및 vCenter Server를 주문하십시오(그 외 필요한 다른 서버 포함).
      **참고:** 적절한 "비부착" 네트워크 업링크가 선택되었는지 확인하십시오. 
  3. 적합한 스토리지를 주문 및 구성하십시오([IBM File Storage for IBM Cloud with VMware용 아키텍처 안내서 ](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html))
  4. 새 VLAN 및 포터블 서브넷을 주문하십시오(자세한 아키텍처 다이어그램 및 조정이 필요할 수 있음). 
  5. vSphere Server와 통신하도록 vCenter를 구성하고 환경을 구성하십시오. 
  6. 라이브 환경에서 백업을 작성하십시오. 
  7. 마이그레이션 플랜 및 연관된 테스트 플랜을 실행하십시오. 
  8. 새 환경에서 백업을 구현하십시오.
  9. 새 환경을 운영하십시오. 
  10. 레거시 환경을 해제하십시오. 
