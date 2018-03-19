---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Solicitando licenças do VMware

Os administradores do VMware sabem que eles podem constatar rapidamente as características da nuvem híbrida com custo reduzido ao implementar no {{site.data.keyword.BluSoftlayer_full}}. Uma das características é que as cargas de trabalho e catálogos do vSphere são provisionados para ambientes do VMware vSphere em data centers do {{site.data.keyword.cloud_notm}} sem modificação para VMs ou guests do VMware. O uso de um hypervisor vSphere e de uma plataforma de gerenciamento/orquestração comuns torna essas implementações possíveis.
{:shortdesc}

A implementação do vSphere também permite o uso de outros componentes. A Tabela 1 contém uma lista de produtos VMware que estão disponíveis para pedido por meio do {{site.data.keyword.slportal}}. As informações de precificação podem ser localizadas em [IBM Cloud for VMware Solutions](http://www.softlayer.com/vmware-solutions).

|Nome do Produto|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="Tabela 1. Os produtos VMware disponíveis no Portal do Cliente" caption-side="top"}

Use as etapas a seguir para solicitar licenças para os produtos VMware que são listados na Tabela 1:
1. Efetue login no [{{site.data.keyword.slportal_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window}.
2. Clique em **Dispositivos > Gerenciados > Licenças do VMware**.
3. Clique em **Solicitar licenças do VMware** no canto superior direito.
4. Clique na lista suspensa sob **Incluir Licença...** para listar os produtos VMware e o número de CPUs para as licenças que você deseja solicitar.
  * **Nota:** o VMware vSphere Enterprise Plus (ESXi 6.0) não é solicitado por meio desse processo. Ele é pedido como um S.O. solicitado quando você solicita o servidor bare metal.
5. É possível ver o preço do produto VMware que você selecionou à direita da tela.
6. Clique em **Continuar** para solicitar as licenças ou você pode clicar em **Incluir licença** para incluir mais licenças.
  * Depois de clicar em **Continuar**, você é levado de volta para a página **Licenças do VMware**, que exibe seus produtos VMware e as chaves de licença.
7. Faça download dos **Arquivos de instalação** no link que é fornecido. É necessário ter uma conexão SSL para a rede privada do IBM Cloud para acessar a página de download.
8. Faça download dos produtos VMware corretos e instale-os manualmente em seu ambiente vSphere.
