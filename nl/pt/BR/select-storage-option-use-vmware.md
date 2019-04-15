---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Armazenamento para uso com sistemas VMware
{: #vmware-storage}

Existem várias opções com relação ao armazenamento. Pode-se optar por soluções privadas, compartilhadas ou trazer suas próprias soluções de armazenamento. Use as informações a seguir para ajudá-lo a decidir qual solução de armazenamento funciona melhor com sua carga de trabalho.

A Tabela 1 contém as camadas de armazenamento e o local onde sua carga de trabalho pode estar.
<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabela 1. Camadas de armazenamento</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Camada 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Camada 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Camada 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Uso de negócios</strong></p>
			</td>
			<td style="width:160px;">
				<p>Aplicativos de produção, bancos de dados e dados de alto desempenho e/ou alta disponibilidade</p>
			</td>
			<td style="width:160px;">
				<p>Aplicativos, bancos de dados e dados de teste e desenvolvimento sem missão crítica</p>
			</td>
			<td style="width:160px;">
				<p>Armazenamento de dados, backup e archive sem missão crítica</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Desempenho </strong></p>
			</td>
			<td style="width:160px;">
				<p>Alto (SSDs, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>Médio (SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>Baixo (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>IOPS garantido</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sim</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Alta disponibilidade (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sim</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Replicação</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sim</p>
			</td>
			<td style="width:160px;">
				<p>Sim</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Capturas instantâneas</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sim</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
			<td style="width:160px;">
				<p>Não</p>
			</td>
		</tr>
	</tbody>
</table>


## Opções de armazenamento privado e compartilhado de VMware

É possível escolher dentre várias opções de armazenamento. Para armazenamento privado, é possível selecionar opções de disco local, VSAN ou QuantaStor. Para armazenamento compartilhado, é possível selecionar o armazenamento de Resistência ou de Desempenho. Se você decidir trazer seu armazenamento, há várias opções “privadas”, incluindo NetApp OnTap Edge, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate e armazenamento definido por software. A Tabela 2 e a Tabela 3 oferecem uma comparação lado a lado das opções para sua conveniência.

## Opções de armazenamento privado

Há várias opções para armazenamento para conectar-se ao VMware em um ambiente de locatário único: 

* Local
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## Armazenamento local

Solicite o {{site.data.keyword.baremetal_short}} no portal do cliente do IBM Cloud com ESX e selecione os discos desejados [SATA, serial attached SCSI (SA SCSI) ou SSD ].
 
É possível trazer sua própria licença ESX, mas é necessário abrir um chamado com o Suporte para informá-los sobre a mudança.

* Cargas de trabalho recomendadas: camada 3
* Desempenho: limitado: dependente do RAID e do tipo de disco. SSDs apresentam um aumento de custo para melhor desempenho.
* Escalabilidade: limitado ao número de slots de unidade no chassi
* Protocolos: não aplicável
* Custo: gasto de capital baixo (CAPEX) e gasto operacional (OPEX)
* HA: não disponível
* Replicação: [Dispositivo virtual vSphere Replication ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Confiabilidade: múltiplos pontos únicos de falha



## vSAN [1]

* Cargas de trabalho recomendadas: camada 1
* Desempenho: mais de 90.000 IOPS por host dependendo da configuração do host
* Escalabilidade: disco de máquina virtual (VMDK) v5.5 de até 2 TB; VMDK v6.0 de até 62 TB. Efetue uma ampliação com mais nós.
* Protocolos: proprietário
* Custo: médio para ambos, CAPEX e OPEX
* HA: suportado para falhas de host e de disco. Domínios de falha são suportados iniciando na v6 do VMware.
* Replicação: [Dispositivo virtual vSphere Replication ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Replicação e recuperação de desastre:
    1. Planeje o backup da VM por meio do VMware vCenter Server
    2. Crie a captura instantânea da VM
    3. Dados DE criados para a VM
    4. Restaure a VM
 * Confiabilidade: tolera até três falhas de host com sete ou mais hosts. Domínios de falha foram introduzidos na v6 do VMware.   

[1] Novo recurso do vSan 6.2, clusters estendidos, permite que os hosts estejam em diferentes pods no mesmo data center (testes de validação estão em andamento). <!-- Should this in progress mention be removed? -->

O vSAN 5.5 está disponível apenas com BYOL (Bring Your Own License). Ele é suportado pelo VMware apenas se você usa um controlador de disco Avago LSI MegaRAID SAS 9361-8i.

O vSAN 6.0 está disponível diretamente no portal do IBM Cloud com base de faturamento de licença de CPU.

## QuantaStor

O [OSNexus Solution Design Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} pode ser usado para ajudar a conectar o VMware com o QuantaStor.

* Cargas de trabalho recomendadas: camadas 2 e 3 
* Desempenho: variável com base no número de unidades, RAID e uso de disco (iSCSI ou NFS)  
* Escalabilidade: a estrutura única da v3 suporta 128 TB; nenhum aumento ou ampliação de capacidade. 
* Protocolos: iSCSI, NFS e SMB 
* Custo: alto para ambos, CAPEX e OPEX 
* HA: não disponível  
* Replicação: recursos de replicação integrados; nenhum SRA disponível. Pode-se usar o Dispositivo de Replicação vSphere também 
* Confiabilidade: ponto único de falha para o gabinete e o controlador RAID.


<a name="NetApp"></a>
## NetApp Data OnTap Edge

Deve-se comprar um dispositivo NetApp do NetApp ou da IBM. É necessário instalar em um {{site.data.keyword.baremetal_short}} em seu data center {{site.data.keyword.BluSoftlayer}}.

Para obter mais informações sobre como conectar o VMware com NetApp, consulte os links a seguir:
* [NetApp ONTAP Select ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: construa um data center em um servidor com os fundamentos do NetApp ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* Cargas de trabalho recomendadas: camadas 2 e 3
* Desempenho: variável com base no número de unidades e RAID
* Escalabilidade: suporta 110 TB; sem ampliação.
* Protocolos: iSCSI, NFS e SMB
* Custo: médio para ambos, CAPEX e OPEX
* HA: não disponível
* Replicação: suporta SnapMirror; também obtida usando [vRealize Automation ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA).
* Confiabilidade: ponto único de falha para o gabinete e o controlador RAID.

<a name="NPS"></a>
## NetApp Private Storage

Deve-se comprar um dispositivo NetApp do NetApp ou da IBM. É necessário instalá-lo em um dos sites de colocação próximos ao seu data center do IBM Cloud e conectá-lo usando Direct Link Colocation ou Direct Link Cloud.

Para obter mais informações sobre como conectar-se ao VMware com NetApp, consulte os links a seguir: 
* [NetApp Private Storage for IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Resumo da solução: NetApp Private Storage for IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* Cargas de trabalho recomendadas: camada 1
* Desempenho: dependente do modelo do NetApp
* Escalabilidade: suporta a adição de unidades e quadros para maior capacidade e IOPS
* Protocolos: iSCSI, NFS e SMB
* Custo: alto para ambos, CAPEX e OPEX
* HA: cabeçotes e controladores duais
* Replicação: suporta SnapVault e SnapMirror; também obtida usando [vRealize Automation ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/products/vrealize-automation).
* Confiabilidade: alta redundância e suporte de MPIO

<a name="IBM"></a>
## IBM Spectrum Accelerate

A opção de armazenamento privado do IBM Spectrum Accelerate não está disponível no portal do cliente do IBM Cloud. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* Cargas de trabalho recomendadas: camada 1
* Desempenho: dependente do número de discos, do SSD (opcional) e da quantidade de memória que é fornecida para cada VM de “nó”.
* Escalabilidade: escala ~8 - 325 TB utilizáveis
  * Capacidade mínima: 3 VMs x 6 unidades
  * Capacidade máxima: 15 VMs x 12 unidades
  * Escala até 144 matrizes virtuais e mais de 40 PB utilizáveis por meio do IBM Hyper-Scale Manager
  * Expansão de capacidade sem interrupção incluindo mais nós
  * 1 x 500 ou 800 GB de SSD por nó suportado
* Protocolos: somente iSCSI
* Custo: dependente do modelo de precificação e das máquinas físicas implementadas para os nós. CAPEX alto; OPEX de médio a baixo, dependendo do licenciamento.
  * Precificado por binário (TiB) de capacidade utilizável
  * Não é ligado a nenhuma configuração de hardware específica. Exemplo: a licença de 200 TiB poderia ser implementada de várias maneiras – uma instância de 200 TiB, duas instâncias de 100 TiB ou quatro instâncias de 50 TiB
  * Oferecido de duas maneiras: licença perpétua [inclui um ano de assinatura e serviço (S e S)] e licença mensal (inclui S e S)
* HA: solução em cluster
* Replicação: obtida usando [vRealize Automation ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/products/vrealize-automation){: new_window}
ou SRA, que pode ser usado para replicar do IBM XIV físico com VMware Site Recovery Manager (SRM)
  * [vSphere Replication ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [Diretrizes do VMware vCenter Site Recovery Manager versão 5.x para IBM XIV Gen3 Storage System ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* Confiabilidade: alta redundância e suporte de MPIO. Qualquer nó disponível pode gerenciar o cluster. Os recursos a seguir não são suportados pelo IBM Spectrum Accelerate neste momento pelo IBM XIV baseado em hardware:
  * Espelhamento de três sites
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG v6
  * Unidades de disco de 6 TB
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * Criptografia de dados em repouso
  * Licenciamento do vStorage for API Array Integration (VAAI) agora alinhado com Volumes Virtuais (VVol)
  * vCenter Operations Manager (VCop)
  * Para obter mais informações sobre o IBM XIV Storage System, consulte [Plataforma e integração de aplicativos para o IBM XIV Storage System ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## Opções de armazenamento compartilhado

Há duas opções de armazenamento que podem ser usadas para se conectar ao VMware em um ambiente de vários locatários: Armazenamento de Bloco e Armazenamento de Arquivo.

### Armazenamento de Bloco e Arquivo

Solicite o {{site.data.keyword.baremetal_short}} no portal do cliente do IBM Cloud com ESX.

No VMware, três valores predefinidos <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> são fornecidos na guia **Armazenamento de detalhes do dispositivo host** – Nome do usuário, Senha (para autenticação CHAP) e IQN do host.

Para obter mais informações sobre armazenamento de bloco de provisão, consulte [Provisionando e gerenciando o armazenamento de bloco](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Para obter mais informações sobre o armazenamento de arquivo de provisão, consulte [Provisionando e gerenciando o IBM File Storage for IBM Cloud](/docs/infrastructure/FileStorage/provisioning-file-storage.html).

* Cargas de trabalho recomendadas: camadas 1, 2 e 3
* Duas maneiras de provisionar desempenho:
    1. Camadas de IOPS de resistência: disponível em 0,25, 2, 4 ou 104 IOPS por GB
    2. IOPS alocado por desempenho: especifique o IOPS independente da capacidade. Recomendado para cargas de trabalho com requisitos de desempenho bem definidos.
    * Parâmetros de desempenho de armazenamento previsíveis.
    * Múltiplos volumes podem ser divididos juntos para alcançar maior IOPS e mais rendimento
* Latência < 10 ms ou mais para 48.000 IOPS
* Escalabilidade: pedido de 20 GB a 12 TB. Não é possível redimensionar o volume depois que ele é solicitado.
* Protocolos: iSCSI e NFS
* Custo: alto para CAPEX (10x para SAN de mesmo tamanho) e OPEX
* HA: cabeçotes e controladores duais
* Replicação: captura instantânea e replicação fornecidas pelo IBM Cloud Private Network; também obtida usando [vRealize Automation ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/products/vrealize-automation){: new_window}, mas sem SRA.
* Confiabilidade: redundância alta; iSCSI usa uma conexão de MPIO; o armazenamento baseado em NFS é roteado por conexões TCP/IP. Captura Instantânea e Replicação ativadas.

A Tabela 2 fornece os prós e contras do armazenamento privado em um ambiente de locatário único.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabela 2. Prós e contras de opções de armazenamento privado do VMware</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; armazenamento privado (locatário único)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>Fatores-chave/opção de armazenamento</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>Local</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>SAN Virtual</p>
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
				<p><strong>Tipo</strong></p>
			</td>
			<td style="width:87px;">
				<p>Local</p>
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
				<p>Monolítico</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Desempenho </strong></p>
			</td>
			<td style="width:87px;">
				<p>Baseado nas especificações de SSD/SA-SCSI; RAID 5/10 adicional pode ser usado para ganhos de leitura/gravação.</p>
			</td>
			<td style="width:95px;">
				<p>Mais de 90.000 IOPS por host dependendo da configuração do host. 100 VMs por host, 32 hosts por cluster, 3.200 VMs por cluster, apenas 2.048 protegidas (v5.5)</p>
				<p>Até 20.000 IOPS, 200 VMs por host, 64 hosts por cluster e 6.000 VMs protegidas por cluster (v6.0).</p>
			</td>
			<td style="width:99px;">
				<p>Baseado em tipos e número de discos selecionados, bem como nas configurações de RAID e no uso de iSCSI ou NFS.</p>
			</td>
			<td style="width:80px;">
				<p>Baseado em tipos e número de discos selecionados, bem como nas ações de configuração de RAID.</p>
			</td>
			<td style="width:80px;">
				<p>Depende do modelo.</p>
			</td>
			<td style="width:96px;">
				<p>Baseado em tipos e número de discos selecionados, bem como nas configurações de RAID e no uso opcional do disco SSD por nó do hypervisor.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Escalabilidade</strong></p>
			</td>
			<td style="width:87px;">
				<p>Crescimento limitado no tamanho e no rendimento de E/S de disco.</p>
			</td>
			<td style="width:95px;">
				<p>Disco de máquina virtual (VMDK) de até 2 TB com a v5.5 e até 62 TB com a v6.0.</p>
				<p>Efetue uma ampliação com mais nós.</p>
			</td>
			<td style="width:99px;">
				<p>QS único de até 128 TB (3.x). Sem aumento ou ampliação.</p>
			</td>
			<td style="width:80px;">
				<p>Até 10 TB; sem ampliação.</p>
			</td>
			<td style="width:80px;">
				<p>Sim, inclua estruturas de disco para capacidade e IOPS.</p>
			</td>
			<td style="width:96px;">
				<p>Escala de ~8 a 325 TB de espaço utilizável.</p>
				<p>A capacidade mínima é 3 VMs x 6 unidades.</p>
				<p>A capacidade máxima é 15 VMs x 12 unidades.</p>
				<p>Aumenta a capacidade para até 144 matrizes virtuais e mais de 40 PB utilizáveis por meio do IBM Hyper-Scale Manager.</p>
				<p>Expansão de capacidade sem interrupção incluindo mais nós.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocolos</strong></p>
			</td>
			<td style="width:87px;">
				<p>NA</p>
			</td>
			<td style="width:95px;">
				<p>Proprietário</p>
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
				<p><strong>Casos de uso</strong></p>
			</td>
			<td style="width:87px;">
				<p>Cargas de trabalho das camadas 2 e 3</p>
			</td>
			<td style="width:95px;">
				<p>Cargas de trabalho da camada 1</p>
			</td>
			<td style="width:99px;">
				<p>Cargas de trabalho das camadas 2 e 3</p>
			</td>
			<td style="width:80px;">
				<p>Cargas de trabalho das camadas 2 e 3</p>
			</td>
			<td style="width:80px;">
				<p>Cargas de trabalho da camada 1</p>
			</td>
			<td style="width:96px;">
				<p>Cargas de trabalho da camada 1</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Alta disponibilidade (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>Disponível com RAID</p>
			</td>
			<td style="width:95px;">
				<p>Sim; falhas de host e de disco; domínios de falha (v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>Não disponível no IBM Cloud.</p>
			</td>
			<td style="width:80px;">
				<p>NA</p>
			</td>
			<td style="width:80px;">
				<p>Sim, cabeçotes e controladores duais.</p>
			</td>
			<td style="width:96px;">
				<p>Sim; solução em cluster.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurabilidade</strong></p>
			</td>
			<td style="width:87px;">
				<p>Número e tipo de discos; níveis de RAID</p>
			</td>
			<td style="width:95px;">
				<p>Controladores específicos necessários.</p>
			</td>
			<td style="width:99px;">
				<p>CPU, memória, cache, número e tipo de discos, além de níveis de RAID.</p>
			</td>
			<td style="width:80px;">
				<p>CPU, memória, cache, número e tipo de discos, além de níveis de RAID.</p>
			</td>
			<td style="width:80px;">
				<p>TBD</p>
			</td>
			<td style="width:96px;">
				<p>CPU, memória, cache, número e tipo de discos, SSD, armazenamento em cache, configuração da porta iSCSI. QOS de ocupação variada.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Recuperação e replicação de desastre</strong></p>
			</td>
			<td style="width:87px;">
				<p>Use vRA para replicar; nenhum SRA.</p>
			</td>
			<td style="width:95px;">
				<p>Use vRA para replicar.</p>
			</td>
			<td style="width:99px;">
				<p>Replicação integrada, nenhum SRA disponível.</p>
			</td>
			<td style="width:80px;">
				<p>Pode-se usar vRA para replicar, SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>Pode-se usar vRA para replicar, SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>vRA ou SRA suportado; replicação entre SDS e/ou dispositivos XIV físicos.</p>
				<p>Capturas instantâneas suportadas; recuperação do aplicativo via IBM FlashCopy Manager.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Confiabilidade</strong></p>
			</td>
			<td style="width:87px;">
				<p>Ponto único de falha sem alta disponibilidade.</p>
			</td>
			<td style="width:95px;">
				<p>Tolera até três falhas de host com sete hosts adicionais.</p>
				<p>Domínios de falha são apresentados na v6.0.</p>
			</td>
			<td style="width:99px;">
				<p>Ponto único de falha (gabinete e controlador RAID) e sem HA.</p>
			</td>
			<td style="width:80px;">
				<p>Ponto único de falha (gabinete e controlador RAID) e sem HA.</p>
			</td>
			<td style="width:80px;">
				<p>Conexão de multipath I/O (MPIO) altamente redundante.</p>
			</td>
			<td style="width:96px;">
				<p>Conexões de MPIO iSCSI altamente redundantes: qualquer nó pode gerenciar o cluster.</p>
			</td>
		</tr>
	</tbody>
</table>

Links da documentação da tabela 2:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: não disponível no portal do cliente – trazer sua própria solução.
  * [Data ONTAP Installation and Administration Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: não disponível no portal do cliente – trazer sua própria solução.
  * [Trabalhando com um sistema IBM Spectrum Accelerate ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

A Tabela 3 fornece os prós e contras do armazenamento compartilhado em um ambiente de diversos locatários.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabela 3. Prós e contras de opções de armazenamento compartilhado do VMware</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>Armazenamento compartilhado de VMware (diversos locatários)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Fatores-chave/opções de armazenamento</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">Resistência de Bloco e Arquivo</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">Desempenho de Bloco e Arquivo</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Tipo</strong></p>
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
				<p><strong>Desempenho </strong></p>
			</td>
			<td style="width:266px;">
				<p>Disponível em 0,25, 2, 4 ou 104 IOPS por GB.</p>
				<p>Parâmetros de desempenho de armazenamento previsíveis.</p>
				<p>Múltiplos volumes podem ser divididos conjuntamente para alcançar maior IOPS e mais rendimento.</p>
			</td>
			<td style="width:271px;">
				<p>O cliente provisiona o nível desejado de desempenho com base nas necessidades de carga de trabalho ou no ponto de preço.</p>
				<p>&nbsp;</p>
				<p>Parâmetros de desempenho de armazenamento previsíveis.</p>
				<p>Múltiplos volumes podem ser divididos conjuntamente para alcançar maior IOPS e mais rendimento.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Escalabilidade</strong></p>
			</td>
			<td style="width:266px;">
				<p>Os tamanhos dos volumes variam de 20 GB a 12 TB. Não pode ser redimensionado depois de pedido.</p>
			</td>
			<td style="width:271px;">
				<p>Os tamanhos dos volumes variam de 20 GB a 12 TB. Não pode ser redimensionado depois de pedido.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocolos</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI e NFS.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI e NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Conexões de host</strong></p>
			</td>
			<td style="width:266px;">
				<p>Máximo de oito para iSCSI e 64 para NFS.</p>
			</td>
			<td style="width:271px;">
				<p>Máximo de oito para iSCSI e 64 para NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Casos de uso</strong></p>
			</td>
			<td style="width:266px;">
				<p>Cargas de trabalho das camadas 1, 2 e 3:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0,25 IOPS por GB: intensidade de E/S baixa. Exemplos de aplicativos incluem o armazenamento de caixas de correio ou compartilhamentos de arquivo no nível do departamento.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS por GB: propósitos gerais. Exemplos de aplicativos incluem a hospedagem de pequenos bancos de dados que auxiliam os aplicativos da web ou imagens de disco de máquina virtual para um hypervisor.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS por GB: intensidade de E/S alta. Exemplos de aplicativos incluem bancos de dados transacionais e outros bancos de dados sensíveis ao desempenho.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS por GB: intensidade de E/S alta. Exemplos de aplicativos incluem analytics.</p>
			</td>
			<td style="width:271px;">
				<p>Cargas de trabalho das camadas 1, 2 e 3:</p>
				<p>Armazenamento baseado em MPIO iSCSI idealmente adequado para aplicativos com uso intensivo de E/S, tais como bancos de dados relacionais que requerem níveis previsíveis de desempenho. Os volumes de armazenamento são fornecidos em tamanhos de 20 GB a 12 TB com IOPS selecionável pelo usuário que varia entre 100 e 48.000 IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>Sim, cabeçotes e controladores duais.</p>
			</td>
			<td style="width:271px;">
				<p>Sim, cabeçotes e controladores duais.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurabilidade</strong></p>
			</td>
			<td style="width:266px;">
				<p>Tamanho e IOPS somente.</p>
			</td>
			<td style="width:271px;">
				<p>Tamanho e IOPS somente.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Recuperação e replicação de desastre</strong></p>
			</td>
			<td style="width:266px;">
				<p>Captura instantânea e Replicação fornecidas, que é feito na rede IBM Cloud Private. É possível usar vRA para replicar no nível da VM; sem SRA.</p>
			</td>
			<td style="width:271px;">
				<p>Captura instantânea e Replicação fornecidas, que é feito na rede IBM Cloud Private. É possível usar vRA para replicar no nível da VM; sem SRA.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Confiabilidade</strong></p>
			</td>
			<td style="width:266px;">
				<p>Altamente redundante, conexão MPIO, conexões TCP/IP roteadas pelo armazenamento de arquivo baseado em NFS. Capturas instantâneas e replicação ativadas.</p>
			</td>
			<td style="width:271px;">
				<p>Altamente redundante, conexão MPIO, conexões TCP/IP roteadas pelo armazenamento de arquivo baseado em NFS.</p>
			</td>
		</tr>
	</tbody>
</table>

Tabela 3 Links da documentação:
* [Armazenamento de bloco](/docs/infrastructure/BlockStorage/index.html)
* [Armazenamento de arquivo](/docs/infrastructure/FileStorage/index.html)
