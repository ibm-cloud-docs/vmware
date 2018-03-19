---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Guia de arquitetura para QuantaStor

É possível solicitar e configurar a solução de armazenamento compartilhado OSNexus QuantaStor para um ambiente VMware ESXi 5. Use as informações a seguir junto com o cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) para configurar uma dessas opções de armazenamento em seu ambiente VMware.

## Etapa 1: solicitando o armazenamento compartilhado QuantaStor

Antes de efetuar um pedido para armazenamento, é necessário determinar as especificações que atendem aos seus requisitos de capacidade e E/S. Essas especificações incluem, mas não estão limitadas a, RAM do servidor, tipo e número de unidades de disco, SSDs para armazenamento em cache, configuração RAID e configuração de rede. Para obter mais informações sobre como escolher a configuração de QuantaStor correta em seu ambiente, consulte [QuantaStor Solution Design Guide para Virtualização ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}.

Para o ambiente de exemplo, é usada uma configuração menor que pode entregar capacidade e E/S suficientes necessárias para as máquinas virtuais (VMs). Certifique-se de compreender os requisitos de capacidade e E/S de suas VMs antes de efetuar seu pedido. Embora o servidor QuantaStor seja expansível, é importante que você dimensione seu hardware inicialmente para evitar atrasos na configuração e na implementação.

### Solicitando o QuantaStor

Use as etapas a seguir para solicitar um servidor QuantaStor.

