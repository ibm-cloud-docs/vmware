---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# VMware 시스템과 사용할 스토리지
스토리지에 관련해서 여러 가지 옵션이 있습니다. 개인용, 공유를 선택하거나 고유 스토리지 솔루션을 가져올 수 있습니다. 다음 정보를 사용하여 사용자 워크로드에 적합한 스토리지 솔루션이 무엇인지 결정하는 데 도움을 받을 수 있습니다. 

표 1은 스토리지 티어 및 워크로드가 놓일 위치를 포함합니다. 
<table border="1" cellpadding="0" cellspacing="0">
        <caption>표 1. 스토리지 티어</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>티어 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>티어 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>티어 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>비즈니스 용도</strong></p>
			</td>
			<td style="width:160px;">
				<p>고성능 및/또는 고가용성 프로덕션 애플리케이션, 데이터베이스 및 데이터</p>
			</td>
			<td style="width:160px;">
				<p>중요하지 않은 업무용 테스트 및 개발 애플리케이션, 데이터베이스 및 데이터</p>
			</td>
			<td style="width:160px;">
				<p>중요하지 않은 업무용 데이터 스토리지, 백업 및 아카이브</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>성능</strong></p>
			</td>
			<td style="width:160px;">
				<p>높음(SSD, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>중간(SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>낮음(SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>보증된 IOPS</strong></p>
			</td>
			<td style="width:160px;">
				<p>예</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>고가용성(HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>예</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>복제</strong></p>
			</td>
			<td style="width:160px;">
				<p>예</p>
			</td>
			<td style="width:160px;">
				<p>예</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>스냅샷</strong></p>
			</td>
			<td style="width:160px;">
				<p>예</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
			<td style="width:160px;">
				<p>아니오</p>
			</td>
		</tr>
	</tbody>
</table>


## VMware 개인용 및 공유 스토리지 옵션

여러 스토리지 옵션 중에서 선택할 수 있습니다. 개인용 스토리지의 경우 로컬 디스크 옵션, VSAN 또는 QuantaStor를 선택할 수 있습니다. 공유 스토리지의 경우 내구성(Endurance) 또는 성능(Performance) 스토리지를 선택할 수 있습니다. 사용자 스토리지를 가져오기로 결정한 경우 NetApp OnTap Edge, NPS(NetApp Private Storage), {{site.data.keyword.IBM}} Spectrum Accelerate 및 소프트웨어 정의 스토리지를 포함하여 여러 “개인용” 옵션이 있습니다. 표 2와 표 3에서는 사용자 편의를 위해 옵션을 나란히 비교합니다. 

## 개인용 스토리지 옵션

단일 테넌트 환경에서 VMware에 연결하기 위한 여러 스토리지 옵션이 있습니다.  

* 로컬
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## 로컬 스토리지

ESX로 IBM Cloud 고객 포털에서 {{site.data.keyword.baremetal_short}}를 주문하고 원하는 디스크[SATA, SA SCSI(Serial Attached SCSI) 또는 SSD]를 선택하십시오.
 
고유 ESX 라이센스를 가져올 수 있지만 변경을 알리기 위해 지원 팀에 티켓을 열어야 합니다. 

* 권장되는 워크로드: 티어 3
* 성능: 제한됨: RAID 및 디스크 유형에 따라 달라집니다. SSD는 성능 향상을 위한 비용 증가를 표시합니다.
* 확장성: 섀시에 있는 드라이브 슬롯의 수로 제한됨
* 프로토콜: 적용할 수 없음
* 비용: 낮은 자본 비용(CAPEX) 및 운영 비용(OPEX)
* HA: 사용할 수 없음
* 복제: [vSphere 복제 가상 어플라이언스 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 신뢰성: 여러 개의 단일 장애 지점



## vSAN [1]

* 권장되는 워크로드: 티어 1
* 성능: 호스트 구성에 따라 호스트당 90K+ IOPS
* 확장성: v5.5 VMDK(virtual machine disk) 최대 2TB, v6.0 VMDK의 경우 최대 62TB입니다. 추가 노드로 확장하십시오. 
* 프로토콜: 독점
* 비용: CAPEX 및 OPEX 둘 다에 대해 중간 수준
* HA: 호스트 및 디스크 장애 모두 지원됨. VMware v6에서 장애 도메인이 지원됩니다. 
* 복제: [vSphere 복제 가상 어플라이언스 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 복제 및 재해 복구:
    1. VMware vCenter Server를 통해 VM 백업 스케줄링
    2. VM 스냅샷 작성
    3. VM에 대해 작성된 데이터 DE
    4. VM 복원
 * 신뢰성: 7개 이상의 호스트에서 최대 3개까지 호스트 장애가 허용됩니다. VMware v6에서 장애 도메인이 도입되었습니다.    

[1] vSan 6.2의 새 기능인 확대 클러스터를 통해 호스트가 동일한 데이터 센터의 다른 Pod에 있을 수 있습니다(유효성 검증 테스트가 진행 중임). <!-- Should this in progress mention be removed? -->

vSAN 5.5는 기존에 보유한 고유 라이센스 사용(BYOL)시에만 사용 가능합니다. Avago LSI MegaRAID SAS 9361-8i 디스크 제어기를 사용하는 경우 VMware에 의해서만 지원됩니다. 

vSAN 6.0은 CPU 라이센스 청구 기반으로 IBM Cloud 포털에서 직접 사용 가능합니다. 

## QuantaStor

[OSNexus Solution Design Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window}를 사용하여 VMware를 QuantaStor와 연결할 수 있습니다.

* 권장되는 워크로드: 티어 2 및 3 
* 성능: 드라이브, RAID 및 디스크 사용의 수를 기반으로 하는 변수(iSCSI 또는 NFS)  
* 확장성: v3 단일 프레임은 128TB를 지원합니다. 확장되지 않습니다. 
* 프로토콜: iSCSI, NFS 및 SMB 
* 비용: CAPEX 및 OPEX 둘 다에 대해 높음 
* HA: 사용할 수 없음  
* 복제: 기본 제공 복제 기능. SRA는 사용할 수 없습니다. vSphere 복제 어플라이언스도 사용할 수 있습니다.  
* 신뢰성: 격납장치 및 RAID 제어기에 대한 단일 장애 지점입니다. 


<a name="NetApp"></a>
## NetApp Data OnTap Edge

NetApp 또는 IBM에서 NetApp 디바이스를 구매해야 합니다. {{site.data.keyword.BluSoftlayer}} 데이터 센터의 {{site.data.keyword.baremetal_short}}에 설치해야 합니다. 

VMware과 NetApp의 연결에 대한 자세한 정보는 다음 링크를 참조하십시오. 
* [NetApp ONTAP Select ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* 권장되는 워크로드: 티어 2 및 3
* 성능: 드라이브 및 RAID 수를 기반으로 하는 변수
* 확장성: 110TB를 지원합니다. 확장되지 않습니다. 
* 프로토콜: iSCSI, NFS 및 SMB
* 비용: CAPEX 및 OPEX 둘 다에 대해 중간 수준
* HA: 사용할 수 없음
* 복제: SnapMirror를 지원합니다. 또한 [vRealize Automation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/products/vrealize-automation){: new_window}을 사용하여 아카이브됩니다.
* 신뢰성: 격납장치 및 RAID 제어기에 대한 단일 장애 지점입니다. 

<a name="NPS"></a>
## NetApp 개인용 스토리지

NetApp 또는 IBM에서 NetApp 디바이스를 구매해야 합니다. IBM Cloud 데이터 센터 주변의 코로케이션 사이트 중 하나에 설치하고 Direct Link 코로케이션 또는 Direct Link Cloud를 사용하여 연결해야 합니다.

NetApp으로 VMware에 연결에 대한 자세한 정보는 다음 링크를 참조하십시오. 
* [NetApp Private Storage for IBM Cloud ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* 권장되는 워크로드: 티어 1
* 성능: NetApp 모델에 따라 다름
* 확장성: 증가한 용량 및 IOPS에 대해 드라이브 및 프레임 추가를 지원합니다. 
* 프로토콜: iSCSI, NFS 및 SMB
* 비용: CAPEX 및 OPEX 둘 다에 대해 높음
* HA: 듀얼 헤드 및 제어기
* 복제: SnapVault 및 SnapMirror를 지원합니다. 또한 [vRealize Automation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/products/vrealize-automation)을 사용하여 아카이브됩니다.
* 신뢰성: 높은 중복성 및 MPIO 지원

<a name="IBM"></a>
## IBM Spectrum Accelerate

IBM Spectrum Accelerate 개인용 스토리지 옵션은 IBM Cloud 고객 포털에서 사용할 수 없습니다. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* 권장되는 워크로드: 티어 1
* 성능: 디스크 수, SSD(선택사항) 및 각 “노드” VM에 지정된 메모리 양에 따라 달라집니다.
* 확장성: ~8 - 325TB 스케일 사용 가능
  * 최소 용량: 3개 VM x 6개 드라이브
  * 최대 용량: 15개 VM x 12개 드라이브
  * IBM Hyper-Scale Manager를 통해 40PB 이상 사용 가능하며 144개로 가상 배열 확장
  * 더 많은 노드를 추가하여 중단 없이 용량 확장
  * 지원되는 노드 당 1 x 500 또는 800GB SSD
* 프로토콜: iSCSI 전용
* 비용: 가격 책정 모델 및 노드에 배치된 실제 머신에 따라 달라집니다. 높은 CAPEX. 라이센싱에 따라 중간부터 낮은 OPEX.
  * 사용 가능한 용량의 2진(TiB) 당 가격이 책정됨
  * 특정 하드웨어 구성과 연결되지 않습니다. 예: 200TiB 라이센스를 1개의 200TiB 인스턴스, 2개의 100TiB 인스턴스 또는 4개의 50TiB 인스턴스 등 다양한 방법으로 배치할 수 있습니다. 
  * 제공되는 두 가지 방법: 영구 라이센스[1년 구독 및 서비스(S&S) 포함] 및 월별 라이센스(S&S 포함)
* HA: 클러스터된 솔루션
* 복제: [vRealize Automation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/products/vrealize-automation){: new_window} 또는 SRA를 사용하여 아카이브되며 VMware의 SRM(Site Recovery Manager)으로 실제 IBM XIV에서 복제하는 데 사용할 수 있습니다. 
  * [vSphere Replication ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* 신뢰성: 높은 중복성 및 MPIO 지원. 사용 가능한 노드는 클러스터를 관리할 수 있습니다. 현재 다음 기능은 하드웨어 기반 IBM XIV에서 IBM Spectrum Accelerate에 의해 지원되지 않습니다. 
  * 세 개 사이트 미러링
  * iSCSI(IBM Hyper-Scale Mobility)
  * USG v6
  * 6TB 디스크 드라이브
  * SMI-S(Storage Management Initiative Specifications) 1.6
  * 저장 데이터 암호화
  * VAAI(vStorage for API Array Integration) 라이센싱이 이제 VVol(Virtual Volumes)에 맞춰 조정됨 
  * VCop(vCenter Operations Manager)
  * IBM XIV Storage System에 대한 자세한 정보는 [Platform and application integration for IBM XIV Storage System ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}을 참조하십시오. 

## 공유 스토리지 옵션

다중 테넌트 환경(블록 스토리지 및 파일 스토리지)에서 VMware에 연결하는 데 사용할 수 있는 두 가지 스토리지 옵션이 있습니다. 

### 블록 및 파일 스토리지

ESX로 IBM Cloud 고객 포털에서 {{site.data.keyword.baremetal_short}}를 주문하십시오. 

VMware의 경우 새 개의 <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> 사전 정의된 값이 **호스트 디바이스 세부사항 스토리지** 탭 – 사용자 이름, 비밀번호(CHAP 인증용) 및 호스트 IQN에 제공됩니다.

블록 스토리지 프로비저닝에 대한 자세한 정보는 [블록 스토리지 프로비저닝 및 관리](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)를 참조하십시오.

파일 스토리지 프로비저닝에 대한 자세한 정보는 [IBM Cloud에 대한 IBM File Storage 프로비저닝 및 관리](/docs/infrastructure/FileStorage/provisioning-file-storage.html)를 참조하십시오.

* 권장되는 워크로드: 티어 1, 2 및 3
* 성능을 프로비저닝하는 두 가지 방법:
    1. 내구성(Endurance) IOPS 티어: GB당 0.25, 2, 4 또는 104 IOPS로 사용 가능
    2. 할당된 IOPS 성능: 용량에 상관없이 IOPS를 지정하십시오. 성능 요구사항이 올바르게 정의된 워크로드에 권장됩니다. 
    * 예측 가능한 스토리지 성능 매개변수
    * 더 높은 IOPS 및 추가 처리량을 달성하기 위해 여러 볼륨을 스트라이핑할 수 있습니다. 
* 대기 시간 <10ms 최대 48,000 IOPS
* 확장성: 20GB에서 12TB까지 주문. 주문한 후에는 볼륨의 크기를 조정할 수 없습니다. 
* 프로토콜: iSCSI 및 NFS
* 비용: CAPEX(동일한 크기의 SAN의 10x) 및 OPEX 둘 다에 대해 높음
* HA: 듀얼 헤드 및 제어기
* 복제: IBM Cloud 사설 네트워크에서 제공된 스냅샷 및 복제. 또한 SRA가 아닌 [vRealize Automation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.vmware.com/products/vrealize-automation){: new_window}을 사용하여 아카이브됩니다. 
* 신뢰성: 높은 중복성. iSCSI는 MPIO 연결을 사용합니다. NFS 기반 스토리지는 TCP/IP 연결을 통해 라우팅됩니다. 스냅샷 및 복제를 사용할 수 있습니다.

표 2에서는 단일 테넌트 환경의 개인용 스토리지에 대한 장점과 단점을 제공합니다. 

<table border="1" cellpadding="0" cellspacing="0">
        <caption>표 2. VMware 개인용 스토리지 옵션의 장단점</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; 개인용 스토리지(단일 테넌트)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>주요 요인/스토리지 옵션</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>로컬</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>가상 SAN</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>유형</strong></p>
			</td>
			<td style="width:87px;">
				<p>로컬</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>모놀리식</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>성능</strong></p>
			</td>
			<td style="width:87px;">
				<p>SSD/SA-SCSI 스펙을 기반으로 합니다. 추가 RAID 5/10을 읽기/쓰기 게인에 사용할 수 있습니다. </p>
			</td>
			<td style="width:95px;">
				<p>호스트 구성에 따라 호스트 당 90K 이상의 IOPS 제공. 호스트 당 100개 VM, 클러스터 당 32개 호스트, 클러스터 당 3,200개 VM, 2,048만 보호됨(v5.5)</p>
				<p>최대 20K IOPS, 호스트 당 200개 VM, 클러스터 당 64개 호스트 및 클러스터 당 6,000개 보호된 VM(v6.0).</p>
			</td>
			<td style="width:99px;">
				<p>선택한 디스크의 유형 및 수와 RAID 구성 및 iSCSI 또는 NFS 사용을 기반으로 합니다.</p>
			</td>
			<td style="width:80px;">
				<p>선택한 디스크의 유형 및 수와 RAID 구성 조치를 기반으로 합니다.</p>
			</td>
			<td style="width:80px;">
				<p>모델에 따라 다릅니다.</p>
			</td>
			<td style="width:96px;">
				<p>선택한 디스크의 유형 및 수와 RAID 구성 및 하이퍼바이저 노드 당 SSD 디스크의 선택적 사용을 기반으로 합니다.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>확장성</strong></p>
			</td>
			<td style="width:87px;">
				<p>크기 및 디스크 I/O 처리량의 증가가 제한적입니다.</p>
			</td>
			<td style="width:95px;">
				<p>v5.5의 경우 VMDK(Virtual machine disk)는 최대 2TB이고 v6.0의 경우 최대 62TB입니다. </p>
				<p>추가 노드로 확장하십시오. </p>
			</td>
			<td style="width:99px;">
				<p>단일 QS 최대 128TB(3.x). 확장되지 않습니다. </p>
			</td>
			<td style="width:80px;">
				<p>최대 10TB. 확장되지 않습니다. </p>
			</td>
			<td style="width:80px;">
				<p>확장할 수 있습니다. 용량 및 IOPS를 확장하려면 디스크 선반을 추가하십시오.</p>
			</td>
			<td style="width:96px;">
				<p>~8에서 325TB까지 사용 가능한 영역을 확장합니다. </p>
				<p>최소 용량은 3개 VM x 6개 드라이브입니다.</p>
				<p>최대 용량은 15개 VM x 12개 드라이브입니다.</p>
				<p>IBM Hyper-Scale Manager를 통해 40PB 이상 사용 가능하며 최대 144개까지 가상 배열을 확장할 수 있습니다.</p>
				<p>더 많은 노드를 추가하여 중단 없이 용량을 확장할 수 있습니다.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>프로토콜</strong></p>
			</td>
			<td style="width:87px;">
				<p>NA</p>
			</td>
			<td style="width:95px;">
				<p>독점</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>유스 케이스</strong></p>
			</td>
			<td style="width:87px;">
				<p>티어 2 및 3 워크로드</p>
			</td>
			<td style="width:95px;">
				<p>티어 1 워크로드</p>
			</td>
			<td style="width:99px;">
				<p>티어 2 및 3 워크로드</p>
			</td>
			<td style="width:80px;">
				<p>티어 2 및 3 워크로드</p>
			</td>
			<td style="width:80px;">
				<p>티어 1 워크로드</p>
			</td>
			<td style="width:96px;">
				<p>티어 1 워크로드</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>고가용성(HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>RAID 지원</p>
			</td>
			<td style="width:95px;">
				<p>예. 호스트 및 디스크 장애. 장애 도메인(v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>IBM Cloud에서 사용할 수 없습니다.</p>
			</td>
			<td style="width:80px;">
				<p>NA</p>
			</td>
			<td style="width:80px;">
				<p>예. 듀얼 헤드 및 제어기</p>
			</td>
			<td style="width:96px;">
				<p>예. 클러스터된 솔루션</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>구성 가능성</strong></p>
			</td>
			<td style="width:87px;">
				<p>디스크의 수 및 유형과 RAID 레벨</p>
			</td>
			<td style="width:95px;">
				<p>특정 제어기가 필요합니다. </p>
			</td>
			<td style="width:99px;">
				<p>CPU, 메모리, 캐시, 디스크 수와 유형 및 RAID 레벨.</p>
			</td>
			<td style="width:80px;">
				<p>CPU, 메모리, 캐시, 디스크 수와 유형 및RAID 레벨.</p>
			</td>
			<td style="width:80px;">
				<p>TBD</p>
			</td>
			<td style="width:96px;">
				<p>CPU, 메모리, 캐시, 디스크 수와 유형, SSD, 캐싱 및 iSCSI 포트 구성. 다중 테넌시 QOS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>재해 복구 및 복제</strong></p>
			</td>
			<td style="width:87px;">
				<p>복제하는 데 vRA를 사용합니다. SRA는 사용되지 않습니다.</p>
			</td>
			<td style="width:95px;">
				<p>복제하는 데 vRA를 사용합니다. </p>
			</td>
			<td style="width:99px;">
				<p>기본 제공 복제를 사용합니다. SRA는 사용할 수 없습니다. </p>
			</td>
			<td style="width:80px;">
				<p>복제하는 데 vRA를 사용할 수 있습니다. SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>복제하는 데 vRA를 사용할 수 있습니다. SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>vRA 또는 SRA가 지원됩니다. SDS 및/또는 실제 XIV 디바이스 간에 복제됩니다. </p>
				<p>스냅샷이 지원됩니다. IBM FlashCopy Manager를 통해 애플리케이션이 복구됩니다.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>신뢰성</strong></p>
			</td>
			<td style="width:87px;">
				<p>HA 없는 단일 장애 지점.</p>
			</td>
			<td style="width:95px;">
				<p>7개 이상의 호스트에서 최대 3개까지 호스트 장애가 허용됩니다. </p>
				<p>v6.0에서 장애 도메인이 도입되었습니다. </p>
			</td>
			<td style="width:99px;">
				<p>단일 장애 지점(격납장치 및 RAID 제어기) 및 HA 없음.</p>
			</td>
			<td style="width:80px;">
				<p>단일 장애 지점(격납장치 및 RAID 제어기) 및 HA 없음.</p>
			</td>
			<td style="width:80px;">
				<p>고도로 중복된 다중 경로 I/O(MPIO) 연결</p>
			</td>
			<td style="width:96px;">
				<p>고도로 중복된 iSCSI MPIO 연결: 모든 노드는 클러스터를 관리할 수 있습니다. </p>
			</td>
		</tr>
	</tbody>
</table>

표 2 문서 링크:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: 고객 포털에서 사용할 수 없음 – 고유 솔루션을 사용하십시오. 
  * [Data ONTAP Installation and Administration Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: 고객 포털에서 사용할 수 없음 – 고유 솔루션을 사용하십시오. 
  * [Working with an IBM Spectrum Accelerate system ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

표 3에서는 다중 테넌트 환경의 공유 스토리지에 대한 장점과 단점을 제공합니다. 

<table border="1" cellpadding="0" cellspacing="0">
        <caption>표 3. VMware 공유 스토리지 옵션의 장단점</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>VMware 공유 스토리지(다중 테넌트)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>주요 요인/스토리지 옵션</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">블록 및 파일 내구성(Endurance)</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">블록 및 파일 성능(Performance)</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>유형</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>성능</strong></p>
			</td>
			<td style="width:266px;">
				<p>GB당 0.25, 2, 4 또는 104 IOPS로 사용 가능</p>
				<p>예측 가능한 스토리지 성능 매개변수</p>
				<p>더 높은 IOPS 및 추가 처리량을 달성하기 위해 여러 볼륨을 스트라이핑할 수 있습니다. </p>
			</td>
			<td style="width:271px;">
				<p>클라이언트는 워크로드 요구사항 또는 기준 가격을 기반으로 원하는 성능 레벨을 프로비저닝합니다. </p>
				<p>&nbsp;</p>
				<p>예측 가능한 스토리지 성능 매개변수</p>
				<p>더 높은 IOPS 및 추가 처리량을 달성하기 위해 여러 볼륨을 스트라이핑할 수 있습니다. </p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>확장성</strong></p>
			</td>
			<td style="width:266px;">
				<p>볼륨의 크기는 20GB에서 12TB 사이입니다. 주문한 후에는 크기를 조정할 수 없습니다. </p>
			</td>
			<td style="width:271px;">
				<p>볼륨의 크기는 20GB에서 12TB 사이입니다. 주문한 후에는 크기를 조정할 수 없습니다. </p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>프로토콜</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI 및 NFS.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI 및 NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>호스트 연결</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI의 경우 최대 8이고 NFS의 경우 64입니다.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI의 경우 최대 8이고 NFS의 경우 64입니다.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>유스 케이스</strong></p>
			</td>
			<td style="width:266px;">
				<p>티어 1, 2 및 3 워크로드:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; GB당 0.25 IOPS: 낮은 I/O 강도. 예제 애플리케이션에는 저장 메일함 또는 부서 레벨 파일 공유가 포함되어 있습니다. </p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; GB당 2 IOPS: 일반적인 목적. 예제 애플리케이션에는 웹 애플리케이션을 지원하는 소형 데이터베이스 호스팅 또는 하이퍼바이저에 대한 가상 머신 디스크 이미지가 포함되어 있습니다. </p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; GB당 4 IOPS: 높은 I/O 강도. 예제 애플리케이션에는 트랜잭션 및 다른 성능에 민감한 데이터베이스가 포함되어 있습니다. </p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; GB당 10 IOPS: 높은 I/O 강도. 예제 애플리케이션에는 분석이 포함되어 있습니다. </p>
			</td>
			<td style="width:271px;">
				<p>티어 1, 2 및 3 워크로드:</p>
				<p>MPIO iSCSI 기반 스토리지는 이상적으로 성능 레벨을 예측할 수 있어야 하는 관계형 데이터베이스와 같은 I/O 집약적인 애플리케이션에 적합합니다. 스토리지 볼륨은 20GB에서 12TB까지 크기가 다양하며, 100에서 48,000 IOPS 범위에서 사용자가 IOPS를 선택할 수 있습니다. </p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>예. 듀얼 헤드 및 제어기</p>
			</td>
			<td style="width:271px;">
				<p>예. 듀얼 헤드 및 제어기</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>구성 가능성</strong></p>
			</td>
			<td style="width:266px;">
				<p>크기 및 IOPS 전용.</p>
			</td>
			<td style="width:271px;">
				<p>크기 및 IOPS 전용.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>재해 복구 및 복제</strong></p>
			</td>
			<td style="width:266px;">
				<p>스냅샷과 복제가 제공되며 IBM Cloud 사설 네트워크에서 수행됩니다. VM 레벨에서 복제하는 데 vRA를 사용할 수 있습니다. SRA는 사용할 수 없습니다.</p>
			</td>
			<td style="width:271px;">
				<p>스냅샷과 복제가 제공되며 IBM Cloud 사설 네트워크에서 수행됩니다. VM 레벨에서 복제하는 데 vRA를 사용할 수 있습니다. SRA는 사용할 수 없습니다.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>신뢰성</strong></p>
			</td>
			<td style="width:266px;">
				<p>고도로 중복된 MPIO 연결 및 TCP/IP 연결을 통해 라우팅되는 NFS 기반 파일 스토리지. 스냅샷 및 복제를 사용할 수 있습니다.</p>
			</td>
			<td style="width:271px;">
				<p>고도로 중복된 MPIO 연결 및 TCP/IP 연결을 통해 라우팅되는 NFS 기반 파일 스토리지. </p>
			</td>
		</tr>
	</tbody>
</table>

표 3 문서 링크:
* [블록 스토리지](/docs/infrastructure/BlockStorage/index.html)
* [파일 스토리지](/docs/infrastructure/FileStorage/index.html)
