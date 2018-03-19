---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware용 EVault 백업 클라이언트

VMware 서버에서 EVault 백업 클라이언트를 설치하는 작업은 대상 ESX Server 내의 쉘 또는 터미널에서 일련의 명령을 통해 수행할 수 있습니다. 이 프로시저에서는 VMware 서버에의 EVault 백업 클라이언트를 설치하는 데 필요한 단계를 설명합니다.
{:shortdesc}

에이전트를 설치하려면 다음 명령을 사용하여 `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` 패키지를 다운로드하고 대상 ESX Server에 복사하십시오. 

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**참고:**  대상 ESX Server에서 로컬로 다음 단계를 수행해야 합니다.

1. 패키지에서 파일을 추출하십시오. 이를 수행하려면, 다음 명령을 사용하십시오(“PACKAGENAME”은 “Agent-VMware-ESX-Server-6.71”일 수 있음).<br/>`tar xvfz PACKAGENAME.tar.gz`
2. 패키지를 추출한 디렉토리로 이동하십시오.
3. 설치 스크립트를 실행하십시오. <br />`# ./install.sh`<br/><br/>
**참고:**  설치 스크립트는 웹 등록(주소, 포트 번호 및 인증) 및 로그 파일 이름과 같은 구성 정보를 입력하도록 대화식으로 프롬프트가 표시됩니다.

이 서버에 대한 WebCC 사용자 이름을 입력하십시오.

4. WebCC 사용자 이름을 요청하는 프롬프트에 대한 입력으로 **EVault 백업 사용자 이름**을 입력하십시오. EVault 백업 사용자 이름를 보기 위한 지시사항에 대해서는 [EVault 백업 스토리지 세부사항 보기](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal) 프로시저를 참조하십시오.
5. WebCC 비밀번호를 요청하는 프롬프트에 대한 입력으로 EVault 백업 비밀번호를 입력하십시오.
6. 설치가 완료되면 완료 메시지가 표시되고 에이전트 디먼이 실행됩니다.


기타 설치 참고:<br/>
설치가 성공하는 경우 Install.log 파일이 설치 디렉토리에 작성됩니다.<br/>
예: `/opt/BUAgent/Install.log`

설치가 실패하고 롤백되는 경우 설치 로그가 `<Installation Failure directory>`에 작성됩니다.<br/>
설치에 실패했지만 롤백되지 않는 경우 설치 로그는 `<Installation Kit directory>`에 작성됩니다.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
위 링크를 보기 위해서는 {{site.data.keyword.BluSoftlayer_full}} VPN에 연결되어 있어야 합니다. IBM Cloud VPN에 연결에 대한 자세한 정보는 [IBM Cloud 인프라 사설 네트워크에 대한 액세스 사용](/docs/customer-portal/getting-started.html#enable-private-network)을 참조하십시오.
