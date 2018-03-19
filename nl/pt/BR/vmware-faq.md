---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQs: VMware 

## Qual nível de licença é ativado quando você implementa o vSphere por meio do portal do IBM Cloud?

Enterprise Plus, o maior nível de licença do vSphere.

## Como o VMware vSphere 6 é licenciado?

A abordagem de licenciamento é ligada ao seu mecanismo de implementação. Você tem duas maneiras de implementar o VMware 6:

1. Quando você implementa o vSphere por meio do portal de controle, o licenciamento VMware Service Provider Program (VSPP) é ativado automaticamente. Na implementação, um usuário padrão "slvmadmin" é incluído no Host para serviços de administração e integração do vSphere no portal de controle.

2. Quando você implementa o vSphere manualmente, é possível trazer sua própria licença e mídia (BYOL/BYOM), o que permite aplicar suas licenças padrão nesses hosts. **Nota:** se desejar usar seu próprio licenciamento de VMWare, é recomendável solicitar o servidor com um SO grátis, como o CentOS ou como o NO OS. Em seguida, instale o S.O. VMWare por meio do IPMI [Virtual ISO](../bare_metal/mount-iso-bare-metal-server.html)

## Posso criar uma nuvem do VMware privada isolada?

Sim, é possível implementar sistemas bare metal e instalar qualquer hypervisor suportado (incluindo VMware ESX) nesses hosts. Também é possível implementar máquinas virtuais usando as ferramentas de gerenciamento nativas. Por padrão, os sistemas são implementados em VLANs para componentes de segregação e de rede (como gateways, roteadores e firewalls) e são usados para criar quase todas as topologias.

## Como o VMware é licenciado?

A abordagem de licenciamento é ligada ao seu mecanismo de implementação. Você tem duas maneiras de implementar o VMware:

1. Quando você implementa o ESX por meio do portal, o licenciamento VMware Service Provider Program (VSPP) é ativado automaticamente. Na implementação, um usuário padrão 'vmadmin' é incluído no servidor ESX para coleta de dados. Não exclua esse usuário padrão. O VSPP cobra pela RAM que é reservada e usada para todas as máquinas virtuais “ligadas“ (não “por soquete“ como uma licença de host padrão).

2. Quando você implementa o ESX manualmente, é possível BYOL (trazer sua própria licença), portanto, é possível aplicar licenças padrão nesses hosts. **Nota:** BYOL não pode ser usado para hosts que são implementados por meio do portal. O VSPP deve ser ativado.

    * Além disso, uma instância do vCenter Server não é necessária para que o VSPP funcione.

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## Posso implementar componentes do VMware diretamente do portal do IBM Cloud?

Sim, você tem duas opções:

1. Selecionar e implementar o hypervisor ESX automaticamente com um sistema bare metal mensal<!-- (Figure 2)-->. Também é possível implementar o gerenciamento do vCenter automaticamente com uma máquina virtual ou sistema bare metal (somente Windows).

2. Implementar um host bare metal com um sistema operacional livre, como CentOS, e subsequentemente instalar o ESX manualmente usando o Console Remoto e o acesso de mídia virtual do host. É possível, então, instalar o vCenter Server manualmente ou implementar o VMware vCenter Server Appliance que opera no Linux.

