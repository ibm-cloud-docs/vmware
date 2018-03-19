---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6로 vCSA(vCenter Server Appliance) 배치 및 구성  

다음 단계에 따라 VMware vCenter Server Appliance를 배치하십시오.
{:shortdesc}

**전제조건**
* 호환 가능한 브라우저가 설치된 Windows 시스템
  * Internet Explorer/Firefox/Chrome
* VMware vCenter Server Appliance를 지원하기 위해 적합한 리소스가 포함된 vSphere 호스트
  * 필수 시스템 리소스에 대한 자세한 정보는 [Minimum requirements for the VMware vCenter Server 6.0 Appliance ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kb.vmware.com/s/article/2106572){: new_window}를 참조하십시오.
* vCSA ISO 이미지
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* ISO 마운트 기능
* IBM Cloud 사설 네트워크에 대한 액세스 권한이 있는 VPN 세션

**vCenter Server Appliance 배치 및 구성**

1. vCSA(vCenter Server Appliance) ISO를 마운트하십시오.
2. 호환 가능한 브라우저에서 vcsa-setup.html을 여십시오.
3. VMware Client 통합 플러그인의 설치를 검토하고 승인하십시오.
4. **허용**을 클릭하십시오.
5. **설치**를 클릭하십시오.
6. 라이센스 계약의 이용 약관을 검토하고 동의한 후 **다음**을 클릭하십시오.
7. FQDN 또는 사설 IP 주소와 vCSA를 설치하려는 VMware 호스트의 사용자 이름 및 비밀번호를 입력하십시오. **다음**을 클릭하십시오.
8. 인증 경고를 허용하려면 **예**를 클릭하십시오.
9. 적절한 어플라이언스 이름 및 OS 비밀번호를 입력하고 **다음**을 클릭하십시오.
10. 배치 유형에 대해 '임베디드 Platform Services Controller로 vCenter Server 설치'를 선택한 후 **다음**을 클릭하십시오.
11. 'SSO 도메인 작성'을 클릭하고 **다음**을 클릭하십시오. <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. 어플라이언스 크기를 선택하고 **다음**을 클릭하십시오.
13. 데이터 저장소를 선택하고 **다음**을 클릭하십시오.
14. '임베디드 데이터베이스(PostgreSQL) 사용'을 선택하고 **다음**을 클릭하십시오.
15. 다음 정보를 입력하여 네트워크 구성을 설정하십시오.
  1. 네트워크
  * IP 주소 패밀리
  * 네트워크 유형
  * 네트워크 주소
  * 시스템 이름
  * 서브넷 마스크
  * 네트워크 게이트웨이
  * 네트워크 DNS 서버
      * 자세한 정보는 [로컬 DNS 분석기 개념](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-)을 참조하십시오.
  * 시간 동기화 구성
  * **다음**을 클릭하십시오.
16. 설정을 검토한 후 **완료**를 클릭하십시오. vCSA 인스턴스가 프로비저닝됩니다. 

