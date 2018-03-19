---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao VMware vSphere 6 

Use o seguinte para começar a usar o vSphere 6.

## Entendendo o ambiente e a configuração

Para otimizar a solução VMware, recomenda-se que você use uma VLAN de Rede Privada e Pública (Opcional, Porta Pública pode ser desativada, se não é necessária) para seu ambiente do VMware vSphere. Esse perfil de fornecimento permite os limites de tráfego de segmento da Camada 2 a seguir:

|Exemplo de ID de VLAN|Descrição|Tipo|Detalhes Adicionais|
|---|---|---|---|
|VLAN1 - **1101**|Gerenciamento, VxLAN|BCR privado|VLAN nativa não identificada, VLAN nativa original na qual os hosts do VMWare são implementados no momento do pedido|
|VLAN4 - **2200**|DMZ de acesso à Internet pública|FCR público|VLAN nativa não identificada, VLAN nativa original na qual os hosts do VMWare são implementados no momento do pedido|
{: caption="Tabela 1. Exemplos de VLAN privada e pública" caption-side="top"}

## Efetuando seu pedido para servidores vSphere
1. Efetue login no [{{site.data.keyword.slportal_full}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window}.
2. Clique em **Conta > Fazer um pedido**.
3. Na seção **Servidor bare metal**, clique em **Mensal**.
4. Selecione os servidores. Consulte as publicações de Suporte do VMware para obter os requisitos mínimos:
  * Os servidores a seguir foram selecionados para o exemplo. **Nota:** ter dois uplinks público e privado ilimitados é um requisito para redundância. Confirme se o data center no qual você criou suas VLANs tem uplinks ilimitados.  
  * Cluster de capacidade (Quantidade: 2)
    * Configuração do servidor: selecione um servidor Intel Xeon v3 na seção 'Servidores multinúcleos de processador dual'
    * Software: S.O. = vSphere Enterprise Plus 6
    * Armazenamento de S.O.: 2 x SATA de 1 TB (configurado como um RAID 1)
    * Armazenamento de Dados: recomenda-se solicitar SATA de 2 TB ou SSD de 1,2 TB ou Armazenamento SAN NFS de Resistência/Desempenho
      * Se você estiver interessado em outros tipos de armazenamento, consulte [Armazenamento para usar com o VMware Systems](select-storage-option-use-vmware.html)
      * Velocidades da Porta de Uplink: redes duais pública e privada de 1 Gbps (sem limites)
        * Uplinks de 10 Gbps são recomendados para soluções VMware vSAN
5. Se você estiver criando uma nova implementação em um novo data center do IBM Cloud, prossiga para a etapa 6. Se esta é uma expansão ou uma implementação em um Data Center existente, selecione a VLAN BCR de Backend + VLAN FCR de Frontend preferenciais. Para o exemplo, a VLAN BCR de Backend é 1101 e a VLAN FCR de Frontend é 2200. **Nota:** se esta for uma nova implementação ou uma nova implementação em um novo DC, as VLANs BCR de Backend e FCR de Frontend serão criadas quando você solicitar o servidor.
6. Insira um **Nome do host** e um **Domínio**.
7. Revise a ordem e clique em **Finalizar sua ordem** para iniciar o processo de fornecimento.

## Efetuando seu pedido para o vCenter Server

O vCenter é um complemento para um Windows Server. Essa configuração aumenta a capacidade para 20 hosts do vSphere. Para implementações maiores, a implementação do vCenter Server Appliance (VCSA) [Implementar e configurar um vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html) diretamente em um cluster do vSphere é recomendada.

Use as etapas a seguir para solicitar um servidor virtual com o vCenter instalado:

1. Efetue login na {{site.data.keyword.slportal_short}}.
2. Clique em **Conta > Fazer um pedido**.
3. Solicite uma Instância do nó pública/privada Bare Metal ou de Servidor Virtual (VSI) **Mensal** sob Servidores Virtuais.
  1. Para que uma Instância do SoftLayer Virtual Server (VSI) se qualifique para o vCenter 6.0, deve-se implementar em pelo menos **4 x Núcleos de 2,0 GHz** e **4 GB de RAM**
  2. Para obter uma listagem de recomendações de implementação do vCenter, consulte o [VMware vCenter Server &trade; 6.0 Deployment Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}.
4. Insira as informações a seguir:
  * Com base na configuração mínima recomendada do servidor
    * Configuração de núcleo da vCPU: 4 x núcleos de 2,0 GHz
    * Configuração de RAM: 12 GB de RAM
    * Software: S.O. = Windows Server 2012 R2 Standard Edition (64 Bits)
    * Complemento Específico do S.O.: vCenter 6
    * Primeiro Disco: 1 x 100 GB (SAN)
    * Segundo Disco: 1 x 50 GB (SAN)
    * Velocidades da Porta de Uplink: Uplinks de Rede Pública e Privada de 1 Gbps

5. Se essa for uma nova implementação em um novo Data Center do IBM Cloud, continue com a etapa 6 abaixo. Se essa implementação é uma expansão ou implementação em um Data Center existente, selecione a VLAN BCR de Backend + VLAN FCR de Frontend preferenciais. Para nosso exemplo, nossa VLAN BCR de Backend é 1101 e a VLAN FCR de Frontend é 2200. (Se essa for uma nova implementação ou uma nova implementação em um novo DC, as VLANs BCR de Backend e FCR de Frontend serão criadas quando você solicitar o servidor)
6. Insira um **Nome do host** e um **Domínio**.
7. Revise a ordem e clique em **Finalizar sua ordem** para iniciar o processo de fornecimento.

## Solicitando sub-redes/endereços IP públicos e privados móveis

**Nota:** não continue se as VLANs não tiverem sido provisionadas completamente.

As sub-redes são usadas para tratar da máquina virtual (VM) guest VMware e do tráfego baseado em kernel do host VMware.

1. No Portal de Controle, clique em **Rede > Gerenciamento de IP > Sub-redes**.
2. Clique em **Solicitar endereços IP** na parte superior direita da tela.
3. Selecione **Privado móvel**.
4. Selecione a VLAN apropriada (Exemplo: bcr01.wdc04: 1101)
5. Clique em **Continuar**.
6. Preencha o formulário **Solicitar endereço IP**.
7. Clique em **Solicitar endereços IP** na parte superior direita da tela.
8. Clique em **Fazer pedido**.
9. Siga esse processo para cada VLAN aplicável (Ex. 1101, 2200)
  1. Para obter mais informações sobre VLANs, consulte [Introdução às VLANs](/docs/infrastructure/vlans/getting-started.html).

|Tipo de Sub-rede|tamanho da sub-rede|Limite de Vlan|Uso de host do vSphere|
|---|---|---|---|
|Móvel - privado|Endereço /27 32|**1101**|VMs de gerenciamento|
|Móvel - privado|Endereço /27 32|**1101**|Portas kernel da VM para iSCSI e vMotion|
|Móvel - privado|Endereço /27 32|**1101**|IPs privados para a VM guest|
|Móvel - público|Endereço /27 32|**2200**|IPs públicos para VMs guest (opcional)|
{: caption="Tabela 2. Sub-redes" caption-side="top"}

### Opcional – Desativando a interface pública no host vSphere

É possível desativar as interfaces públicas do vSphere para propósitos de segurança quando você não as usa.

1. No Portal de Controle, clique em **Dispositivos > Lista de dispositivos**.
2. Clique no nome de seu host vSphere.
3. Clique na tabela Configuração e role para baixo até a seção Rede.
4. Selecione **Desconectar** para os pares eth1 e eth3 de cada host vSphere aplicável para todos os hosts

Isso também pode ser executado por meio do [{{site.data.keyword.slapi_full}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window}.

## Criando e configurando o vSphere Data Center Cluster <! -- criar e configurar deve ser tarefas separadas -- >

Agora é possível efetuar login no servidor vCenter e configurar o cluster do vSphere.

1. No Portal de Controle, clique em **Dispositivos > Lista de dispositivos**
2. Localize seu dispositivo do vCenter e clique em seu nome.
3. Role para baixo na tela **Detalhes do dispositivo** até a seção **Rede** do servidor e anote o **Endereço IP privado**.
4. Role para baixo na tela **Detalhes do dispositivo** e anote as **Senhas** para o Windows OS e o vCenter Software.
5. Abra uma sessão Microsoft Remote Desktop (RDP) e conecte-se ao seu vCenter Server por meio de seu endereço IP público.
6. Efetue login usando as senhas que você obteve na etapa 4. **Nota:** uma conexão VPN ativa para o IBM Cloud precisará estar em vigor se o endereço IP privado for usado para acessar o vCenter. Para obter mais informações sobre o acesso VPN, consulte [Ativar acesso à rede privada da infraestrutura do IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network).
7. Faça download e instale o [vSphere Client tradicional ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} ou use o vSphere Web Client por meio do link `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Efetue login no vCenter com o endereço IP e as senhas que você obteve nas etapas 3 e 4.
9. Clique com o botão direito no nome do servidor vCenter na área de janela esquerda e selecione **Novo data center**.
10. Insira um nome apropriado para o data center.
11. Clique com o botão direito no data center e selecione **Novo cluster**.
12. Insira um nome de cluster. NÃO ative Recursos do Cluster, vSphere HA ou vSphere DRS neste momento.
13. Clique em **Avançar**.
14. Deixe **EVC** desativado e clique em **Avançar**.
15. Aceite o _padrão para armazenar o swapfile no mesmo diretório que a máquina virtual_ e clique em **Avançar**.
16. Clique em **Concluir** para concluir o cluster.
17. Clique com o botão direito no novo cluster que você acabou de criar e selecione **Incluir host**.
18. Insira o endereço IP ou nome do host de um dos hosts vSphere e insira **Raiz** no campo **Nome do usuário** e a senha para o host no campo **Senha**.
19. Clique em **Avançar** apesar da tela Resumo do Host, Designar Licença, Modo de Lockdown e clique em **Concluir** para concluir a inclusão de seu host no Cluster
20. Repita as etapas 18 e 19 para todos os outros hosts vSphere em seu cluster. Você verá cada host vSphere sob o novo cluster depois de ter concluído.

### Configurando a construção de rede básica para os hosts vSphere

Use as etapas a seguir para configurar a construção básica para os hosts vSphere em seu cluster.

1. Selecione o primeiro host vSphere e clique na guia **Configuração**.
2. Na seção **Hardware**, selecione **Rede**. É necessário já ter vSwitch0 com vmnic0; clique em **Propriedades** ao lado de vSwitch0.
3. Selecione **Adaptadores de rede** na janela **Propriedades de vSwitch** e clique no botão **Incluir**.
4. Selecione vmnic2 para incluir em vSwitch0 e clique em **Avançar**.
5. Certifique-se de que ambos os vmnics sejam **Adaptadores ativos** e clique em **Avançar**.
6. Clique em **Concluir**.
7. Clique na guia **Portas** e certifique-se de que vSwitch esteja destacado; clique em **Editar**.
8. Clique na guia **Geral** e mude o **MTU** para 9000 (quadro gigante).
9. Clique na guia **Associação de NIC**, mude o balanceamento de carga para o hash **Rotear com base no IP** e clique em **OK**.
10. Use as etapas 1 a 8 para configurar o vmnics para os outros hosts vSphere em seu cluster.

Um grupo da porta agora precisa ser incluído para vMotion. O grupo pode ser criado como um Virtual Standard Switch (VSS) ou um Virtual Distributed Switch (VDS). Para propósitos do nosso exemplo, criaremos um comutador VSS.

1. Selecione a guia **Configuração** e selecione **Rede**.
2. Clique em **Propriedades...** para vSwitch0.
3. Clique em **Incluir...** para criar um Grupo da Porta.
4. Selecione **VMkernel** e clique em **Avançar**.
5. Preencha as Propriedades do grupo da porta com as informações a seguir:
  * **Rótulo da Rede:** um nome apropriado para o grupo da porta.
  * **ID da VLAN (Opcional):** o ID da VLAN para o tráfego do vMotion (1101 para nosso exemplo). O ID da VLAN permitirá que o VMware identifique o tráfego para a VLAN específica.
  * Selecione **Usar este grupo da porta para vMotion**.
6. Clique em **Avançar**.
7. Insira um **Endereço IP móvel** para a VLAN. (É possível obter o endereço IP da porta no portal do SoftLayer, **Rede > Gerenciamento de IP > VLANs**. Selecione a VLAN correta e, sob **Sub-redes**, você verá um intervalo de endereço IP móvel. Se você não possui um Endereço IP Móvel disponível ou se tiver esgotado seu conjunto atual, siga as etapas na seção 'Solicitar sub-redes/endereços IP privados' para solicitar um endereço IP móvel adicional.
8. Clique em **Avançar** e, em seguida, **Concluir** para concluir.

Use as etapas a seguir para criar um Grupo da Porta para o tráfego de dados da VM.

1. Clique em **Propriedades...** para vSwitch0 e selecione **Incluir, máquina virtual**.
2. Preencha as **Propriedades do grupo da porta** com as informações a seguir:
  * **Rótulo da Rede:** insira o nome do Grupo da Porta, por exemplo, Dados da VM.
  * **ID da VLAN (Opcional):** insira um ID da VLAN, usamos 1101 para o nosso exemplo. O ID da VLAN permite que o VMware identifique o tráfego para a VLAN.

### Opcional - Instalando licenças Add On VMware (NSX, vRealize, vSAN, etc.)

Agora que o ambiente do VMware está ativo, você está pronto para continuar com a implementação de configurações adicionais, VMs guest ou VMware Add Ons. As licenças para VMware Add Ons também podem ser adquiridas por meio do portal de controle do IBM Cloud e incluídas por meio de seu console do vCenter. Para obter mais informações sobre como solicitar e gerenciar licenças do VMware Add On, consulte [VMware vSphere 6: solicitando e gerenciando licenças](vmware-vsphere-6-ordering-and-managing-licenses.html).

## Próximas Etapas
Agora você tem um ambiente VMware de site único básico em execução em um data center do IBM Cloud. A configuração básica tem apenas um armazenamento de dados local, tornando-a uma configuração simplificada que não contém recursos como DRS do VMware, HA, DRS de Armazenamento e um firewall.

Para obter mais informações, consulte [FAQs: VMware](vmware-faq.html). 
