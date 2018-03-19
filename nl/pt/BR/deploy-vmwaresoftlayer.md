---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Usando cookbooks para implementações do VMware

Os administradores do VMware podem perceber rapidamente as características de nuvem híbrida com custo reduzido ao implementar na nuvem global de nível corporativo do {{site.data.keyword.BluSoftlayer_full}}. As cargas de trabalho e catálogos do vSphere podem ser provisionados para ambientes do VMware vSphere dentro de data centers do {{site.data.keyword.cloud_notm}} sem modificação de VMs ou guests do VMware. Essas implementações se tornam possíveis usando um hypervisor vSphere e uma plataforma de gerenciamento/orquestração comuns. As implementações do vSphere também podem alavancar outros componentes do VMware vCloud Suite – vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator e NSX.

O objetivo principal da série de cookbooks do VMware é ajudar os administradores do vSphere na implementação de ambientes do VMware vSphere dentro de uma infraestrutura do IBM Cloud. Os cookbooks não são destinados a treinar você para administrar o vSphere. Para obter mais informações sobre como administrar o vSphere, consulte [Educação do VMware ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}.

O {{site.data.keyword.cloud_notm}} possui vários recursos específicos que dão aos administradores do VMware a flexibilidade para consumir instâncias bare metal e construções de rede, armazenamento, backup e recuperação em um modo de autoatendimento. É possível, então, usar essas construções para implementar as implementações do vSphere totalmente funcionais, que podem ser construídas para estender ou substituir implementações do vSphere no local (VMware@Home).

Os cookbooks a seguir estão disponíveis para administradores:

* [Construir um ambiente do VMware de site único](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html): você, como administrador do vSphere, percorre as etapas de construção de seu ambiente, incluindo o uso de qualquer armazenamento de bloco de resistência ou desempenho ou QuantaStor.
* [Migrar cargas de trabalho do vSphere![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}: são apresentados cenários para ajudá-lo a migrar cargas de trabalho [máquinas virtuais (VMs)] para o VMware após sua implementação do vSphere ser implementada em um data center do IBM Cloud.
* [Alavancar NSX® ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}: é possível alavancar o VMware NSX para fornecer construções de rede de definição de software (SDN) para implementações do VMware@SoftLayer.
* [Catalogic ECX ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}: é possível gerenciar e analisar o CopyData em uma infraestrutura de TI híbrida. A infraestrutura é implementada na infraestrutura do IBM Cloud usando a plataforma de gerenciamento inteligente Copy Data da Catalogic Software, ECX, e usando a infraestrutura do NetApp Private Storage e do VMware vSphere.
* [Backup do VMware ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}: esse cookbook descreve abordagens alternativas para backup, recuperação e arquivamento de cargas de trabalho baseadas no VMware (VMs) que estão em execução em uma implementação do VMware.
* [Recuperação de desastres do VMware ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}: esse cookbook detalha dois casos de uso que estabelecem uma solução de recuperação de desastre (DR) usando o VMware. O primeiro compara um ambiente VMware no local que permite que uma carga de trabalho no local seja recuperada ou vice-versa. O segundo recupera cargas de trabalho do VMware em um segundo data center do {{site.data.keyword.cloud_notm}}.
* [Criptografia Vormetric do VMware ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}: casos de uso ilustram como o Vormetric protege as cargas de trabalho do VMware criptografando dados da VM.
* [Implementar uma solução de nuvem confiável com a IBM, VMware e HyTrust ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}: é possível integrar os vários elementos arquiteturais para criar uma cadeia de confiança de hardware até os aplicativos hypervisor e de gerenciamento.


**Nota:** os cookbooks são destinados a administradores experientes do vSphere. Alguns tópicos que são cobertos consideram que o leitor tenha habilidades básicas de implementação para instalar e configurar o vSphere e o vCenter.
