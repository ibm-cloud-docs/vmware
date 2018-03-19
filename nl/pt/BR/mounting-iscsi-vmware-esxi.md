---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Montando o iSCSI VMWare ESXi

A montagem do iSCSI no VMWare ESXi pode ser feita em poucas etapas e apenas com os detalhes do nó do servidor e de armazenamento.
{:shortdesc}

1. Efetue login no vSphere usando o IP privado primário e o usuário **raiz** e a senha raiz.
* Na página de boas-vindas, clique na guia **Configuração**.
* Clique em **Adaptadores de armazenamento** e, em seguida, em **Incluir…**.
* Clique em **OK** para incluir o Adaptador iSCSI do Software.
* Confirme clicando em **OK**.
* Após a atualização, você verá o novo iSCSI Adaptado listado.
* Clique em **Propriedades** na área de janela inferior.
* Na janela Propriedades, clique em **Configurar** próximo à parte inferior e configure o **Nome** com o IQN para o servidor (localizado na página do dispositivo de armazenamento sob hosts autorizados).
* Clique na guia **Descoberta dinâmica** e, em seguida, clique em **Incluir...**.
* O servidor iSCSI será o IP de destino do dispositivo de armazenamento, em seguida, clique no botão **CHAP..** .
* Selecione **Utilizar CHAP** e desmarque **Herdar do pai**. Insira o **Nome de usuário** (localizado na página do dispositivo de armazenamento sob hosts autorizados) e sua senha.
* Selecione **Não utilizar o CHAP** na seção CHAP mútuo e, em seguida, clique em **OK**.
* Agora você verá o dispositivo na Janela de Descoberta Dinâmica, clique em **Fechar**.
* Confirme a nova varredura dos dispositivos de armazenamento.
* Em seguida, você verá o dispositivo na área de janela inferior cinza e 'desmontado'.
* Clique com o botão direito no nome do dispositivo e selecione **conectar**.
* Clique no menu **Armazenamento de dados** na coluna esquerda, em seguida, clique em **Incluir armazenamento** e escolha **Disco/LUN**.
* Clique no dispositivo com 'iqn'.
* Escolha a versão do sistema de arquivos desejada e clique em **Avançar**, em seguida, continue com o assistente.
* Depois de concluído, será possível usar o iSCSI conforme necessário para o host e as VMs que você cria.



Conectar um dispositivo Data Transfer Service iSCSI é igual, exceto que você precisa obter o IQN do servidor. Você conclui as etapas a seguir no console ESXi:

Primeiro é necessário obter o dispositivo:

`esxcfg-scsidevs -a | grep iSCSI`

Em seguida, será necessário obter o IQN (nesse caso, vmhba33 é o dispositivo iSCSI):

`vmkiscsi-tool -I -l vmhba33`
