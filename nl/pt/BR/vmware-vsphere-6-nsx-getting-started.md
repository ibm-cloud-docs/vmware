---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao VMware vSphere 6 NSX 

O NSX é implementado como uma titularidade de licença para você aplicar à sua infraestrutura. O {{site.data.keyword.BluSoftlayer_full}} fornece as licenças em uma base por processador (a precificação não muda para o número de núcleos por CPU). Uma licença NSX é necessária em cada servidor que usa um componente NSX (Gerenciamento, Controle ou Plano de dados). O NSX inclui recursos de rede extras para a plataforma. É possível criar uma rede de sobreposição robusta para a segurança do sistema, a segmentação do locatário e ambientes de nuvem híbrida que abrangem provedores ou se estendem de nuvens particulares no local.
{:shortdesc}

É possível incluir firewalls, balanceamento de carga, VPN, serviços NAT e microssegmentação baseada em VXLAN em seu ambiente com suporte para automação por meio de uma API RESTful.

## Incluindo licenças
As licenças são incluídas nos servidores usando o processo a seguir:
1. Efetue login no vCenter Server com o vSphere Client.
* Em **Administração**, clique em **Licenciamento**.
* Clique em **Soluções**.
* Na lista de produtos, clique em **VMware NSX for vSphere**.
* Clique em **Chave de licença** ou **Inserir nova chave de licença**.
* Clique em **OK**.

## Instalando o NSX

1. Implemente o NSX Manager.
* Registre o NSX Manager no vCenter Server.
* O vSphere Web Client implementa as instâncias do NSX Controller por meio do NSX Manager.
* Prepare hosts do vSphere usando o NSX Manager para instalar os VIBs nos hosts no cluster.
* Após os Controladores NSX serem implementados em todos os hosts aplicáveis, defina e configure os componentes do NSX tais como Gateways de Extremidade, Balanceadores de Carga e Firewalls.

## Considerações de implementação

A ativação do NSX para uma solução requer que você use nós do vSphere extras além dos nós de cálculo padrão.

**NSX Manager**<br />
O IBM Informix Virtual Appliance no Cluster de Gerenciamento tem um relacionamento 1:1 com o vCenter. Os recursos normais do vSphere HA são recomendados. O NSX Manager inclui recursos de backup planejado/on demand e requer conectividade IP para vCenter, controlador, recursos do NSX Edge e hosts ESXi. O NSX Manager é implementado na mesma sub-rede/VLAN que o vCenter, mas não é estritamente necessário. O dimensionamento típico da VM é o seguinte:

|Liberação do NSX|vCPU|Memória|Disco do OS|
|---|---|---|---|
|6.2 Small|4|12 GB|60 GB|
|6.2 Default|4|16 GB|60 GB|
|6.2 Large Scale|4|24 GB|60 GB|
{: caption="Tabela 1. Dimensionamento típico da VM do NSX Manager" caption-side="top"}

**Nós do controlador NSX**<br />
Os nós do controlador NSX são implementados como dispositivos virtuais na UI do NSX Manager. Cada dispositivo se comunica por meio de um endereço IP distinto que normalmente está dentro da mesma sub-rede que o NSX Manager, mas isso não é obrigatório. É recomendável implementar pelo menos três VMs do controlador para pelo menos três nós físicos do vSphere separados. Eles agem como ativo-ativo-ativo com delimitação de tarefa que é definida pelo NSX Manager. Se um nó falhar, ocorrerá um failover da "maioria das regras" para redistribuir a carga de trabalho para os controladores restantes. O NSX não impinge nativamente essa prática de design. É possível usar as regras nativas de antiafinidade do vSphere para evitar implementar mais de um nó do controlador no mesmo servidor ESXi. O dimensionamento típico de VM por VM é o seguinte:

|VMs do Controlador|vCPU|Reserva|Memória|Disco do OS|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="Tabela 2. Dimensionamento típico da VM do controlador NSX" caption-side="top"}

**Comutador NSX**
Um Virtual Distributed Switch (VDS) atualizado é implementado para todos os hosts para implementar os recursos distribuídos.

**NSX Edge Services Gateway**<br />
Implementado como dispositivos da VM multi-função conforme necessário no ambiente. Somente para roteamento, um cluster ativo de até oito gateways pode ser implementado. Para quaisquer/todos os outros serviços, ele é implementado em uma implementação de espera ativa. As comunicações que são externas ao ambiente da VM requerem IPs móveis designados pelo IBM Cloud para incluir quaisquer conjuntos NAT, VIPs e terminais VPN.

|Formulário do Gateway|vCPU|Memória|Uso Específico|
|---|---|---|---|
|Extra Grande|6|8 GB|Adequado para LB de alto desempenho L7|
|Quad-Grande|4|1 GB|Adequado para ECMP de alto desempenho e implementação FW|
|Grande|2|1 GB|DC pequeno e serviço único|
|Compacto|1|512 MB|Implementações pequenas ou uso de serviço único ou PoC|
{: caption="Tabela 3. Serviços do NSX Edge" caption-side="top"}