1. Efetue login no [{{site.data.keyword.slportal_full}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} e clique em **Conta > Efetuar um Pedido**.
2. Selecione {{site.data.keyword.baremetal_short}}, Mensalmente na tela pop-up.
3. Selecione o servidor apropriado com a capacidade para armazenar os números de discos que são necessários em seu ambiente na página Lista de servidores. [Para o ambiente de exemplo, um sistema de 12 núcleos (ou seja, núcleo dual hexadecimal) com 12 compartimentos de unidade é selecionado.]
4. Insira as opções de configuração a seguir:
  * **Data Center:** local das VLANs e hosts ESXi que foram criados anteriormente
  * **Servidor:** Xeon de núcleo hexadecimal de processador dual
  * **RAM:** 64 GB
  * **Sistema Operacional:** OSNexus QuantaStor 3.x (4 TB)
  * **Unidades de Disco Rígido:**
    * Discos 1 e 2: SATA de 500 GB em RAID 1
    * Modelo de Partição: Linux Básico
    * Discos 3 a 10: SAS de 600 GB 15.000 em RAID 10
  * **Largura da Banda Pública:** somente rede privada
  * **Velocidades da Porta de Uplink:** uplinks de rede privada redundantes de 10 Gbps
5. Clique em **Continuar seu pedido**.

**Nota:** o servidor de armazenamento está configurado com duas interfaces de rede que são desvinculadas para que duas sub-redes diferentes possam ser usadas para balancear a carga do tráfego para a matriz de armazenamento.

### Concluindo a configuração

Agora você tem um dispositivo QuantaStor em seu carrinho de compras. Agora, é necessário designar a VLAN privada, o nome do host e o domínio para o dispositivo para que ele possa ser provisionado corretamente.

1. Designe as VLANs a seguir e crie nomes de hosts para os dispositivos: host QuantaStor – VLAN de backend: (1102 no ambiente)
2. Selecione seu método de pagamento, concorde com os Termos e Condições e clique em Finalizar seu pedido.

**Nota** não prossiga para a Etapa 3 até que o servidor seja provisionado e esteja acessível por meio da VPN ou do servidor virtual.

## Etapa 2: ativando o adaptador de software iSCSI para hosts de gerenciamento e de capacidade

O adaptador de software iSCSI deve ser ativado em cada host de gerenciamento e capacidade e seu nome qualificado de iSCSI (IQN) coletado antes que os volumes iSCSI sejam montados. Use as etapas a seguir para ativar o adaptador de software iSCSI:

1. Acesse um host de gerenciamento ou de capacidade ESXi e selecione Gerenciar, Armazenamento, Adaptadores de armazenamento.
2. Clique no sinal de mais verde (+) e inclua o Adaptador de Software iSCSI.
3. Clique no vmhba que corresponde ao Adaptador de Software iSCSI e registre o Nome iSCSI (Figura 1) na seção Detalhes do adaptador após ele ser ativado.
4. Execute as etapas 1 a 3 para cada Adaptador de Software iSCSI em cada host de gerenciamento e de capacidade ESXi.

## Etapa 3: configurando o QuantaStor

Após o servidor ser provisionado, será possível configurar o dispositivo de armazenamento compartilhado. Especificamente, você configura a rede e os volumes de iSCSI e designa volumes aos hosts. 

Por exemplo, o volume vmk3 tem vmnic0 que se conecta à Sub-rede Privada Móvel A na VLAN de armazenamento. O volume vmk4 tem vmnic2 que se conecta à Sub-rede Privada Móvel B na VLAN de armazenamento. O servidor QuantaStor também tem dois adaptadores de rede privada, eth4 e eth6, que se conectam à VLAN de armazenamento.

### Configurando a rede

1. Abra um navegador da web e acesse o endereço IP do QuantaStor listado na página **Dispositivos** no [{{site.data.keyword.slportal_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window}.
2. Insira o **Nome do usuário administrativo** e a **Senha** (localizado na seção Senhas na página **Detalhes do dispositivo**). Antes de continuar, observe os dispositivos de rede privada que são usados pelo servidor QuantaStor, como eth4.
3. Acesse **Sistema de armazenamento > Portas de rede**.
4. Selecione o adaptador privado que está ativo (exemplo: eth4) na lista de adaptadores de rede. Clique com o botão direito e selecione **Modificar porta de rede** no menu pop-up.
5. Limpe a caixa de seleção **iSCSI ativado** para desativar conexões iSCSI para esse adaptador e clique em **OK**.
6. Selecione o adaptador privado que não está ativo, mas está designado à rede privada (por exemplo, eth6).
7. Clique com o botão direito no adaptador eth6 e selecione **Modificar porta de rede** no menu pop-up.
8. Selecione um **Tipo de configuração** igual a **Estático** na tela **Modificar porta de rede**.
9. Insira um endereço IP privado primário, uma sub-rede e um gateway para o adaptador. Use um endereço da linha de Armazenamento se você estiver usando a planilha de VLAN do cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html).
10. Limpe a caixa de seleção **iSCSI ativado** para desativar as conexões iSCSI para este adaptador.
11. Clique com o botão direito no adaptador privado e selecione **Ativar porta de rede** para colocar o adaptador on-line depois de configurá-lo com um endereço IP.
12. Clique em **OK** para ativar a porta após a verificação do endereço IP.

### Abrindo um chamado de suporte

É necessário abrir um chamado de suporte depois de configurar um segundo adaptador com um endereço IP privado primário. Abrir o chamado ajuda a garantir que o endereço IP que você usou não seja usado se outra máquina for provisionada na VLAN.

1. Clique em **Suporte** > **Incluir chamado** e insira as informações a seguir:
  * Assunto: pergunta da rede privada
  * Título: reservar e designar o endereço IP privado
  * Dispositivos Associados: 'selecione o servidor QuantaStor'
  * Detalhes: reservar e designar na VLAN. Esse endereço IP é usado para o segundo adaptador no servidor QuantaStor.

### Configurando o QuantaStor

Agora que a matriz pode aceitar conexões de ambos os adaptadores, as interfaces virtuais dos adaptadores que estão nas sub-redes do Caminho do armazenamento A e do Caminho do armazenamento B devem ser designadas.

  1. Clique com o botão direito na interface do adaptador privado inicial (eth4) e selecione **Criar interface virtual** no menu pop-up.
  2. Insira um endereço IP privado móvel e uma sub-rede para o adaptador na tela pop-up resultante e certifique-se de que **iSCSI ativado** esteja marcada.
  3. Use um endereço da linha Caminho do armazenamento A se você estiver usando a planilha de VLAN.
  4. Registre o endereço IP que é usado na seção Notas na página Endereço IP móvel.
  5. Selecione a interface do adaptador privado inicial (eth4) para ligar a interface virtual e clique em **OK**.
  6. Clique com o botão direito na outra interface do adaptador privado (eth6) e selecione **Criar interface virtual** no menu pop-up.
  7. Insira um endereço IP privado móvel e uma sub-rede para o adaptador e certifique-se de que **iSCSI ativado** esteja marcada na janela pop-up resultante.
  8. Use um endereço da linha Caminho do armazenamento B se você estiver usando a planilha de VLAN.
  9. Registre esse endereço IP como usado na seção Notas na página Endereço IP móvel.
  10. Selecione a outra interface do adaptador privado (eth6) para ligar a interface virtual e clique em **OK**.

Após o servidor QuantaStor ser configurado com endereços IP e interfaces virtuais, será necessário configurar o roteamento para certificar-se de que o tráfego de saída use a interface correta (porque há duas NICs em diferentes sub-redes).

1. Use SSH no servidor QuantaStor com suas credenciais de raiz e anexe as linhas a seguir a /etc/network/interfaces. Supondo que eth4 e eth6 sejam as NICs na rede privada:
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### Criando um conjunto de armazenamento

Em seguida, deve-se criar um conjunto de armazenamento que será usado para alocar volumes antes que se possa criar volumes ou compartilhamentos.

1. Clique com o botão direito em **Conjuntos de armazenamentos** e selecione **Criar conjunto de armazenamentos**.
2. Insira as informações a seguir na tela **Criar conjunto de armazenamentos**:
  * Nome: insira o nome apropriado para o conjunto de armazenamentos. Exemplo: StoragePool-01
  * Tipo do Conjunto: padrão (zfs)
  * Perfil de E/S: virtualização
  * Discos a Serem Utilizados para o Conjunto de Armazenamentos: sdb
3. Clique em **OK**.

Se sdb não estiver disponível para inclusão em um conjunto, é devido a uma partição que existe e está sendo identificada como inicializável. É necessário usar gdisk no console Quantastor para remover a partição e quaisquer entradas /etc/fstab. Em seguida, é necessário criar volumes para ESXi para consumo.

### Criando volumes de armazenamento do iSCSI

É necessário criar dois volumes de armazenamento. Um volume é usado para VMs de gerenciamento no cluster de gerenciamento e o outro para VMs no cluster de capacidade. Conclua as etapas a seguir para criar os volumes de armazenamento do iSCSI:

1. Clique com o botão direito em **Volumes de armazenamento** e selecione **Criar volume de armazenamento** no menu pop-up.
2. Insira as informações para os volumes de armazenamento. **Nota:** embora sua configuração possa diferir dependendo da capacidade de carga de trabalho e de armazenamento, o exemplo mostra os valores na Tabela 1 e na Tabela 2 para cada volume de armazenamento.

|Campo|Valor|
|---|---|
|Nome|Mgmt-LUN0|
|Conjunto de armazenamentos|[Nome do conjunto de armazenamentos configurado na etapa anterior]|
|Tamanho|500 GB|
|% Reservado|50|
|Compactação|Ativado|
{: caption="Tabela 1. Volume de gerenciamento do iSCSI" caption-side="top"}

|Campo|Valor|
|---|---|
|Nome|Capacidade-LUN0|
|Conjunto de armazenamentos|[Nome do conjunto de armazenamentos configurado na etapa anterior]|
|Tamanho|3 TB|
|% Reservado|50|
|Compactação|Ativado|
{: caption="Tabela 2. Volume de capacidade do iSCSI" caption-side="top"}

### Designando acesso ao host aos volumes

É necessário configurar o QuantaStor para permitir o acesso dos hosts ESXi por meio de cada IQN do host após os volumes serem configurados.

1. Navegue para a página de administração do QuantaStor e clique com o botão direito no menu **Hosts** e selecione **Incluir host**.
2. Insira as informações a seguir na tela **Incluir host**:
  * Nome do Host: insira um nome do host apropriado. O nome do host não tem o nome completo do domínio (FQDN), mas deve descrever o host. Exemplo: MyESXiHostName
  * Tipo de Sistema Operacional: VMware
  * Inicializador: botão de opções Nome qualificado de iSCSI (IQN)
  * Nome Qualificado de iSCSI: o IQN para o respectivo host.
3. Clique em **OK**.

Siga essas etapas para cada host de gerenciamento e de capacidade no ambiente do ESXi.

Depois de incluir cada host nos clusters de gerenciamento e capacidade, siga essas etapas:

1. Clique com o botão direito no menu **Grupos de hosts** e selecione **Criar grupo de hosts…**.
2. Insira 'ManagementCluster' no campo **Nome** e selecione todos os hosts que estão no cluster de gerenciamento.
3. Clique em **OK**. Será criado um grupo de hosts que poderemos designar a um determinado volume.

Repita esse processo para o cluster de capacidade.

1. Clique no menu **Volumes de armazenamento**.
2. Clique com o botão direito no volume **Mgmt-Lun0** e selecione **Designar/Remover acesso ao host**.
3. Confirme se **Mgmt-Lun0** é uma opção no menu suspenso e selecione o grupo de hosts que você criou na etapa anterior. Essa opção permite que cada host ESXi no cluster de gerenciamento acesse o volume Mgmt-Lun0. Faça o mesmo para **Capacidade-LUN0**

## Etapa 4: montando volumes em clusters de gerenciamento/capacidade

Efetue login no vSphere Web Client e acesse **Hosts** sob as **Listas de inventários do vCenter**.

Use as etapas a seguir para montar o volume nos hosts ESXi:

1. Selecione um host e clique em **Gerenciar, Armazenamento,** > **Adaptadores de armazenamento**.
2. Selecione **Destinos** > **Descoberta dinâmica** > **Incluir…**.
3. Insira o endereço IP que está designado ao dispositivo de armazenamento QuantaStor em Caminho do armazenamento A na tela **Incluir servidor de destino de envio**.
4. Deixe **3260** como a Porta e clique em **OK**.
5. Clique em **Descoberta dinâmica** > **Incluir…**. Repita as etapas 4 e 5 para o Caminho do armazenamento B.

O host ESXI está pronto para varrer novamente o adaptador de software iSCSI para descobrir o volume Mgmt-Lun0.

1. Selecione o ícone **Varrer adaptadores de armazenamento novamente** (Figura 9) na tela **Adaptadores de armazenamento**.
2. Deixe a opção padrão na tela pop-up resultante e clique em **OK**.
3. Clique em **Ações, novo armazenamento de dados** após o volume ser descoberto e formate-o como **VMFS-5**.
4. Confirme que a formatação está concluída e clique em **Dispositivos de armazenamento, Detalhes do dispositivo, Editar caminhos múltiplos…**.
5. Selecione **Round robin** para a **Política de seleção de caminho** e clique em **OK**.

Agora que o volume Mgmt-Lun0 foi conectado a um único host, deve-se voltar para os outros hosts de gerenciamento no cluster e repetir o processo para incluir o volume. No entanto, não é necessário formatar o volume pois ele já está formatado com VMFS-5 e é exibido como tal após a descoberta.

## Etapa 5: desativando o ACK atrasado em hosts vSphere ESXi

O ACK atrasado precisará ser desativado quando as LUNs de armazenamento forem anexadas aos hosts de gerenciamento e capacidade.

1. Acesse o ambiente do vSphere e selecione **Adaptadores de armazenamento** > **Adaptador de software iSCSI** > **Opções avançadas**.
2. Clique em **Editar** e role até o final da tela Opções avançadas.
3. Limpe a caixa de seleção **DelayedAck** e clique em **OK**.

Para obter mais informações sobre ACK atrasado relacionado a VMware, consulte [Base de conhecimento do VMware](https://kb.vmware.com/s/article/1002598).

Agora é possível retornar para o cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) e concluir a configuração do ambiente.
