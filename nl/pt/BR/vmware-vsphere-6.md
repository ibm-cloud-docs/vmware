---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opções de licenciamento do VMware 

Os administradores do VMware podem perceber rapidamente as características de nuvem híbrida com custo reduzido ao implementar em uma nuvem global de nível corporativo do {{site.data.keyword.BluSoftlayer_full}}. Um diferenciador chave do {{site.data.keyword.BluSoftlayer_notm}} é que as cargas de trabalho e catálogos do vSphere podem ser provisionados para os ambientes do VMware vSphere dentro dos data centers do {{site.data.keyword.BluSoftlayer_notm}} sem modificar VMs ou guests do VMware. Essas implementações se tornam possíveis usando um hypervisor vSphere e uma plataforma de gerenciamento/orquestração comuns.

Além de oferecer o vSphere 6 Enterprise Plus License, o {{site.data.keyword.BluSoftlayer_notm}} oferece licenciamento mensal para vCenter, NSX, vRealize, vSAN e Site Recovery Manager (SRM).

## VMware vSphere

**Uso desejado:** plataforma de S.O. de virtualização do servidor bare metal que abstrai recursos de processador, memória, armazenamento e rede para criar múltiplos servidores virtuais em um único servidor físico. Múltiplos servidores físicos podem ser armazenados em cluster juntos para criar uma nuvem particular.

**Interface com o usuário:** vCenter Clients, API do VMware, CLI do VMware

**Recursos:**
* Migração em tempo real do vMotion
* Alta disponibilidade
* Tolerância a falhas
* Replicação
* Virtualização Nvidia GRID vGPU
* Otimização de capacidade de carga de trabalho
* Distributed Resources Scheduler (DRS)
* Thin Provisioning
* Controle de E/S de rede

## VMware vCenter

**Uso desejado:** para centralizar o gerenciamento dos recursos de cálculo em cada host vSphere. Embora os hosts vSphere possam ser gerenciados individualmente, colocá-los sob o controle do vCenter ativa os recursos a seguir:

**Interface com o usuário:** Web Client, Thick Client, API do VMware API, CLI do VMware

**Recursos:**
* Controle e visibilidade centralizados para todos os aspectos em hosts vSphere gerenciados e máquinas virtuais guest.
* Fornece uma única área de janela de visualização da interface de vidro por meio do Web client do vCenter para a rede de cálculo e o gerenciamento de armazenamento.
* Otimização proativa. Permite a alocação e a otimização de recursos para eficiência máxima entre os hosts vSphere.
* Função de gerenciamento estendido para outros complementos e serviços integrados, como NSX, vRealize, vSAN e Site Recovery Manager (SRM).
* Monitoramento, alerta, planejamento. Os administradores de nuvem podem visualizar eventos, alertas no Web client do vCenter e configurar ações planejadas.
* Mecanismo de automação. O vCenter é o mecanismo que executa as tarefas que são fornecidas para ele por meio da interface da web do vSphere API. VMware vRealize Automation e vRealize Orchestration são exemplos de aplicativos que conduzem ações do vCenter por meio da API do VMware.

## VMware NSX

**Uso desejado:** o NSX oferece recursos Software-Defined Network (SDN) cruciais para apoiar as operações da plataforma de nuvem.

**Interface com o usuário:** vCenter Clients, API do VMware, CLI do VMware

**Recursos:**
* Balanceamento de carga
* Firewalls
* Roteamento
* Comutadores lógicos
* VPN
* Segmentação de VxLAN/terminais de túnel

## VMware vRealize

**Uso desejado:** o VMware vRealize Suite é uma plataforma de gerenciamento de nuvem preparada para empresas que pode ser usada para gerenciar uma nuvem heterogênea e híbrida.

**Interface com o usuário:** vCenter Clients, API do VMware, CLI do VMware

**Modelo de Licença:** por processador por mês

**Recursos:**
* vRealize Automation: entrega automatizada de infraestrutura personalizada, aplicativos e serviços de TI customizados
* vRealize Operations: funcionamento inteligente, desempenho, capacidade e orquestração de gerenciamento de configuração
* vRealize Log Insight: gerenciamento de log e análise do log tempo real.

## VMware vSAN

**Uso desejado:** o VMware vSAN é uma tecnologia de armazenamento distribuído que permite que unidades de armazenamento local em cada host vSphere sejam agregadas e agrupadas em um dispositivo de armazenamento não compartilhado que é acessível a todos os hosts em um cluster vSAN.

**Interface com o usuário:** vCenter Clients, API do VMware, CLI do VMware

**Recursos:**
* Armazenamento baseado em host distribuído
* Arquitetura sem compartilhamento
* Aumenta a capacidade para 64 nós
* Baixa latência
* Tolerância a falhas configurável

## VMware Site Recovery Manager (SRM)

**Uso desejado:** o VMware Site Recovery Manager (SRM) permite a disponibilidade e a mobilidade de aplicativos entre sites que estão em ambientes de nuvem particular. Tirando proveito da encapsulação e do isolamento de máquinas virtuais, o Site Recovery Manager permite a automação simplificada de recuperação de desastre para atender aos objetivos de tempo de recuperação (RTOs). O SRM também ajuda a reduzir os custos que estão associados aos planos de continuidade de negócios e a atingir resultados previsíveis de baixo risco para recuperação de um ambiente virtual.

**Interface com o usuário:** vCenter Clients, API do VMware, CLI do VMware

**Recursos:**
* Teste de recuperação sem interrupção
* Fluxos de trabalho de orquestração automatizados
* Recuperação automatizada de configurações de rede e de segurança
* Extensibilidade para automação customizada
* vCenter vMotion com orquestração cruzada
* Planos de recuperação centralizados
* Gerenciamento baseado em política
