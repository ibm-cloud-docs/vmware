---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# LSI 3108 기반 제어기에서 안정성을 위한 vSAN 구성

LSI 3108 시리즈 제어기로 vSAN을 실행할 때 디바이스 관련 장애를 방지하려면 EXSi 쉘에서 다음 명령을 실행하십시오.

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

다음을 참고하십시오.

* 이러한 명령은 vSAN 클러스터에 있는 각 ESXi 호스트에서 실행해야 합니다.
* 이러한 명령은 즉시 적용됩니다. 다시 부팅하지 않아도 됩니다. 
* 이러한 명령의 결과로 지속적인 변경이 수행되며 다시 부팅해도 구성된 상태로 남습니다. 

자세한 정보는 VMware 지식 기반 주제 [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://kb.vmware.com/s/article/2144936){: new_window}을 참조하십시오.
